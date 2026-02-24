# /investigate

Deep-dive investigation of a specific indicator, IP address, domain, file hash, threat actor,
or suspicious activity pattern. Runs full IOC enrichment across all connected threat intelligence
sources and correlates against internal telemetry.

## Usage

```
/investigate 203.0.113.47
/investigate malicious-domain.example.com
/investigate d41d8cd98f00b204e9800998ecf8427e
/investigate "APT29" --type actor
/investigate --source siem "unusual outbound connections from finance subnet"
/investigate CVE-2024-12345 --type vulnerability
```

## What This Command Does

Invokes the threat-intelligence skill (Workflow 1: Indicator Enrichment and Workflow 2: Actor
Profiling) to run a comprehensive investigation. For indicators: queries all connected TI platforms
in parallel, correlates against SIEM telemetry, and produces a structured enrichment report with
disposition and recommended action. For actors: builds a full profile with TTPs, infrastructure,
and targeting assessment. For vulnerabilities: provides exploitation status, affected versions,
and exposure assessment.

## Parameters

| Parameter | Values | Default |
|-----------|--------|---------|
| `--type` | `indicator`, `actor`, `vulnerability`, `auto` | `auto` (inferred) |
| `--source` | `siem`, `edr`, `user-report`, `external` | Not set |
| `--depth` | `quick`, `full` | `full` |
| `--format` | `report`, `tlp-white`, `stix` | `report` |
| `--add-to-watchlist` | Flag — no value | Not set |

## Workflow

1. Parse input to determine indicator type (IP, domain, hash, CVE, actor name, or free text)
2. Load `security.local.md` for tool stack and sector context
3. Run parallel enrichment queries across connected platforms:
   - VirusTotal: reputation, passive DNS, related samples
   - AbuseIPDB: abuse reports and confidence score (for IPs)
   - Shodan: service exposure and banner data (for IPs)
   - OpenCTI: related threat actors, campaigns, and TTOs
   - Feedly: recent intelligence articles referencing this indicator
   - SIEM: internal observations — has this indicator appeared in our environment?
   - CISA KEV: exploitation status (for CVEs)
4. Synthesize findings into enrichment report with disposition assessment
5. If `--add-to-watchlist` is set, prepare indicator for SIEM/TI platform ingestion
6. Generate recommended actions with explicit analyst decision points

## Output

**Standard report includes:**
- Indicator summary with disposition (Malicious / Suspicious / Clean / Unknown)
- Source-by-source findings with timestamps
- Associated threat actors and campaigns
- Infrastructure context (hosting, ASN, country, CDN/shared flags)
- Internal exposure: has this been observed in our environment?
- Recommended action with rationale
- Raw IOC data formatted for watchlist/SIEM ingestion

**Actor investigation additionally includes:**
- Full actor profile (see threat-intelligence skill Workflow 2)
- TTP mapping to MITRE ATT&CK
- Relevance assessment for your sector and geography
- Hunt hypotheses derived from actor TTPs

## When to Use This

- **During incident triage:** Enrich indicators pulled from an active alert before deciding severity
- **After a threat-brief flags something:** Drill into a specific actor, campaign, or CVE
- **Routine IOC investigation:** Analyst-submitted IPs/domains/hashes requiring disposition
- **Threat hunting preparation:** Profile an actor before designing a hunt
- **Vendor/partner risk:** Investigate an IP or domain associated with a third party
- **Vulnerability context:** Understand if a CVE is being actively exploited before emergency patching

## Dependencies

**Recommended (in priority order):**
1. VirusTotal — core reputation data for all indicator types
2. SIEM — internal correlation (critical for determining actual exposure)
3. OpenCTI — structured actor and campaign data
4. AbuseIPDB — IP-specific abuse reputation
5. Feedly — recent intelligence articles

**Minimal mode:** Provide raw indicator value; the command generates an investigation template
with instructions for manual enrichment via free web tools. Output will note what each source
would have added if connected.

## Related

- **Skill:** `skills/threat-intelligence/SKILL.md` (Workflows 1 and 2)
- **Command:** `/threat-brief` — for broad landscape briefing before drilling into specifics
- **Command:** `/triage-alert` — when an investigation reveals an active incident
- **Skill:** `skills/incident-response/SKILL.md` — when investigation transitions to IR
