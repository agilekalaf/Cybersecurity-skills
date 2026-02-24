# /threat-brief

Generate a structured threat intelligence briefing for your organization's sector and geography,
pulling current threat actor activity, actively exploited vulnerabilities, and emerging campaigns.

## Usage

```
/threat-brief
/threat-brief --audience soc
/threat-brief --audience leadership --period weekly
/threat-brief --sector financial-services --region north-america
/threat-brief --focus ransomware
```

## What This Command Does

Invokes the threat-intelligence skill (Workflow 4: Daily Threat Brief) to produce a structured
briefing covering current threat actor activity, actively exploited CVEs, and sector-relevant
campaigns. Output is calibrated to the audience — technical detail for SOC, strategic framing for
leadership. Sector and region default to values in `security.local.md` if not specified.

## Parameters

| Parameter | Values | Default |
|-----------|--------|---------|
| `--audience` | `soc`, `leadership`, `board` | `soc` |
| `--period` | `daily`, `weekly`, `monthly` | `daily` |
| `--sector` | Industry sector name | From `security.local.md` |
| `--region` | `north-america`, `emea`, `apac`, `global` | From `security.local.md` |
| `--focus` | `ransomware`, `nation-state`, `phishing`, `vulnerabilities`, `all` | `all` |

## Workflow

1. Load `security.local.md` for sector, region, and tool configuration
2. Query Feedly and OpenCTI for sector-relevant threat activity in the specified period
3. Pull CISA KEV for newly added exploited vulnerabilities
4. Query VirusTotal and threat intelligence platforms for active campaigns
5. Synthesize into the threat-intelligence skill's Brief Template
6. Format output for the specified audience

## Output

**For `--audience soc`:**
- Top 3-5 active threats with technical IOCs and ATT&CK technique references
- Newly exploited CVEs relevant to your tool stack
- Indicators to add to watchlists
- Hunt hypotheses for highest-priority threats

**For `--audience leadership`:**
- 1-paragraph executive summary of the threat environment
- Risk-framed description of top threats (business impact language)
- Recommended actions at program level
- No raw IOCs or technical detail

**For `--audience board`:**
- 3-5 bullet strategic summary
- Comparison to prior period ("threat level trending up/stable/down")
- Single recommended decision or awareness item

## When to Use This

- **SOC morning standup:** Daily briefing to orient the team before shift
- **Weekly leadership update:** Threat context for security leadership review
- **After a major industry incident:** "What does [recent major breach] mean for us?"
- **Board meeting prep:** Threat landscape slide background
- **New intelligence triggers:** When a significant new threat emerges requiring rapid assessment

## Dependencies

**Required:** At least one of: Feedly, OpenCTI, or CISA KEV access (free, no MCP required for KEV)

**Recommended:** Feedly + OpenCTI + VirusTotal for full workflow. CISA KEV integration for
vulnerability exploitation status.

**Minimal mode:** Without MCP connections, the command generates a template and asks the analyst
to populate it from manual sources, with structured guidance on what to look for.

## Related

- **Skill:** `skills/threat-intelligence/SKILL.md` (Workflow 4 — this command is a direct entry point)
- **Command:** `/investigate` — for deep-dive investigation of a specific indicator or actor
- **Command:** `/triage-alert` — for operational response when a threat becomes an incident
