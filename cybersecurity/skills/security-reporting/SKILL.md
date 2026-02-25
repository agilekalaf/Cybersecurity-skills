---
name: security-reporting
description: >
  Security reporting, board reporting, CISO report, executive security report, security dashboard,
  KPI reporting, security metrics, OKR tracking, security program report, monthly security report,
  quarterly security review, board presentation, ELT security briefing, security scorecard,
  NIST CSF maturity report, security posture report, "report for the board", "prepare security metrics",
  "executive security summary", program status report, security KPIs, incident metrics,
  vulnerability metrics, compliance metrics, security ROI, risk reporting for leadership.
---

# Security Reporting

This skill produces audience-appropriate security reports — from SOC operational dashboards to
board-level risk briefings. It aggregates data from other skills' outputs and connected tool sources,
generates KPI scorecards, tracks OKR progress, and translates technical security metrics into
business-relevant narratives. Every audience gets the right level of detail: boards see risk and
investment, ELTs see program health and resource status, operations teams see metrics and trends.

> **Philosophy: People Led, AI Driven (PLAID)**
>
> Security reporting is where technical security work becomes visible to the organization's leaders
> and stakeholders. The words and numbers in a board report carry the CISO's credibility. This skill
> handles the aggregation, structuring, and drafting of security reports — but the CISO or security
> leader who presents or publishes a report takes ownership of its accuracy and framing. AI-generated
> draft reports must be reviewed against actual data sources before publication. Never publish a
> report with AI-generated numbers you haven't verified. The draft is a starting point, not a
> finished product.

---

## Before You Begin

Load your `security.local.md` to calibrate this skill. Key fields used:

- **Board and ELT reporting cadence** — calibrates report structure and period
- **Key metrics tracked** — determines which KPIs to include and their targets
- **Board-level risk indicators** — focuses board reports on what your board has asked to see
- **Active compliance frameworks** — includes relevant maturity and compliance status
- **Incident SLAs** — populates MTTD/MTTR metrics against your defined targets

---

## Roles This Skill Serves

**Primary:** Security Leadership (CISO, Deputy CISO, Security Directors)

**Also useful for:**
- GRC: compliance posture sections and framework maturity reporting
- Security Operations: operational metric aggregation and trend analysis
- Security Architecture: program health and investment reporting

---

## Workflow 1: Board Security Report

Use quarterly (or per your board reporting cadence) to produce a board-level security briefing.
Board audiences want business risk framing, not technical detail.

### Board report template

```markdown
# Cybersecurity Program Report — Board of Directors
**Period:** [Q1 2025 | Month Year]
**Prepared by:** [CISO Name]
**Classification:** Board Confidential

---

## Executive Summary
[3-5 sentences: current threat environment, program health, top risk, and key ask or decision
if applicable. Write in plain English — no acronyms, no jargon. Answer "are we secure enough?"
with honest nuance: "We are materially better than last year in X. Our most significant exposure
remains Y, which we are addressing through Z."]

---

## Threat Environment
[2-3 sentences on the relevant threat landscape — what's targeting our sector, any major industry
incidents in the period that are relevant to our risk profile. Reference threat-brief output.]

**Our threat level this period:** [Elevated / Normal / Declining] vs. prior period

---

## Security Program Health

| Metric | This period | Prior period | Target | Status |
|--------|------------|-------------|--------|--------|
| Mean Time to Detect (MTTD) | [X hrs] | [Y hrs] | [<Z hrs] | [On target / At risk / Missed] |
| Mean Time to Respond (MTTR) | [X hrs] | [Y hrs] | [<Z hrs] | [On target] |
| Critical vuln remediation SLA | [X%] | [Y%] | [>Z%] | |
| Security training completion | [X%] | [Y%] | [>Z%] | |
| Phishing simulation click rate | [X%] | [Y%] | [<Z%] | |
| MFA coverage | [X%] | [Y%] | [100%] | |

**Overall program health:** [Green / Amber / Red]

---

## Top Risks

### Risk 1: [Risk name]
**Status:** [Increasing / Stable / Decreasing]
[2-3 sentences: what the risk is, what's being done, what the board should know]

### Risk 2: [Risk name]
[Same structure]

### Risk 3: [Risk name]
[Same structure]

---

## Significant Events This Period
[Major incidents, near-misses, or security events worth board awareness — with business impact
framing, not technical detail. If no significant events: "No material security incidents this period."]

---

## Compliance Posture
| Framework | Status | Key action |
|-----------|--------|-----------|
| [NIST CSF 2.0] | [Tier 3 — on track for Tier 3.5 by Q4] | [Control area in progress] |
| [SOC 2 Type II] | [Audit window: [dates] — preparation on track] | [Evidence collection in progress] |

---

## Investment and Resources
[1 paragraph or table: any significant investment decisions, resource constraints, or asks for the board.
Frame in business terms: "the $X investment in Y reduces Z risk by W%."]

---

## Decisions Required
[If any board decision or approval is needed — otherwise "No board decisions required this period."]

---

*Prepared with AI-assisted drafting. All data verified by [CISO name] before publication.*
```

