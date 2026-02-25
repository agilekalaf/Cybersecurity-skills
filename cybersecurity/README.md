# Cybersecurity Plugin for Claude Code

AI-augmented workflows for cybersecurity teams — from SOC analysts triaging alerts to CISOs
preparing board reports. This plugin provides structured, repeatable security workflows powered
by AI, configurable to any organization's tools, frameworks, and risk appetite.

> **Disclaimer:** This plugin assists with cybersecurity workflows but does not replace professional
> security judgment. AI-generated analysis should be reviewed by qualified security professionals
> before being relied upon for security decisions.

---

## Governing Philosophy: PLAID

**People Led, AI Driven.**

AI handles the speed-intensive analytical work: IOC enrichment, control mapping, report drafting,
gap analysis, evidence organization. Humans retain decision authority: containment actions, risk
acceptance, audit attestations, policy approval, and any decision with real-world consequences.

Every skill in this plugin is built on this principle. AI accelerates; humans decide.

---

## Who This Is For

Seven security personas, one plugin:

| Role | Primary skills | Primary commands |
|------|---------------|-----------------|
| **Security Operations** | incident-response, threat-intelligence, vulnerability-management | /triage-alert, /investigate, /threat-brief |
| **Governance, Risk & Compliance** | compliance-assessment, policy-management, risk-assessment, audit-support | /assess-compliance, /assess-risk |
| **Identity & Access Management** | access-review | /review-access |
| **Application Security** | security-architecture-review, ai-agent-review | /scan-skills |
| **Security Architecture & Engineering** | security-architecture-review, vulnerability-management | /scan-skills |
| **Security Leadership** | security-reporting, risk-assessment, compliance-assessment | /prep-report, /assess-risk |
| **AI Security** | ai-agent-review, ai-governance | /scan-skills |

---

## Quick Start

### 1. Install the plugin

```bash
# Clone or copy the cybersecurity/ directory to your Claude plugins location
# Following the pattern from anthropics/knowledge-work-plugins
```

### 2. Configure your organization

```bash
cp security.local.example.md security.local.md
# Edit security.local.md with your organization's details
# DO NOT commit security.local.md — add it to .gitignore
```

### 3. Connect MCP tools (optional but recommended)

```bash
cp .mcp.json.example .mcp.json  # .mcp.json is already the config file
# Edit .mcp.json with your tool credentials
# See CONNECTORS.md for setup instructions
```

Fastest path: add **Feedly + VirusTotal** for immediate threat intelligence capability.
Everything else works without connectors.

### 4. Run your first command

```
/threat-brief                          # Daily threat briefing for your sector
/triage-alert "suspicious login alert" # Triage an alert
/assess-compliance --framework nist-csf-2.0  # Run a quick maturity assessment
```

---

## Full Directory Structure

```
cybersecurity/
├── .claude-plugin/
│   └── plugin.json                    # Plugin manifest
├── .mcp.json                          # MCP connector configuration
├── CONNECTORS.md                      # Connector setup guide
├── LICENSE                            # Apache 2.0
├── README.md                          # This file
├── security.local.example.md          # Org config template (copy to security.local.md)
│
├── commands/                          # Slash command entry points
│   ├── assess-compliance.md           # /assess-compliance
│   ├── assess-risk.md                 # /assess-risk
│   ├── investigate.md                 # /investigate
│   ├── prep-report.md                 # /prep-report
│   ├── review-access.md               # /review-access
│   ├── scan-skills.md                 # /scan-skills
│   ├── threat-brief.md                # /threat-brief
│   └── triage-alert.md                # /triage-alert
│
├── skills/                            # Full workflow documentation
│   ├── access-review/SKILL.md
│   ├── ai-agent-review/SKILL.md
│   ├── ai-governance/SKILL.md
│   ├── audit-support/SKILL.md
│   ├── compliance-assessment/SKILL.md
│   ├── incident-response/SKILL.md
│   ├── policy-management/SKILL.md
│   ├── risk-assessment/SKILL.md
│   ├── security-architecture-review/SKILL.md
│   ├── security-reporting/SKILL.md
│   ├── threat-intelligence/SKILL.md
│   └── vulnerability-management/SKILL.md
│
└── frameworks/                        # Compliance framework reference modules
    ├── README.md
    ├── cmmc.md
    ├── iso-27001.md
    ├── mitre-atlas.md
    ├── nerc-cip.md
    ├── nist-800-53.md
    ├── nist-ai-rmf.md
    ├── nist-csf-2.0.md
    ├── owasp-llm-top-10.md
    └── soc2.md
```

