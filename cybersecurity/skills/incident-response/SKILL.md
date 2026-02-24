---
name: incident-response
description: >
  Security incident response, IR, alert triage, breach investigation, containment, eradication, recovery,
  forensic investigation, DFIR, compromise assessment, ransomware response, phishing investigation,
  account takeover, data breach, insider threat, "we've been hacked", "suspicious activity",
  "something is wrong on the network", malware outbreak, lateral movement investigation,
  security incident playbook, SOC workflow, incident handling.
---

# Incident Response

This skill guides you through the full incident response lifecycle — from initial alert triage through
containment, eradication, and recovery — with structured output at each phase designed to support both
real-time decision-making and post-incident documentation. It implements a PICERL-based workflow
(Preparation, Identification, Containment, Eradication, Recovery, Lessons Learned) adapted for
AI-augmented response.

> **Philosophy: People Led, AI Driven (PLAID)**
>
> In incident response, speed matters — but wrong decisions made fast are worse than correct decisions
> made carefully. This skill accelerates the analytical and documentation work (IOC enrichment, ATT&CK
> mapping, timeline reconstruction, stakeholder communication drafts) so that the human responder can
> focus on decision-making, judgment calls, and actions that carry real consequences: network isolation,
> account suspension, executive notification. Every containment or eradication action this skill recommends
> requires human authorization before execution. The AI proposes; the analyst decides.

---

## Before You Begin

Load your `security.local.md` to calibrate this skill to your environment. The skill will use:

- **Severity definitions** — to correctly classify incidents using your organization's tiers
- **Escalation contacts** — to generate correctly addressed notification drafts
- **Tool stack** — to route enrichment queries to the right MCP connectors
- **Incident SLAs** — to flag when response timelines are approaching breach

If `security.local.md` is not available, the skill uses generic severity definitions (Critical/High/Medium/Low)
and will note where organization-specific calibration is needed.

---

## Roles This Skill Serves

**Primary:** Security Operations (SOC analysts, incident responders)

**Also useful for:**
- Security Architecture: post-incident architectural gap identification
- Security Leadership: executive communication and board reporting on significant incidents
- GRC: regulatory notification requirements and compliance implications of incidents

---

## Phase 1: Alert Triage and Initial Classification

Use this phase when receiving a new alert, SIEM detection, user report, or external notification.
Goal: determine in under 15 minutes whether this is a true positive requiring full IR engagement.

### Inputs for triage

Provide as much of the following as available:

```
Alert source:         [SIEM rule name | EDR detection | User report | External notification]
Alert timestamp:      [UTC preferred]
Affected asset(s):    [Hostname, IP, user account, application]
Alert summary:        [Copy-paste raw alert or describe in plain language]
Initial indicators:   [IPs, domains, hashes, email addresses, file paths]
Asset criticality:    [Business context for affected system if known]
```

### Triage output template

```markdown
## Alert Triage: [Alert ID or brief description] — [Date]

**Disposition:** [True Positive | Likely True Positive | Likely False Positive | False Positive]
**Severity:** [SEV 1 Critical | SEV 2 High | SEV 3 Medium | SEV 4 Low]
**Confidence:** [High | Medium | Low] — [one-sentence rationale]

### What happened (initial understanding)
[2-4 sentence summary of what the alert indicates, in plain language]

### Affected scope (known at triage)
| Asset | Type | Criticality | Owner |
|-------|------|-------------|-------|
| [hostname/IP/user] | [Endpoint/Server/Account/Network] | [Critical/High/Med/Low] | [Team or contact] |

### ATT&CK mapping (initial)
| Tactic | Technique | Confidence |
|--------|-----------|------------|
| [e.g., Initial Access] | [T1566.001 Spearphishing Attachment] | [High/Med/Low] |

### Indicators of Compromise
| Indicator | Type | Context | Enrichment status |
|-----------|------|---------|-------------------|
| [value] | [IP/Domain/Hash/Email] | [Where observed] | [Pending/Clean/Malicious] |

### Immediate recommended actions
1. [Most urgent action — analyst decision required]
2. [Second action]
3. [Preserve/collect evidence actions]

### Next phase
[Recommend: Close as FP | Monitor | Open SEV X incident | Escalate immediately]
```

