# Cybersecurity Plugin for Claude Cowork — Build Specification

## What this is

You are building an open-source cybersecurity plugin for Claude Cowork (and Claude Code), modeled on Anthropic's official knowledge-work-plugins repository (https://github.com/anthropics/knowledge-work-plugins). Specifically, it follows the architectural patterns established by the legal plugin in that repo.

This plugin provides AI-augmented workflows for cybersecurity teams — from SOC analysts triaging alerts to CISOs preparing board reports. It is platform-agnostic (tools connect via MCP), framework-aware (loads compliance frameworks as needed), and organization-customizable (via a local config file).

The governing philosophy is **PLAID (People Led, AI Driven)**: AI handles speed-intensive analytical work; humans retain decision authority. Every recommendation is framed as a recommendation, not a conclusion.

## What already exists

Three skill files, two command files, and a config template have already been written and are in the project directory. These are your **pattern templates** — every new file you create should match their style, structure, depth, and conventions. Read them carefully before generating anything new.

Existing files:
```
cybersecurity/
├── security.local.example.md          ← Org-specific config template (Tier 3)
├── skills/
│   ├── incident-response/SKILL.md     ← Pattern template for "traditional security" skills
│   ├── threat-intelligence/SKILL.md   ← Pattern template for tool-heavy orchestration skills
│   └── ai-agent-review/SKILL.md       ← Pattern template for "AI security" skills
└── commands/
    ├── threat-brief.md                ← Pattern template for proactive commands
    └── investigate.md                 ← Pattern template for reactive commands
```

## Architecture: Three-tier design

The plugin uses a three-tier architecture that separates portable workflow logic from framework-specific knowledge from organization-specific configuration:

**Tier 1 — Skills (framework-agnostic workflow patterns)**
SKILL.md files that define *how* to execute a security workflow. These are portable across any organization. They reference framework modules and local config but don't hardcode specifics.

**Tier 2 — Framework Modules (loadable context packs)**
Markdown reference files in `frameworks/` that provide control mappings, maturity definitions, assessment criteria, and regulatory requirements for specific compliance frameworks. Skills load the relevant module(s) based on what's configured in the org's local config.

**Tier 3 — Organization-Specific Config (security.local.md)**
The org's playbook — risk appetite, tool stack, escalation contacts, active frameworks, maturity targets, AI governance policy. This file is NOT committed to the repo; `security.local.example.md` is the template. Already written.

## Roles (7 personas the plugin serves)

Each skill notes which roles it primarily serves and adjusts depth/language accordingly.

1. **Security Operations** — SOC analysts, incident responders, threat hunters. Day-to-day detection and response.
2. **Governance, Risk & Compliance** — Framework assessments, audit prep, policy management, regulatory reporting.
3. **Identity & Access Management** — Access reviews, privilege management, identity governance.
4. **Application Security** — Secure code review, SDLC integration, vulnerability assessment, API security.
5. **Security Architecture & Engineering** — Reference architectures, tool evaluations, secure design patterns, cloud security posture.
6. **Security Leadership** — CISO/CTSO-level. Board reporting, risk quantification, program strategy, vendor management, budget justification.
7. **AI Security** — AI governance, agent security review, AI risk assessment, model deployment evaluation.

## Full file manifest — what to build

### Files that already exist (DO NOT recreate — use as pattern reference)
- `security.local.example.md`
- `skills/incident-response/SKILL.md`
- `skills/threat-intelligence/SKILL.md`
- `skills/ai-agent-review/SKILL.md`
- `commands/threat-brief.md`
- `commands/investigate.md`

### Skills to create (9 remaining)