---

## Skills Reference

### Security Operations

**incident-response** — Full incident response lifecycle. Alert triage, investigation,
containment, eradication, recovery, and lessons learned. PICERL-based workflow with ATT&CK
mapping and IOC enrichment built in.

**threat-intelligence** — IOC enrichment, threat actor profiling, campaign tracking, and
threat hunt hypothesis generation. Orchestrates Feedly, OpenCTI, VirusTotal, AbuseIPDB,
Shodan, and CISA KEV.

**vulnerability-management** — Risk-based prioritization beyond CVSS. Combines exploitation
intelligence (CISA KEV, threat feeds), asset criticality, and exposure to surface what actually
needs to be fixed. Tracks SLA compliance and manages exceptions.

### Governance, Risk & Compliance

**compliance-assessment** — Framework-based maturity scoring, gap analysis, and remediation
roadmaps. Loads framework modules dynamically. Supports multi-framework assessment with
overlap analysis (NIST CSF + SOC 2 + ISO 27001 simultaneously).

**policy-management** — Policy drafting, review, control mapping, and exception tracking.
Produces audit-quality policy documents with control cross-references.

**risk-assessment** — Individual risk assessment, risk register management, risk heat maps,
and third-party vendor risk assessment. Supports qualitative matrix and FAIR-referenced
quantitative approaches.

**audit-support** — Evidence collection planning, control testing worksheets, finding
tracking, and auditor communication templates. Works closely with compliance-assessment.

### Identity & Access Management

**access-review** — Periodic access certification, least-privilege analysis, SoD conflict
detection, orphan account identification, and privileged access assessment. PAM coverage scoring.

### Application Security / Security Architecture

**security-architecture-review** — Design review, cloud posture assessment, zero trust
evaluation, and architectural risk identification. Pre-build (design review) and post-build
(existing system assessment) modes.

### Security Leadership

**security-reporting** — Board-ready metrics, ELT dashboards, KPI/OKR scorecards. Every
audience gets the right level of detail — boards see risk and investment; operations teams
see metrics and trends.

### AI Security

**ai-agent-review** — Security assessment of AI agents, plugins, and MCP servers against
OWASP LLM Top 10, MITRE ATLAS, and NIST AI RMF. Quick scan (5-point checklist) and full
governance-ready assessment report.

**ai-governance** — Organizational AI governance framework. Deployment approval process,
acceptable use policy, AI risk register, and NIST AI RMF alignment. PLAID is the default
philosophy; organizations can configure their own.

---

## Commands Reference

| Command | What it does | Primary skill |
|---------|-------------|---------------|
| `/threat-brief` | Daily/weekly threat intelligence briefing for your sector | threat-intelligence |
| `/investigate [ioc]` | Deep-dive investigation of an indicator, actor, or CVE | threat-intelligence |
| `/triage-alert` | Rapid triage of an incoming alert or suspicious activity report | incident-response |
| `/assess-compliance` | Framework assessment, gap analysis, or remediation roadmap | compliance-assessment |
| `/review-access` | Access certification, privilege analysis, SoD conflict detection | access-review |
| `/assess-risk` | Risk assessment and risk register entry for a scenario or vendor | risk-assessment |
| `/prep-report` | Board briefing, ELT update, or operational dashboard narrative | security-reporting |
| `/scan-skills` | Security review of AI agents, plugins, or MCP servers | ai-agent-review |

---

## Three-Tier Architecture

The plugin separates portable logic from framework knowledge from org-specific configuration:

```
Tier 1: Skills          — Framework-agnostic workflow patterns (skills/*/SKILL.md)
Tier 2: Framework Modules — Loadable compliance framework references (frameworks/*.md)
Tier 3: Local Config    — Organization-specific settings (security.local.md)
```

