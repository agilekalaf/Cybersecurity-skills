# NIST AI Risk Management Framework 1.0

**Issuing body:** National Institute of Standards and Technology (NIST)
**Version:** 1.0
**Published:** January 2023
**Document:** NIST AI 100-1
**Companion:** AI RMF Playbook (NIST Trustworthy and Responsible AI Resource Center)

---

## Purpose

The NIST AI Risk Management Framework (AI RMF) provides guidance for organizations to address
risks in the design, development, deployment, and use of AI systems. It is voluntary, non-prescriptive,
and outcomes-based — intentionally flexible to apply across AI technologies, sectors, and use cases.
The AI RMF is structured to help organizations incorporate trustworthiness considerations (validity,
reliability, safety, security, resilience, explainability, fairness, privacy) into their AI lifecycle.

For cybersecurity teams, the AI RMF is most relevant as a governance and risk management tool —
it provides the framework for organizational AI governance that the ai-governance skill operationalizes.

---

## Framework Structure

The AI RMF has two parts:

**Part 1 — Framing AI Risks:** Defines AI risk, trustworthy AI characteristics, and how the
framework can be used by different stakeholders.

**Part 2 — Core (GOVERN, MAP, MEASURE, MANAGE):** The operational risk management framework
organized into 4 functions.

---

## The Four Core Functions

### GOVERN
Establishes organizational structures, policies, and processes for AI risk management.
Govern cuts across all other functions — an organization cannot effectively Map, Measure, or Manage
AI risks without governance structures in place.

| Category | Description |
|----------|-------------|
| GV-1.1 | AI risk management policy exists |
| GV-1.2 | Accountability for AI risk across teams |
| GV-1.3 | Risk tolerance established and communicated |
| GV-1.4 | Organizational structure to support AI risk management |
| GV-1.5 | Continuous learning and improvement processes |
| GV-1.6 | Policies and practices for teams involved in AI |
| GV-1.7 | AI risk management priorities communicated and understood |
| GV-2.x | Accountability and responsibility defined |
| GV-3.x | Workforce training on AI risks |
| GV-4.x | Teams and workforces engaged |
| GV-5.x | Organizational policies for AI risk |
| GV-6.x | Policies for AI risk in procurement/acquisition |

### MAP
Identifies and classifies AI risks in context — categorizing AI use cases, affected stakeholders,
and risk scenarios.

| Category | Description |
|----------|-------------|
| MP-1.x | AI context established (purpose, capabilities, limitations, stakeholders) |
| MP-2.x | Scientific basis and knowledge about AI systems |
| MP-3.x | AI risks identified and categorized |
| MP-4.x | Impact assessments conducted |
| MP-5.x | Practices in place to address specific risk categories |

**Key MAP activities for enterprise AI deployment:**
- Define the AI system's purpose and intended use cases
- Identify all stakeholders and potentially affected parties
- Document data sources, training data, and associated risks
- Identify potential failure modes and their consequences

### MEASURE
Quantifies and analyzes identified AI risks using metrics and evaluation methods.

| Category | Description |
|----------|-------------|
| MS-1.x | AI risk assessment approaches defined |
| MS-2.x | AI system testing and evaluation in practice |
| MS-3.x | AI risks tracked over time |
| MS-4.x | Risk mitigation effectiveness measured |

**Key MEASURE activities:**
- Define metrics for AI performance, reliability, and fairness
- Test AI system behavior including adversarial inputs and edge cases
- Monitor AI outputs in production for drift or unexpected behavior
- Measure effectiveness of risk controls

### MANAGE
Allocates resources and implements plans to address identified AI risks.

| Category | Description |
|----------|-------------|
| MG-1.x | Risks identified with MAP and MEASURE addressed |
| MG-2.x | Risk treatment plans in place |
| MG-3.x | AI risk response plans |
| MG-4.x | Risk activities documented and reported |

**Key MANAGE activities:**
- Implement controls to mitigate identified risks
- Define escalation paths when AI systems behave unexpectedly
- Maintain AI risk register and treatment plans
- Decommission AI systems that cannot be adequately managed

---

## Trustworthy AI Characteristics

The AI RMF identifies these trustworthiness characteristics that AI systems should embody:

| Characteristic | Description | Security relevance |
|---------------|-------------|-------------------|
| **Valid and reliable** | Performs as intended consistently | Baseline for all AI use |
| **Safe** | Does not create harm to people or environment | Critical for agentic systems |
| **Secure and resilient** | Withstands adversarial inputs; recovers from failures | Core security concern |
| **Explainable and interpretable** | Outputs can be understood and examined | Required for human oversight |
| **Privacy-enhanced** | Privacy principles integrated by design | Data governance alignment |
| **Fair** | Free from harmful bias | Governance and legal consideration |
| **Accountable and transparent** | Responsible parties identified; information accessible | Audit and governance |

---

## AI Risk Taxonomy

The AI RMF identifies several categories of AI risk relevant to enterprise deployments:

| Risk type | Description |
|-----------|-------------|
| **Accuracy/performance failures** | Model performs incorrectly on real inputs |
| **Security vulnerabilities** | Adversarial attacks, data poisoning, model theft |
| **Privacy violations** | Exposure of PII from training data; inference attacks |
| **Bias and fairness** | Discriminatory outputs affecting individuals or groups |
| **Safety failures** | Agentic systems taking harmful actions |
| **Opacity** | Inability to explain or audit AI decisions |
| **Supply chain** | Compromised components in AI development pipeline |
| **Human-AI interaction** | Over-reliance on AI outputs; automation bias |

---

## Relationship to NIST CSF

| AI RMF Function | CSF Alignment |
|-----------------|---------------|
| GOVERN | CSF 2.0 Govern (GV) function — organizational cybersecurity governance |
| MAP | CSF Identify (ID) — understanding the risk landscape |
| MEASURE | CSF Detect (DE) — measuring and monitoring risk |
| MANAGE | CSF Respond (RS) + Recover (RC) — managing risk when it materializes |

Organizations already using NIST CSF can extend their governance structure to AI by mapping
AI RMF activities to their existing CSF program. The Govern function in CSF 2.0 is particularly
well-aligned with AI RMF GOVERN.

---

## Using AI RMF with the ai-governance Skill

The ai-governance skill uses the AI RMF to:

1. **GOVERN:** Assess whether organizational AI governance structures exist (policy, accountability,
   training, risk tolerance) before approving new AI deployments
2. **MAP:** Require that AI deployment proposals document purpose, stakeholders, data, and
   potential impacts before review
3. **MEASURE:** Define what metrics will track the AI system's risk and performance in production
4. **MANAGE:** Require response plans — what happens if the AI system behaves unexpectedly?

The AI deployment risk assessment template in the ai-governance skill maps directly to these functions.

---

## Regulatory Context

| Jurisdiction / Sector | Relevance |
|----------------------|-----------|
| U.S. federal agencies | NIST AI RMF referenced in Executive Order 14110 on Safe, Secure, and Trustworthy AI (2023) |
| EU AI Act | AI RMF concepts align with EU AI Act risk-based approach; both use risk categorization |
| Financial services | Regulators (OCC, CFPB) reference AI risk management frameworks in guidance |
| Healthcare | FDA's AI/ML-based SaMD guidance aligns with AI RMF principles |
| Defense | DoD AI strategy references responsible AI principles aligned with AI RMF |

---

## Source

NIST AI RMF 1.0: https://airc.nist.gov/RMF_Overview

AI RMF Playbook (implementation guidance): https://airc.nist.gov/Docs/2

NIST AI 100-1 (full document): https://doi.org/10.6028/NIST.AI.100-1
