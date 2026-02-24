# MCP Connector Guide

This document describes all MCP connector categories supported by the Cybersecurity Plugin,
which skills use each one, and how to set them up. The plugin is designed to degrade gracefully —
every skill works without any MCP connections, and each connection you add unlocks more capabilities.

---

## Quick Start: Fastest Path to a Working Plugin

**Zero connectors — works today:**
Install the plugin, configure `security.local.md`, and all skills work from manual input.
You get structured workflows, output templates, and AI-assisted analysis. No connectors needed.

**Add three connectors for immediate operational value:**

1. **Feedly** — enables threat intelligence briefings and actor tracking
2. **VirusTotal** — enables IOC enrichment for any indicator
3. **CISA KEV** — free, no setup required; integrated via web fetch; enables exploitation status

These three connectors deliver the threat-intelligence and /threat-brief workflows immediately
with about 30 minutes of setup.

**Next priority additions by role:**
- SOC analysts: SIEM + EDR → incident-response and triage-alert workflows
- GRC teams: GRC Platform + Documentation → compliance-assessment and audit-support workflows
- IAM teams: Entra ID or Okta → access-review workflows
- Leadership: no additional connectors needed; security-reporting works from provided data

---

## Connector Categories

### 1. SIEM / Log Management
**Skills that use this:** incident-response (all phases), threat-intelligence (hunting), security-reporting (metrics)

**What it enables:**
- Timeline queries during incident investigation
- Correlated event context for alert triage
- Detection coverage validation for threat hunt hypotheses
- Operational metrics for security reporting

**Supported platforms:**
| Platform | MCP server | Setup complexity |
|----------|-----------|-----------------|
| Microsoft Sentinel | `@anthropic-mcp/sentinel` | Medium — requires Azure app registration |
| Splunk | `@anthropic-mcp/splunk` | Medium — requires API token |
| Google Chronicle | `@anthropic-mcp/chronicle` | Medium — requires GCP service account |
| Elastic Security | `@anthropic-mcp/elastic` | Medium — requires API key |

**Required permissions:** Read access to logs and alerts. Write access only if you want automated
alert tagging or case creation (not required for core functionality).

**Setup (Sentinel example):**
1. Create an Azure app registration with Sentinel Reader role on the workspace
2. Note: Tenant ID, Client ID, Client Secret, Workspace ID
3. Add to `.mcp.json` sentinel block; remove placeholder entries

**Graceful degradation:** Without SIEM, provide raw log excerpts manually. Triage and investigation
workflows still produce structured output from manually provided context.

---

### 2. SOAR / Automation
**Skills that use this:** incident-response (playbook execution coordination)

**What it enables:**
- Playbook status visibility during incident response
- Automated enrichment results fed into investigation
- Containment action tracking

**Supported platforms:** Sentinel SOAR (Logic Apps), Splunk SOAR (Phantom), Palo Alto XSOAR, Tines

**Note:** SOAR connectivity is optional — the plugin recommends actions but does not execute
containment steps autonomously. Human authorization is required for all containment actions.

---

### 3. Identity & Access Management
**Skills that use this:** access-review (primary), incident-response (account investigation), audit-support

**What it enables:**
- Current access data pull for recertification campaigns
- Privileged account inventory from PAM platforms
- Authentication log queries during investigations
- MFA enrollment status reporting

**Supported platforms:**
| Platform | MCP server | Primary use |
|----------|-----------|-------------|
| Microsoft Entra ID | `@anthropic-mcp/microsoft-graph` | User access, group membership, auth logs |
| Okta | `@anthropic-mcp/okta` | User access, MFA status, auth logs |
| SailPoint IdentityNow | `@anthropic-mcp/sailpoint` | IGA workflows, access requests, certifications |
| CyberArk | `@anthropic-mcp/cyberark` | PAM vault coverage, privileged account data |

**Required permissions:**
- Entra ID: `User.Read.All`, `Group.Read.All`, `Directory.Read.All`, `AuditLog.Read.All`
- Okta: Read-only API token (System Log, Users, Groups scopes)
- SailPoint: Read access to identities, entitlements, and certification campaigns
- CyberArk: Read access to safe contents and account properties

---

### 4. Vulnerability Scanner
**Skills that use this:** vulnerability-management (primary), security-reporting (metrics)

**What it enables:**
- Automated scan result ingestion for risk-based prioritization
- SLA compliance tracking from live scan data
- Asset criticality correlation from scanner asset inventory

**Supported platforms:**
| Platform | MCP server | Notes |
|----------|-----------|-------|
| Qualys VMDR | `@anthropic-mcp/qualys` | Cloud-based; API v2 |
| Tenable.io / Tenable.sc | `@anthropic-mcp/tenable` | Access key + Secret key |
| Rapid7 InsightVM | `@anthropic-mcp/rapid7` | API key required |
| Microsoft Defender VM | `@anthropic-mcp/defender-endpoint` | Shares auth with MDE |

**Required permissions:** Read access to vulnerability findings, asset data, and scan schedules.

**Graceful degradation:** Export vulnerability findings from your scanner UI to CSV and provide
as input. The vulnerability-management skill analyzes provided data structures.

---

### 5. Endpoint / EDR
**Skills that use this:** incident-response (investigation), threat-intelligence (hunting)

**What it enables:**
- Process trees and file activity for endpoint investigation
- Host isolation commands (analyst-authorized only)
- Network connection data from endpoints
- Threat hunt query execution against endpoint telemetry

