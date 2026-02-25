# NERC CIP — Critical Infrastructure Protection Standards

**Issuing body:** North American Electric Reliability Corporation (NERC)
**Enforced by:** Federal Energy Regulatory Commission (FERC) in the US; applicable regulators in Canada
**Current version:** CIP-002 through CIP-014 (various versions; active standards as approved by FERC)
**Applicability:** Electric utilities and operators of the Bulk Electric System (BES) in North America

---

## Purpose

NERC CIP standards establish mandatory cybersecurity requirements for the protection of the North
American Bulk Electric System (BES). Unlike voluntary frameworks, NERC CIP is a mandatory reliability
standard with civil penalty authority. FERC can impose penalties up to $1 million per violation per
day. NERC CIP applies exclusively to registered entities that operate or own assets connected to the
BES — it does not apply to distribution systems or non-BES generation.

**Who must comply:** Transmission operators (TOPs), reliability coordinators (RCs), balancing
authorities (BAs), distribution providers (DPs) with BES elements, generation owners/operators
above thresholds, and applicable market participants.

---

## BES Cyber System Categorization

The scope of NERC CIP requirements depends on the impact categorization of Bulk Electric System
Cyber Systems (BCS). Impact level determines which controls apply and at what rigor.

| Impact Level | Criteria (simplified) | Control scope |
|-------------|----------------------|---------------|
| **High** | Largest control centers; systems affecting the widest geographic area of the BES | All CIP requirements at highest rigor |
| **Medium** | Smaller control centers; certain generation and transmission assets | Most CIP requirements; some exceptions |
| **Low** | Assets not meeting High or Medium criteria but associated with BES | Streamlined requirements (CIP-003-8) |

CIP-002 defines the full categorization methodology. Asset owners must perform a BES Cyber Asset
identification and impact rating exercise — this is the foundation of all NERC CIP compliance.

---

## CIP Standards Summary

| Standard | Title | Description |
|----------|-------|-------------|
| **CIP-002** | BES Cyber System Categorization | Identify and categorize BES Cyber Systems by impact level |
| **CIP-003** | Security Management Controls | Governance: security policies, leadership accountability, low impact requirements |
| **CIP-004** | Personnel and Training | Background checks, training, access management for personnel |
| **CIP-005** | Electronic Security Perimeters | Define and protect Electronic Security Perimeters (ESPs) |
| **CIP-006** | Physical Security of BES Cyber Systems | Physical security of assets in Physical Security Perimeters (PSPs) |
| **CIP-007** | Systems Security Management | Ports/services, patch management, malware prevention, logging |
| **CIP-008** | Incident Reporting and Response Planning | IR plan, incident reporting to E-ISAC and NERC |
| **CIP-009** | Recovery Plans | Recovery plans for BES Cyber Systems |
| **CIP-010** | Configuration Change Management and Vulnerability Management | Baselines, change management, vulnerability assessments |
| **CIP-011** | Information Protection | BES Cyber System Information (BCSI) protection and secure disposal |
| **CIP-012** | Communications Between Control Centers | Protect real-time communications between control centers |
| **CIP-013** | Supply Chain Risk Management | Cybersecurity risk management for industrial control system hardware, software, and services |
| **CIP-014** | Physical Security (Transmission) | Physical security for high-impact transmission substations |

---

## Key Compliance Concepts

### Electronic Security Perimeters (ESPs)
Logical perimeters around BES Cyber Systems. All access points to ESPs must be controlled with
robust access management (CIP-005). Interactive Remote Access (IRA) to ESPs requires additional
controls including multi-factor authentication and encrypted communications.

### Physical Security Perimeters (PSPs)
Physical perimeters protecting High and Medium impact BES Cyber Assets. Visitor management,
logging, and physical access controls required (CIP-006).

### Protected Cyber Assets (PCAs)
Assets within an ESP that are not BES Cyber Assets themselves but communicate with BES Cyber
Assets and require protection.

### Transient Cyber Assets (TCAs)
Laptops, portable media, and similar devices used temporarily within or connecting to ESPs.
CIP-010 has specific requirements for TCAs including antivirus, patch requirements, and review
of software on TCAs before use.

### BES Cyber System Information (BCSI)
Sensitive operational and configuration information about BES Cyber Systems. Protected under
CIP-011.

---

## Compliance and Enforcement

| Topic | Detail |
|-------|--------|
| Penalty authority | FERC: up to $1,000,000 per violation per day |
| Self-reporting | Self-reported violations are treated more favorably; encourage a culture of reporting |
| Compliance monitoring | NERC and Regional Entities audit registered entities; spot checks and targeted audits |
| Regional Entities | NERC delegates enforcement to 7 regional entities (e.g., WECC, SERC, RFC) |
| Violation severity | NERC uses a Find, Fix, Track, and Report (FFT) process for less severe violations |
| Evidence retention | CIP standards specify evidence retention requirements (typically 3 years) |
| Evidence requirements | Very specific — CIP requires documented evidence of compliance for each requirement |

---

## Assessment Approach for NERC CIP

NERC CIP compliance assessment requires a structured approach:

1. **Asset inventory and categorization (CIP-002):** Identify all BES Cyber Systems and rate impact
2. **Gap assessment per standard:** Map current controls to each CIP requirement and identify gaps
3. **Evidence review:** CIP is evidence-based compliance — document what evidence exists for each requirement
4. **Violation risk factor (VRF) assessment:** NERC assigns VRFs (Lower/Medium/High/Critical) to each requirement
5. **Prioritize by VRF:** Focus remediation on Critical and High VRF requirements first
6. **Evidence remediation:** Where gaps exist, create the documentation, processes, or controls required

**Key difference from other frameworks:** NERC CIP is prescriptive and binary — you either have
compliant evidence or you have a potential violation. Unlike NIST CSF's maturity approach, NERC CIP
is requirements-based.

---

## Relationship to Other Frameworks

| Framework | Relationship |
|-----------|-------------|
| NIST CSF 2.0 | NERC CIP maps to NIST CSF at the subcategory level; CISA publishes mapping guidance; see `frameworks/nist-csf-2.0.md` |
| NIST 800-53 | CIP requirements map to 800-53 control families; useful for identifying supplemental controls |
| IEC 62443 | The ICS/OT security standard; NERC CIP and IEC 62443 are complementary for OT security |

---

## Source

All current NERC CIP standards: https://www.nerc.com/pa/Stand/Pages/CIPStandards.aspx

NERC Reliability Standards (complete current versions): https://www.nerc.com/pa/Stand/Pages/ReliabilityStandards.aspx
