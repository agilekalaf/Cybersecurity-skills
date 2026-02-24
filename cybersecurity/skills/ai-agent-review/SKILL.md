---
name: ai-agent-review
description: >
  AI agent security review, LLM security assessment, plugin security review, MCP server security,
  AI tool evaluation, language model security, prompt injection risk assessment, agentic system review,
  AI security audit, reviewing Claude plugins, reviewing AI workflows, AI supply chain risk,
  evaluating an AI agent, "is this AI tool safe to use", "security review of this plugin",
  agentic security, AI tool approval, MCP connector evaluation, autonomous agent risk.
---

# AI Agent Security Review

This skill performs structured security reviews of AI agents, plugins, MCP servers, and agentic
workflows before organizational deployment. It evaluates against OWASP LLM Top 10, MITRE ATLAS,
and NIST AI RMF to identify prompt injection risks, data handling issues, excessive permissions,
and supply chain concerns. Output ranges from a quick five-point checklist to a full security
assessment report depending on depth and context provided.

> **Philosophy: People Led, AI Driven (PLAID)**
>
> The irony of AI reviewing AI is not lost here. This skill applies systematic security analysis
> to AI systems with full awareness of its own limitations: it cannot exhaustively test runtime
> behavior, it cannot audit closed-source model weights, and its analysis is only as good as the
> documentation and code provided. Use this skill to structure your review, catch common failure
> modes, and generate a risk-assessed recommendation — but have a human security practitioner
> validate the output before making deployment decisions. An AI that approves AI without human
> sign-off is exactly the governance failure this skill exists to prevent.

---

## Before You Begin

Load your `security.local.md` to calibrate this review. Key fields used:

- **AI governance policy** — what your organization has defined as acceptable AI use and data handling
- **Data classification limits** — which data tiers are permitted in AI processing pipelines
- **Human-in-the-loop requirements** — what decision types require human authorization
- **Approved AI tools** — whether the tool under review is already partially approved

If `security.local.md` is not available, the skill defaults to conservative posture (PLAID philosophy
applied at its strictest) and notes where organization-specific policy would change the assessment.

---

## Roles This Skill Serves

**Primary:** AI Security

**Also useful for:**
- Security Architecture: evaluating AI tools for enterprise deployment
- GRC: AI governance compliance and risk acceptance documentation
- Security Leadership: approval gate decisions and risk acceptance sign-off

---

## Workflow 1: Quick Scan (5-Minute Checklist)

Use for rapid initial screening before deeper evaluation. Invoke via `/scan-skills --depth quick`.

### Inputs for quick scan

```
What to review:    [Plugin directory path | GitHub URL | Skill file(s) | Tool name]
Context:           [What this tool is supposed to do]
Deployment target: [Who will use it and with what data]
```

### Quick scan output

```markdown
## Quick Security Scan: [Tool/Plugin Name]

✅ = Pass   ⚠️ = Concern (explain)   ❌ = Fail (block or require remediation)

**[✅/⚠️/❌] 1. Scope and permissions**
Does the agent request only the permissions necessary for its stated purpose?
[Finding]

**[✅/⚠️/❌] 2. Data handling and exfiltration risk**
Does the agent avoid transmitting sensitive data to uncontrolled external endpoints?
[Finding]

**[✅/⚠️/❌] 3. Prompt injection resistance**
Are there mechanisms to resist prompt injection from untrusted content processed by the agent?
[Finding]

**[✅/⚠️/❌] 4. Human-in-the-loop controls**
Are irreversible or high-stakes actions gated on human confirmation?
[Finding]

**[✅/⚠️/❌] 5. Supply chain and provenance**
Is the source of this agent known and trustworthy? Are dependencies auditable?
[Finding]

**Overall disposition:** [Approved for use | Approved with conditions | Requires full review | Do not deploy]
**Conditions / next steps:** [If not outright approved, what is required]
```

---

## Workflow 2: Full Security Assessment

Use for production deployment decisions, high-risk tools, or tools processing sensitive data.
Invoke via `/scan-skills --depth full`.

### Inputs for full assessment

```
Tool/plugin name:      [Name]
Source:                [GitHub URL | Internal repo | Vendor package]
Tool documentation:    [Link or paste]
Skill/plugin files:    [Paste or provide path to review]
Deployment context:    [Who uses it, what data it touches, what systems it connects to]
Data classification:   [What's the highest classification of data this tool will process?]
Frameworks to apply:   [owasp-llm | atlas | ai-rmf | all (default)]
```

### Full assessment template

