# MITRE ATLAS — Adversarial Threat Landscape for Artificial Intelligence Systems

**Issuing body:** MITRE Corporation
**Version:** Current (continuously updated)
**URL:** https://atlas.mitre.org
**Relationship to ATT&CK:** ATLAS is to AI/ML systems as ATT&CK is to traditional IT systems

---

## Purpose

MITRE ATLAS (Adversarial Threat Landscape for AI Systems) is a knowledge base of adversary tactics,
techniques, and case studies for attacks targeting machine learning systems and AI-enabled technologies.
It documents how adversaries target, subvert, and abuse AI/ML components — extending the MITRE ATT&CK
framework into the AI domain. ATLAS is used by AI security teams to understand the threat landscape
for AI deployments, design defenses, and assess AI systems against known attack patterns.

**Relevance to enterprise AI deployments:** As organizations deploy AI agents, LLM-powered tools,
and agentic workflows, ATLAS provides the threat taxonomy for understanding how these systems can
be attacked — complementing OWASP LLM Top 10 (see `frameworks/owasp-llm-top-10.md`).

---

## Relationship to MITRE ATT&CK

| Dimension | ATT&CK | ATLAS |
|-----------|--------|-------|
| Target | Traditional IT systems | AI/ML systems and AI-enabled applications |
| Tactics | 14 tactics (Reconnaissance through Impact) | AI-specific tactics |
| Techniques | ~600+ techniques | AI-specific techniques (smaller, growing set) |
| Case studies | Red team exercises, CTI reports | Documented AI attack incidents and research |
| Maturity | Mature, widely adopted | Newer, actively growing |
| Integration | Primary security framework | Extension for AI-specific threats |

ATLAS uses a similar structure to ATT&CK (tactics → techniques → sub-techniques) and is designed
to be used alongside ATT&CK — for AI systems, you need both.

---

## ATLAS Tactic Categories

ATLAS organizes adversary behavior into tactic categories relevant to ML system attacks:

| Tactic | Description | Example adversary goal |
|--------|-------------|------------------------|
| **Reconnaissance** | Gather information about target AI systems | Identify model architecture, training data sources, API endpoints |
| **Resource Development** | Acquire resources to support AI attacks | Collect adversarial examples, develop attack tools, gather substitute training data |
| **Initial Access** | Gain access to target ML systems | Exploit public-facing APIs, compromise ML supply chain, abuse legitimate access |
| **ML Attack Staging** | Prepare ML-specific attack components | Train shadow models, develop adversarial perturbations, stage poisoned data |
| **Model Access** | Interact with target ML model | Query ML model via API, gain physical access to model, access through legitimate means |
| **Execution** | Run adversarial ML operations | Execute adversarial input attack, run prompt injection |
| **Persistence** | Maintain foothold in AI pipeline | Backdoor ML model, poison ongoing training data pipeline |
| **Defense Evasion** | Avoid detection of ML attacks | Craft inputs to evade ML detectors, use adversarial examples to bypass classifiers |
| **Discovery** | Learn about AI environment | Discover ML artifacts, discover in-context window information |
| **Collection** | Gather ML data and model artifacts | Collect model outputs for model inversion, exfiltrate training data |
| **Exfiltration** | Extract data via ML systems | Infer training data through model queries, extract via LLM output |
| **Impact** | Degrade, disrupt, or corrupt AI functionality | Evade ML model, corrupt model outputs, disrupt ML service availability |

---

## Key Techniques Relevant to Enterprise AI Agents

### Prompt Injection (via ATLAS + OWASP LLM)
Adversary injects instructions into data processed by an LLM agent, causing it to execute
unintended actions. Two variants:
- **Direct:** Attacker directly manipulates the user input to the LLM
- **Indirect:** Attacker embeds instructions in content the LLM processes (web pages, documents,
  tool outputs) — the agent is "hijacked" by external content

**Defense:** Strict output validation, privilege separation between user content and system instructions,
human-in-the-loop for action execution.

### Model Inversion / Data Extraction
Adversary extracts memorized training data by carefully querying the model. Risk for models
trained on sensitive organizational data.

**Defense:** Differential privacy in training, data minimization, monitoring for extraction patterns.

### Supply Chain Compromise
Adversary compromises AI components in the supply chain — pre-trained model weights, data pipelines,
ML libraries, model repositories.

**Defense:** Model provenance verification, dependency pinning, integrity checks on model artifacts.

### Model Backdoor (Trojan)
Adversary poisons a model during fine-tuning or training so it behaves normally except on
specific "trigger" inputs, where it produces attacker-desired outputs.

**Defense:** Model evaluation on adversarial test sets, fine-tuning only from trusted, auditable data.

### Adversarial Example Attacks
Carefully crafted inputs that cause the model to misclassify or produce incorrect outputs,
often imperceptible to humans. Relevant for vision models and security classification systems.

**Defense:** Adversarial training, ensemble methods, input preprocessing.

---

## Case Studies

ATLAS maintains a library of documented real-world AI attack incidents and research demonstrations.
These include attacks on:
- Autonomous vehicle perception systems
- NLP classifiers used in content moderation
- Malware detection ML models (adversarial bypass)
- LLM-based systems (prompt injection incidents)
- Facial recognition systems (adversarial examples)

Case studies are referenced by technique and continuously updated. Consult https://atlas.mitre.org/studies
for current case studies — do not reproduce them here.

---

## Using ATLAS in the ai-agent-review Skill

The ai-agent-review skill uses ATLAS to evaluate:

1. Which ATLAS tactics are relevant given the agent's capabilities and attack surface
2. Whether the agent's design defends against key techniques (especially prompt injection,
   supply chain compromise, and excessive agency)
3. Whether monitoring exists to detect ATLAS-described attack behaviors in production

For enterprise AI agent deployments, the highest-priority ATLAS concerns are:
- Prompt injection (direct and indirect)
- Supply chain compromise of model or plugin
- Excessive agency enabling impact-phase attacks
- Data exfiltration through LLM outputs

---

## Relationship to OWASP LLM Top 10

ATLAS and OWASP LLM Top 10 (see `frameworks/owasp-llm-top-10.md`) are complementary:

| Dimension | ATLAS | OWASP LLM Top 10 |
|-----------|-------|-----------------|
| Perspective | Adversary TTPs | Developer/deployer vulnerabilities |
| Scope | Broad ML/AI attack landscape | LLM application-specific risks |
| Use case | Threat modeling, detection | Secure development, deployment review |
| Structure | Tactics → Techniques → Case studies | Top 10 risk categories with examples |
| Best used for | Understanding how attacks unfold | Understanding what to build defensively |

Use ATLAS to understand the threat; use OWASP LLM Top 10 to understand what to defend.

---

## Source

MITRE ATLAS: https://atlas.mitre.org

ATLAS Navigator: https://mitre-atlas.github.io/atlas-navigator/

MITRE ATLAS GitHub: https://github.com/mitre-atlas/atlas-data
