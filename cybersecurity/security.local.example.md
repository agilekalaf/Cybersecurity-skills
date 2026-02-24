# security.local.md — Organization Security Configuration

> **DO NOT commit this file.** Add `security.local.md` to your `.gitignore`.
> This file contains organization-specific configuration that must remain local.
> Copy this example to `security.local.md` and customize before using the plugin.

---

## Organization Profile

```
Organization name:       [Your Organization Name]
Industry sector:         [Financial Services | Healthcare | Energy/Utilities | Technology |
                          Manufacturing | Government | Retail | Other]
Employee count:          [<500 | 500-5,000 | 5,000-50,000 | >50,000]
Geographic footprint:    [US-only | North America | EMEA | Global]
Regulatory environment:  [List primary regulators, e.g., SEC, FINRA, OCC, HIPAA/HHS, NERC/FERC]
Security team size:      [Approximate headcount]
```

---

## Active Compliance Frameworks

List all frameworks your organization actively manages. Skills load the relevant
framework module from `frameworks/` based on this list.

```
Primary framework:    [nist-csf-2.0 | iso-27001 | nerc-cip | cmmc | soc2]
Additional frameworks:
  - [nist-800-53]
  - [soc2]
  - [cmmc]
  - [Add others as applicable]

Current maturity target (NIST CSF tiers): [Tier 2 → Tier 3 | Tier 3 → Tier 4]
Next major audit:    [Framework + target date]
Certification status: [e.g., ISO 27001 certified through 2026-03]
```

---

## Risk Appetite

These settings calibrate how the risk-assessment and compliance-assessment skills
prioritize findings and recommendations.

```
Overall risk appetite:     [Conservative | Moderate | Aggressive]
Risk tolerance by category:
  Operational:             [Low | Medium | High]
  Regulatory/compliance:   [Low | Medium | High]
  Reputational:            [Low | Medium | High]
  Technology/cyber:        [Low | Medium | High]

Risk acceptance authority:
  Low risk (<$X):          [Role, e.g., Security Manager]
  Medium risk ($X–$Y):     [Role, e.g., CISO]
  High risk (>$Y):         [Role, e.g., CRO or Board]

Risk quantification methodology: [Qualitative matrix | FAIR | Other]
```

---

## Security Tool Stack

List deployed tools by category. Skills use this to route MCP queries to the right
connectors and to tailor recommendations to your actual environment.

### SIEM / Log Management
```
Primary SIEM:        [Microsoft Sentinel | Splunk | Chronicle | Elastic | Other]
Log retention:       [Hot: X days | Warm: Y days | Cold: Z days]
UEBA enabled:        [Yes | No]
```

### SOAR / Automation
```
Platform:            [Sentinel SOAR | Splunk SOAR/Phantom | Palo Alto XSOAR | Tines | None]
Automation maturity: [Ad hoc | Playbook-driven | Fully automated with human review]
```

### Endpoint / EDR
```
Platform:            [Microsoft Defender for Endpoint | CrowdStrike | SentinelOne | Other]
Coverage:            [~X% of endpoints]
Mobile (MDM):        [Intune | Jamf | Other | None]
```

### Identity & Access Management
```
Primary IdP:         [Entra ID | Okta | Ping | Other]
PAM solution:        [CyberArk | BeyondTrust | Delinea | None]
IGA platform:        [SailPoint | Saviynt | None]
MFA coverage:        [% of users | All users | Admin only]
Privileged accounts: [Approximate count]
```

### Vulnerability Management
```
Scanner:             [Qualys | Tenable | Rapid7 | Microsoft Defender | Other]
Scan frequency:      [Continuous | Weekly | Monthly]
CMDB/Asset inventory: [ServiceNow | Axonius | Tanium | Other | None]
SLA targets:
  Critical (CVSS 9+):  X days
  High (CVSS 7–8.9):   Y days
  Medium (CVSS 4–6.9): Z days
  Low (<4):            As-scheduled
```

### Cloud Security
```
Cloud providers:     [Azure | AWS | GCP | Multi-cloud]
CSPM:                [Defender for Cloud | Prisma Cloud | Wiz | Native tools]
Container/K8s:       [AKS | EKS | GKE | None]
```

### GRC Platform
```
Platform:            [Archer | ServiceNow GRC | LogicGate | Hyperproof | Spreadsheets | None]
Risk register:       [In GRC platform | Separate tool | Spreadsheet]
Policy management:   [In GRC platform | SharePoint | Confluence | Other]
```

