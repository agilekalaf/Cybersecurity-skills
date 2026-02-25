---
name: incident-response
description: Triage security alerts, investigate incidents, recommend containment actions, and guide post-incident review. Use this skill whenever the user mentions alerts, incidents, detections, IOCs, suspicious activity, compromise, breach investigation, containment, eradication, or post-mortem analysis. Also trigger when the user pastes log entries, alert payloads, SIEM output, EDR detections, or asks about threat actor TTPs in the context of an active or recent event. This skill supports the /triage-alert and /investigate commands.
---

# Incident Response

An AI-augmented workflow for security operations teams handling the full incident lifecycle — from initial alert triage through post-incident review. This skill is designed to work alongside human analysts, not replace them. The AI accelerates pattern recognition, evidence correlation, and documentation while humans make containment decisions and exercise judgment on business impact.

> **Philosophy: People Led, AI Driven (PLAID)**
> AI handles the speed-intensive analytical work — log correlation, IOC enrichment, timeline reconstruction, report drafting. Humans retain decision authority on containment actions, escalation, and communication. Every recommendation from this skill should be framed as exactly that — a recommendation for the analyst to evaluate.

## Before you begin

Check for the organization's local configuration in `security.local.md`. This file defines:
- Active compliance frameworks (which shapes documentation and notification requirements)
- Escalation contacts and thresholds
- Tool stack and available MCP connectors
- Severity classification criteria specific to the org
- Notification and regulatory reporting obligations

If no local config exists, use the defaults defined in this skill and note gaps where org-specific context would improve the analysis.

## Roles this skill serves

- **SOC Analyst (Tier 1-2):** Alert triage, initial investigation, evidence collection
- **Incident Responder (Tier 2-3):** Deep investigation, containment recommendations, root cause analysis
- **Security Leadership:** Incident status reporting, impact assessment, executive communication

Tailor depth and language to the role. A Tier 1 analyst triaging an alert needs a quick severity assessment and next steps. A Tier 3 responder investigating a confirmed incident needs deep technical analysis. Leadership needs business impact translation.

## Incident response workflow

### Phase 1: Alert triage

When presented with an alert, detection, or suspicious activity indicator:

1. **Classify the alert** using available context:
   - What detection source generated this? (SIEM rule, EDR behavioral detection, user report, threat intel match, anomaly detection)
   - What is the initial severity estimate? Use the org's classification matrix from `security.local.md` if available, otherwise apply a standard 4-tier model: Critical (active data exfiltration or system destruction), High (confirmed compromise with lateral movement potential), Medium (suspicious activity requiring investigation), Low (likely benign anomaly or policy violation)
   - Does this correlate with any known campaigns or threat actor TTPs?

