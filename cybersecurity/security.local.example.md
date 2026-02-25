# Security Configuration — Organization Playbook

> Copy this file to `security.local.md` and customize for your organization.
> This file is your org's security identity — it tells the agent who you are,
> what you care about, and how you operate. Skills reference this file to
> tailor their behavior to your environment.
>
> This file should NOT be committed to public repositories. Add `security.local.md`
> to your `.gitignore`.

## Organization profile

- **Organization:** [Your company name]
- **Industry:** [Utilities / Healthcare / Financial Services / Technology / Government / etc.]
- **Regulatory environment:** [List primary regulators — e.g., FERC, NERC, state PUC, FTC, HHS]
- **Security team size:** [approximate headcount]
- **Security program maturity:** [Initial / Developing / Defined / Managed / Optimizing — or use your framework's maturity scale]

## Governance philosophy

<!-- Define your team's operating philosophy. This shapes how the agent frames
     recommendations, reports, and escalations. Example below uses PLAID
     (People Led, AI Driven) — replace with your own or remove. -->

We follow a People Led, AI Driven (PLAID) approach to security operations:
- AI augments human analysts — it does not replace judgment or decision authority
- Containment and remediation actions require human approval
- AI-generated findings are recommendations, not conclusions
- Transparency in AI-assisted analysis: reports note where AI contributed
- Speed through automation, accuracy through human oversight

## Active compliance frameworks

<!-- List the frameworks your organization is actively measured against.
     Skills will load the corresponding framework modules from frameworks/
     and apply their control mappings, maturity models, and reporting requirements. -->

- **Primary:** NIST CSF 2.0 (current maturity: 2.4, target: 3.0 by Q4 2026)
- **Regulatory:** NERC CIP (applicable to BES Cyber Systems)
- **Privacy:** CCPA/CPRA (California consumer data), state-specific privacy laws
- **Voluntary:** SOC 2 Type II (customer trust, annual audit cycle)

## Severity classification

<!-- Define how your org classifies incident and vulnerability severity.
     Skills use this for consistent triage and escalation. -->

| Severity | Definition | Response SLA | Escalation |
|----------|-----------|-------------|------------|
| Critical | Active data exfiltration, ransomware execution, safety system compromise | 15 min initial response | Immediate — CISO + Legal + Exec |
| High | Confirmed compromise, lateral movement, regulated data exposure | 1 hour initial response | SOC Lead + IR Team |
| Medium | Suspicious activity requiring investigation, unpatched critical CVE on exposed system | 4 hours initial response | SOC Lead |
| Low | Policy violation, informational alert, low-risk vulnerability | Next business day | Standard ticket |

## Escalation contacts

<!-- Skills reference these for escalation recommendations. -->

- **SOC Lead:** [name / role / contact method]
- **Incident Commander (on-call):** [rotation schedule or contact]
- **CISO / CTSO:** [name / contact method / when to escalate]
- **Legal counsel:** [name / contact — for breach notification decisions]
- **Communications:** [name / contact — for public-facing incident response]
- **Executive sponsor:** [name / title — for business impact decisions]

## Tool stack

<!-- Map your tools to the connector categories used in .mcp.json.
     Skills use this to know what's available and what queries to construct. -->

| Category | Tool(s) | MCP Available | Notes |
|----------|---------|---------------|-------|
| SIEM / Log Management | [e.g., Microsoft Sentinel] | Yes / No | [query language, retention period] |
| SOAR / Automation | [e.g., Sentinel SOAR] | Yes / No | [approved playbook scope] |
| Identity & Access | [e.g., Entra ID, SailPoint, CyberArk] | Yes / No | [which for what — IAM vs PAM vs SSO] |
| Vulnerability Scanner | [e.g., Qualys, Defender Vuln Mgmt] | Yes / No | [scan frequency, scope] |
| EDR / Endpoint | [e.g., Defender for Endpoint] | Yes / No | [isolation capability, OS coverage] |
| Ticketing | [e.g., ServiceNow] | Yes / No | [incident vs request workflows] |
| GRC Platform | [e.g., Archer, Hyperproof] | Yes / No | [what's tracked here vs elsewhere] |
| Threat Intelligence | [e.g., Feedly, OpenCTI] | Yes / No | [commercial vs open source feeds] |
| Cloud Security | [e.g., Defender for Cloud] | Yes / No | [cloud providers in scope] |
| Email / Collaboration | [e.g., Exchange, Teams] | Yes / No | [notification and escalation channels] |
| Documentation | [e.g., SharePoint, Confluence] | Yes / No | [where policies, evidence, reports live] |

## AI governance

<!-- Define guardrails for how AI agents operate in your environment.
     The ai-agent-review and ai-governance skills reference this section. -->

**Approved AI platforms:** [e.g., Claude (Anthropic), internal ML models — list what's sanctioned]

**Data classification for AI:**
- **Allowed in AI context:** [e.g., public data, internal non-sensitive, anonymized metrics]
- **Restricted — requires approval:** [e.g., PII, customer data, financial data]
- **Prohibited:** [e.g., BES Cyber System details, authentication credentials, classified/regulated data with explicit prohibitions]

**Agent deployment requirements:**
- All plugins/skills require security review before deployment (use ai-agent-review skill)
- MCP connections to production systems require approval from [role/team]
- Agents with write access to any system require human-in-the-loop confirmation
- Agent activity must be logged to [logging destination]
- Quarterly review of all active agent deployments and permissions

**Human-in-the-loop requirements by risk tier:**
- **Tier 1 (read-only analysis):** Agent can operate autonomously, human reviews output
- **Tier 2 (recommendations with action):** Agent recommends, human approves and executes
- **Tier 3 (direct system interaction):** Agent prepares action, human approves, agent executes with audit trail
- **Tier 4 (critical systems):** No autonomous agent access — human performs all actions, agent assists with analysis only

## Reporting and metrics

<!-- Define what leadership needs to see and how often.
     The security-reporting skill uses this to generate appropriate reports. -->

**Board reporting:** Quarterly — risk posture summary, major incidents, compliance status, program progress
**ELT reporting:** Monthly — KPI dashboard, NIST CSF maturity progress, open risk items, budget status
**Operational reporting:** Weekly — alert volume and disposition, vulnerability SLA compliance, incident status
**Key metrics tracked:**
- NIST CSF 2.0 maturity score by function (Govern, Identify, Protect, Detect, Respond, Recover)
- Mean time to detect (MTTD) and mean time to respond (MTTR)
- Vulnerability remediation SLA compliance by severity
- Phishing simulation click rates
- Access review completion rates
- [Add your org-specific KPIs]

## Notification and regulatory obligations

<!-- Map your notification requirements so incident response and compliance
     skills can flag deadlines automatically. -->

| Trigger | Regulation | Notification deadline | Notify whom | Notes |
|---------|-----------|----------------------|-------------|-------|
| Personal data breach affecting CA residents | CCPA/CPRA | Without unreasonable delay | Affected individuals + CA AG if >500 | Assess with legal |
| BES Cyber System incident | NERC CIP-008 | 1 hour (for reportable events) | E-ISAC, CISA | Specific criteria for reportable events |
| [Add your obligations] | | | | |
