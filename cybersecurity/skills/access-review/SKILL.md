---
name: access-review
description: >
  Access review, access certification, user access review, privilege review, SoD analysis,
  separation of duties, privileged access, orphan accounts, access recertification, UAR,
  quarterly access review, annual access review, identity governance, least privilege,
  over-provisioned accounts, excessive permissions, access audit, "who has access to",
  "review this user's permissions", stale accounts, dormant accounts, role-based access review,
  entitlement review, access rights analysis, IGA, identity lifecycle.
---

# Access Review

This skill executes structured access certification workflows — from periodic access recertification
to targeted privilege analysis, separation of duties (SoD) conflict detection, and orphan account
identification. It is designed to work with identity and access management platforms to pull current
access data, apply least-privilege analysis, and produce certification-ready reports that support
both operational decisions and compliance evidence requirements.

> **Philosophy: People Led, AI Driven (PLAID)**
>
> Access decisions carry direct security and compliance consequences: granting unnecessary access
> creates risk; revoking access incorrectly causes operational disruption. This skill accelerates
> the analytical work — pulling access data, identifying anomalies, flagging SoD conflicts,
> and structuring certification reports — so that access reviewers focus on decisions, not data
> gathering. Every access revocation recommendation requires human confirmation. The skill identifies
> what to review; managers and system owners decide what to do with it. Automated bulk revocation
> without human review is exactly the workflow this skill is designed to prevent.

---

## Before You Begin

Load your `security.local.md` to calibrate this skill. Key fields used:

- **Identity & Access Management tools** — determines which MCP connectors to query (Entra ID, SailPoint, CyberArk, Okta)
- **Privileged accounts count** — scopes the privileged access review effort
- **Active compliance frameworks** — many frameworks (SOC 2, ISO 27001, NERC CIP) have specific access review periodicity requirements
- **Industry sector** — regulatory requirements for access review vary by sector (financial services, healthcare, utilities)

---

## Roles This Skill Serves

**Primary:** IAM (identity analysts, access reviewers), GRC (compliance requirement owners)

**Also useful for:**
- Security Operations: incident investigation — "what access did this user have?"
- Security Leadership: privileged access risk reporting
- Audit Support: access review evidence for certifications and audits

---

## Workflow 1: Periodic Access Certification

Use to conduct quarterly, semi-annual, or annual access recertification campaigns across a defined scope.

### Inputs for access certification

```
Review scope:        [All users | Specific application | Specific role | Privileged accounts only |
                      Specific department | Org-wide]
Review period:       [Quarterly | Semi-annual | Annual]
Frameworks driving:  [SOC 2 | ISO 27001 | NERC CIP | Internal policy]
Identity sources:    [Entra ID | SailPoint | Okta | CyberArk | Manual list]
Focus areas:         [All access | Privileged only | SoD | Orphan accounts | All]
```

### Access certification report template

```markdown
## Access Certification Report
**Review period:** [Q1 2025 / Dates: YYYY-MM-DD through YYYY-MM-DD]
**Scope:** [Application name / Department / Org-wide]
**Conducted by:** [IAM team / GRC team]
**Review completed:** [Date]
**Compliance driver:** [Framework requirement, e.g., SOC 2 CC6.2]

### Executive Summary
| Metric | Count |
|--------|-------|
| Total accounts reviewed | [N] |
| Access confirmed appropriate | [N] ([%]) |
| Access modified (downscoped) | [N] ([%]) |
| Access revoked | [N] ([%]) |
| Accounts disabled (orphaned) | [N] ([%]) |
| SoD conflicts identified | [N] |
| SoD conflicts remediated | [N] |
| Review completion rate | [%] (of assigned reviewers who responded) |

### Review completion status
| Department / System | Reviewer | Assigned | Completed | On time |
|--------------------|----------|----------|-----------|---------|
| [Department] | [Manager name] | [N accounts] | [Date] | [Yes/No] |
| [Department] | [Manager name] | [N accounts] | [Pending] | [Overdue] |

### Findings Requiring Action
| Account | Access | Finding | Risk | Recommended action | Owner |
|---------|--------|---------|------|-------------------|-------|
| [username] | [System/Role] | [Over-provisioned / Orphaned / SoD conflict] | [High/Med/Low] | [Revoke / Modify / Accept] | [Manager] |

### Evidence for audit
- Review request records: [Reference / location]
- Manager certification responses: [Reference / location]
- Modification/revocation tickets: [Reference / location]
- This report: [Location — do not store access data in unsecured locations]
```

---

## Workflow 2: Privileged Access Analysis