---

## Phase 2: Investigation and Scope Determination

Use this phase after confirming a true positive. Goal: determine the full blast radius —
what was accessed, what was exfiltrated, how the attacker got in, and how far they've moved.

### Investigation queries to run (via MCP tools)

- **SIEM:** Timeline of events for affected accounts and hosts (±4 hours around initial alert)
- **EDR:** Process tree, file writes, network connections, persistence mechanisms on affected endpoints
- **Identity:** Authentication logs — successful and failed — for affected accounts
- **Network:** Firewall/proxy logs for external communications from affected assets
- **Email:** If phishing suspected, pull message headers, attachments, recipients, and any link clicks

### Investigation output template

```markdown
## Incident Investigation: [Incident ID] — [Date]

**Incident type:** [Malware | Ransomware | Account Compromise | Data Exfiltration |
                    Insider Threat | Phishing | Unauthorized Access | Other]
**Estimated start time:** [When attacker activity appears to have begun]
**Detection lag:** [Time between estimated start and detection]

### Attack timeline
| Time (UTC) | Event | Source | Confidence |
|------------|-------|--------|------------|
| [timestamp] | [What happened] | [Log source] | [High/Med/Low] |

### Entry vector
[How the attacker got in — phishing, exposed service, credential stuffing, insider, etc.]
[Confidence level and supporting evidence]

### Confirmed scope
- Systems accessed: [List]
- Accounts compromised: [List]
- Data potentially accessed: [Classification and volume if known]
- Lateral movement observed: [Yes/No — describe if yes]
- Persistence mechanisms identified: [List]
- Data exfiltration evidence: [Yes/No/Unknown — describe if yes]

### ATT&CK kill chain mapping
| Phase | Tactic | Technique(s) | Evidence |
|-------|--------|--------------|----------|
| [1] | [Reconnaissance] | [T1595] | [Source] |
| [2] | [Initial Access] | [T1566.001] | [Source] |
| ... | ... | ... | ... |

### Regulatory notification triggers
- Personal data involved: [Yes/No/Unknown]
- HIPAA breach threshold: [Triggered/Not triggered/Unknown]
- Applicable breach notification law: [State/GDPR/CCPA/etc. — assess per org's footprint]
- Notification deadline: [If triggered, note the clock start and deadline]
```

---

## Phase 3: Containment

Containment actions carry real consequences. Present recommendations for analyst authorization;
do not execute autonomously.

### Containment options by incident type

| Incident Type | Short-term Containment | Long-term Containment |
|---------------|----------------------|----------------------|
| Account compromise | Disable account, revoke sessions/tokens | Reset credentials, review all activity, MFA enforcement |
| Endpoint malware | Network isolation (via EDR) | Reimage, restore from clean backup |
| Ransomware | Isolate affected segment, disable file shares | Identify patient zero, preserve forensics |
| Data exfiltration | Block egress destinations, preserve logs | Revoke credentials, DLP controls |
| Insider threat | Preserve evidence BEFORE alerting — legal hold | HR/Legal process, account suspension |
| Phishing campaign | Block sender/domain, pull similar messages | User awareness notification |

### Containment decision record template

```markdown
## Containment Decision Record — [Incident ID]

**Decision made by:** [Name, Role]
**Decision timestamp:** [UTC]

### Actions authorized
| Action | Target | Business impact | Authorized by |
|--------|--------|----------------|---------------|
| [Isolate endpoint] | [hostname] | [Service X unavailable] | [Name] |

### Actions deferred and rationale
| Action | Rationale for deferral |
|--------|----------------------|
| [Action considered] | [Why not taken yet — evidence preservation, business continuity, etc.] |

### Stakeholders notified
| Role | Notified at | Method |
|------|-------------|--------|
| [CISO] | [Time] | [Email/Teams/Phone] |
```

