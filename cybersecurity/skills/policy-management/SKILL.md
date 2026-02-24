---
name: policy-management
description: >
  Security policy management, policy drafting, policy review, policy writing, policy update,
  policy exception, acceptable use policy, information security policy, password policy,
  access control policy, incident response policy, policy-to-control mapping, policy lifecycle,
  exception tracking, risk acceptance, policy gap analysis, "draft a security policy",
  "update our policy", "we need a policy for", policy library management, policy governance,
  standards and procedures, control framework policy mapping.
---

# Policy Management

This skill supports the full security policy lifecycle — from drafting and reviewing policies to
mapping them to compliance framework controls, tracking exceptions, and managing policy governance
workflows. It produces policy-quality documents that meet common audit and regulatory standards,
and maintains the linkage between policy requirements and the framework controls they satisfy.

> **Philosophy: People Led, AI Driven (PLAID)**
>
> Security policies carry organizational authority and legal weight. This skill drafts and structures
> policy content at speed — synthesizing requirements from frameworks, industry standards, and your
> organizational context — but policy adoption requires human deliberation. The CISO or designated
> authority who signs a policy takes on accountability for its requirements. AI drafts; humans own.
> Every policy draft this skill produces must be reviewed, adapted to organizational context, approved
> through your defined governance process, and signed by an accountable human leader before publication.

---

## Before You Begin

Load your `security.local.md` to calibrate this skill. Key fields used:

- **Active compliance frameworks** — ensures drafted policies satisfy relevant framework requirements
- **Risk appetite** — calibrates policy stringency (conservative risk appetite → stricter policy requirements)
- **Tool stack** — ensures policies reference the actual tools and systems in your environment
- **Industry sector and regulatory environment** — tailors regulatory references in policies

---

## Roles This Skill Serves

**Primary:** GRC (policy analysts, compliance managers), Security Leadership

**Also useful for:**
- IAM: drafting access control policies and privilege management standards
- Application Security: secure development lifecycle policies and standards
- Security Operations: incident response and acceptable use policies
- HR/Legal: coordinating on acceptable use and data handling policies

---

## Workflow 1: Policy Drafting

Use to create a new security policy or update an existing one.

### Inputs for policy drafting

```
Policy type:        [Acceptable Use | Access Control | Incident Response | Vulnerability Management |
                     Data Classification | Password / Authentication | Encryption | Remote Work |
                     Third-Party Risk | AI Acceptable Use | Custom: describe]
Audience:           [All employees | IT staff | Developers | Executives | Third parties]
Framework alignment: [Which framework controls this policy should satisfy]
Regulatory context:  [Applicable regulations: HIPAA, PCI-DSS, GDPR, SOX, NERC CIP, etc.]
Existing policy:     [Paste current policy text if updating, or "new" if drafting from scratch]
Org context:         [Key org-specific requirements — tools, systems, exceptions to standard practice]
```

### Policy document template

```markdown
# [Policy Name]
**Policy ID:** [e.g., SEC-POL-001]
**Version:** [e.g., 1.0]
**Status:** [Draft | Under Review | Approved | Superseded]
**Classification:** [Internal | Confidential]
**Owner:** [Role — e.g., Chief Information Security Officer]
**Approved by:** [Role — pending signature]
**Approval date:** [Pending]
**Review cycle:** [Annual | Biennial]
**Next review date:** [Date]

---

## 1. Purpose
[2-3 sentences: Why does this policy exist? What risk does it address?]

## 2. Scope
[Who and what does this policy apply to? Include: employees, contractors, systems, locations,
third-party access. Be explicit about any exclusions.]

## 3. Policy Statement
[The core requirements — written in clear, mandatory language ("must", "shall", "is required to").
Use subsections for distinct requirement areas. Avoid jargon. Each statement should be testable
— auditors should be able to confirm compliance or non-compliance.]

### 3.1 [Requirement Area 1]
- [Specific requirement]
- [Specific requirement]

### 3.2 [Requirement Area 2]
- [Specific requirement]

## 4. Roles and Responsibilities
| Role | Responsibilities |
|------|-----------------|
| [CISO] | [Policy ownership, exception approval] |
| [IT/Security team] | [Implementation, monitoring] |
| [All employees] | [Compliance, reporting violations] |
| [Managers] | [Enforcement within their teams] |

## 5. Standards and Procedures
[Reference supporting standards, procedures, and guidelines that provide implementation detail.
Policies state "what"; procedures state "how".]
- Supporting standard: [Standard name and reference]
- Procedure: [Procedure name and reference]
- Tool guidance: [Relevant tool or system documentation]

## 6. Exceptions
Exceptions to this policy must be submitted to [role] using [process/form reference].
Exceptions require:
- Business justification
- Risk assessment documenting the accepted risk
- Compensating controls
- Time-bound approval (maximum exception duration: [period])
- Review by [role] and approval by [role]

## 7. Compliance and Enforcement
Violations of this policy may result in [disciplinary action up to and including termination,
legal action, and regulatory reporting as applicable]. [Team] monitors compliance via [methods].

## 8. Related Documents
- [Related policy name] ([Policy ID])
- [Framework reference: e.g., NIST CSF PR.AC — Access Control]
- [Regulatory reference: e.g., HIPAA §164.312(a)]

## 9. Revision History
| Version | Date | Author | Summary of changes |
|---------|------|--------|-------------------|
| 1.0 | [Date] | [Author] | Initial version |
```