---

## Workflow 2: ELT / Leadership Security Briefing

Use monthly (or per cadence) for executive leadership team briefings. More operational detail than
board reports; still business-framed.

### ELT briefing template

```markdown
# Monthly Security Briefing — Executive Leadership Team
**Period:** [Month Year]
**Prepared by:** [CISO Name / Security team]

## This Month's Highlights
- [Bullet: significant positive development]
- [Bullet: risk or issue requiring ELT awareness]
- [Bullet: program milestone achieved or upcoming]

## Security Operations Metrics
| Metric | This month | Last month | 3-month trend | Target |
|--------|-----------|-----------|---------------|--------|
| Security alerts processed | [N] | [N] | [↑/→/↓] | |
| Confirmed incidents | [N] | [N] | | |
| MTTD | [X hrs] | [Y hrs] | | [Target] |
| MTTR | [X hrs] | [Y hrs] | | [Target] |
| Phishing reports from users | [N] | [N] | | |

## Vulnerability Status
| Priority | Open | Overdue SLA | % within SLA |
|----------|------|-------------|--------------|
| Critical | [N] | [N] | [%] |
| High | [N] | [N] | [%] |

## Top Action Items (Next 30 Days)
| Action | Owner | Due | Status |
|--------|-------|-----|--------|
| [Action] | [Team] | [Date] | [On track / At risk] |

## Requests for Business Leaders
[Any specific asks of ELT members — supporting security initiatives, awareness messages, approvals]
```

---

## Workflow 3: KPI / OKR Scorecard

Use to track security program objectives and key results against targets.

### Security OKR scorecard template

```markdown
## Security Program OKR Scorecard
**Period:** [Quarter/Year]

### Objective 1: [e.g., Achieve Tier 3 maturity across all NIST CSF functions]
| Key Result | Target | Current | % Complete | Status |
|------------|--------|---------|-----------|--------|
| [Achieve Tier 3 in Govern function] | [Q2 2025] | [Tier 2.5] | [75%] | [On track] |
| [KR 2] | | | | |

### Objective 2: [e.g., Reduce critical vulnerability remediation time by 40%]
| Key Result | Target | Current | % Complete | Status |
|------------|--------|---------|-----------|--------|
| [Reduce MTTR for Critical CVEs from X to Y days] | [Y days] | [Z days] | [%] | |

[Repeat for each objective]

### Overall program health: [Green / Amber / Red]
[One-paragraph narrative on progress toward annual objectives]
```

---

## Working with Tools

### MCP connectors this skill uses

| Connector | Used for | Priority |
|-----------|----------|----------|
| **GRC Platform** | Compliance posture, risk register summary | High |
| **SIEM** | Operational metrics: alert volumes, MTTD, incident counts | High |
| **Vulnerability Scanner** | Vulnerability metrics: open counts, SLA compliance | High |
| **Identity Platform** | MFA coverage, access review completion | Medium |
| **Ticketing** | Incident and vulnerability tracking metrics | Medium |
| **Documentation** | Publishing reports to SharePoint/Confluence | Medium |

### Data aggregation without MCP connections

Without tool connectivity, the skill produces report templates with clearly marked data fields.
Provide metric values manually and the skill will produce the narrative, trend analysis, and
audience-appropriate framing.

---

## What This Skill Does NOT Do

- **Does not generate accurate metrics from no data.** It structures reports and produces templates; actual metric values must come from tools or manual input.
- **Does not replace the CISO's voice.** Board and executive reports must reflect the CISO's own assessment and language — AI drafts should be substantially rewritten to sound like the leader presenting them.
- **Does not produce legally required regulatory filings.** SEC cybersecurity disclosure filings, HIPAA breach notifications, and similar regulatory submissions require legal review.
- **Does not make investment recommendations.** Budget framing in reports is illustrative; security investment decisions require business case analysis and human judgment.
- **Does not benchmark against industry peers.** It can reference general benchmark ranges if provided, but authoritative benchmarking requires industry data sources.
- **Does not track individual employee metrics.** This skill focuses on program-level data, not individual performance.
