# /triage-alert

Rapidly triage an incoming security alert, SIEM detection, or suspicious activity report.
Produces a structured triage summary with severity classification, ATT&CK mapping, IOC enrichment,
and recommended next steps.

## Usage

```
/triage-alert
/triage-alert --severity-override high
/triage-alert --source siem "SignInAttempts from TOR exit node for admin@example.com"
/triage-alert --source edr "mimikatz.exe executed on WORKSTATION-042"
/triage-alert --quick
/triage-alert --source user-report "suspicious email with macro attachment"
```

## What This Command Does

Invokes Phase 1 of the incident-response skill (Alert Triage and Initial Classification) to
evaluate an incoming alert or report and determine its disposition, severity, and recommended
response within 15 minutes. Runs parallel IOC enrichment if threat intelligence MCP connectors
are available. Produces a structured triage output ready for incident ticketing or handoff.

## Parameters

| Parameter | Values | Default |
|-----------|--------|---------|
| `--severity-override` | `critical`, `high`, `medium`, `low` | Auto-assessed |
| `--source` | `siem`, `edr`, `email`, `user-report`, `external`, `network` | Not set |
| `--quick` | Flag — abbreviated output, no IOC enrichment | Full triage |
| `--format` | `report`, `ticket`, `slack` | `report` |

## Workflow

1. Load `security.local.md` for severity definitions, escalation contacts, and tool stack
2. Parse the alert input — determine indicator types and extract IOCs
3. If SIEM connected: pull correlated events for affected assets (±30 min context)
4. If EDR connected: check process tree and host history for affected endpoints
5. Run parallel IOC enrichment across connected threat intelligence sources
6. Classify severity using organization's definitions from `security.local.md`
7. Map observed behaviors to MITRE ATT&CK techniques
8. Generate triage output with recommended next steps and explicit decision points

## Output

**Standard triage report includes:**
- Disposition (True Positive / Likely True Positive / Likely False Positive / False Positive)
- Severity classification with rationale
- Affected assets and their business context
- ATT&CK tactic and technique mapping with confidence
- IOC enrichment summary (disposition per indicator)
- Recommended immediate actions (each requiring analyst authorization)
- Recommendation: close, monitor, open incident, or escalate immediately

**With `--quick` flag:**
- Disposition, severity, and top 3 recommended actions only
- No ATT&CK mapping or IOC enrichment detail

**With `--format ticket`:**
- Output structured as incident ticket fields for direct import to ServiceNow or Jira

## When to Use This

- **Every new alert requiring triage** — this is the standard SOC first-response workflow
- **User-reported suspicious activity** — when an employee flags a suspicious email, file, or behavior
- **External notifications** — when an ISAC, partner, or external researcher reports an indicator
- **SIEM alert storm** — triage multiple alerts in parallel to prioritize response effort
- **After-hours handoff** — generate a structured handoff document for the next shift

## Dependencies

**Minimal (no MCP):** Accepts raw alert text or description; performs structural triage without enrichment.

**Recommended:**
1. SIEM — correlated event context dramatically improves accuracy
2. EDR — host context for endpoint alerts
3. Threat Intelligence (VirusTotal, OpenCTI) — IOC enrichment
4. Ticketing — for `--format ticket` output with automatic ticket creation

## Related

- **Skill:** `skills/incident-response/SKILL.md` (Phase 1 — this command is the entry point)
- **Command:** `/investigate` — for deeper IOC investigation after initial triage
- **Skill phases:** After triage confirms a true positive, continue with incident-response skill
  Phases 2-5 for full investigation, containment, eradication, and recovery
