---
name: threat-intelligence
description: Consume, correlate, and operationalize cyber threat intelligence from multiple sources. Use this skill whenever the user mentions threat intelligence, threat feeds, IOC enrichment, threat actors, APT groups, TTPs, MITRE ATT&CK mapping, threat landscape, threat hunting, indicators of compromise, campaign tracking, vulnerability exploitation intelligence, CVE threat context, or sector-specific threat briefings. Also trigger when the user asks about recent cyber attacks, ransomware campaigns, nation-state activity, emerging threats, or wants to enrich an IP address, domain, hash, or URL with reputation and context data. This skill supports the /threat-brief and /investigate commands and works closely with the incident-response skill during active investigations.
---

# Threat Intelligence

A skill for consuming, correlating, and operationalizing cyber threat intelligence across the full intelligence lifecycle — from raw feed ingestion through finished intelligence products. This skill serves both the proactive side of TI (situational awareness, threat landscape monitoring, hunt hypothesis generation) and the reactive side (IOC enrichment, incident context, attribution support).

The threat intelligence MCP ecosystem is one of the most mature in cybersecurity. This skill is designed to orchestrate across multiple TI sources simultaneously, correlating results to produce higher-confidence assessments than any single source provides alone.

> **Philosophy: People Led, AI Driven (PLAID)**
> AI excels at the speed-intensive parts of threat intelligence — ingesting high-volume feeds, correlating indicators across sources, mapping TTPs to frameworks, and drafting intelligence products. Humans provide the analytical judgment that turns information into intelligence: assessing source reliability, evaluating adversary intent, making attribution calls, and deciding what matters for *this* organization. Every output from this skill is an analytical input for the human analyst, not a finished conclusion.

## Before you begin

Check `security.local.md` for:
- Industry sector and regulatory environment (shapes threat relevance filtering)
- Active threat intelligence sources and MCP connectors configured
- Intelligence requirements (standing questions the security team needs answered)
- Sector ISACs the org participates in (E-ISAC for utilities, FS-ISAC for financial, H-ISAC for health, etc.)
- Classification and handling markings in use (TLP, organizational sensitivity levels)
- Critical assets and crown jewels (for relevance scoring)

## Roles this skill serves

- **Threat Intelligence Analyst:** Primary consumer. Feed monitoring, indicator management, intelligence production, hunt support.
- **SOC Analyst:** IOC enrichment during alert triage, contextualizing detections, identifying campaigns behind individual alerts.
- **Threat Hunter:** Hypothesis generation from TI, translating adversary TTPs into detection queries, proactive search for unreported compromise.
- **Security Leadership:** Threat landscape briefings, risk-informed decision making, communicating threat posture to executives and the board.
- **Incident Responder:** Attribution context during investigations, understanding adversary playbooks to anticipate next moves.

Adjust depth and output format to role. A SOC analyst enriching an IP during triage needs a fast reputation check and campaign context. A TI analyst building a threat landscape briefing needs comprehensive source synthesis and confidence assessments.

## MCP tool landscape

This skill orchestrates across multiple MCP-connected intelligence sources. The ecosystem is unusually rich — here's what's available and how each source contributes:

### Strategic intelligence (threat landscape, campaigns, actors)

**Feedly Threat Graph** — Commercial TI platform with pre-mapped relationships between actors, campaigns, malware, and vulnerabilities across 10,000+ sources. Strongest for: trending threats, campaign tracking, vulnerability exploitation intelligence, sector-specific filtering. The Feedly MCP server enables natural language queries against the Threat Graph — "What ransomware campaigns targeted US utilities in the last 30 days" returns structured, attributed intelligence, not just search results.

**OpenCTI** — Open source TI platform using STIX2 data model with a GraphQL API. Strongest for: structured threat data management, relationship mapping between entities, collaborative analysis, MISP integration. The OpenCTI MCP server supports both read and write operations — you can query existing intelligence and create new entities to enrich the knowledge base.

**MISP** — Open source TI sharing platform with a large community feed ecosystem. Strongest for: indicator sharing, community-sourced intelligence, automated feed ingestion, event correlation.