### Ticketing / Workflow
```
Primary:             [ServiceNow | Jira | Zendesk | Other]
Incident tracking:   [Same as above | Separate system]
```

### Threat Intelligence
```
Platforms:           [Feedly | OpenCTI | MISP | Recorded Future | Other]
Feeds subscribed:    [CISA KEV | FS-ISAC | H-ISAC | TAXII feeds | Other]
TI team:             [Dedicated team | Ad hoc | External MSSP | None]
```

### Email / Collaboration
```
Email platform:      [Microsoft 365 | Google Workspace | Other]
Collaboration:       [Teams | Slack | Other]
```

---

## Escalation Contacts

```
Security Operations Center:
  SOC lead:          [Name, email, phone/Teams]
  After-hours:       [Pager/on-call method]

Incident Response:
  IR lead:           [Name, contact]
  External IR retainer: [Firm name, contact]

Security Leadership:
  CISO:              [Name, contact]
  Deputy CISO:       [Name, contact]

Legal / Privacy:
  General Counsel:   [Name, contact]
  Privacy Officer:   [Name, contact]

Communications / PR:
  Contact:           [Name, contact]

Executive team (for major incidents):
  CEO / COO:         [Contact method]

Regulatory contacts:
  [Regulator name]:  [Contact / notification method]
```

---

## Incident Severity Definitions

Calibrate to match your organization's classification scheme. The incident-response
skill will use these to set severity in triage output.

```
SEV 1 (Critical):
  Definition:   Active breach with data exfiltration, ransomware execution, or
                significant operational impact. Executive notification required.
  SLA:          Acknowledge within 15 min, contain within 4 hours.

SEV 2 (High):
  Definition:   Confirmed compromise of critical system or significant unauthorized
                access. CISO notification required.
  SLA:          Acknowledge within 30 min, contain within 24 hours.

SEV 3 (Medium):
  Definition:   Suspicious activity requiring investigation, policy violation with
                potential impact.
  SLA:          Acknowledge within 2 hours, resolve within 72 hours.

SEV 4 (Low):
  Definition:   Policy violation, low-risk event requiring documentation.
  SLA:          Acknowledge within 8 hours, resolve within 2 weeks.
```

---

## AI Governance Policy

The ai-governance and ai-agent-review skills use this section to calibrate
recommendations against your organization's stated AI policy.

```
AI governance philosophy:  [PLAID (default) | Organization-specific (describe below)]
AI risk appetite:          [Conservative | Moderate | Aggressive]

Approved AI tools:
  - [Tool name, approved use cases, data classification limit]

Prohibited AI use cases:
  - Feeding PII/PHI/financial data to external AI models without DPA
  - [Add organization-specific prohibitions]

Human-in-the-loop requirements:
  High-stakes decisions:   Always required (examples: access termination, IR containment)
  Routine analysis:        AI-assisted with analyst review
  Reporting:               AI draft with human review and sign-off

AI deployment approval:
  Approver:      [Role, e.g., CISO + AI Governance Committee]
  Process:       [Link to AI intake process or describe here]

Data classification limits for AI:
  Public data:         Approved for external AI
  Internal data:       Approved for approved internal AI only
  Confidential:        Internal AI only with DLP controls
  Restricted/Secret:   No AI processing without explicit approval
```

---

## Reporting and Metrics

The security-reporting skill uses these targets to evaluate KPI performance.

```
Board reporting cadence:   [Quarterly | Biannual | Annual]
ELT reporting cadence:     [Monthly | Quarterly]
Operational metrics cadence: [Weekly | Bi-weekly]

Key metrics tracked:
  Mean Time to Detect (MTTD):     Target: X hours
  Mean Time to Respond (MTTR):    Target: Y hours
  Vulnerability SLA compliance:   Target: >Z%
  Phishing simulation rate:       Target: <Z% click rate
  Security training completion:   Target: >Z%
  Patch compliance (critical):    Target: >Z% within SLA
  Access review completion:       Target: 100% within period

Board-level risk indicators:
  - [List the 3-5 metrics your board tracks]
```

---

## Custom Notes

Use this section for any organization-specific context that doesn't fit the categories
above — historical incidents, known technical debt, regulatory findings in remediation,
or any standing exceptions to standard workflows.

```
[Free-form organization-specific notes]
```
