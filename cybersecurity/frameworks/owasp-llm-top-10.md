# OWASP Top 10 for LLM Applications — 2025

**Issuing body:** OWASP Foundation (Open Worldwide Application Security Project)
**Version:** LLM AI Security Top 10 — 2025 Edition
**Project:** OWASP Top 10 for Large Language Model Applications
**URL:** https://genai.owasp.org

---

## Purpose

The OWASP Top 10 for LLM Applications identifies the most critical security risks for applications
built on large language models. It is the most immediately actionable security framework for teams
building, deploying, or evaluating LLM-powered tools, AI agents, and plugin-based agentic systems.
Alongside MITRE ATLAS (see `frameworks/mitre-atlas.md`), it forms the core technical evaluation
criteria in the ai-agent-review skill.

This framework is updated as the LLM application security landscape evolves. The 2025 edition
reflects lessons learned from widespread enterprise LLM deployment.

---

## The Top 10 — 2025 Edition

### LLM01: Prompt Injection
**Risk:** Malicious content in data processed by an LLM manipulates the model into performing
unintended actions, ignoring instructions, or leaking information. Occurs when user-supplied input
or external content (retrieved documents, tool outputs, web pages) overrides system instructions.

- **Direct prompt injection:** Attacker directly crafts a malicious user prompt
- **Indirect prompt injection:** Attacker embeds instructions in external content the LLM processes
  (web page, document, database result, email body)

**Impact:** Agent takeover, data exfiltration, unauthorized actions, bypass of safety controls.

**Defenses:** Privilege separation; treat all external content as untrusted; human confirmation for
high-stakes actions; output validation; reject anomalous instructions from external content.

**Traditional OWASP parallel:** SQL Injection — both involve untrusted input being interpreted as instructions.

---

### LLM02: Sensitive Information Disclosure
**Risk:** LLMs inadvertently reveal confidential information — from training data (memorized PII,
proprietary data), system prompts (revealing business logic or internal architecture), or by
reasoning over confidential context and including it in outputs shared with unauthorized parties.

**Impact:** PII exposure, trade secret disclosure, system architecture leakage enabling further attacks.

**Defenses:** Data minimization in training; differential privacy; output filtering; system prompt
protection; don't rely on system prompt confidentiality as a security control.

---

### LLM03: Supply Chain
**Risk:** LLM supply chains include pre-trained models, fine-tuning datasets, plugins, and
dependencies — all potential injection points for backdoors, malicious behavior, or compromised
functionality. Downloading a model from an unverified source or using an unvetted plugin introduces
supply chain risk.

**Impact:** Backdoored models, compromised plugins executing attacker code, poisoned data pipelines.

**Defenses:** Model provenance verification; use only trusted sources; pin model versions and
dependencies; scan plugins before deployment; review plugin permissions and behavior.

**Aligns with:** MITRE ATLAS supply chain compromise techniques.

---

### LLM04: Data and Model Poisoning
**Risk:** Adversaries manipulate training data or fine-tuning datasets to introduce backdoors,
bias, or degraded performance. Poisoning can cause models to behave incorrectly on specific inputs
(backdoor) or generally (bias injection, performance degradation).

**Impact:** Biased or incorrect outputs, backdoored model behavior, security control bypass.

**Defenses:** Training data provenance and integrity validation; anomaly detection on training
datasets; red-teaming fine-tuned models before deployment; limit who can contribute to training data.

---

### LLM05: Improper Output Handling
**Risk:** LLM outputs are passed to downstream systems without adequate validation or sanitization.
If LLM output is rendered as HTML, executed as code, passed to a database query, or used in system
commands without sanitization, traditional injection vulnerabilities apply to AI-generated content.

**Impact:** XSS, SQL injection, command injection, SSRF — via AI-generated content.

**Defenses:** Treat LLM output as untrusted input to downstream systems; apply the same output
validation and sanitization as for user-supplied input; don't execute LLM-generated code without review.

**Traditional OWASP parallel:** Output encoding and injection prevention — but the untrusted source
is the LLM rather than the user.

---

### LLM06: Excessive Agency
**Risk:** LLM agents are given more permissions, tool access, or autonomy than necessary for their
stated purpose. When an agent can take high-impact actions (send emails, delete files, execute code,
make API calls) without human confirmation, a compromised or confused agent causes real harm.

**Impact:** Data loss, unauthorized external communications, financial transactions, system changes.

