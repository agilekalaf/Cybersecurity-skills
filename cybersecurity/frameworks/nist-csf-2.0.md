# NIST Cybersecurity Framework 2.0

**Issuing body:** National Institute of Standards and Technology (NIST)
**Version:** 2.0
**Published:** February 2024
**Document:** NIST CSWP 29

---

## Purpose

NIST CSF 2.0 provides a voluntary framework of cybersecurity outcomes to help organizations of any
size, sector, or maturity understand, assess, prioritize, and communicate their cybersecurity risk
management practices. Version 2.0 significantly expanded the original framework with the addition
of the Govern function and explicitly extended the target audience beyond critical infrastructure
to all organizations. It is designed to be used alongside other frameworks and risk management
approaches, not as a standalone control catalog.

---

## Key Change from CSF 1.1: The Govern Function

CSF 2.0 added a sixth function — **Govern (GV)** — to address the organizational context and
accountability structures that make all other functions effective. This reflects industry recognition
that cybersecurity governance failure (poor board awareness, unclear accountability, inadequate
resources) is a root cause of program failures across sectors. The Govern function sits at the
center of the framework wheel, influencing all other functions.

---

## Framework Structure

The framework is organized as: **Functions → Categories → Subcategories**

- **6 Functions** — broad cybersecurity outcomes (Govern, Identify, Protect, Detect, Respond, Recover)
- **22 Categories** — groups of cybersecurity outcomes within each function
- **106 Subcategories** — specific, measurable outcomes at the operational level

Organizations assess maturity at the Function or Category level for executive reporting, and
at the Subcategory level for detailed gap analysis and control mapping.

---

## Functions and Categories

### Govern (GV) — NEW in CSF 2.0
Establishes, communicates, and monitors the organization's cybersecurity risk management strategy,
expectations, and policy.

| Category | Code | Description |
|----------|------|-------------|
| Organizational Context | GV.OC | Understanding the mission, stakeholders, and environment |
| Risk Management Strategy | GV.RM | Priorities, constraints, and risk tolerance established |
| Roles & Responsibilities | GV.RR | Cybersecurity roles and authorities defined |
| Policy | GV.PO | Cybersecurity policy established and communicated |
| Oversight | GV.OV | Results of risk management activities reviewed |
| Cybersecurity Supply Chain | GV.SC | Supply chain risk management integrated |

### Identify (ID)
Understand the organization's assets, suppliers, and related cybersecurity risks.

| Category | Code | Description |
|----------|------|-------------|
| Asset Management | ID.AM | Assets inventoried and managed |
| Risk Assessment | ID.RA | Cybersecurity risks identified and prioritized |
| Improvement | ID.IM | Improvements identified from assessments and incidents |

### Protect (PR)
Use safeguards to manage cybersecurity risks.

| Category | Code | Description |
|----------|------|-------------|
| Identity Management & Access Control | PR.AA | Access to assets managed |
| Awareness & Training | PR.AT | Personnel are trained |
| Data Security | PR.DS | Data managed consistent with risk strategy |
| Platform Security | PR.PS | Hardware, software, and services managed |
| Technology Infrastructure Resilience | PR.IR | Resilience mechanisms in place |

### Detect (DE)
Find and analyze possible cybersecurity attacks and compromises.

| Category | Code | Description |
|----------|------|-------------|
| Continuous Monitoring | DE.CM | Assets and users monitored for anomalies |
| Adverse Event Analysis | DE.AE | Anomalies analyzed to characterize incidents |

### Respond (RS)
Take action regarding a detected cybersecurity incident.

| Category | Code | Description |
|----------|------|-------------|
| Incident Management | RS.MA | Incidents managed |
| Incident Analysis | RS.AN | Investigations conducted |
| Incident Response Reporting | RS.CO | Response activities coordinated |
| Incident Mitigation | RS.MI | Incidents contained |

### Recover (RC)
Restore assets and operations affected by a cybersecurity incident.

| Category | Code | Description |
|----------|------|-------------|
| Incident Recovery Plan Execution | RC.RP | Recovery plans executed |
| Incident Recovery Communication | RC.CO | Restoration activities communicated |

---

## Implementation Tiers

Tiers describe the maturity of an organization's cybersecurity risk management practices.
Tiers are not maturity levels — organizations should target the tier appropriate to their risk,
not always strive for Tier 4.

| Tier | Name | Characteristics |
|------|------|----------------|
| **Tier 1** | Partial | Cybersecurity risk management is ad hoc. Limited awareness of organizational risk. No formal processes. |
| **Tier 2** | Risk Informed | Risk management practices approved at executive level but not organization-wide policy. Some awareness of supply chain risks. |
| **Tier 3** | Repeatable | Organization-wide risk management policy formally approved and expressed as policy. Consistent processes in place. |
| **Tier 4** | Adaptive | Organization actively adapts cybersecurity practices based on continuous improvement, threat intelligence sharing, and lessons learned. |

**Tier progression guidance:** Most organizations should target Tier 2 → Tier 3. Tier 4 is
appropriate for high-maturity organizations with continuous improvement programs and external
intelligence sharing.

---

## Common Assessment Approach

1. **Scope:** Define what organizational units, systems, or processes are in scope
2. **Current Profile:** Assess which CSF outcomes are currently achieved and at what tier
3. **Target Profile:** Define the desired tier for each function based on risk appetite
4. **Gap Analysis:** Compare Current to Target Profile; identify and prioritize gaps
5. **Action Plan:** Develop prioritized action plan to close gaps
6. **Review:** Repeat on a defined cadence (typically annual)

For the compliance-assessment skill, Subcategory-level assessment provides the most detailed
gap analysis. Function-level assessment is sufficient for executive reporting.

---

## Framework Mappings

| Framework | Mapping availability |
|-----------|---------------------|
| NIST SP 800-53 Rev 5 | Full subcategory mapping in NIST cross-reference; see `frameworks/nist-800-53.md` |
| ISO/IEC 27001:2022 | NIST publishes an informative reference mapping; see `frameworks/iso-27001.md` |
| NIST AI RMF 1.0 | Govern function has strong alignment; see `frameworks/nist-ai-rmf.md` |
| SOC 2 TSC | AICPA publishes a CSF → TSC mapping; see `frameworks/soc2.md` |
| CMMC 2.0 | CMMC maps to NIST 800-171 which maps to 800-53 which maps to CSF |

---

## Regulatory Context

| Sector | Regulatory driver |
|--------|------------------|
| Financial services | FFIEC recommends CSF; SEC cybersecurity rules reference CSF |
| Healthcare | HHS promotes CSF alongside HIPAA Security Rule |
| Energy/utilities | CISA promotes CSF; NERC CIP has separate requirements for BES |
| Federal contractors | FedRAMP requires NIST 800-53 (which maps to CSF) |
| Defense contractors | CMMC (maps through 800-171 to 800-53 to CSF) |
| All sectors | CISA promotes CSF as the baseline for Critical Infrastructure Protection |

**Not a regulation:** NIST CSF is voluntary for private sector organizations. However,
it is increasingly referenced in regulatory guidance and contractual requirements.

---

## Source

Full framework text, implementation guidance, and cross-references: https://www.nist.gov/cyberframework