---

## Workflow 2: Control Mapping Matrix

Use to map an existing policy library to framework controls, identify coverage gaps, and document
which controls each policy satisfies for audit purposes.

### Control mapping template

```markdown
## Policy-to-Control Mapping: [Framework Name]
**Generated:** [Date]
**Policy library version:** [Date of policy snapshot]

### Mapping table

| Framework Control | Control Description | Satisfying Policy | Policy Section | Coverage |
|------------------|--------------------|--------------------|----------------|----------|
| [NIST CSF GV.PO-01] | [Organizational cybersecurity policy exists] | [SEC-POL-001 Information Security Policy] | [Section 3] | [Full/Partial/Gap] |
| [NIST CSF PR.AA-01] | [Identities and credentials are managed] | [SEC-POL-003 Access Control Policy] | [Section 3.1] | [Full] |
| [Control ID] | [Description] | [Policy name] | [Section] | [Coverage] |

### Gap analysis
| Framework Control | Gap | Risk | Recommended action |
|------------------|-----|------|-------------------|
| [Control not covered by any policy] | [No policy exists] | [High/Med/Low] | [Draft new policy | Add to existing policy] |
```

---

## Workflow 3: Exception Register

Use to track active policy exceptions, their risk acceptance, and review schedules.

### Exception register template

```markdown
## Policy Exception Register
**Last updated:** [Date]
**Owner:** [GRC team or named individual]

| Exception ID | Policy | Requester | Business justification | Compensating controls | Risk level | Approved by | Approval date | Expiry date | Review status |
|-------------|--------|-----------|----------------------|--------------------|-----------|-------------|---------------|-------------|--------------|
| EXC-2024-001 | [Policy name] | [Team] | [Justification] | [Controls] | [High/Med/Low] | [CISO] | [Date] | [Date] | [Active/Expired/Pending renewal] |

### Exceptions approaching expiry (next 60 days)
| Exception ID | Policy | Expiry | Action required |
|-------------|--------|--------|----------------|
| [ID] | [Policy] | [Date] | [Renew | Close | Escalate] |

### Exceptions exceeding risk threshold
[List any exceptions rated High risk that have been active >180 days — these require CISO review]
```

---

## Working with Tools

### MCP connectors this skill uses

| Connector | Used for | Priority |
|-----------|----------|----------|
| **Documentation** (SharePoint, Confluence) | Retrieve existing policies for review, publish approved policies | High |
| **GRC Platform** (Archer, ServiceNow GRC) | Policy lifecycle management, control mapping, exception tracking | High |
| **Ticketing** (ServiceNow, Jira) | Policy review workflow, exception request tracking | Medium |

### Graceful degradation

Without documentation platform access, the skill drafts policies in markdown format for manual
publication. Without GRC platform access, control mapping and exception registers are produced as
structured markdown tables for manual import.

---

## What This Skill Does NOT Do

- **Does not provide legal advice.** Policy language with legal implications (employment terms, data subject rights, regulatory compliance statements) requires legal review.
- **Does not approve policies.** Drafts must go through your organization's governance process with appropriate human approval.
- **Does not automatically publish policies.** Human review and approval gate publication.
- **Does not create procedures or work instructions.** This skill focuses on policies (the "what"). Procedures (the "how") are a distinct document type.
- **Does not manage policy training or attestation workflows.** Policy awareness programs are out of scope; focus is on the policy documents themselves.
- **Does not cover privacy policies or terms of service.** External-facing privacy documentation has distinct requirements handled by privacy/legal teams.
