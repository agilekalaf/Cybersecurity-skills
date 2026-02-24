# /scan-skills

Security review of AI agents, plugins, MCP servers, or skill files. Produces a quick checklist
or a full security assessment report against OWASP LLM Top 10, MITRE ATLAS, and NIST AI RMF.

## Usage

```
/scan-skills ./path/to/plugin
/scan-skills https://github.com/org/ai-plugin --depth full
/scan-skills ./skills/custom-skill/SKILL.md --depth quick
/scan-skills --depth full --framework owasp-llm
/scan-skills ./mcp-server/ --output findings-only
/scan-skills "agent description and capabilities" --depth quick
```

## What This Command Does

Invokes the ai-agent-review skill to perform a structured security assessment of an AI tool,
plugin, MCP server, or agentic workflow. At `--depth quick`, produces a 5-point checklist in
minutes. At `--depth full`, runs a comprehensive assessment against OWASP LLM Top 10, MITRE
ATLAS, and NIST AI RMF, producing a governance-ready report that includes a human sign-off field.
Every deployment decision still requires human authorization — this command generates the evidence
for that decision.

## Parameters

| Parameter | Values | Default |
|-----------|--------|---------|
| `--depth` | `quick`, `full` | `full` |
| `--framework` | `owasp-llm`, `atlas`, `ai-rmf`, `all` | `all` |
| `--output` | `summary`, `report`, `findings-only` | `report` |
| `--context` | Brief description of deployment context | Not set |
| `--data-class` | `public`, `internal`, `confidential`, `restricted` | `internal` |

## Workflow

**For `--depth quick`:**
1. Parse the provided plugin/skill/description for surface-level analysis
2. Evaluate against 5 quick-scan criteria:
   - Scope and permissions (least privilege)
   - Data handling and exfiltration risk
   - Prompt injection resistance
   - Human-in-the-loop controls for high-stakes actions
   - Supply chain and provenance
3. Produce ✅ / ⚠️ / ❌ checklist with disposition and conditions

**For `--depth full`:**
1. Load `security.local.md` for AI governance policy and data classification limits
2. Load relevant framework modules (`frameworks/owasp-llm-top-10.md`, `frameworks/mitre-atlas.md`,
   `frameworks/nist-ai-rmf.md`) based on `--framework`
3. Review all provided source files, documentation, and dependency manifests
4. Conduct structured assessment against each framework
5. Perform permission and scope analysis
6. Conduct supply chain assessment (dependencies, version pinning, update mechanism)
7. Generate full assessment report with findings table and deployment recommendation
8. Produce governance decision record requiring human sign-off

## Output

**`--depth quick`:**
- 5-point ✅ / ⚠️ / ❌ checklist
- Overall disposition: Approved / Approved with conditions / Requires full review / Do not deploy
- Next steps

**`--depth full` / `--output report`:**
- Tool summary and deployment context
- OWASP LLM Top 10 assessment (all 10 categories)
- MITRE ATLAS tactic assessment
- NIST AI RMF function assessment
- Permission and scope analysis
- Supply chain assessment with dependency table
- Findings summary table with severity and remediation
- Deployment recommendation with conditions
- Governance decision record (requires human sign-off before deployment)

**`--output findings-only`:**
- Findings table only — for teams who want findings without the full report structure

## When to Use This

- **Before deploying any new AI tool or plugin:** Standard governance gate
- **Reviewing open-source AI plugins:** Community plugins require security review before use
- **MCP server evaluation:** Before connecting a new MCP server to your AI environment
- **Periodic re-review:** AI tools should be re-assessed after major updates
- **Self-review of skills you've built:** Validate your own plugins before publishing
- **Responding to AI governance requests:** Produce documented evidence of AI security review

## Dependencies

**Minimal (no MCP):** Works from manually provided plugin code, documentation, or descriptions.
Highest value workflow for this command is providing the actual skill/plugin files for review.

**Useful:**
- Documentation platform: retrieve plugin documentation and prior assessments
- GRC Platform: store assessment results as AI governance evidence
- GitHub access (gh CLI): source code review, dependency audit

## Related

- **Skill:** `skills/ai-agent-review/SKILL.md` (full documentation and assessment templates)
- **Skill:** `skills/ai-governance/SKILL.md` — governance policy that these reviews satisfy
- **Frameworks:** `frameworks/owasp-llm-top-10.md`, `frameworks/mitre-atlas.md`, `frameworks/nist-ai-rmf.md`
- **Command:** `/assess-risk` — AI deployment risks feed the enterprise risk register