### Tactical intelligence (IOC enrichment, reputation)

**VirusTotal** — File, URL, domain, and IP analysis against 70+ security vendor engines. Strongest for: malware sample analysis, detection ratios, behavioral reports, relationship graphs between indicators.

**Shodan** — Internet-connected device intelligence. Strongest for: attack surface assessment, exposed service enumeration, vulnerability scanning context, infrastructure reconnaissance.

**AbuseIPDB** — Community-driven IP reputation database. Strongest for: quick IP reputation checks, abuse reports, ISP context.

**Cyber Sentinel** — Aggregator MCP server that unifies VirusTotal, AbuseIPDB, URLhaus, Shodan, ThreatFox, and MalwareBazaar into a single query interface with confidence scoring. Strongest for: rapid multi-source IOC enrichment in a single call.

### Detection intelligence (rules, signatures, hunt queries)

**Security Detections** — Aggregates Sigma rules, Splunk ESCU detections, Elastic rules, and KQL queries into a searchable database with MITRE ATT&CK mappings and CVE tracking. Strongest for: translating TI into detection content, finding existing rules for observed TTPs, gap analysis against ATT&CK coverage.

**CISA KEV** — Known Exploited Vulnerabilities catalog. Strongest for: prioritizing patching based on confirmed exploitation, regulatory compliance (BOD 22-01 for federal, best practice for everyone).

### Tool selection logic

Not every query needs every source. Match tools to the intelligence question:

| Intelligence question | Primary sources | Secondary sources |
|---|---|---|
| "What's the threat landscape for my sector?" | Feedly, OpenCTI | MISP |
| "Enrich this IOC" | Cyber Sentinel (aggregated), VirusTotal | Shodan, AbuseIPDB |
| "Tell me about this threat actor" | Feedly, OpenCTI | MISP, Security Detections |
| "What CVEs are being actively exploited?" | Feedly, CISA KEV | VirusTotal, Security Detections |
| "Build detection content for these TTPs" | Security Detections | Feedly (for TTP context), OpenCTI |
| "Is this IP/domain malicious?" | Cyber Sentinel, VirusTotal | Shodan, AbuseIPDB |
| "What should I hunt for this week?" | Feedly, OpenCTI, CISA KEV | Security Detections |

When multiple sources are queried, synthesize results rather than presenting each source's output separately. Conflicting assessments between sources are valuable analytical signals — note them explicitly with confidence reasoning.

## Core workflows

### Workflow 1: Threat landscape briefing (/threat-brief)

Produce a situational awareness briefing tailored to the organization's sector, threat profile, and intelligence requirements. This is the proactive, "start of day" workflow.

1. **Gather current intelligence** using available MCP sources:
   - Query Feedly for trending threats, active campaigns, and newly exploited vulnerabilities relevant to the org's sector (from `security.local.md`)
   - Query OpenCTI for recent reports, newly tracked actors, and updated indicator sets
   - Query CISA KEV for newly added exploited vulnerabilities
   - Check sector ISAC feeds if available

2. **Filter for relevance.** Not everything matters to every org. Apply relevance filters based on `security.local.md`:
   - Sector targeting — Is this threat actor or campaign known to target our industry?
   - Technology overlap — Do we run the software, hardware, or services being targeted?
   - Geographic relevance — Does the threat target our operating regions?
   - TTP overlap — Do the techniques used align with gaps in our detection coverage?
   - Severity/impact threshold — Does this meet the minimum threshold for leadership attention?

3. **Synthesize into a briefing.** Structure the output for the intended audience:

