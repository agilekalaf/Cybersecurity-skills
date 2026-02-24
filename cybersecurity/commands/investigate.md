# /investigate

Deep-dive investigation on a specific indicator of compromise, threat actor, incident, or anomaly.

## Usage

```
/investigate 185.220.101.45
/investigate abc123def456...  (file hash)
/investigate evil-domain.com
/investigate --actor APT29
/investigate --campaign Scattered Spider
/investigate --cve CVE-2024-3400
```

## What this command does

This command takes a specific indicator, entity, or reference point and performs comprehensive multi-source investigation — enrichment, correlation, context gathering, and pivoting to related indicators. It's the reactive counterpart to `/threat-brief`: where threat-brief asks "what should I know today," investigate asks "tell me everything about this specific thing."

## Parameters

The primary input is the indicator or entity to investigate. The command auto-detects indicator type:

- **IP address:** Reputation, geolocation, ASN, open ports, associated domains, abuse reports, campaign associations
- **Domain/hostname:** Reputation, WHOIS, DNS history, associated IPs, malware associations, categorization
- **File hash (MD5/SHA1/SHA256):** Detection ratios, behavioral analysis, malware family, campaign associations, related samples
- **URL:** Reputation, redirect chain, hosted content analysis, associated infrastructure
- **Email address:** Reputation, associated domains, breach history, campaign usage

Named entity flags:
- **--actor [name]:** Threat actor deep profile — aliases, TTPs, campaigns, targeting, infrastructure patterns
- **--campaign [name]:** Campaign analysis — timeline, targets, TTPs, IOCs, attribution
- **--cve [CVE-ID]:** Vulnerability threat context — who's exploiting it, with what malware, targeting what sectors, exploit availability

Optional modifiers:
- **--depth:** How far to pivot from the initial indicator. `shallow` (direct enrichment only), `standard` (one level of pivoting), `deep` (full infrastructure mapping). Default: `standard`.
- **--output:** Format preference. `summary` (quick verdict), `full` (complete report), `iocs` (indicator list for blocking/detection). Default: `full`.

## Workflow

1. **Parse and classify the input** — identify indicator type or entity class.

2. **Select appropriate intelligence sources** using the threat-intelligence skill's tool selection logic. Not every source applies to every indicator type.

3. **Execute primary enrichment** — query all relevant sources for direct intelligence on the indicator.

4. **Correlate results** — synthesize across sources. Flag agreements (high confidence) and disagreements (analytical interest). Identify associated campaigns, actors, and malware families.

5. **Pivot to related indicators** (if depth allows) — follow relationships to associated infrastructure. An IP resolving to a domain that hosts a known C2 panel tells a story that the IP alone doesn't.

6. **Map to ATT&CK** — if behavioral data is available, map observed techniques to the ATT&CK framework.

7. **Generate actionable output** — enrichment summary, verdict with confidence, recommended actions, and detection content where applicable.

## Output

Varies by input type but always includes:
- **Verdict** with confidence level and multi-source basis
- **Enrichment detail** from each responding source
- **Context** — campaigns, actors, malware families, related indicators
- **ATT&CK mapping** where behavioral data exists
- **Recommended actions** — block, monitor, hunt, investigate further, or dismiss
- **Pivot opportunities** — related indicators worth investigating

For `--actor` and `--campaign` investigations, output includes full profiles as defined in the threat-intelligence skill's actor profiling and campaign analysis workflows.

For `--cve` investigations, output includes exploitation status, threat actor usage, malware leveraging the vulnerability, affected products, patch status, and compensating controls.

## When to use this

- During alert triage — enrich indicators from a SIEM alert before deciding on escalation
- During incident response — build context on adversary infrastructure and TTPs
- Proactive hunting — investigate a suspicious indicator found during a hunt
- Vulnerability prioritization — understand whether a CVE is being actively exploited and by whom
- Peer intelligence — a sector partner shares indicators; investigate before ingesting into your environment

## Dependencies

**Required:** At least one IOC enrichment source connected via MCP (VirusTotal, Cyber Sentinel, or equivalent).

**Recommended:** Cyber Sentinel (aggregated enrichment) + Feedly (campaign/actor context) + OpenCTI (structured relationships) + Shodan (infrastructure) + Security Detections (detection rules for observed TTPs).

## Related

- `/threat-brief` — Proactive situational awareness (strategic, broad)
- `/triage-alert` — Quick alert assessment (references investigate for deep-dive)
- `threat-intelligence` skill — The domain knowledge powering this command
- `incident-response` skill — Investigation phase workflow that calls on this command's outputs
