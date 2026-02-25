---
name: ai-governance
description: >
  AI governance, AI policy, AI risk management, AI deployment governance, acceptable use of AI,
  AI acceptable use policy, generative AI policy, LLM governance, AI risk assessment,
  AI decision review, AI ethics, responsible AI, AI oversight, human-in-the-loop,
  AI model deployment, AI tool approval process, AI intake, AI risk register,
  "can we use this AI tool", "governance for AI", "AI policy for our organization",
  NIST AI RMF, AI risk framework, agentic AI governance, AI program governance,
  AI vendor evaluation, shadow AI, unauthorized AI use, AI data handling policy.
---

# AI Governance

This skill provides the policy framework for organizational AI deployment decisions — establishing
governance structures, evaluating AI deployment proposals against risk criteria, determining
acceptable use boundaries, and assessing data classification implications of AI usage. It works in
partnership with the ai-agent-review skill (governance sets policy; ai-agent-review operationalizes
it for specific tools) and feeds AI risk entries into the risk-assessment skill's risk register.

PLAID (People Led, AI Driven) is the default governance philosophy baked into this skill. Organizations
can substitute their own AI governance framework by documenting it in `security.local.md`.

> **Philosophy: People Led, AI Driven (PLAID)**
>
> The central governance question for any AI deployment is not "can the AI do this?" but "should
> the AI do this, and with what human oversight?" PLAID establishes that AI accelerates work and
> augments human capability, but humans retain decision authority — especially for high-stakes,
> irreversible, or ethically complex decisions. This skill institutionalizes that principle: every
> AI deployment goes through a governance process that explicitly identifies what humans control,
> what the AI assists with, and where human approval gates exist. Governance is not a blocker to
> AI adoption; it is what makes AI adoption sustainable and trustworthy.

---

## Before You Begin

Load your `security.local.md` to calibrate this skill. Key fields used:

- **AI governance philosophy** — defaults to PLAID; org-specific philosophy substituted if documented
- **AI risk appetite** — Conservative / Moderate / Aggressive
- **Approved AI tools** — list of already-approved tools to avoid redundant review
- **Prohibited AI use cases** — hard stops that governance cannot override
- **Human-in-the-loop requirements** — what decision types always require human authorization
- **Data classification limits for AI** — what data may flow through AI systems

---

## Roles This Skill Serves

**Primary:** AI Security, Security Leadership, GRC

**Also useful for:**
- IT and business units evaluating AI tools for adoption
- Legal and privacy teams: data protection implications of AI deployments
- Security Architecture: AI in infrastructure and development environments
- All employees: understanding what AI use is permitted and what isn't

---

## Workflow 1: AI Deployment Risk Assessment

Use when evaluating a new AI tool, agent, or workflow for organizational deployment.
The security review of the specific tool (code, permissions, supply chain) is handled by
the ai-agent-review skill — this workflow assesses the governance and risk context.

### Inputs for AI deployment assessment

```
Tool / system name:    [Name]
Proposed use case:     [What will this AI be used for?]
User population:       [Which teams or roles will use it?]
Data to be processed:  [What data will flow through this AI? Classification level?]
Deployment model:      [SaaS (vendor-hosted) | Self-hosted | API access | Local/on-device]
Decision types:        [What decisions will this AI assist with or make?]
Stakes level:          [Reversible / Partially reversible / Irreversible]
Vendor:                [Vendor name — for SaaS / API deployments]
```

### AI deployment risk assessment template