```
## Threat Intelligence Briefing
**Period:** [date range, typically last 24-72 hours]
**Prepared for:** [org name / team]
**Classification:** [TLP marking per org policy]

### Priority Items
Items requiring attention or action from the security team.

**[PRIORITY-1] [Title — concise description of threat]**
- **Relevance:** [Why this matters to *this* organization specifically]
- **Threat actor/campaign:** [attribution if available, with confidence level]
- **Targeted sector(s):** [sectors affected]
- **TTPs observed:** [ATT&CK technique IDs and names]
- **IOCs:** [key indicators, if actionable for detection]
- **Recommended action:** [specific steps — check exposure, deploy detection, hunt, patch, monitor]
- **Sources:** [which intelligence sources reported this]

[Repeat for each priority item — aim for 3-5, not an exhaustive list]

### Vulnerability Exploitation Intelligence
Newly exploited vulnerabilities with active threat actor campaigns.

| CVE | Product | CVSS | Exploitation Status | Relevant to Us? | Action |
|-----|---------|------|-------------------|-----------------|--------|
| [CVE-ID] | [product] | [score] | [CISA KEV / active campaign / PoC available] | [Yes/No + reason] | [patch/mitigate/monitor] |

### Threat Landscape Summary
Broader trends and developments that inform strategic posture but don't require immediate action.

- [Trend 1: brief description with source]
- [Trend 2: brief description with source]
- [Trend 3: brief description with source]

### Intelligence Gaps
Questions we couldn't answer with available sources, or areas where confidence is low.

- [Gap 1: what we don't know and why it matters]
```

4. **Generate detection artifacts** where appropriate. For priority items with actionable TTPs, check Security Detections for existing rules. If coverage gaps exist, note them as recommendations for the detection engineering team.

### Workflow 2: IOC enrichment (/investigate support)

When presented with a specific indicator — IP address, domain, file hash, URL, email address — perform multi-source enrichment:

1. **Identify the indicator type** and select appropriate sources. Don't query sources that can't handle the indicator type (e.g., Shodan is for IPs, not file hashes).

2. **Query sources in parallel** where possible. Use Cyber Sentinel for aggregated lookups when available; fall back to individual source queries when needed.

3. **Synthesize results** into an enrichment summary:

```
## IOC Enrichment: [indicator value]
**Type:** [IP / Domain / Hash / URL / Email]
**Query time:** [timestamp]

### Verdict: [Malicious / Suspicious / Benign / Unknown]
**Confidence:** [High / Medium / Low]
**Basis:** [which sources agree/disagree and why]

### Reputation
| Source | Verdict | Detail |
|--------|---------|--------|
| [VirusTotal] | [malicious: 12/89 engines] | [detection names, first/last seen] |
| [AbuseIPDB] | [abuse confidence: 87%] | [report count, categories] |
| [Shodan] | [open ports: 22, 80, 443] | [services, OS, org, location] |

### Context
- **Associated campaigns:** [campaign names if attributed]
- **Associated threat actors:** [actor names with confidence]
- **Associated malware families:** [malware names]
- **ATT&CK techniques:** [if behavioral data available]
- **First seen / Last seen:** [earliest and latest observation dates across sources]
- **Related indicators:** [pivoted indicators — associated IPs, domains, hashes]

### Recommended Actions
1. [Specific action based on verdict — block, monitor, investigate further, dismiss]
2. [Additional context-dependent recommendation]
```

4. **Support pivoting.** If initial enrichment reveals related indicators (e.g., a malicious domain resolves to an IP that hosts other malicious domains), offer to enrich the related indicators. This is how a single IOC leads to a full infrastructure map.

### Workflow 3: Threat actor profiling

When asked about a specific threat actor or group:

1. **Query structured sources** — OpenCTI and Feedly for actor profiles, associated campaigns, known TTPs, targeting patterns, and attributed indicators.

2. **Build an actor profile:**