---

## Phase 4: Eradication and Recovery

### Eradication checklist

- [ ] All persistence mechanisms identified and removed
- [ ] All compromised credentials rotated
- [ ] All attacker-controlled infrastructure blocked (IPs, domains, C2)
- [ ] Malware artifacts removed or systems reimaged
- [ ] Vulnerabilities exploited during attack patched or mitigated
- [ ] Integrity of backups confirmed before recovery

### Recovery validation

Before returning systems to production, verify:
- System imaging/restoration completed from known-clean backup
- Security controls re-enabled and functioning (AV/EDR active, logging active)
- No evidence of reinfection in first 24 hours post-recovery
- Access controls reviewed and tightened as appropriate

---

## Phase 5: Lessons Learned

### Post-Incident Review template

```markdown
## Post-Incident Review: [Incident ID]
**Date of review:** [Date]
**Facilitator:** [Name]
**Attendees:** [Teams represented]

### Incident summary (for record)
[2-3 sentences — what happened, how it was detected, how it was resolved]

### Timeline (final)
[Complete attack and response timeline]

### What worked well
- [Detection controls that fired]
- [Response actions that were effective]
- [Team coordination that worked]

### What needs improvement
- [Detection gaps — what should we have caught earlier?]
- [Response delays — where were the bottlenecks?]
- [Playbook gaps — what wasn't covered?]

### Action items
| Item | Owner | Due date | Priority |
|------|-------|----------|----------|
| [Control improvement] | [Team] | [Date] | [High/Med/Low] |

### Metrics
- Time to detect: [X hours/days from estimated start]
- Time to contain: [X hours from detection]
- Time to eradicate: [X hours]
- Time to recover: [X hours]
- Total business impact: [Systems affected, downtime, data risk]
```

---

## Working with Tools

### MCP connectors this skill uses

| Connector Category | Used for | Graceful degradation |
|-------------------|----------|----------------------|
| **SIEM** (Sentinel, Splunk, Chronicle) | Timeline queries, correlation, alert enrichment | Provide raw log excerpts manually |
| **EDR** (Defender, CrowdStrike, SentinelOne) | Process trees, file activity, network connections | Collect via endpoint investigation |
| **Identity** (Entra ID, Okta, SailPoint) | Auth logs, session data, group membership at time of incident | Pull from IdP UI manually |
| **Threat Intelligence** (Feedly, OpenCTI, VirusTotal) | IOC enrichment, actor attribution, malware identification | Use free enrichment tools (VirusTotal, URLScan) |
| **Ticketing** (ServiceNow, Jira) | Incident record creation and tracking | Document in any available system |
| **Email** (Exchange/M365, Google) | Phishing investigation, mail header analysis | Export headers manually |

### Recommended MCP priority for IR workflows

1. SIEM — core detection and timeline data
2. EDR — endpoint forensics
3. Threat Intelligence — IOC enrichment and context
4. Identity — account investigation

---

## What This Skill Does NOT Do

- **Does not execute containment actions autonomously.** Every containment decision requires explicit human authorization.
- **Does not provide legal advice** on breach notification requirements. It identifies potential triggers; legal counsel determines obligations.
- **Does not replace dedicated forensics tooling.** For court-admissible forensics, use certified DFIR tools and practitioners.
- **Does not guarantee complete scope determination.** AI-assisted investigation accelerates the work but does not substitute for thorough human analysis.
- **Does not cover OT/ICS incidents.** Industrial control system incidents have specialized response requirements not addressed here.
- **Does not manage long-term remediation programs.** Post-incident remediation at program level belongs in the vulnerability-management and compliance-assessment skills.