```markdown
## AI Agent Security Assessment: [Tool/Plugin Name]
**Assessment date:** [Date]
**Reviewer:** [Human reviewer name — required for governance record]
**Frameworks applied:** OWASP LLM Top 10, MITRE ATLAS, NIST AI RMF
**Source reviewed:** [URL or path]
**Version/commit:** [Specific version or commit hash — assessments are point-in-time]

---

### 1. Tool Summary
**Purpose:** [What the tool does]
**Intended users:** [Roles that will use it]
**Data processed:** [What data flows through this tool]
**External connections:** [What external services does it call]
**Permissions requested:** [What access does it require]

---

### 2. OWASP LLM Top 10 Assessment
*(Reference: frameworks/owasp-llm-top-10.md)*

| # | Risk | Status | Finding |
|---|------|--------|---------|
| LLM01 | Prompt Injection | [✅/⚠️/❌/N/A] | [Finding] |
| LLM02 | Sensitive Information Disclosure | [✅/⚠️/❌/N/A] | [Finding] |
| LLM03 | Supply Chain | [✅/⚠️/❌/N/A] | [Finding] |
| LLM04 | Data and Model Poisoning | [✅/⚠️/❌/N/A] | [Finding] |
| LLM05 | Improper Output Handling | [✅/⚠️/❌/N/A] | [Finding] |
| LLM06 | Excessive Agency | [✅/⚠️/❌/N/A] | [Finding] |
| LLM07 | System Prompt Leakage | [✅/⚠️/❌/N/A] | [Finding] |
| LLM08 | Vector and Embedding Weaknesses | [✅/⚠️/❌/N/A] | [Finding] |
| LLM09 | Misinformation | [✅/⚠️/❌/N/A] | [Finding] |
| LLM10 | Unbounded Consumption | [✅/⚠️/❌/N/A] | [Finding] |

---

### 3. MITRE ATLAS Risk Assessment
*(Reference: frameworks/mitre-atlas.md)*

Evaluate which ATLAS tactics are relevant given the tool's capabilities and attack surface:

| ATLAS Tactic | Relevant? | Assessment |
|--------------|-----------|------------|
| ML Attack Staging | [Yes/No] | [Finding if relevant] |
| Reconnaissance | [Yes/No] | |
| Resource Development | [Yes/No] | |
| Initial Access (ML) | [Yes/No] | |
| ML Model Access | [Yes/No] | |
| Execution (ML) | [Yes/No] | |
| Persistence (ML) | [Yes/No] | |
| Defense Evasion (ML) | [Yes/No] | |
| Collection (ML) | [Yes/No] | |
| Exfiltration via ML | [Yes/No] | |
| Impact (ML) | [Yes/No] | |

---

### 4. NIST AI RMF Alignment
*(Reference: frameworks/nist-ai-rmf.md)*

| AI RMF Function | Assessment |
|-----------------|------------|
| **GOVERN** — Are governance structures in place for this tool's deployment? | [Assessment] |
| **MAP** — Has the AI risk context been mapped (use cases, stakeholders, data)? | [Assessment] |
| **MEASURE** — Are there mechanisms to measure and monitor AI risk in production? | [Assessment] |
| **MANAGE** — Are there response plans if the tool behaves unexpectedly? | [Assessment] |

---

### 5. Permission and Scope Analysis

**Principle of least privilege assessment:**
[Does the tool request only what it needs? List each permission and evaluate necessity]

**Excessive agency risks:**
[Can the tool take irreversible actions? Are they gated on human confirmation?]

**Data exfiltration paths:**
[What external endpoints does the tool call? Are those connections auditable?]

---

### 6. Supply Chain Assessment

**Source trustworthiness:** [Known author/organization | Verified open source | Unknown]
**Dependency audit:**
| Dependency | Version pinned? | Known vulnerabilities? | License |
|------------|----------------|----------------------|---------|
| [package] | [Yes/No] | [Check result] | [License] |

**Update mechanism:** [How are updates delivered? Is there version pinning?]

---

### 7. Findings Summary

| Finding | Severity | OWASP/ATLAS ref | Remediation required |
|---------|----------|-----------------|----------------------|
| [Finding description] | [Critical/High/Medium/Low] | [Reference] | [Required action] |

---

### 8. Deployment Recommendation

**Overall risk rating:** [Critical | High | Medium | Low]
**Recommendation:** [Approve | Approve with conditions | Requires remediation | Do not deploy]

**Conditions for approval (if applicable):**
- [ ] [Condition 1]
- [ ] [Condition 2]

**Risk acceptance required from:** [Role/authority level per security.local.md]
**Reviewer sign-off:** _________________________ Date: _________
```

---

## Working with Tools

### MCP connectors this skill uses

| Connector | Used for | Priority |
|-----------|----------|----------|
| **Documentation** (SharePoint, Confluence) | Retrieving tool documentation, existing assessments | Medium |
| **GitHub (via gh CLI or MCP)** | Source code review, dependency audit, version history | High for code review |
| **GRC Platform** | Recording assessment results, tracking remediation | Medium |
| **Ticketing** | Creating remediation tracking tickets | Low |

This skill is primarily document-driven rather than API-driven. The highest value MCP connection is
access to source code repositories for the tool under review.

---

## What This Skill Does NOT Do

- **Does not perform dynamic testing or fuzzing.** It reviews design, documentation, and code — it does not run the tool and test it at runtime.
- **Does not audit model weights or training data.** Black-box model behavior is not assessable through this skill.
- **Does not provide a security guarantee.** A clean review finding indicates the design appears sound; it does not certify the tool is free of vulnerabilities.
- **Does not make deployment decisions autonomously.** Human sign-off is required on every deployment decision — see the governance record template above.
- **Does not cover on-premise/self-hosted model deployments.** Infrastructure security for self-hosted models is covered by the security-architecture-review skill.
- **Does not assess business value or ROI.** This skill assesses security risk only; business value decisions belong to the tool's sponsor.