**Supported platforms:**
| Platform | MCP server | Notes |
|----------|-----------|-------|
| Microsoft Defender for Endpoint | `@anthropic-mcp/defender-endpoint` | Azure app registration |
| CrowdStrike Falcon | `@anthropic-mcp/crowdstrike` | OAuth2 client credentials |
| SentinelOne | `@anthropic-mcp/sentinelone` | API token |

**Required permissions:** Read for investigation; note that isolation and remediation actions
require elevated permissions — these are never taken autonomously by the plugin.

---

### 6. Ticketing / Workflow
**Skills that use this:** incident-response, vulnerability-management, access-review, risk-assessment, audit-support

**What it enables:**
- Automatic ticket creation from findings
- Remediation tracking from generated tickets
- SLA monitoring through ticket age data

**Supported platforms:**
| Platform | MCP server | Notes |
|----------|-----------|-------|
| ServiceNow | `@anthropic-mcp/servicenow` | Username + password or OAuth |
| Jira | `@anthropic-mcp/jira` | API token + email |

**Required permissions:** Create and read tickets in the security project/queue.

---

### 7. GRC Platform
**Skills that use this:** compliance-assessment, risk-assessment, policy-management, audit-support, security-reporting

**What it enables:**
- Pull existing control assessments for compliance scoring
- Create and update risk register entries
- Store audit evidence and findings
- Policy lifecycle management

**Supported platforms:**
| Platform | MCP server | Notes |
|----------|-----------|-------|
| Hyperproof | `@anthropic-mcp/hyperproof` | OAuth2 |
| ServiceNow GRC | `@anthropic-mcp/servicenow` | Same as ticketing connector |
| LogicGate | `@anthropic-mcp/logicgate` | API key |
| Archer RSA | `@anthropic-mcp/archer` | Username + password |

**Graceful degradation:** All GRC skills produce structured markdown output that can be manually
imported to any GRC platform. The plugin does not require a GRC platform connection to function.

---

### 8. Threat Intelligence
**Skills that use this:** threat-intelligence (primary), vulnerability-management (exploitation context), incident-response (IOC enrichment)

**Start here.** This is the highest-value connector category for the fastest time-to-value.

**Supported platforms:**
| Platform | MCP server | Priority | Cost |
|----------|-----------|----------|------|
| Feedly | `@anthropic-mcp/feedly` | High | Paid (Threat Intelligence tier) |
| OpenCTI | `@anthropic-mcp/opencti` | High | Free (self-hosted) or paid cloud |
| VirusTotal | `@anthropic-mcp/virustotal` | High | Freemium (free API has rate limits) |
| AbuseIPDB | `@anthropic-mcp/abuseipdb` | Medium | Freemium |
| Shodan | `@anthropic-mcp/shodan` | Medium | Paid (Freelancer tier+) |
| CISA KEV | (web fetch, no MCP needed) | High | Free |
| Cyber Sentinel | `@anthropic-mcp/cyber-sentinel` | Medium | Varies |

**CISA KEV note:** The Known Exploited Vulnerabilities catalog is queried directly as a web source —
no MCP connector required. KEV status is included in all vulnerability prioritization and IOC
enrichment workflows automatically.

**Recommended minimum:** Feedly + VirusTotal. This covers threat intelligence briefings,
actor tracking, and IOC enrichment for most operational workflows.

---

### 9. Cloud Security / CSPM
**Skills that use this:** security-architecture-review (primary), vulnerability-management

**What it enables:**
- Pull existing CSPM findings for cloud architecture review
- Identity configuration data for cloud access review
- Cloud asset inventory for attack surface analysis

**Supported platforms:**
| Platform | MCP server | Cloud coverage |
|----------|-----------|----------------|
| Microsoft Defender for Cloud | `@anthropic-mcp/defender-cloud` | Azure, multicloud |
| Prisma Cloud | `@anthropic-mcp/prisma-cloud` | AWS, Azure, GCP |
| Wiz | `@anthropic-mcp/wiz` | AWS, Azure, GCP |

**Required permissions:** Read access to security findings and resource configurations.

---

### 10. Documentation
**Skills that use this:** policy-management, compliance-assessment, audit-support, ai-governance

**What it enables:**
- Retrieve existing policies for review and update
- Pull prior assessment reports as context
- Store generated policy documents and reports
- Evidence retrieval during audit support

**Supported platforms:**
| Platform | MCP server | Notes |
|----------|-----------|-------|
| Microsoft SharePoint / OneDrive | `@anthropic-mcp/sharepoint` | Azure app registration |
| Confluence | `@anthropic-mcp/confluence` | API token |
| Google Drive | `@anthropic-mcp/google-drive` | OAuth2 / service account |

---

## Adding a New MCP Connector

If your tool is not listed above:

1. Check if an MCP server exists: https://github.com/modelcontextprotocol/servers
2. Add the connector configuration to `.mcp.json` in the appropriate category
3. Identify which skills benefit and update `security.local.md` tool stack accordingly
4. Open a pull request to add the connector to this guide for other users

---

## Credential Security

**Never hardcode credentials in `.mcp.json`.** Use environment variables:
- Set credentials in your shell environment or a `.env` file (excluded from git)
- Use a secrets manager (HashiCorp Vault, AWS Secrets Manager, Azure Key Vault) for production
- The `.mcp.json` file references environment variable names — the actual values should not appear in the file

**Add to `.gitignore`:**
```
.env
security.local.md
```