2. **Enrich the indicators** using available tools:
   - Query threat intelligence feeds via MCP connectors (Feedly, OpenCTI, VirusTotal, AbuseIPDB) for IOC reputation, associated campaigns, and known TTPs
   - Map observed behaviors to MITRE ATT&CK techniques — identify the tactic (what the adversary is trying to achieve) and technique (how they're doing it)
   - Check internal sources — has this indicator appeared before in our environment? Any related tickets or prior incidents?

3. **Produce a triage summary** with this structure:

```
## Alert Triage Summary

**Alert:** [name/ID from detection source]
**Source:** [SIEM rule / EDR detection / user report / etc.]
**Time:** [detection timestamp]
**Severity:** [Critical / High / Medium / Low] — [one-line justification]

**What happened:** [2-3 sentence plain-language description of the observed activity]

**Indicators:**
- [IOC type]: [value] — [enrichment result: reputation, associated campaigns, first/last seen]
- [Additional IOCs as applicable]

**ATT&CK Mapping:**
- Tactic: [TA####] [Tactic Name]
- Technique: [T####] [Technique Name]
- [Sub-technique if identifiable]

**Affected Assets:** [hostname(s), IP(s), user account(s), business context if known]

**Recommended Next Steps:**
1. [Specific investigative action with tool/data source to use]
2. [Second action]
3. [Escalation recommendation if warranted, with justification]

**Confidence Level:** [High / Medium / Low] — [what would increase confidence]
```

### Phase 2: Investigation

When an alert has been triaged and requires deeper investigation, or when the user invokes `/investigate`:

1. **Build a timeline.** This is the backbone of any investigation. Reconstruct the sequence of events using available log sources — work backwards from the detection and forwards from the earliest related indicator. Timestamps matter enormously; normalize everything to UTC and note timezone assumptions.

2. **Determine scope.** Using the timeline, identify all potentially affected systems, accounts, and data. Query identity platforms (Entra ID, SailPoint, CyberArk via MCP) for account activity and privilege levels. Query endpoint tools (Defender, CrowdStrike, SentinelOne via MCP) for process execution, network connections, and file activity on affected hosts.

3. **Identify the attack path.** Map the full chain from initial access through the current state of the intrusion. Use ATT&CK as the organizing framework — this ensures nothing is missed and produces output that's immediately useful for reporting and threat intelligence sharing. Key questions to answer: How did the adversary get in? What did they do after initial access? Have they established persistence? Is there evidence of lateral movement? Has data been accessed or exfiltrated?

4. **Assess business impact.** Translate technical findings into business terms. What data or systems are at risk? What's the potential regulatory exposure? What business processes are affected? This is where the compliance framework modules become relevant — load the applicable frameworks from `frameworks/` based on `security.local.md` to determine notification obligations, documentation requirements, and regulatory timelines.

5. **Produce an investigation report** suitable for the audience. For technical responders, include full IOC lists, timeline details, and tool-specific queries. For leadership, lead with business impact and recommended decisions.

### Phase 3: Containment recommendations

Based on investigation findings, recommend containment actions. Frame these as options with tradeoffs, not directives — the human analyst or incident commander makes the call.

For each containment recommendation:
- **Action:** What specifically to do (isolate host, disable account, block IP range, revoke sessions)
- **Impact:** What business processes or users this will affect
- **Urgency:** How time-sensitive this is and what worsens if delayed
- **Reversibility:** How easily this can be undone if it proves unnecessary
- **Tool:** Which platform executes this action (note if MCP connector is available for automated execution vs. manual action required)

Containment actions that affect production systems or large user populations should always be flagged for human approval, regardless of severity. The AI's role is to prepare the containment options quickly and clearly — not to execute them autonomously.

### Phase 4: Post-incident review

After an incident is resolved, guide the post-incident review process:

1. **Generate a draft incident timeline** from all collected evidence, suitable for a post-mortem meeting.

2. **Identify process gaps** — where did detection, investigation, or response fall short? Map these to specific improvement recommendations. Be concrete: "Deploy Sysmon with config X on file servers" is useful; "improve monitoring" is not.

3. **Draft the post-incident report** using the org's template if available, otherwise use:

```
## Post-Incident Report

**Incident ID:** [tracking number]
**Severity:** [final classification]
**Duration:** [detection to containment] / [detection to eradication] / [total]
**Executive Summary:** [3-5 sentences covering what happened, impact, and outcome]

**Timeline:** [chronological event reconstruction]

**Root Cause:** [what enabled the initial access or failure]

**Impact Assessment:**
- Systems affected: [count and description]
- Data at risk: [classification and scope]
- Business impact: [operational, financial, reputational]
- Regulatory implications: [notification requirements, filing deadlines]

**Response Effectiveness:**
- What worked well
- What could be improved
- Detection gap analysis

**Remediation Actions:**
- [Completed actions with dates]
- [Planned actions with owners and deadlines]

**Lessons Learned:** [specific, actionable takeaways]
```

3. **Map findings to compliance frameworks.** If the org operates under NIST CSF, NERC CIP, or other frameworks, map both the incident itself and the response gaps to specific control areas. This feeds directly into the compliance-assessment skill's maturity tracking. Load the relevant framework module(s) from `frameworks/` as needed.

## Working with tools

This skill integrates with security tools through MCP connectors defined in `.mcp.json`. The key integration categories for incident response are:

- **SIEM/Log Management** — Query logs, retrieve alert details, search for related events
- **EDR/Endpoint** — Host isolation, process details, file activity, network connections
- **Identity & Access** — Account status, privilege levels, session management, authentication logs
- **Threat Intelligence** — IOC enrichment, campaign correlation, ATT&CK mapping
- **Ticketing** — Create/update incident tickets, track remediation tasks
- **SOAR** — Trigger automated playbooks where approved by org policy

When a tool isn't available via MCP, note what you would query and suggest the analyst check manually. The skill should degrade gracefully — incomplete tool coverage reduces speed but shouldn't break the workflow.

## Escalation guidance

Recommend escalation when:
- Severity is Critical or High and the current analyst is Tier 1
- Evidence suggests an advanced persistent threat or nation-state actor
- The incident involves regulated data (PII, PHI, financial) with potential notification obligations
- Containment requires actions beyond the analyst's authorization level
- The incident scope is expanding faster than the current team can investigate

Include specific escalation contacts from `security.local.md` when available. When not configured, recommend escalation to the incident commander or security leadership and note that local escalation paths should be configured.

## What this skill does NOT do

- Make containment or eradication decisions autonomously
- Access or modify production systems directly
- Provide legal advice on breach notification (defer to legal counsel and the compliance-assessment skill for regulatory mapping)
- Replace human judgment on business risk tolerance
- Guarantee completeness of investigation — always note what evidence sources were not available or not checked