```markdown
## AI Deployment Risk Assessment: [Tool/Use Case Name]
**Assessment date:** [Date]
**Requested by:** [Business unit / team]
**Assessed by:** [Security / governance reviewer]
**Frameworks applied:** NIST AI RMF, PLAID governance criteria

---

### 1. Use Case Assessment

**Proposed use:** [Description]
**Value proposition:** [Why is this being proposed?]
**Decision support or decision-making?** [Assists human decisions | Makes recommendations | Takes autonomous action]
**Reversibility:** [All actions reversible | Partially reversible | Includes irreversible actions]

**PLAID alignment check:**
| Principle | Assessment |
|-----------|-----------|
| People retained in decision authority | [Yes / Partially / No — explain] |
| AI role clearly bounded | [Yes / No — explain what the AI does vs. what humans do] |
| Human confirmation gates for high-stakes actions | [Yes / No / Not applicable] |
| Output review by qualified human before reliance | [Yes / No — explain] |
| Scope to minimum necessary AI involvement | [Yes / No — explain] |

---

### 2. Data Risk Assessment

| Data element | Classification | Volume | AI access type | Risk |
|-------------|---------------|--------|---------------|------|
| [Data type] | [Public/Internal/Confidential/Restricted] | [Approximate] | [Training / Inference / Storage] | [Risk assessment] |

**Data handling concerns:**
- Is data sent to an external AI provider (vendor-hosted / API)? [Yes/No]
- Is a Data Processing Agreement (DPA) in place or required? [Yes/No/TBD]
- Does processing trigger GDPR, HIPAA, or other regulatory requirements? [Yes/No — specify]
- Risk of sensitive data exfiltration via AI prompt/response: [High/Medium/Low]

**Data classification verdict:**
[Based on org's data classification limits in security.local.md, is this data permitted to
flow through this AI system?]
[ ] Approved — within permitted classification limits
[ ] Conditional — requires DPA, DLP controls, or other safeguards before approval
[ ] Not approved — data classification exceeds permitted limits for this deployment model

---

### 3. NIST AI RMF Assessment
*(Reference: frameworks/nist-ai-rmf.md)*

| AI RMF Function | Criteria | Status | Notes |
|-----------------|----------|--------|-------|
| **GOVERN** | AI governance policy exists and applies to this deployment | [Met / Partial / Not met] | |
| **GOVERN** | Roles and responsibilities for this AI system defined | [Met / Partial / Not met] | |
| **MAP** | AI risk context documented (use cases, affected parties) | [Met / Partial / Not met] | |
| **MAP** | Potential negative impacts identified | [Met / Partial / Not met] | |
| **MEASURE** | Metrics to monitor AI performance and risk defined | [Met / Partial / Not met] | |
| **MEASURE** | Mechanism to detect and report AI failures | [Met / Partial / Not met] | |
| **MANAGE** | Response plan if AI behaves unexpectedly | [Met / Partial / Not met] | |
| **MANAGE** | Decommission process defined | [Met / Partial / Not met] | |

---

### 4. AI Risk Register Entry

```
Risk ID:            [AIRISK-YYYY-NNN]
Tool/system:        [Name]
Use case:           [Description]
Risk statement:     There is a risk that [specific AI failure mode or misuse] will result in
                    [specific impact] to [affected stakeholders].
Likelihood:         [High / Medium / Low]
Impact:             [High / Medium / Low]
Residual risk:      [High / Medium / Low — after proposed controls]
Treatment:          [Accept / Mitigate / Reject]
```

---

### 5. Governance Decision

**Risk rating:** [Critical | High | Medium | Low]
**Decision:** [Approve | Approve with conditions | Reject]

**Conditions (if applicable):**
- [ ] DPA executed with vendor
- [ ] DLP controls configured to prevent restricted data from entering AI prompts
- [ ] Human review gate implemented for AI outputs before operational use
- [ ] Training materials deployed to user population
- [ ] Monitoring controls configured
- [ ] Review schedule established: [date]

**Approved by:** _________________________ (CISO or AI Governance Committee)
**Date:** _____________
**Decision record location:** [GRC platform reference]
```

---

## Workflow 2: AI Acceptable Use Policy Template

Use to draft or update your organization's AI acceptable use policy.

