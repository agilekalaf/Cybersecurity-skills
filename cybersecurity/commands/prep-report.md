# /prep-report

Prepare an audience-appropriate security report — board briefing, ELT update, or operational
dashboard narrative — by aggregating data from other skills' outputs and connected tool sources.

## Usage

```
/prep-report --audience board --period quarterly
/prep-report --audience elt --period monthly
/prep-report --audience board --focus compliance
/prep-report --audience elt --focus incidents,vulnerabilities
/prep-report --audience board --period quarterly --focus all
/prep-report --audience operational --period weekly
```

## What This Command Does

Invokes the security-reporting skill to produce a draft security report calibrated to the specified
audience. Pulls metric data from connected tool sources (SIEM, vulnerability scanner, GRC platform)
and structures the report using the templates appropriate for the audience: board (risk framing,
strategic context), ELT (program health, resource status), or operational (metrics, trends,
action items). All drafts require human review and metric validation before publication.

## Parameters

| Parameter | Values | Default |
|-----------|--------|---------|
| `--audience` | `board`, `elt`, `operational` | Required |
| `--period` | `weekly`, `monthly`, `quarterly`, `annual` | `monthly` |
| `--focus` | `compliance`, `incidents`, `risk`, `vulnerabilities`, `program`, `all` | `all` |
| `--compare` | Prior period date for trend analysis | Auto (prior period) |
| `--format` | `narrative`, `slides`, `data` | `narrative` |

## Workflow

1. Load `security.local.md` for reporting cadence, KPI targets, board-level risk indicators
2. Pull operational metrics from connected sources:
   - SIEM: alert volumes, MTTD, incident counts for the period
   - Vulnerability scanner: open count, SLA compliance, remediation rate
   - GRC platform: compliance maturity, risk register summary, open findings
   - Identity: MFA coverage, access review completion
3. Load relevant skill outputs from the period (compliance assessments, risk assessments, incident reports)
4. Generate audience-appropriate draft:
   - Board: executive narrative, risk framing, top metrics, decisions required
   - ELT: program health, metrics with trend, top action items, resource status
   - Operational: full metrics dashboard, KPI scorecard, team workload
5. Flag any metrics that could not be pulled automatically for manual population

## Output

**`--audience board`:**
- Executive summary paragraph (state of security in plain English)
- Threat environment context
- Program health scorecard (5-8 metrics with traffic lights)
- Top 3 risks with narrative
- Significant events summary
- Compliance posture snapshot
- Decisions required section (or "none required this period")
- AI-assistance disclosure line

**`--audience elt`:**
- Monthly highlights (3 bullets: win, concern, milestone)
- Operations metrics table with trends
- Vulnerability status summary
- Top action items with owners and dates
- Requests for business leaders

**`--audience operational`:**
- Full metrics dashboard data
- KPI/OKR scorecard vs. targets
- Team workload and capacity indicators
- 30-day action list

**With `--format slides`:**
- Output structured as slide-ready bullet points and table data

## When to Use This

- **Before board meeting:** Quarterly board cybersecurity briefing preparation
- **Monthly leadership cycle:** ELT security update for leadership team meeting
- **SOC weekly review:** Operational metrics and trend report for team standup
- **Annual report:** Annual security program summary for board or audit committee
- **Incident aftermath:** Special report following a significant security event
- **Budget season:** Annual program performance report to support budget request

## Dependencies

**Minimal (no MCP):** Produces fully structured templates with all data fields marked for manual
population. Most useful workflow: run the command, then populate metrics from tool UIs.

**Recommended for automated metric pull:**
1. SIEM — operational metrics
2. Vulnerability Scanner — vulnerability metrics
3. GRC Platform — compliance and risk data
4. Identity Platform — access metrics

## Related

- **Skill:** `skills/security-reporting/SKILL.md` (full documentation and all report templates)
- **Command:** `/assess-compliance` — compliance scorecard feeds board and ELT reports
- **Command:** `/assess-risk` — risk register summary feeds board risk section
- **Skill:** `skills/incident-response/SKILL.md` — incident metrics and summaries for reporting
