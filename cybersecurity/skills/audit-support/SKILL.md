---
name: audit-support
description: >
  Audit support, audit preparation, audit evidence collection, control testing, audit response,
  audit finding remediation, audit request, evidence package, control testing worksheet,
  auditor request, PBC list, prepared by client, audit management, external audit, internal audit,
  ISO 27001 audit, SOC 2 audit, NERC CIP audit, CMMC assessment, regulatory exam, audit readiness,
  "prepare for audit", "collect evidence for", "auditor asked for", audit finding tracking,
  audit remediation, audit coordination, audit management, evidence gathering.
---

# Audit Support

This skill manages the full audit lifecycle — from evidence collection and control testing
documentation through audit response coordination and finding remediation tracking. It works
closely with the compliance-assessment skill (assessments feed audit preparation) and produces
the structured evidence packages, control testing worksheets, and finding trackers that auditors
and assessors require. Designed for both external certification audits (ISO 27001, SOC 2, CMMC)
and regulatory examinations (NERC CIP enforcement, FFIEC exams, HIPAA audits).

> **Philosophy: People Led, AI Driven (PLAID)**
>
> Audits are high-stakes attestations. The evidence you provide to an auditor is a representation
> of your organization's actual control environment — and misrepresenting it, even inadvertently,
> carries regulatory and legal consequences. This skill accelerates evidence collection, control
> testing documentation, and auditor communication — but the humans who own each control are
> responsible for the accuracy of evidence submitted. A compliance analyst reviews every evidence
> package before submission; the CISO owns the overall audit relationship and any management
> responses to findings. AI assists with organization and documentation; humans attest to accuracy.

---

## Before You Begin

Load your `security.local.md` to calibrate this skill. Key fields used:

- **Active compliance frameworks** — determines the applicable control requirements and evidence standards
- **Next major audit** — calibrates urgency and pacing
- **GRC platform** — primary system of record for audit evidence and finding tracking
- **Documentation platform** — where evidence artifacts are stored
- **Tool stack** — identifies evidence sources for each control category

The compliance-assessment skill should be run before this skill for new audit cycles — assessment
output feeds directly into the evidence collection plan.

---

## Roles This Skill Serves

**Primary:** GRC (compliance analysts, audit coordinators)

**Also useful for:**
- Security Operations: providing operational evidence (SIEM logs, incident records)
- IAM: providing access control evidence (access reviews, provisioning records)
- Security Leadership: management response drafting, executive briefings for auditors

---

## Workflow 1: Evidence Collection Matrix

Use at the start of an audit cycle to build a structured plan mapping audit requests to controls,
evidence sources, and responsible owners.

### Inputs for evidence collection planning

```
Audit type:          [ISO 27001 | SOC 2 | CMMC | NERC CIP | SOX ITGC | HIPAA | Internal | Regulatory exam]
Audit scope:         [Full certification | Specific control domains | Specific systems]
Audit dates:         [Field work window: YYYY-MM-DD through YYYY-MM-DD]
PBC list:            [Paste auditor's prepared-by-client (PBC) request list if available]
Prior audit:         [Date and any outstanding findings from last audit]
```

### Evidence collection matrix template

```markdown
## Audit Evidence Collection Matrix
**Audit:** [Audit type and scope]
**Field work period:** [Dates]
**Collection coordinator:** [Name / Role]
**Matrix created:** [Date]
**Last updated:** [Date]

| Request # | Auditor request | Control reference | Evidence description | Evidence location | Owner | Due date | Status |
|-----------|----------------|------------------|---------------------|------------------|-------|----------|--------|
| PBC-001 | [Auditor's request text] | [Control ID, e.g., ISO A.9.2.3] | [What to collect: policy document, screenshot, export] | [SharePoint path / GRC ticket] | [Team or person] | [Date] | [Not started / In progress / Ready / Submitted] |
| PBC-002 | [Access review evidence] | [SOC 2 CC6.2] | [Last quarterly access review report] | [GRC platform] | [IAM team] | [Date] | [In progress] |

### Collection status summary
| Status | Count | % |
|--------|-------|---|
| Not started | [N] | [%] |
| In progress | [N] | [%] |
| Ready for review | [N] | [%] |
| Submitted to auditor | [N] | [%] |

### Upcoming deadlines (next 7 days)
| Request # | Description | Owner | Due | Risk |
|-----------|-------------|-------|-----|------|
| [PBC-XXX] | [Description] | [Owner] | [Date] | [At risk / On track] |
```

---

## Workflow 2: Control Testing Worksheet

Use to document control testing methodology and results, providing auditors with evidence that
controls were tested and operating effectively during the audit period.

### Control testing worksheet template