```markdown
# AI Acceptable Use Policy
**Version:** [1.0]
**Status:** [Draft — requires review and approval per governance process]
**Applies to:** All employees, contractors, and third parties with access to [Organization] systems

---

## Purpose
[Organization] is committed to harnessing the benefits of AI tools while managing the associated
risks to data security, privacy, regulatory compliance, and decision quality. This policy establishes
requirements for the acceptable use of AI tools by anyone working on behalf of [Organization].

## Governance Philosophy
[Organization] adopts the [PLAID / organization-specific] governance framework for AI:
[2-3 sentences describing the core principle — e.g., PLAID: People Led, AI Driven].

## Approved Tools
| Tool | Approved for | Data classification limit | Conditions |
|------|-------------|--------------------------|-----------|
| [Tool name] | [Use cases] | [Internal data max] | [Review AI output before relying on it] |

## Prohibited Uses
The following uses of AI tools are prohibited:
- Inputting [Confidential / Restricted] data into external AI tools without an approved DPA
- Using AI to make autonomous decisions in [list high-stakes categories] without human review
- Using AI tools not on the approved list without completing the AI intake process
- [Organization-specific prohibitions]

## AI Intake Process
Before using a new AI tool for organizational work:
1. Submit an AI tool request to [team/process]
2. Security review will be conducted using the ai-agent-review skill
3. Governance decision will be made by [role] within [timeline]
4. Approved tools are added to the approved tool list; decisions are documented

## Human Oversight Requirements
The following decision types always require human review of AI output before action:
- [List from security.local.md human-in-the-loop requirements]
- Any decision that is difficult or impossible to reverse
- Any decision affecting an individual's rights, employment, or significant interests

## Violations
Violations of this policy may result in [disciplinary action, access revocation, etc.].
```

---

## Workflow 3: AI Risk Register

Use to maintain an ongoing register of AI-related risks across the organization's AI portfolio.

### AI risk register template

```markdown
## AI Risk Register
**Last updated:** [Date]
**Owner:** [AI Governance / Security team]

| Risk ID | Tool/System | Use case | Risk description | Likelihood | Impact | Residual risk | Treatment | Owner | Review date |
|---------|-------------|---------|-----------------|-----------|--------|--------------|-----------|-------|-------------|
| AIRISK-001 | [Tool] | [Use case] | [Risk statement] | [H/M/L] | [H/M/L] | [H/M/L] | [Mitigate/Accept] | [Owner] | [Date] |

### Active high residual risks
[Highlight any risks rated High or Critical — these require CISO awareness]

### AI portfolio summary
| Status | Count |
|--------|-------|
| Approved AI deployments | [N] |
| Pending review | [N] |
| Rejected / decommissioned | [N] |
| Unknown / shadow AI (identified but not reviewed) | [N] |
```

---

## Relationship to Other Skills

| Skill | Relationship |
|-------|-------------|
| **ai-agent-review** | Governance sets the criteria; agent review operationalizes them for specific tools |
| **risk-assessment** | AI risks feed into the enterprise risk register |
| **policy-management** | AI acceptable use policy is managed through policy lifecycle skill |
| **compliance-assessment** | AI governance maps to NIST AI RMF, which maps to NIST CSF Govern function |
| **audit-support** | AI governance evidence collection for auditors |

---

## Working with Tools

### MCP connectors this skill uses

| Connector | Used for | Priority |
|-----------|----------|----------|
| **Documentation** (SharePoint, Confluence) | AI policy publication, governance decision records | High |
| **GRC Platform** | AI risk register management, governance workflow | High |
| **Ticketing** (ServiceNow, Jira) | AI intake process workflow | Medium |

---

## What This Skill Does NOT Do

- **Does not perform technical security reviews of specific AI tools.** That is the ai-agent-review skill's domain.
- **Does not provide legal advice on AI regulation.** EU AI Act, state AI laws, and sector-specific AI regulations require qualified legal counsel.
- **Does not approve or reject AI tools autonomously.** The governance decision requires human authority — the CISO or AI Governance Committee makes the call.
- **Does not monitor AI tools in production.** Runtime monitoring is an operational security function beyond this skill's scope.
- **Does not cover AI used in products sold to customers.** This skill governs internal enterprise AI use; product AI has distinct governance requirements.
- **Does not address AI bias or fairness comprehensively.** Algorithmic fairness in decision-making systems requires specialized expertise beyond cybersecurity governance.