```
## Threat Actor Profile: [Actor Name]
**Also known as:** [aliases across naming conventions — Mandiant, CrowdStrike, Microsoft, etc.]
**Type:** [nation-state / cybercrime / hacktivist / unknown]
**Attribution confidence:** [confirmed / likely / possible / unattributed]
**Active since:** [first observed date]
**Last observed activity:** [most recent reported campaign]

### Targeting
- **Sectors:** [targeted industries]
- **Regions:** [geographic targets]
- **Motivation:** [espionage / financial / disruption / ideological]

### TTPs (MITRE ATT&CK)
| Tactic | Technique | Notes |
|--------|-----------|-------|
| [Initial Access] | [T1566 Phishing] | [specifics — spearphishing with macro-enabled docs] |
| [Execution] | [T1059.001 PowerShell] | [specifics] |
| ... | ... | ... |

### Recent Campaigns
- **[Campaign name]** ([date range]): [brief description, targets, outcome]
- **[Campaign name]** ([date range]): [brief description, targets, outcome]

### Relevance to [Organization]
[Assessment of whether this actor's targeting, TTPs, and motivation align with the org's threat profile — this is the judgment section]

### Detection Opportunities
[Specific detection recommendations based on the actor's known TTPs, referencing available detection rules from Security Detections where applicable]
```

### Workflow 4: Threat hunt hypothesis generation

When asked to support proactive threat hunting:

1. **Identify hunt basis** — What's driving this hunt? Options include:
   - TI-driven: New threat actor or campaign intelligence suggests possible undetected compromise
   - Gap-driven: ATT&CK coverage analysis reveals detection blind spots
   - Anomaly-driven: Unusual activity observed but not yet classified
   - Compliance-driven: Regulatory requirement to hunt for specific threat categories

2. **Generate hunt hypotheses** with supporting intelligence:

```
## Hunt Hypothesis: [concise hypothesis statement]
**Basis:** [TI report / ATT&CK gap / anomaly / regulatory]
**Priority:** [High / Medium / Low]
**Confidence that this TTP is relevant to us:** [High / Medium / Low — with reasoning]

### Intelligence Support
[What TI says about this threat — actor, campaign, sector targeting, frequency]

### What to look for
[Specific observable behaviors, log patterns, or artifacts]

### Data sources needed
[Which logs, tools, or telemetry to query]

### Sample queries
[SIEM/EDR queries where possible — KQL for Sentinel, SPL for Splunk, etc. Pull from Security Detections MCP if available]

### Expected results
- **If found:** [what it means, next steps, escalation path]
- **If not found:** [what that tells us — clean, insufficient visibility, or wrong hypothesis]
```

## Confidence and source assessment

Threat intelligence is only as good as its sourcing. Apply standard intelligence community confidence language:

- **High confidence:** Multiple independent, reliable sources with corroborating evidence. Technical indicators validated. Assessment unlikely to change with new information.
- **Medium confidence:** Some corroborating sources, but gaps exist. Plausible alternative explanations. Assessment could change with new information.
- **Low confidence:** Single source, or sources with limited reliability. Significant analytical assumptions. Assessment is preliminary.

When sources disagree, present both positions and explain the divergence. A VirusTotal verdict of "clean" combined with an OpenCTI association with a known campaign is more interesting than either data point alone — it could mean the indicator was recently weaponized and detection hasn't caught up, or it could mean a false positive in the TI correlation.

Never state attribution as fact unless multiple high-confidence sources agree. Default to hedged language: "associated with," "attributed by [source] to," "consistent with TTPs used by."

## Handling classification and sharing

Respect Traffic Light Protocol (TLP) markings on intelligence:
- **TLP:RED** — Named recipients only. Do not include in reports distributed beyond the named audience.
- **TLP:AMBER+STRICT** — Organization only. Do not share with external parties.
- **TLP:AMBER** — Organization and clients/customers on need-to-know.
- **TLP:GREEN** — Community-wide sharing permitted.
- **TLP:CLEAR** — No restrictions.

When synthesizing from multiple sources with different TLP levels, the output inherits the most restrictive marking. Note this in the report header.

## What this skill does NOT do

- Make attribution determinations independently — attribution is an analytical judgment that requires human assessment of source reliability, geopolitical context, and alternative explanations
- Access classified intelligence sources — this skill works with commercially and publicly available intelligence
- Replace a human threat intelligence analyst's judgment on what matters to the organization
- Guarantee completeness — threat intelligence is inherently incomplete, and emerging threats may not yet appear in any source
- Generate offensive tools, exploits, or attack capabilities — this skill is defensive-only
