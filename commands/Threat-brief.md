# /threat-brief

Generate a threat intelligence briefing tailored to your organization's sector, threat profile, and intelligence requirements.

## Usage

```
/threat-brief
/threat-brief --sector utilities --period 24h
/threat-brief --focus ransomware
/threat-brief --focus apt --sector energy
/threat-brief --cve-only
```

## What this command does

This command produces a situational awareness briefing by querying your connected threat intelligence sources, filtering for relevance to your organization, and synthesizing the results into an actionable format. Think of it as your AI-augmented intelligence analyst doing the morning brief.

## Parameters

- **--sector:** Override the sector from `security.local.md`. Useful when preparing briefings for peer organizations or sector partners.
- **--period:** Time window for intelligence gathering. Default: 72 hours. Options: `24h`, `48h`, `72h`, `7d`, `30d`.
- **--focus:** Narrow the briefing to a specific threat category. Options: `ransomware`, `apt`, `vulnerability`, `insider`, `supply-chain`, `sector` (sector-specific threats only).
- **--cve-only:** Produce only the vulnerability exploitation intelligence section — quick view of what's being actively exploited.
- **--audience:** Tailor depth and language. Options: `soc` (technical, detection-focused), `leadership` (business impact, strategic), `full` (comprehensive). Default: `full`.

## Workflow

1. **Load organizational context** from `security.local.md` — sector, critical assets, intelligence requirements, tool stack.

2. **Query connected intelligence sources** using the threat-intelligence skill:
   - Feedly Threat Graph for trending threats and campaigns
   - OpenCTI for structured threat data and recent reports
   - CISA KEV for newly exploited vulnerabilities
   - Sector ISAC feeds if configured
   - MISP for community-sourced indicators

3. **Filter for organizational relevance** — sector targeting, technology overlap, geographic relevance, TTP overlap with detection gaps, severity threshold.

4. **Synthesize into briefing format** appropriate for the audience parameter.

5. **Generate detection recommendations** — for priority items, check Security Detections for existing rules covering the observed TTPs and flag coverage gaps.

## Output

A structured briefing containing:
- **Priority items** (3-5) requiring team attention or action, with relevance justification and recommended actions
- **Vulnerability exploitation intelligence** table with CVEs actively being weaponized
- **Threat landscape summary** of broader trends
- **Intelligence gaps** where available sources couldn't answer key questions
- **Detection artifacts** where actionable TTPs map to deployable rules

## When to use this

- Start of shift / start of day — get situational awareness before diving into the queue
- Preparing for leadership briefings — generate the raw intelligence, then tailor for your audience
- After a major industry event — quickly assess whether a newly reported campaign or vulnerability affects your environment
- Weekly threat review meetings — produce the standing briefing that grounds the discussion

## Dependencies

**Required:** At least one strategic intelligence source connected via MCP (Feedly or OpenCTI).

**Recommended:** Feedly + OpenCTI + CISA KEV + Security Detections for a complete briefing. The command degrades gracefully — fewer sources means a less comprehensive briefing, but it will work with whatever is available and note the gaps.

## Related

- `/investigate` — Deep-dive on a specific IOC, actor, or incident (reactive, specific)
- `threat-intelligence` skill — The domain knowledge that powers this command
- `incident-response` skill — Consumes TI during active incident investigation
- `security-reporting` skill — Can incorporate threat briefings into leadership reports