**Defenses:** Least-privilege for tool permissions; require human confirmation for irreversible or
high-impact actions; scope agent capabilities to minimum necessary; implement agent action logging.

**PLAID alignment:** This is the technical instantiation of the PLAID principle — People Led, AI Driven.
Excessive agency is what happens when AI Driven becomes AI Deciding.

---

### LLM07: System Prompt Leakage
**Risk:** System prompts — containing business logic, internal instructions, persona definitions,
and sometimes sensitive configuration — are extracted by adversaries through carefully crafted
queries that cause the model to repeat, summarize, or paraphrase its instructions.

**Impact:** Business logic exposure, security control bypass, competitive intelligence leakage.

**Defenses:** Do not put secrets in system prompts; treat system prompts as potentially discoverable;
use retrieval-augmented generation (RAG) with access controls rather than embedding all context in the prompt.

---

### LLM08: Vector and Embedding Weaknesses
**Risk:** Retrieval-Augmented Generation (RAG) systems retrieve content from vector databases to
supplement LLM context. Vulnerabilities include: poisoning the vector store with malicious documents,
cross-context information leakage between tenants sharing a vector store, and insufficient access
controls on retrieved content.

**Impact:** Prompt injection via retrieved content, data leakage across users, retrieval of
unauthorized content.

**Defenses:** Access controls on vector database content (retrieved content should respect the
querying user's permissions); monitor for unusual retrieval patterns; validate content before
ingestion into vector stores.

---

### LLM09: Misinformation
**Risk:** LLMs generate plausible-sounding but incorrect information (hallucinations) that is
presented authoritatively and acted upon. In security contexts, this includes incorrect vulnerability
assessments, wrong remediation guidance, fabricated threat intelligence, and inaccurate compliance
assessments.

**Impact:** Incorrect security decisions, failed remediations, false confidence in security posture.

**Defenses:** Human review of AI-generated security content before action; ground outputs in retrieved
facts rather than pure generation; implement output validation against authoritative sources;
train users to treat AI output as a draft requiring verification, not a final answer.

**PLAID relevance:** This is the foundational risk that PLAID governance addresses — humans must
review AI outputs before relying on them for consequential decisions.

---

### LLM10: Unbounded Consumption
**Risk:** Adversaries exploit LLM applications through resource exhaustion — crafting inputs that
cause excessive token consumption, API calls, or processing time. In multi-agent systems, a
single poisoned instruction can trigger a cascade of expensive operations.

**Impact:** Service disruption, cost explosion (especially pay-per-token APIs), denial of service.

**Defenses:** Rate limiting on API endpoints; token budget limits per user/session; cost alerts;
timeouts on agent execution; anomaly detection on usage patterns.

---

## Summary Table

| Risk | Primary concern | ATLAS alignment | Traditional parallel |
|------|----------------|-----------------|---------------------|
| LLM01 Prompt Injection | Agent manipulation | Execution, Impact | SQL Injection |
| LLM02 Information Disclosure | Data leakage | Collection, Exfiltration | Insecure Direct Object Reference |
| LLM03 Supply Chain | Compromised components | Resource Development | Software supply chain attack |
| LLM04 Data Poisoning | Training data integrity | ML Attack Staging | Data tampering |
| LLM05 Output Handling | Downstream injection | Impact | Output encoding failures |
| LLM06 Excessive Agency | Unauthorized actions | Execution, Impact | Privilege escalation |
| LLM07 System Prompt Leakage | Architecture exposure | Discovery | Information disclosure |
| LLM08 Vector/Embedding | RAG attack surface | Initial Access | Injection via retrieved data |
| LLM09 Misinformation | Incorrect AI outputs | — | N/A (AI-specific) |
| LLM10 Unbounded Consumption | Resource exhaustion | Impact | Denial of Service |

---

## Using This Framework in ai-agent-review

The ai-agent-review skill evaluates all 10 categories for every full review. The quick scan
(5-point checklist) focuses on the highest-impact categories:
- LLM01 (Prompt Injection) — most common and highest impact
- LLM02 (Information Disclosure) — data handling risk
- LLM03 (Supply Chain) — provenance and trust
- LLM06 (Excessive Agency) — autonomous action risk
- LLM09 (Misinformation) — output reliability in security contexts

---

## Source

OWASP Top 10 for LLM Applications: https://genai.owasp.org

OWASP LLM AI Security Guide (extended guidance): https://owasp.org/www-project-top-10-for-large-language-model-applications/
