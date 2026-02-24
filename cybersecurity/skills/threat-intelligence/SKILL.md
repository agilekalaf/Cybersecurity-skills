---
name: threat-intelligence
description: >
  Threat intelligence, threat hunting, IOC analysis, indicator enrichment, actor profiling,
  threat actor research, malware analysis, campaign tracking, CTI, cyber threat intelligence,
  threat landscape briefing, who is attacking us, attacker attribution, TTP analysis,
  MITRE ATT&CK mapping, threat feeds, vulnerability exploitation intelligence,
  "is this IP malicious", "who owns this domain", "what does this hash do",
  intelligence-driven detection, proactive threat hunting, threat hunt hypothesis.
---

# Threat Intelligence

This skill orchestrates threat intelligence workflows — from individual indicator enrichment to full
actor profiling, campaign tracking, and intelligence-driven threat hunt hypothesis generation. It is
designed to be heavily tool-connected: the more MCP connectors available, the richer the output.
It functions in degraded mode with no connections, relying on analyst-provided context and open sources.

> **Philosophy: People Led, AI Driven (PLAID)**
>
> Threat intelligence work requires judgment that tools alone cannot provide: understanding geopolitical
> context, distinguishing signal from noise in feeds, recognizing when an "indicator" is actually
> infrastructure shared across benign services, and deciding what's worth acting on. This skill
> accelerates the mechanical work — querying feeds, correlating indicators, structuring actor profiles —
> so analysts spend their time on interpretation and decision-making rather than data gathering.
> Attribution assessments are always stated with explicit confidence levels. Never treat AI-generated
> attribution as definitive without corroborating intelligence.

---

## Before You Begin

Load your `security.local.md` to calibrate this skill. Key fields used:

- **Industry sector** — focuses threat actor relevance (financial sector actors vs. energy sector vs. defense)
- **Tool stack / Threat Intelligence platforms** — routes queries to your deployed feeds
- **Geographic footprint** — filters geopolitical relevance
- **SIEM** — enables proactive threat hunting by pushing indicators into detection rules

If `security.local.md` is not available, indicate your industry and geographic region at the start of
the session for appropriately targeted intelligence.

---

## Roles This Skill Serves

**Primary:** Security Operations (threat intelligence analysts, threat hunters, SOC analysts)

**Also useful for:**
- Security Leadership: threat landscape briefings, executive summaries, board-level threat context
- Incident Response: IOC enrichment and actor attribution during active investigations
- Security Architecture: understanding attacker TTPs to validate defensive architecture
- Vulnerability Management: exploitation intelligence to prioritize patching

---

## Workflow 1: Indicator Enrichment

Use when you have one or more indicators (IP addresses, domains, URLs, file hashes, email addresses)
and need to determine their nature and disposition rapidly.

### Enrichment query sequence

When MCP tools are connected, run these queries in parallel per indicator type:

| Indicator Type | Primary sources | Secondary sources |
|---------------|-----------------|-------------------|
| IP address | VirusTotal, AbuseIPDB, Shodan | OpenCTI, internal SIEM |
| Domain / URL | VirusTotal, URLScan.io, Feedly | WHOIS, PassiveDNS, OpenCTI |
| File hash (MD5/SHA1/SHA256) | VirusTotal, MalwareBazaar | EDR telemetry, internal TI |
| Email address | Header analysis, domain reputation | Breach data (HaveIBeenPwned) |
| CVE / vulnerability | CISA KEV, NVD, Feedly exploit intel | Vendor advisories |

### Enrichment output template

```markdown
## Indicator Enrichment Report — [Date/Time UTC]

**Requested by:** [Analyst name or ticket reference]
**Context:** [Investigation ID, alert reference, or reason for query]

### Indicator Summary
| Indicator | Type | Disposition | Confidence | First seen | Last seen |
|-----------|------|-------------|------------|------------|-----------|
| [value] | [IP/Domain/Hash/Email] | [Malicious/Suspicious/Clean/Unknown] | [High/Med/Low] | [Date] | [Date] |

### Detail: [Indicator value]
**Reputation:** [Summary of reputation across sources]
**Associated malware/campaigns:** [If known]
**Threat actor association:** [If known, with confidence]
**Infrastructure context:** [Hosting provider, ASN, country, CDN/shared hosting flags]
**Detection coverage:** [Are your current detection rules catching this? Check SIEM]
**Recommended action:** [Block | Monitor | Investigate further | No action — explain]

### Source citations
| Source | Result | Retrieved |
|--------|--------|-----------|
| VirusTotal | [X/Y engines, last analysis date] | [timestamp] |
| AbuseIPDB | [Confidence score, report count] | [timestamp] |
| OpenCTI | [Associated objects] | [timestamp] |
| Feedly | [Related articles] | [timestamp] |
```

---

## Workflow 2: Threat Actor Profiling

Use when investigating a possible actor attribution, preparing threat landscape briefings,
or building threat hunt hypotheses based on actor TTPs.

### Actor profile template

