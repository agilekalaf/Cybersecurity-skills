---
name: compliance-assessment
description: >
  Compliance assessment, framework assessment, maturity assessment, gap analysis, control assessment,
  NIST CSF assessment, ISO 27001 gap analysis, SOC 2 readiness, CMMC assessment, NERC CIP compliance,
  NIST 800-53 assessment, security maturity model, compliance gap, where are we against the framework,
  audit readiness, compliance posture, control mapping, remediation roadmap, compliance scoring,
  "how mature are we", "are we compliant", compliance program review, framework-based evaluation.
---

# Compliance Assessment

This skill executes framework-based security maturity assessments, gap analyses, and remediation
roadmaps against one or more compliance frameworks. It dynamically loads the relevant framework
module(s) from `frameworks/` based on your configured frameworks, evaluates current-state controls,
scores maturity, and generates prioritized remediation plans. It supports multi-framework assessments
for organizations that operate under simultaneous regulatory obligations.

> **Philosophy: People Led, AI Driven (PLAID)**
>
> Compliance assessments are high-stakes documents — they inform board reporting, regulatory filings,
> and multi-year investment decisions. This skill accelerates the mechanical work of mapping controls,
> scoring maturity, and structuring output, but every maturity rating requires human validation
> against actual evidence. An AI-generated score is a hypothesis, not an audit finding. Security
> leaders sign off on assessment results; they do not delegate that responsibility to an AI system.
> Use this skill to do the drafting; use your judgment and evidence to determine the final score.

---

## Before You Begin

Load your `security.local.md` to calibrate the assessment. Key fields used:

- **Active compliance frameworks** — determines which framework modules to load from `frameworks/`
- **Current maturity target** — sets the baseline for gap analysis (where we are vs. where we need to be)
- **Next major audit** — calibrates urgency and prioritization of remediation items
- **Tool stack** — informs control evidence availability
- **Risk appetite** — influences remediation prioritization

This skill will load the appropriate framework module(s) automatically:
- `frameworks/nist-csf-2.0.md` for NIST CSF 2.0
- `frameworks/nist-800-53.md` for NIST SP 800-53 Rev 5
- `frameworks/iso-27001.md` for ISO/IEC 27001:2022
- `frameworks/nerc-cip.md` for NERC CIP
- `frameworks/cmmc.md` for CMMC 2.0
- `frameworks/soc2.md` for SOC 2

---

## Roles This Skill Serves

**Primary:** GRC (compliance analysts, framework assessors), Security Leadership

**Also useful for:**
- Security Architecture: control implementation guidance and technical control mapping
- Security Operations: understanding operational control requirements
- Audit Support: feeds directly into audit-support skill evidence collection

---

## Workflow 1: Maturity Scorecard

Use to generate a current-state maturity score across framework functions or control domains.
Best for executive reporting and board presentations.

### Inputs for maturity assessment

```
Framework(s):      [nist-csf-2.0 | nist-800-53 | iso-27001 | nerc-cip | cmmc | soc2 | multiple]
Scope:             [Full organization | Specific business unit | Specific system | Cloud environment]
Assessment basis:  [Self-assessment | Prior audit findings | Evidence review | Workshop facilitation]
Assessment date:   [Date — maturity is point-in-time]
Prior assessment:  [Date and score of last assessment, if available — enables trend analysis]
```

### Maturity scorecard template

```markdown
## Security Maturity Scorecard: [Framework Name]
**Organization:** [Name or scope]
**Assessment date:** [Date]
**Assessor:** [Name / Role — human validation required]
**Methodology:** [Self-assessment | Third-party | Evidence-based]

### Overall Maturity: [Tier/Level/Rating]
[One-paragraph narrative of overall security posture]

### Function / Domain Scores

#### NIST CSF 2.0 (example — adapt for other frameworks)
| Function | Current Tier | Target Tier | Score | Trend |
|----------|-------------|-------------|-------|-------|
| Govern (GV) | [1-4] | [1-4] | [%] | [↑/→/↓] |
| Identify (ID) | [1-4] | [1-4] | [%] | |
| Protect (PR) | [1-4] | [1-4] | [%] | |
| Detect (DE) | [1-4] | [1-4] | [%] | |
| Respond (RS) | [1-4] | [1-4] | [%] | |
| Recover (RC) | [1-4] | [1-4] | [%] | |
| **Overall** | **[1-4]** | **[1-4]** | **[%]** | |

### Maturity level definitions
*(Loaded from the applicable framework module in `frameworks/`)*

### Key strengths
- [Control area performing well — with evidence basis]
- [Control area performing well]

### Critical gaps requiring immediate attention
- [Gap with highest risk/compliance impact]
- [Gap with regulatory consequence]
```

---

## Workflow 2: Gap Analysis

Use to produce a structured list of control gaps against framework requirements, with risk ratings
and remediation guidance. Best for planning and prioritization.

### Gap analysis template