Each SKILL.md must include:
- YAML frontmatter with `name` and `description` (description should be "pushy" for triggering — include multiple trigger phrases and contexts, see existing skills for examples)
- Opening paragraph explaining what the skill does
- PLAID philosophy callout (blockquote format, tailored to the skill's domain)
- "Before you begin" section referencing `security.local.md`
- "Roles this skill serves" section with role-appropriate guidance
- Core workflow(s) with structured output templates
- "Working with tools" section describing relevant MCP connector categories
- "What this skill does NOT do" boundary section
- Target length: 150-300 lines. Enough to be genuinely useful, not so long it bloats context.

**1. compliance-assessment/SKILL.md**
- Primary roles: GRC, Security Leadership
- Purpose: Framework-based maturity assessment, gap analysis, remediation planning
- Key workflow: Load applicable framework module(s) from `frameworks/`, assess current state against control requirements, identify gaps, score maturity, generate remediation roadmap
- Must support multi-framework assessment (orgs often operate under NIST CSF + NERC CIP + SOC 2 simultaneously)
- Output: Maturity scorecard, gap analysis with prioritized remediation, framework-specific evidence requirements
- References: compliance-assessment loads framework modules dynamically based on security.local.md config
- MCP connectors: GRC platform, documentation/evidence stores, ticketing

**2. policy-management/SKILL.md**
- Primary roles: GRC, Security Leadership
- Purpose: Policy drafting, review cycles, exception tracking, mapping policies to controls
- Key workflow: Draft or review security policies, map policy requirements to framework controls, track policy exceptions and their risk acceptance
- Output: Policy documents, control mapping matrices, exception registers with risk justification
- MCP connectors: Documentation (SharePoint/Confluence), GRC platform, ticketing

**3. access-review/SKILL.md**
- Primary roles: IAM, GRC
- Purpose: Periodic access certification, privilege analysis, SoD conflict detection, orphan account identification
- Key workflow: Pull access data from identity platforms, analyze against least-privilege principles, identify over-provisioned accounts, detect separation of duties conflicts, generate certification reports
- Output: Access review report with findings, SoD conflict matrix, orphan account list, remediation recommendations
- MCP connectors: Identity & Access (Entra ID, SailPoint, CyberArk, Okta), ticketing

**4. vulnerability-management/SKILL.md**
- Primary roles: Security Operations, Security Architecture
- Purpose: Vulnerability triage, risk-based prioritization, remediation tracking, SLA compliance
- Key workflow: Ingest vulnerability scan results, prioritize using risk context (CVSS + threat intelligence on active exploitation + asset criticality + exposure), track remediation against SLAs, escalate overdue items
- Should integrate with threat-intelligence skill for exploitation context (CISA KEV, Feedly exploit intelligence)
- Output: Prioritized vulnerability report, SLA compliance dashboard data, exception/risk acceptance documentation
- MCP connectors: Vulnerability scanner (Qualys, Tenable, Defender), threat intelligence, ticketing, CMDB

**5. security-architecture-review/SKILL.md**
- Primary roles: Security Architecture, Application Security
- Purpose: Design review against security patterns, cloud posture assessment, zero trust evaluation
- Key workflow: Review proposed architecture/design against security reference patterns, evaluate cloud configurations, assess zero trust maturity, identify architectural risks
- Output: Architecture review findings with risk ratings, recommended design changes, compensating controls
- MCP connectors: Cloud security (Defender for Cloud, Prisma, Wiz), documentation

**6. risk-assessment/SKILL.md**
- Primary roles: GRC, Security Leadership
- Purpose: Risk register management, risk quantification, third-party/vendor risk assessment, risk reporting
- Key workflow: Identify risks, assess likelihood and impact (support both qualitative and quantitative approaches), document in risk register format, track treatment plans, assess third-party/vendor risks
- Should support common risk quantification approaches (risk matrices, FAIR methodology reference)
- Output: Risk register entries, risk heat maps (data for visualization), vendor risk assessments, risk treatment plans
- MCP connectors: GRC platform, ticketing, documentation

**7. security-reporting/SKILL.md**
- Primary roles: Security Leadership
- Purpose: Board-ready metrics, ELT dashboards, KPI/OKR tracking, program status reporting
- Key workflow: Aggregate data from other skills' outputs and tool sources, generate audience-appropriate reports (board vs ELT vs operational), track KPIs/OKRs against targets
- Should reference the reporting requirements and metrics from security.local.md
- Output: Board report drafts, ELT dashboard narratives, KPI scorecards, NIST CSF maturity trend reports
- MCP connectors: GRC platform, SIEM (for operational metrics), vulnerability scanner (for vuln metrics), documentation

**8. audit-support/SKILL.md**
- Primary roles: GRC
- Purpose: Evidence collection, control testing documentation, audit response coordination, finding remediation tracking
- Key workflow: Map audit requests to controls, identify evidence sources, compile evidence packages, document control testing results, track audit findings through remediation
- Should work closely with compliance-assessment skill (assessments feed audits)
- Output: Evidence collection matrices, control testing worksheets, audit finding tracker, remediation status reports
- MCP connectors: GRC platform, documentation/evidence stores, ticketing, identity (for access-related evidence)

**9. ai-governance/SKILL.md**
- Primary roles: AI Security, Security Leadership, GRC
- Purpose: Policy framework for AI deployment decisions, acceptable use governance, AI risk management
- Key workflow: Evaluate AI deployment proposals against governance criteria, assess data classification implications, determine human-in-the-loop requirements, map to AI risk frameworks (NIST AI RMF, MITRE ATLAS)
- Works closely with ai-agent-review (governance sets policy, agent-review operationalizes it)
- Should reference PLAID principles as the default governance philosophy, with security.local.md allowing orgs to substitute their own
- Output: AI deployment risk assessments, governance decision records, AI acceptable use policy templates, AI risk register entries
- MCP connectors: Documentation, GRC platform, ticketing

### Commands to create (6 remaining)

Each command file must include:
- Title with slash command name
- Usage examples showing common invocations with parameters
- "What this command does" explanation
- Parameters section
- Workflow section (numbered steps referencing which skill(s) are invoked)
- Output section describing what the user gets
- "When to use this" with concrete scenarios
- Dependencies (required and recommended MCP connections)
- Related commands and skills
- Target length: 60-100 lines. Commands are concise entry points, not full documentation.

**1. commands/triage-alert.md**
- Invokes: incident-response skill (Phase 1: Alert triage)
- Input: Alert payload, log entry, SIEM output, or natural language description of suspicious activity
- Parameters: --severity-override, --source (SIEM/EDR/user-report), --quick (abbreviated output)
- Output: Triage summary with severity, ATT&CK mapping, enriched IOCs, recommended next steps

**2. commands/assess-compliance.md**
- Invokes: compliance-assessment skill
- Input: Framework name(s) and scope
- Parameters: --framework (nist-csf, nerc-cip, iso-27001, etc.), --scope (full/function/category), --format (scorecard/gaps/roadmap)
- Output: Maturity assessment, gap analysis, or remediation roadmap depending on format parameter

**3. commands/review-access.md**
- Invokes: access-review skill
- Input: User account, role, group, or scope for periodic review
- Parameters: --scope (user/role/group/org-wide), --focus (privilege/sod/orphan/all), --period (review period)
- Output: Access review findings with recommendations

**4. commands/assess-risk.md**
- Invokes: risk-assessment skill
- Input: Risk scenario description, vendor name, or system reference
- Parameters: --type (operational/vendor/project/system), --methodology (qualitative/fair), --register (add to risk register)
- Output: Risk assessment with scoring, treatment options, risk register entry

**5. commands/prep-report.md**
- Invokes: security-reporting skill
- Input: Report type and audience
- Parameters: --audience (board/elt/operational), --period (monthly/quarterly/annual), --focus (compliance/incidents/risk/program/all)
- Output: Audience-appropriate security report draft

**6. commands/scan-skills.md**
- Invokes: ai-agent-review skill
- Input: Plugin directory path, GitHub URL, or skill file(s)
- Parameters: --depth (quick/full), --framework (owasp-llm/atlas/ai-rmf), --output (summary/report/findings-only)
- Output: Quick scan result (5-point checklist) or full security review report

### Framework Modules to create (9 files)

Each framework module in `frameworks/` is a structured reference document that skills load for context. These are NOT full framework reproductions (copyright concerns and they'd be massive). They are structured summaries optimized for AI consumption during assessments.

Each framework module must include:
- Framework name, version, and issuing body
- Brief purpose statement (2-3 sentences)
- Structure overview (how the framework is organized)
- Key components table (control families/functions/domains with brief descriptions)
- Maturity model or tier definitions (if applicable)
- Common assessment approach
- Mapping relationships to other frameworks (e.g., NIST CSF ↔ 800-53 ↔ ISO 27001)
- Regulatory context (who requires this and when)
- Target length: 80-150 lines. Enough for the AI to conduct a meaningful assessment, not a reproduction of the full framework document.

**1. frameworks/nist-csf-2.0.md**
- NIST Cybersecurity Framework 2.0 (2024)
- 6 Functions (Govern, Identify, Protect, Detect, Respond, Recover), Categories, Subcategories
- Implementation Tiers (1-4) with definitions
- Note: CSF 2.0 added the Govern function — this is a significant change from 1.1

**2. frameworks/nist-800-53.md**
- NIST SP 800-53 Rev 5
- 20 control families with descriptions
- Baseline mappings (Low/Moderate/High)
- Relationship to NIST CSF (800-53 controls map to CSF subcategories)

**3. frameworks/nerc-cip.md**
- NERC Critical Infrastructure Protection standards
- CIP-002 through CIP-014 with descriptions
- BES Cyber System categorization (High/Medium/Low impact)
- Enforcement and penalty context
- Specific to electric utilities and bulk electric system operators

**4. frameworks/iso-27001.md**
- ISO/IEC 27001:2022
- ISMS requirements overview
- Annex A control themes (Organizational, People, Physical, Technological)
- Certification process summary
- Mapping to NIST CSF and 800-53

**5. frameworks/cmmc.md**
- Cybersecurity Maturity Model Certification 2.0
- 3 levels with descriptions
- Relationship to NIST 800-171
- DoD supply chain context and assessment requirements

**6. frameworks/soc2.md**
- SOC 2 (AICPA Trust Services Criteria)
- 5 Trust Service Categories (Security, Availability, Processing Integrity, Confidentiality, Privacy)
- Type I vs Type II distinction
- Common audit cycle and evidence requirements

**7. frameworks/mitre-atlas.md**
- MITRE ATLAS (Adversarial Threat Landscape for AI Systems)
- Tactic categories for AI/ML systems
- Key technique descriptions relevant to enterprise AI agent deployments
- Case studies reference (point to ATLAS website, don't reproduce)
- Relationship to ATT&CK for positioning

**8. frameworks/nist-ai-rmf.md**
- NIST AI Risk Management Framework 1.0
- 4 Functions (Govern, Map, Measure, Manage) with categories
- AI risk taxonomy
- Relationship to NIST CSF for organizations already using CSF

**9. frameworks/owasp-llm-top-10.md**
- OWASP Top 10 for LLM Applications (2025)
- All 10 categories with descriptions and examples
- Mapping to traditional OWASP Top 10 where applicable
- Practical relevance: this is the most actionable framework for day-to-day AI agent security reviews

### Plugin scaffolding files (4 files)

**1. .claude-plugin/plugin.json**
- Follow the exact format from the legal plugin in anthropics/knowledge-work-plugins
- Plugin name: "cybersecurity"
- Description: "AI-augmented cybersecurity operations — incident response, threat intelligence, compliance assessment, vulnerability management, risk analysis, and AI security governance. Supports SOC analysts through CISOs with framework-aware, tool-agnostic workflows configurable to any organization's security program."
- List all skills and commands

**2. .mcp.json**
- Define all MCP connector categories with placeholder configurations
- Categories (from our architecture):
  - SIEM/Log Management (Sentinel, Splunk, Chronicle, Elastic)
  - SOAR/Automation (Sentinel SOAR, Phantom, XSOAR, Tines)
  - Identity & Access (Entra ID, SailPoint, CyberArk, Okta)
  - Vulnerability Scanner (Qualys, Tenable, Rapid7, Defender)
  - Endpoint/EDR (Defender for Endpoint, CrowdStrike, SentinelOne)
  - Ticketing/Workflow (ServiceNow, Jira)
  - GRC Platform (Archer, ServiceNow GRC, LogicGate, Hyperproof)
  - Threat Intelligence (Feedly, OpenCTI, VirusTotal, Cyber Sentinel, Shodan, AbuseIPDB, CISA KEV)
  - Cloud Security (Defender for Cloud, Prisma Cloud, Wiz)
  - Email/Collaboration (Exchange, Teams, Slack)
  - Documentation (SharePoint, Confluence, Google Drive)
- Include comments explaining each connector category
- Format as working examples with placeholder credentials/URLs

**3. CONNECTORS.md**
- Comprehensive connector documentation
- For each MCP connector category: what it does, which skills use it, setup instructions (or links to MCP server repos), required permissions, graceful degradation notes
- Highlight the "try this first" path: Feedly + OpenCTI + Cyber Sentinel gives you threat intelligence workflows immediately with minimal setup
- Include a quick-start section for the fastest path to a working plugin

**4. README.md**
- This is the front door. It must:
  - Open with a clear, compelling description of what this plugin does and who it's for
  - Include the PLAID philosophy summary
  - Show the full directory structure
  - List all roles, skills, and commands with one-line descriptions
  - Explain the three-tier architecture (skills → frameworks → local config)
  - Provide a quick-start guide (install, configure security.local.md, connect MCP servers, run /threat-brief)
  - Document the framework module system and how to add new frameworks
  - Include a "Getting started by role" section showing which commands/skills are most relevant for each persona
  - Note that ICS/OT Security and additional industry-specific extensions are planned
  - Include contributing guidelines
  - Apache 2.0 license reference
  - Disclaimer: "This plugin assists with cybersecurity workflows but does not replace professional security judgment. AI-generated analysis should be reviewed by qualified security professionals before being relied upon for security decisions."

**5. LICENSE**
- Apache 2.0 (matching the knowledge-work-plugins repo)

## Style and convention guide

Based on the existing files, maintain these conventions:

**SKILL.md files:**
- YAML frontmatter: `name` (kebab-case) and `description` (aggressive trigger phrasing)
- H1 title matching the skill name in title case
- Opening paragraph: what this skill does, 2-3 sentences
- PLAID blockquote: `> **Philosophy: People Led, AI Driven (PLAID)**` followed by skill-specific principles
- Sections use H2 (`##`). Subsections use H3 (`###`).
- Structured output templates use fenced code blocks with markdown inside
- Tables for structured comparisons (severity matrices, tool selection, framework mappings)
- "What this skill does NOT do" is always the final section — bulleted list of explicit boundaries
- Tone: authoritative but practical. Write like a senior security practitioner explaining to a capable colleague, not like a textbook or a vendor marketing doc.

**Command files:**
- H1 title with slash command: `# /command-name`
- Usage section with code block showing example invocations
- Concise — commands are entry points, not full documentation. The skill does the heavy lifting.
- Always end with Dependencies and Related sections

**Framework modules:**
- H1 title with framework name and version
- Structured for AI consumption — tables and clear hierarchies, not prose-heavy
- Include cross-references to other framework modules where mappings exist
- Do NOT reproduce copyrighted framework content verbatim. Summarize, structure, and reference.

**General:**
- No emojis in skill or command files (the quick scan checkmarks ✅ ⚠️ ❌ in ai-agent-review are the one exception — those serve a functional purpose)
- American English
- Oxford comma
- Line length: wrap at ~120 characters for readability in editors
- Cross-references between files use relative paths and are explicit about which skill/command/framework is being referenced

## Build order

Suggested build sequence to maintain consistency:

1. Read all existing files thoroughly — internalize the patterns
2. Generate the 9 remaining skills (these are the most important files)
3. Generate the 6 remaining commands
4. Generate the 9 framework modules
5. Generate plugin scaffolding (plugin.json, .mcp.json, CONNECTORS.md, README.md, LICENSE)
6. Review all cross-references between files for consistency
7. Verify the complete directory structure matches the manifest

## Final directory structure

```
cybersecurity/
├── .claude-plugin/
│   └── plugin.json
├── .mcp.json
├── CONNECTORS.md
├── LICENSE
├── README.md
├── security.local.example.md
├── commands/
│   ├── assess-compliance.md
│   ├── assess-risk.md
│   ├── investigate.md
│   ├── prep-report.md
│   ├── review-access.md
│   ├── scan-skills.md
│   ├── threat-brief.md
│   └── triage-alert.md
├── skills/
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
└── frameworks/
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

Total: 33 files (6 existing + 27 to generate)

## Important reminders

- This is an open-source contribution intended to be published on GitHub. Write with the assumption that security professionals worldwide will read, evaluate, and fork this.
- The plugin should work out of the box with zero MCP connections (graceful degradation everywhere) and get progressively more powerful as connections are added.
- Do not reproduce copyrighted framework content verbatim. Summarize and structure.
- Every skill must be genuinely useful, not placeholder content. A SOC analyst should be able to read the incident-response skill and immediately improve their workflow.
- The AI security skills (ai-agent-review, ai-governance) are the differentiator. No one else has published these. Make them exceptional.