```markdown
## Threat Actor Profile: [Actor name / alias]
**Profile date:** [Date]
**Confidence in attribution:** [High | Medium | Low | Speculative]

### Identity
| Field | Detail |
|-------|--------|
| Primary alias(es) | [e.g., APT29, Cozy Bear, Midnight Blizzard] |
| Nation-state sponsorship | [Country — with confidence level] |
| Motivation | [Espionage | Financial | Hacktivism | Disruption | Unknown] |
| Active since | [Approximate year] |
| Target sectors | [e.g., Government, Financial, Defense, Energy] |
| Target geographies | [e.g., US, Western Europe, Ukraine] |

### TTPs (MITRE ATT&CK)
| Tactic | Technique | Notes |
|--------|-----------|-------|
| Initial Access | [T-code: description] | [Actor-specific use] |
| Execution | [T-code: description] | |
| Persistence | [T-code: description] | |
| Defense Evasion | [T-code: description] | |
| Command & Control | [T-code: description] | |
| Exfiltration | [T-code: description] | |

### Known infrastructure (IOCs — may be stale)
[List with dates — flag that IOCs rotate frequently and age rapidly]

### Relevance to our organization
**Targeting relevance:** [High/Medium/Low — based on our sector and geography]
**Historical activity against similar orgs:** [Known incidents if public]
**Recommended defensive focus:** [Which TTPs to prioritize in detection engineering]

### Intelligence sources
[List public reports, vendor blogs, and platform references — do not reproduce verbatim]
```

---

## Workflow 3: Threat Hunt Hypothesis Generation

Use when preparing for a proactive threat hunt session. Takes actor TTPs or emerging threat
intelligence and converts them into testable hypotheses with suggested data sources and queries.

### Inputs

```
Actor / campaign:    [Actor name, CVE, or malware family — or describe threat scenario]
Hunt window:         [Timeframe to search, e.g., last 90 days]
Target environment:  [Scope — all endpoints, specific subnet, cloud, identity]
Known TTPs to focus: [Optional — specific techniques to prioritize]
```

### Hunt hypothesis template

```markdown
## Threat Hunt: [Hunt name] — [Date]

**Hypothesis:** If [actor/malware] has established a foothold in our environment,
we would expect to observe [specific behavior] in [specific data source].

**Priority:** [High | Medium | Low]
**Estimated effort:** [Hours or days]

### Hunt hypotheses

#### Hypothesis 1: [Short name]
- **Statement:** [Full hypothesis statement]
- **Data source:** [SIEM index, EDR telemetry, proxy logs, etc.]
- **Suggested query logic:** [Describe what to search — field names, values, patterns]
- **Expected volume:** [High/Medium/Low — to set analyst expectations]
- **True positive indicators:** [What a hit looks like]
- **False positive risks:** [Common benign activity that mimics this]

[Repeat for each hypothesis]

### Detection opportunities
[ATT&CK techniques identified in this hunt that don't have existing detection coverage —
feed into detection engineering backlog]
```

---

## Workflow 4: Daily Threat Brief

Use to produce a structured threat briefing for SOC morning standup or leadership consumption.
See also the `/threat-brief` command which invokes this workflow directly.

### Brief template

```markdown
## Threat Brief — [Date]

**Prepared for:** [SOC | Security Leadership | Board]
**Period:** [Last 24 hours | Last 7 days]

### Today's top threats (sector-relevant)
1. [Threat/campaign name] — [2-sentence summary] — **Relevance: High/Med/Low**
2. [Threat/campaign name] — [summary] — **Relevance: High/Med/Low**
3. [Threat/campaign name] — [summary] — **Relevance: High/Med/Low**

### Vulnerabilities under active exploitation
| CVE | CVSS | CISA KEV? | Description | Our exposure |
|-----|------|-----------|-------------|--------------|
| [CVE-XXXX-XXXXX] | [X.X] | [Yes/No] | [Brief description] | [Exposed/Not exposed/Unknown] |

### Newly observed indicators (sector-relevant, last 24h)
[IP ranges, domains, campaigns to add to watchlists — flag as actionable]

### Intelligence collection priorities
[What to watch for in coming period]
```

---

## Working with Tools

### MCP connectors this skill uses

| Connector | Used for | Priority |
|-----------|----------|----------|
| **Feedly** | Threat intelligence feeds, actor tracking, news ingestion | High — enables most workflows |
| **OpenCTI** | Structured threat actor data, IOC correlation, STIX/TAXII | High — primary TI platform |
| **VirusTotal** | Indicator reputation, malware identification, passive DNS | High — essential for enrichment |
| **AbuseIPDB** | IP reputation, abuse reports | Medium — supplements VirusTotal |
| **Shodan** | Internet exposure data for IPs, service fingerprinting | Medium — infrastructure context |
| **CISA KEV** | Confirmed exploitation status for vulnerabilities | High — free, authoritative |
| **Cyber Sentinel** | Integrated threat intelligence and analysis | Medium — if deployed |
| **SIEM** | Indicator correlation against internal telemetry, hunt query execution | High for hunting workflows |

### Graceful degradation

Without MCP connectors, provide raw indicator values and the skill will:
- Structure the enrichment template for manual population
- Suggest specific free web tools for each indicator type (VirusTotal web, URLScan, AbuseIPDB web)
- Generate hunt hypotheses using ATT&CK TTP descriptions for manual query translation

---

## What This Skill Does NOT Do

- **Does not provide definitive attribution.** Actor attribution at speed without corroborating intelligence is speculation. Confidence levels are always stated explicitly.
- **Does not replace a human TI analyst.** Context interpretation, source evaluation, and strategic intelligence assessment require practitioner judgment.
- **Does not reproduce or scrape proprietary threat reports.** It synthesizes and references; it does not republish vendor-proprietary intelligence.
- **Does not perform active scanning or reconnaissance.** It queries threat intelligence sources, not target infrastructure.
- **Does not generate detection rules autonomously.** It generates hunt hypotheses and suggests query logic; detection engineers translate these into production rules with validation.
- **Does not cover classified intelligence.** This skill operates on commercially available and open-source intelligence only.
