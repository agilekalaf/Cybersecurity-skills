# Framework Modules

This directory contains structured reference modules for security and AI compliance frameworks.
Skills in this plugin load the relevant framework module(s) dynamically based on configuration in
`security.local.md`.

## Available Framework Modules

| File | Framework | Version | Primary skills |
|------|-----------|---------|---------------|
| `nist-csf-2.0.md` | NIST Cybersecurity Framework | 2.0 (2024) | compliance-assessment, security-reporting |
| `nist-800-53.md` | NIST SP 800-53 | Rev 5 (2020) | compliance-assessment, security-architecture-review |
| `iso-27001.md` | ISO/IEC 27001 | 2022 | compliance-assessment, audit-support |
| `nerc-cip.md` | NERC Critical Infrastructure Protection | Current | compliance-assessment, audit-support |
| `cmmc.md` | Cybersecurity Maturity Model Certification | 2.0 | compliance-assessment |
| `soc2.md` | SOC 2 (AICPA Trust Services Criteria) | TSC 2022 | compliance-assessment, audit-support |
| `mitre-atlas.md` | MITRE ATLAS | Current | ai-agent-review, ai-governance |
| `nist-ai-rmf.md` | NIST AI Risk Management Framework | 1.0 (2023) | ai-governance, ai-agent-review |
| `owasp-llm-top-10.md` | OWASP Top 10 for LLM Applications | 2025 | ai-agent-review, scan-skills |

## About These Modules

These modules are **structured summaries optimized for AI consumption** — not reproductions of
the source frameworks. They contain:

- Framework structure and key components (organized for rapid assessment)
- Maturity model or tier definitions where applicable
- Mapping relationships to other frameworks in this directory
- Regulatory context (who requires this and when)
- Source links to authoritative documents

**Important:** These modules do not substitute for the source framework documents. For compliance
programs, regulatory filings, and audit purposes, always reference and rely on the official
framework documents from their issuing bodies.

## Adding New Framework Modules

To add support for a new framework:

1. Create a new `.md` file in this directory following the structure of existing modules
2. Include: framework name/version/issuing body, purpose, structure, key components table,
   maturity model (if applicable), assessment approach, cross-framework mappings, regulatory context
3. Update `security.local.md` template to include the framework as an option
4. Update `plugin.json` to list the new framework module
5. Update this README

**Planned additions:** IEC 62443 (ICS/OT security), PCI-DSS 4.0, HIPAA Security Rule,
FedRAMP, SOC 1, DORA (EU).

## Copyright Note

Framework content in these modules is summarized and structured — not reproduced verbatim.
Security framework documents (ISO 27001, NIST publications, NERC CIP) are copyrighted by their
issuing bodies. NIST publications are in the public domain; ISO and IEC publications require
purchase; NERC standards are available at nerc.com.
