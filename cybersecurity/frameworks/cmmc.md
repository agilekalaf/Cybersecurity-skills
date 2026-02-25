# CMMC 2.0 — Cybersecurity Maturity Model Certification

**Issuing body:** U.S. Department of Defense (DoD), Office of the Under Secretary of Defense for Acquisition and Sustainment
**Version:** CMMC 2.0
**Program status:** Final rule published December 2024; phased implementation in DoD contracts
**Applicability:** Defense Industrial Base (DIB) — contractors handling Federal Contract Information (FCI) or Controlled Unclassified Information (CUI)

---

## Purpose

CMMC 2.0 establishes cybersecurity requirements for DoD contractors and subcontractors who handle
Federal Contract Information (FCI) or Controlled Unclassified Information (CUI) on behalf of the
Department of Defense. It replaces CMMC 1.0 and is designed to protect sensitive defense information
from adversary theft — a significant national security concern given documented nation-state targeting
of the defense supply chain. Unlike voluntary frameworks, CMMC certification will be a contract
prerequisite — companies without the required CMMC level cannot bid on relevant DoD contracts.

**Who must comply:** Any organization in the DoD supply chain that handles FCI (all contractors) or
CUI (most contractors above the subthreshold). Subcontractors handling CUI passed down from a prime
are also in scope.

---

## CMMC 2.0 Levels

| Level | Name | Description | Assessment type | Based on |
|-------|------|-------------|----------------|---------|
| **Level 1** | Foundational | Basic cyber hygiene protecting FCI | Annual self-assessment + annual affirmation | 17 practices from FAR 52.204-21 |
| **Level 2** | Advanced | Protecting CUI — the most common level | Third-party assessment (C3PAO) for critical programs; self-assessment for others + annual affirmation | 110 practices from NIST SP 800-171 Rev 2 |
| **Level 3** | Expert | Protecting CUI against advanced persistent threats (APTs) | Government-led assessment (DCSA) | 110+ practices; includes select NIST 800-172 requirements |

---

## Relationship to NIST 800-171

CMMC Level 2 is directly derived from NIST SP 800-171 Rev 2, which itself is a subset of NIST
SP 800-53. Organizations with a current NIST 800-171 compliance program have the foundation for
CMMC Level 2 — but CMMC adds the certification element (independent verification by a C3PAO).

| CMMC Level | NIST basis | Key difference |
|-----------|------------|----------------|
| Level 1 | FAR 52.204-21 (basic safeguarding) | Self-assessed; fewer requirements |
| Level 2 | NIST 800-171 Rev 2 (110 practices across 14 domains) | Third-party certification required for most |
| Level 3 | NIST 800-171 + select 800-172 practices | DoD/DCSA-led assessment |

---

## NIST 800-171 Domains (Level 2 Foundation)

| Domain | Abbreviation | Practice count |
|--------|-------------|----------------|
| Access Control | AC | 22 |
| Awareness and Training | AT | 3 |
| Audit and Accountability | AU | 9 |
| Configuration Management | CM | 9 |
| Identification and Authentication | IA | 11 |
| Incident Response | IR | 3 |
| Maintenance | MA | 6 |
| Media Protection | MP | 9 |
| Personnel Security | PS | 2 |
| Physical Protection | PE | 6 |
| Risk Assessment | RA | 5 |
| Security Assessment | CA | 4 |
| System and Communications Protection | SC | 16 |
| System and Information Integrity | SI | 7 |

---

## Assessment and Certification Process

### Level 2 Assessment (C3PAO)

1. **System Security Plan (SSP):** Document how each of the 110 practices is implemented
2. **Plan of Action & Milestones (POA&M):** Document any practices not yet fully implemented
   (Note: POA&M practices are scored — not all POA&M items are acceptable at time of certification)
3. **C3PAO selection:** Choose a CMMC Third-Party Assessment Organization (C3PAO) from the
   CMMC Accreditation Body (CyberAB) marketplace
4. **Assessment:** C3PAO reviews documentation and tests implementation
5. **Score submission:** Scores submitted to DoD's Supplier Performance Risk System (SPRS)
6. **Certification:** If assessment score meets the required level, certification granted
7. **Annual affirmation:** Senior official affirms continued compliance annually

### Scoring

NIST 800-171 defines a scoring methodology: each of the 110 practices has a weighted point value.
Maximum score is 110. DoD sets minimum score thresholds. POA&M items carry partial credit.

---

## Key Implementation Considerations

### CUI Identification
Before implementing controls, contractors must identify where CUI exists in their environment
(systems, storage, data flows). This scoping exercise often reveals unexpected CUI exposure.

### Enclave approach
Many organizations create a CUI enclave — a segmented environment for CUI processing — to limit
the scope of CMMC assessment to systems that touch CUI rather than the entire enterprise.

### Subcontractor flow-down
CMMC requirements must flow down to subcontractors handling CUI. Prime contractors are responsible
for ensuring their subcontractors meet applicable CMMC requirements — this creates supply chain
risk management obligations.

### External Service Providers (ESPs)
Cloud services and managed service providers that handle CUI must be FedRAMP authorized at
Moderate or equivalent. This affects choices of cloud platforms and SaaS tools.

---

## Relationship to Other Frameworks

| Framework | Relationship |
|-----------|-------------|
| NIST SP 800-171 | CMMC Level 2 IS 800-171; see `frameworks/nist-800-53.md` for the 800-53 superset |
| NIST SP 800-53 | 800-171 is derived from 800-53 Moderate baseline; 800-53 compliance covers 800-171 |
| NIST CSF 2.0 | CMMC maps through 800-171 → 800-53 → CSF; CSF Tier 3 organizations generally have strong CMMC Level 2 posture |
| ISO 27001 | Not accepted as CMMC substitute; ISO 27001 certified orgs still need CMMC assessment |

---

## Regulatory Context

CMMC is mandatory for DoD contracts. Implementation timeline:

- **Phase 1 (from December 2025):** CMMC Level 1 self-assessments required in contracts
- **Phase 2:** Level 2 self-assessments required in contracts for applicable programs
- **Phase 3:** Level 2 C3PAO assessments required for critical programs
- **Phase 4 (full implementation):** All applicable CMMC requirements enforceable in contracts

*Timeline details subject to DoD implementation guidance; verify current status at cmmc.mil*

---

## Source

CMMC program: https://www.acq.osd.mil/cmmc/

NIST SP 800-171 Rev 2: https://csrc.nist.gov/publications/detail/sp/800-171/rev-2/final

CMMC Accreditation Body (C3PAO marketplace): https://cyberab.org