Use to review privileged accounts (admin accounts, service accounts, break-glass accounts) against
least-privilege principles and privileged access management (PAM) requirements.

### Privileged access analysis template

```markdown
## Privileged Access Analysis
**Date:** [Date]
**Scope:** [Domain | Cloud | Application | Global]

### Privileged account inventory
| Account | Type | Privilege level | Systems | Last login | MFA enrolled | In PAM vault | Finding |
|---------|------|----------------|---------|------------|-------------|-------------|---------|
| [username] | [Human admin / Service acct / Break-glass] | [Global admin / Domain admin / etc.] | [Systems] | [Date or Never] | [Yes/No] | [Yes/No] | [Finding] |

### High-risk findings

#### Accounts with admin rights not in PAM vault
[List — these are unmanaged privileged credentials, critical finding]

#### Accounts with no recent activity (>90 days)
[List — candidates for disablement or removal]

#### Admin accounts without MFA
[List — immediate remediation required in most frameworks]

#### Service accounts with interactive login enabled
[List — service accounts should not have interactive login in most environments]

### PAM coverage assessment
| Privilege type | Total accounts | In PAM vault | Coverage % | Target |
|---------------|----------------|--------------|------------|--------|
| Domain admins | [N] | [N] | [%] | 100% |
| Cloud global admins | [N] | [N] | [%] | 100% |
| Application admins | [N] | [N] | [%] | [Target] |
| Service accounts | [N] | [N] | [%] | [Target] |
```

---

## Workflow 3: Separation of Duties Conflict Detection

Use to identify accounts that hold combinations of permissions that violate SoD policies —
particularly relevant for financial systems, ERP, and privileged access.

### Common SoD conflict patterns

| Conflict | Risk | Common in |
|---------|------|-----------|
| Create + approve purchase orders | Financial fraud | ERP systems (SAP, Oracle) |
| Make + approve journal entries | Financial manipulation | Accounting systems |
| Provision accounts + approve access | Unauthorized access | IAM systems |
| Develop + deploy to production | Unauthorized code deployment | Development environments |
| Initiate + approve wire transfers | Financial fraud | Banking systems |
| Access backup systems + target systems | Ransomware staging | Infrastructure |

### SoD conflict matrix template

```markdown
## SoD Conflict Analysis
**System:** [System name]
**Date:** [Date]
**Policy reference:** [Policy ID or framework control]

| Account | Conflicting permission 1 | Conflicting permission 2 | Conflict type | Risk | Status |
|---------|------------------------|------------------------|--------------|------|--------|
| [username] | [Permission / Role] | [Permission / Role] | [e.g., Create + Approve] | [High] | [Pending remediation] |

### Remediation options
For each conflict, options are:
1. **Remove one permission** — preferred where operationally feasible
2. **Compensating control** — detective monitoring (audit log review, alerting on conflict exercise)
3. **Risk acceptance** — for low-risk conflicts with documented business necessity
```

---

## Working with Tools

### MCP connectors this skill uses

| Connector | Used for | Priority |
|-----------|----------|----------|
| **Entra ID / Okta** | Pull current access, group membership, last login data | High — core data source |
| **SailPoint / Saviynt** | IGA platform for access request history, role definitions, certification campaigns | High if deployed |
| **CyberArk / BeyondTrust** | PAM vault coverage, privileged account inventory | High for privileged access review |
| **Ticketing** (ServiceNow, Jira) | Create revocation and modification tickets | Medium |
| **GRC Platform** | Store certification results as compliance evidence | Medium |

### Graceful degradation

Without identity platform connectivity, provide access data exports (CSV or JSON from IdP admin UI)
and the skill will analyze them structurally. Note that manual exports may not include all account
attributes — flag any gaps in the report.

---

## What This Skill Does NOT Do

- **Does not execute access changes autonomously.** Every modification and revocation requires human authorization through your IAM change process.
- **Does not design SoD rule sets from scratch.** The skill applies common SoD patterns; defining organizational SoD policy is a human GRC and business process activity.
- **Does not cover physical access control systems.** Badge/facility access management is out of scope.
- **Does not audit application-level permissions within specific SaaS tools** without data provided by the analyst. Access review requires data from each system.
- **Does not replace IGA platform functionality.** Where SailPoint, Saviynt, or equivalent is deployed, use those platforms for the certification workflow — this skill supplements and analyzes, not replaces.
- **Does not provide legal interpretation of access control requirements.** Regulatory requirements (e.g., HIPAA minimum necessary, FFIEC) require qualified counsel for definitive interpretation.