```markdown
## Control Testing Worksheet
**Control:** [Control ID and name, e.g., ISO A.9.4.1 — Information access restriction]
**Testing period:** [Audit period covered]
**Tested by:** [Name / Role]
**Test date:** [Date]
**Reviewed by:** [Reviewer name / Role — required]

### Control Description
**Control objective:** [What this control is designed to achieve]
**Control owner:** [Team or individual accountable for the control]
**Control type:** [Preventive / Detective / Corrective]
**Control frequency:** [Continuous / Daily / Weekly / Monthly / Annual / Event-driven]
**Automated or manual:** [Automated / Manual / Hybrid]

### Control Design Assessment
**Is the control designed adequately to meet the control objective?** [Yes / No / Partially]
**Design assessment rationale:** [Explanation]

### Testing Methodology
**Population:** [All transactions / Sample — define population]
**Sample size:** [N — if sampling, note sampling methodology]
**Test procedures:**
1. [Step 1: what was examined]
2. [Step 2: how it was tested]
3. [Step 3: what evidence was reviewed]

### Test Results
| Test step | Result | Evidence reference | Notes |
|-----------|--------|-------------------|-------|
| [Step 1] | [Pass / Fail / N/A] | [Evidence ID or location] | [Notes] |

**Overall control effectiveness:** [Effective / Partially effective / Ineffective]
**Exceptions noted:** [None | List exceptions with detail]

### Conclusion
**Operating effectiveness opinion:** [Effective / Ineffective]
**Basis for conclusion:** [Summary of what testing supports this conclusion]
**Recommendation:** [If exceptions — remediation recommendation]
```

---

## Workflow 3: Audit Finding Tracker

Use to manage audit findings from initial identification through remediation and validation.

### Finding tracker template

```markdown
## Audit Finding Tracker
**Audit:** [Audit name and period]
**Last updated:** [Date]
**Tracker owner:** [GRC team lead]

| Finding ID | Severity | Finding description | Control reference | Root cause | Remediation plan | Owner | Target date | Status | Validation date |
|-----------|----------|-------------------|------------------|-----------|-----------------|-------|-------------|--------|----------------|
| [AUD-2024-F001] | [High/Med/Low] | [Auditor's finding text] | [Control ID] | [Root cause analysis] | [Specific remediation steps] | [Owner] | [Date] | [Open/In progress/Remediated/Validated] | [Date if validated] |

### Finding status summary
| Severity | Total | Open | In progress | Remediated (pending validation) | Closed |
|----------|-------|------|-------------|--------------------------------|--------|
| High | [N] | [N] | [N] | [N] | [N] |
| Medium | [N] | [N] | [N] | [N] | [N] |
| Low | [N] | [N] | [N] | [N] | [N] |

### Overdue findings (past target remediation date)
[List findings past their target date — these require escalation]

### Management response template (for formal audit reports)
> Finding: [Finding description]
>
> Management response: [Organization name] agrees with / partially agrees with / disagrees with
> this finding. [Explanation of our position and remediation plan.] Target completion: [Date].
> Responsible party: [Role].
```

---

## Workflow 4: Auditor Communication

Use to draft responses to auditor questions, preliminary findings, and management letters.

### Communication principles

- **Be factual and precise.** Auditors note vague or over-broad responses.
- **Respond only to what was asked.** Volunteering unrequested information can create scope creep.
- **Address disagreements professionally.** If you believe a finding is incorrect, present specific evidence and request reconsideration — do not dismiss without basis.
- **Track all communications.** Maintain a log of all auditor interactions, requests, and responses.

### Auditor response template

```markdown
**To:** [Auditor name / Audit firm]
**From:** [Your name / Role]
**Re:** Response to [PBC request # / Finding # / Question reference]
**Date:** [Date]

[Direct response to the request — specific, factual, evidence-referenced]

Evidence provided:
- [Document name / ID]: [Brief description and location]
- [Document name / ID]: [Brief description]

[If requesting clarification or disagreeing with a finding:]
[Specific factual basis for your position, with evidence references]

Please confirm receipt and advise if additional information is needed.
```

---

## Working with Tools

### MCP connectors this skill uses

| Connector | Used for | Priority |
|-----------|----------|----------|
| **GRC Platform** (Archer, ServiceNow GRC) | Finding tracking, evidence storage, audit workflow | High |
| **Documentation** (SharePoint, Confluence) | Evidence artifact retrieval and storage | High |
| **Ticketing** (ServiceNow, Jira) | Remediation task tracking for findings | Medium |
| **Identity** (Entra ID, Okta) | Access control evidence (provisioning, review records) | Medium |
| **SIEM** | Log-based control evidence (authentication, monitoring) | Medium |

---

## What This Skill Does NOT Do

- **Does not attest to control effectiveness.** Only qualified humans (internal auditors, control owners, or accredited external auditors) can attest to control effectiveness.
- **Does not conduct formal certification audits.** ISO 27001, SOC 2, CMMC, and similar certifications require accredited assessment bodies.
- **Does not provide legal advice on audit findings.** Findings with regulatory consequences require qualified legal counsel.
- **Does not automatically collect evidence.** It builds the collection plan and templates; actual evidence retrieval requires human action or MCP-connected tools.
- **Does not draft opinions or representations.** Management responses and representations to auditors carry legal weight and must be human-authored and approved.
- **Does not manage auditor relationships.** The CISO and GRC leadership own the audit relationship; this skill supports the operational work.
