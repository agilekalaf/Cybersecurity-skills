# SOC 2 — Trust Services Criteria

**Issuing body:** American Institute of Certified Public Accountants (AICPA)
**Standard:** SOC 2 (System and Organization Controls 2)
**Current criteria:** Trust Services Criteria 2022 (TSC 2022)
**Applicability:** Technology and SaaS companies; any service organization that stores, processes, or transmits customer data

---

## Purpose

SOC 2 is an auditing framework for service organizations — particularly technology companies —
that evaluates controls relevant to security, availability, processing integrity, confidentiality,
and privacy. SOC 2 reports are produced by independent CPA firms and are widely requested by
enterprise customers as third-party assurance of a vendor's security controls. Unlike ISO 27001,
SOC 2 is not a certification — it is an attestation report. The report describes the auditor's
opinion on whether controls were suitably designed (Type I) and/or operating effectively (Type II).

---

## Trust Service Categories

| Category | Abbreviation | Required | Description |
|----------|-------------|----------|-------------|
| **Security** | CC | **Always required** | Protection against unauthorized access to systems |
| **Availability** | A | Optional | Systems available for operation as agreed |
| **Processing Integrity** | PI | Optional | System processing is complete, valid, accurate, timely |
| **Confidentiality** | C | Optional | Information designated confidential is protected |
| **Privacy** | P | Optional | Personal information collected, used, retained, and disposed of per commitments |

Most organizations begin with Security only (the common criteria). Additional categories are added
based on customer requirements and the nature of the service.

---

## Type I vs. Type II

| Type | What it tests | When used |
|------|-------------|----------|
| **Type I** | Control design — are controls suitably designed to meet criteria? Point-in-time assessment. | First-time SOC 2; faster path; provides limited assurance to customers |
| **Type II** | Control operating effectiveness over a defined period (typically 6-12 months). | Annual renewal; stronger customer assurance; required by most enterprise contracts |

**Standard path:** Type I in Year 1 (often a 3-month prep + audit), Type II in Year 2+ (typically
12-month audit period, then annual renewal).

---

## Common Criteria (CC) — Security Category Structure

The Security category (CC) is organized into logical groupings:

| Group | Code | Description |
|-------|------|-------------|
| Control Environment | CC1 | COSO framework; organizational integrity and accountability |
| Communication and Information | CC2 | Information to support internal controls; communication to external parties |
| Risk Assessment | CC3 | Risk identification, analysis, and response |
| Monitoring | CC4 | Ongoing and separate evaluations of controls |
| Control Activities | CC5 | Control policies, technology deployment |
| Logical and Physical Access | CC6 | **Core technical controls** — the most evidence-intensive category |
| System Operations | CC7 | System monitoring, incident response, and change management |
| Change Management | CC8 | Authorized, tested, and approved changes |
| Risk Mitigation | CC9 | Business disruption risk mitigation |

**CC6 is the heart of SOC 2** — it covers access provisioning, MFA, encryption, physical security,
and is where most technical control evidence is concentrated.

---

## Common Evidence Requirements

| Control area | Common evidence |
|-------------|----------------|
| Access provisioning | Provisioning tickets, approval records |
| Access reviews | Quarterly access certification results |
| MFA enforcement | Configuration screenshots, MFA enrollment reports |
| Encryption at rest | Cloud configuration, key management records |
| Encryption in transit | TLS configuration evidence |
| Vulnerability management | Scan results, remediation tickets, SLA compliance reports |
| Incident response | IR plan, tabletop exercise records, incident tickets |
| Change management | Change advisory board records, deployment approvals |
| Vendor management | Vendor SOC 2 reports or questionnaires |
| Background checks | HR records (redacted as needed) |
| Security awareness training | Training completion records |
| Business continuity | BCP/DR plan, test results |
| Physical security | Access logs, badge control records, CCTV policy |

---

## Audit Cycle and Readiness

### Type II Readiness Timeline (typical)

| Phase | Duration | Activities |
|-------|----------|-----------|
| **Readiness assessment** | 1-3 months | Gap assessment against TSC; identify control deficiencies |
| **Control implementation** | 2-4 months | Close gaps identified in readiness assessment |
| **Audit period begins** | — | Controls must operate effectively throughout the period |
| **Audit period** | 6-12 months | Maintain controls; collect and organize evidence continuously |
| **Fieldwork** | 4-8 weeks | Auditor reviews evidence; interviews; testing |
| **Report issuance** | 2-4 weeks after fieldwork | Draft review; management response; final report |

### Exception management
If a control fails during the audit period, auditors will note it as an exception. Exceptions
are not automatically fatal to the report — auditors assess whether the exception is isolated
or systemic, whether compensating controls exist, and whether remediation occurred.

---

## SOC 2 vs. ISO 27001

| Dimension | SOC 2 | ISO 27001 |
|-----------|-------|-----------|
| Type | Attestation report | Certification |
| Geographic recognition | Primarily US-centric | Global |
| Scope | Service-specific | Organizational ISMS |
| Criteria | AICPA TSC (prescriptive) | ISO 27001 + Annex A (flexible) |
| Renewal | Annual | 3-year certification cycle |
| Report output | Auditor's report shared with customers | Certificate + registration |
| Common in | SaaS, cloud services | Enterprise, global supply chain |

Many organizations pursue both — ISO 27001 for global enterprise customers, SOC 2 for US tech customers.

---

## Mapping to Other Frameworks

| Framework | Mapping |
|-----------|---------|
| NIST CSF 2.0 | AICPA publishes a TSC → CSF mapping; strong overlap especially CC5-CC9 with Detect/Respond | see `frameworks/nist-csf-2.0.md` |
| NIST 800-53 | TSC criteria map to 800-53 control families; 800-53 compliance provides strong SOC 2 evidence base |
| ISO 27001 | Significant overlap; some organizations use ISO 27001 Annex A as evidence for SOC 2; gaps in CC2 (communication) and CC3 (risk) categories common |

---

## Source

AICPA Trust Services Criteria: https://www.aicpa-cima.com/resources/download/2017-trust-services-criteria

SOC 2 guide: https://www.aicpa-cima.com/professional-insights/download/soc-2-reporting-on-an-examination-of-controls-at-a-service-organization-relevant-to-security-availability-processing-integrity-confidentiality-or-privacy