**Tier 1 — Skills** define *how* to execute a security workflow. They are portable across
any organization and reference framework modules and local config without hardcoding specifics.

**Tier 2 — Framework Modules** provide structured compliance framework references that skills
load as needed. They are AI-consumption-optimized summaries — not reproductions of source documents.
See `frameworks/README.md` for the current module library and how to add new frameworks.

**Tier 3 — Local Config** (`security.local.md`) is your organization's playbook: risk appetite,
tool stack, escalation contacts, active frameworks, maturity targets, AI governance policy.
This file is never committed to the repo.

---

## Getting Started by Role

### I'm a SOC analyst
1. Configure `security.local.md` with your SIEM, EDR, and severity definitions
2. Connect SIEM + EDR + VirusTotal in `.mcp.json`
3. Use `/triage-alert` as your first-response workflow
4. Use `/investigate` for deep-dive IOC investigation
5. Use `/threat-brief` for daily team standup briefings

### I'm a GRC / compliance professional
1. Configure `security.local.md` with your active frameworks and maturity targets
2. Connect your GRC platform and documentation store
3. Use `/assess-compliance --framework [your-framework]` for gap analysis
4. Use audit-support skill for evidence collection planning
5. Use `/assess-risk` to feed compliance gaps into the risk register

### I'm a CISO or security leader
1. Configure all sections of `security.local.md` — especially reporting cadence and board metrics
2. Use `/prep-report --audience board` for quarterly board briefings
3. Use `/assess-risk` for risk quantification and board-level risk framing
4. Use the ai-governance skill to establish your AI governance posture

### I'm evaluating AI tools for deployment
1. Gather the plugin/tool's documentation, source code, and deployment context
2. Use `/scan-skills --depth quick [path]` for rapid screening
3. Use `/scan-skills --depth full [path]` for deployment-gate assessment
4. Use the ai-governance skill to document the governance decision

---

## Framework Module System

The `frameworks/` directory contains structured reference modules for supported compliance
frameworks. When a skill needs framework-specific knowledge (e.g., NIST CSF control categories,
SOC 2 evidence requirements), it loads the relevant module dynamically.

**Currently supported frameworks:**
NIST CSF 2.0 · NIST SP 800-53 Rev 5 · ISO/IEC 27001:2022 · NERC CIP ·
CMMC 2.0 · SOC 2 · MITRE ATLAS · NIST AI RMF 1.0 · OWASP LLM Top 10 (2025)

**Adding new frameworks:** See `frameworks/README.md` for the structure guide and contribution process.

**Planned additions:** IEC 62443 (ICS/OT), PCI-DSS 4.0, HIPAA Security Rule, FedRAMP, DORA (EU).

---

## Roadmap

- **ICS/OT Security** — Skills for operational technology environments (IEC 62443, NERC CIP OT-specific)
- **Additional industry extensions** — Healthcare (HIPAA), Financial Services (FFIEC), Defense (CMMC)
- **More framework modules** — PCI-DSS 4.0, FedRAMP, DORA
- **Extended AI security** — ML pipeline security, AI red teaming workflows

Contributions welcome — see Contributing section.

---

## Contributing

This plugin is open source under Apache 2.0. Contributions are welcome:

- **New skills:** Follow the structure in existing `skills/*/SKILL.md` files
- **New commands:** Follow the structure in existing `commands/*.md` files
- **New framework modules:** Follow the structure guide in `frameworks/README.md`
- **Bug reports and improvements:** Open an issue or pull request

When contributing skills or commands, ensure they:
- Follow the PLAID philosophy and never recommend autonomous high-stakes actions
- Include a "What this skill does NOT do" section with clear boundaries
- Degrade gracefully when MCP connectors are not available
- Are written for real practitioners — not as marketing copy or academic descriptions

---

## License

Apache License 2.0. See `LICENSE` for full text.

---

## Disclaimer

This plugin assists with cybersecurity workflows but does not replace professional security
judgment. AI-generated analysis should be reviewed by qualified security professionals before
being relied upon for security decisions. All recommendations are starting points for human
review, not final determinations.