```markdown
## Compliance Gap Analysis: [Framework Name]
**Scope:** [Systems / organizational scope]
**Assessment date:** [Date]
**Framework version:** [e.g., NIST CSF 2.0, ISO/IEC 27001:2022]

### Gap Summary
| Severity | Count | % of total |
|----------|-------|------------|
| Critical (must remediate before audit) | [N] | [%] |
| High (material gap with regulatory risk) | [N] | [%] |
| Medium (partial implementation) | [N] | [%] |
| Low (process refinement needed) | [N] | [%] |

### Detailed Gaps

#### [Control ID / Category Name]
| Field | Detail |
|-------|--------|
| Framework reference | [Control ID, subcategory, or requirement number] |
| Control requirement | [What the framework requires] |
| Current state | [What we actually have] |
| Gap | [What's missing] |
| Severity | [Critical / High / Medium / Low] |
| Risk if unaddressed | [Business / regulatory consequence] |
| Remediation approach | [Recommended path to close the gap] |
| Effort estimate | [Low / Medium / High] |
| Evidence required | [What would demonstrate compliance] |
| Owner | [Team or role responsible] |

[Repeat for each gap]
```

---

## Workflow 3: Remediation Roadmap

Use to produce a prioritized, time-phased plan for closing gaps. Best for annual planning,
budget justification, and program governance.

### Roadmap template

```markdown
## Compliance Remediation Roadmap: [Framework Name]
**Prepared:** [Date]
**Planning horizon:** [12 months | 18 months | 24 months]

### Executive Summary
[2-3 sentences: current posture, path to target, investment required]

### Prioritization methodology
Gaps are prioritized by: (1) regulatory risk — items with audit findings or regulator attention first;
(2) exploitability — gaps in controls relevant to actively exploited attack patterns;
(3) effort efficiency — high-impact, low-effort wins scheduled early.

### Phase 1: Immediate (0-3 months) — Critical Gaps
| Gap | Remediation | Owner | Estimated effort | Cost impact |
|-----|-------------|-------|-----------------|-------------|
| [Gap description] | [Action] | [Team] | [Effort] | [$range or FTE] |

### Phase 2: Near-term (3-9 months) — High Priority
[Same table structure]

### Phase 3: Strategic (9-18 months) — Program Maturity
[Same table structure]

### Multi-framework overlap analysis
*(For organizations under multiple frameworks)*

| Control Area | NIST CSF | ISO 27001 | SOC 2 | Shared remediation opportunity |
|-------------|----------|-----------|-------|-------------------------------|
| [Area] | [Gap?] | [Gap?] | [Gap?] | [Single remediation that closes multiple gaps] |
```

---

## Multi-Framework Assessment

For organizations under simultaneous framework obligations, the skill identifies overlapping control
requirements to maximize remediation efficiency. Common mappings are loaded from the framework modules:

- NIST CSF 2.0 ↔ NIST 800-53 Rev 5 (native NIST mapping)
- NIST 800-53 ↔ ISO 27001:2022 (NIST cross-reference document)
- SOC 2 TSC ↔ NIST CSF (AICPA mapping)
- CMMC ↔ NIST 800-171 (native CMMC basis)

When running a multi-framework assessment, specify all active frameworks in the input and the skill
will produce a unified gap analysis that identifies which remediations satisfy multiple frameworks simultaneously.

---

## Working with Tools

### MCP connectors this skill uses

| Connector | Used for | Priority |
|-----------|----------|----------|
| **GRC Platform** (Archer, ServiceNow GRC, LogicGate) | Pull existing control assessments, update scores, manage evidence | High — primary data source |
| **Documentation** (SharePoint, Confluence) | Retrieve policy documents as evidence, pull prior assessment reports | High |
| **Ticketing** (ServiceNow, Jira) | Create remediation tracking tickets from gap analysis output | Medium |
| **Identity** (Entra ID, Okta) | Access control evidence for identity-related controls | Medium |
| **Vulnerability Scanner** | Evidence for vulnerability management control assessments | Medium |

### Graceful degradation

Without GRC platform connectivity, the skill works from manually provided assessment data.
Input your control status as a structured list or paste prior audit findings, and the skill will
score, gap-analyze, and roadmap from that input.

---

## What This Skill Does NOT Do

- **Does not conduct external audits or produce audit opinions.** This skill supports self-assessment and preparation; formal audit opinions require accredited auditors.
- **Does not produce compliance certification.** ISO 27001, SOC 2, and CMMC certifications require independent assessment by accredited bodies.
- **Does not reproduce framework documents verbatim.** It references the framework modules in `frameworks/`; those modules are structured summaries, not substitutes for the source documents.
- **Does not replace legal or regulatory counsel.** Regulatory compliance has legal dimensions that require qualified counsel.
- **Does not automatically validate evidence.** Maturity scores generated here are hypotheses based on stated controls; evidence must be human-validated before use in audit contexts.
- **Does not cover all frameworks.** See `frameworks/README.md` for the current list of supported frameworks and how to add new ones.
