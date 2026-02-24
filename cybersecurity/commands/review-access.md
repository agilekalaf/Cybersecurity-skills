# /review-access

Conduct a structured access review for a user account, role, group, or organizational scope.
Analyzes access against least-privilege principles, detects SoD conflicts, identifies orphaned
accounts, and produces a certification-ready report.

## Usage

```
/review-access --scope user:jsmith@example.com
/review-access --scope role:GlobalAdmin --focus privilege
/review-access --scope group:FinanceTeam --focus sod
/review-access --scope org-wide --focus orphan
/review-access --scope application:SAP-ERP --period quarterly
/review-access --scope privileged --focus all
```

## What This Command Does

Invokes the access-review skill to pull access data from connected identity platforms and analyze
it against least-privilege principles, organizational SoD rules, and access policy requirements.
Produces a structured report suitable for manager certification, compliance evidence, or IAM
remediation planning. Covers human accounts, service accounts, and privileged access depending
on scope.

## Parameters

| Parameter | Values | Default |
|-----------|--------|---------|
| `--scope` | `user:[upn]`, `role:[role-name]`, `group:[group-name]`, `application:[name]`, `org-wide`, `privileged` | Required |
| `--focus` | `privilege`, `sod`, `orphan`, `certification`, `all` | `all` |
| `--period` | `monthly`, `quarterly`, `semi-annual`, `annual` | `quarterly` |
| `--format` | `report`, `certification`, `ticket` | `report` |
| `--framework` | Compliance framework driving the review | From `security.local.md` |

## Workflow

1. Load `security.local.md` for IAM tool configuration, compliance frameworks, and escalation contacts
2. Query connected identity platforms (Entra ID, Okta, SailPoint) for access data in scope
3. For privileged access: query PAM platform (CyberArk, BeyondTrust) for vault coverage
4. Apply analysis based on `--focus`:
   - `privilege`: least-privilege assessment, admin account analysis
   - `sod`: match against common SoD conflict patterns for the system type
   - `orphan`: accounts with no recent activity (>90 days) or no associated active employee
   - `certification`: manager review format with approve/revoke/modify options
5. Generate findings with risk ratings and recommended actions
6. If `--format ticket`: create remediation tickets in connected ticketing system

## Output

**Standard report includes:**
- Executive summary: accounts reviewed, findings by severity, action rate
- Detailed findings table: account, access, finding type, risk, recommendation
- Privileged access coverage assessment (PAM vault coverage)
- SoD conflict matrix (if `--focus sod` or `all`)
- Orphan account list with last login data (if `--focus orphan` or `all`)

**`--format certification`:**
- Manager-ready certification report with approve / revoke / modify decision for each account
- Formatted for distribution to access reviewers

**Compliance evidence section:**
- Framework control reference satisfied by this review
- Dates and scope for audit documentation

## When to Use This

- **Quarterly access review:** Scheduled recertification for all users or key systems
- **Pre-audit preparation:** Demonstrate access control effectiveness to auditors
- **Post-departure review:** When an employee leaves — verify their access was fully revoked
- **Privileged access audit:** Quarterly admin account review
- **Incident investigation:** "What access did this user have?" during an investigation
- **SoD compliance:** After financial system changes, verify SoD controls are intact

## Dependencies

**Minimal (no MCP):** Accepts a manually provided access export (CSV/JSON) for analysis.
Useful when running ad hoc reviews without platform connectivity.

**Recommended:**
1. Entra ID / Okta — primary access data source for SaaS and cloud
2. SailPoint / Saviynt — IGA platform with historical access data
3. CyberArk / BeyondTrust — privileged account data
4. Ticketing — automated remediation ticket creation

## Related

- **Skill:** `skills/access-review/SKILL.md` (full documentation)
- **Command:** `/assess-compliance` — access reviews feed compliance assessments (ISO A.9, NIST PR.AA)
- **Skill:** `skills/audit-support/SKILL.md` — access review evidence for certifications
- **Skill:** `skills/incident-response/SKILL.md` — access investigation during active incidents
