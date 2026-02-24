# /assess-risk

Assess a security risk scenario, vendor, or system and produce a structured risk register entry,
risk heat map data, or vendor risk assessment. Supports both qualitative (risk matrix) and
quantitative (FAIR-referenced) methodologies.

## Usage

```
/assess-risk "Ransomware attack on ERP system"
/assess-risk --type vendor "Acme Cloud Storage" --methodology qualitative
/assess-risk --type operational "Unpatched legacy SCADA systems" --register
/assess-risk --type project "Cloud migration to Azure" --methodology fair
/assess-risk --type system "Customer-facing API" --register
/assess-risk "Third-party access from managed service provider"
```

## What This Command Does

Invokes the risk-assessment skill to evaluate a described risk scenario, vendor, or system and
produce a structured risk assessment. Structures the analysis using the configured risk methodology
(qualitative matrix or FAIR-referenced quantitative approach), documents residual risk after
controls, recommends a risk treatment approach, and optionally formats the output as a risk
register entry ready for import to your GRC platform.

## Parameters

| Parameter | Values | Default |
|-----------|--------|---------|
| `--type` | `operational`, `vendor`, `project`, `system`, `regulatory` | Auto-assessed |
| `--methodology` | `qualitative`, `fair` | From `security.local.md` |
| `--register` | Flag — format output as risk register entry | Not set |
| `--heatmap` | Flag — include heat map coordinates | Not set |
| `--update` | Existing risk ID to update | Not set |

## Workflow

1. Load `security.local.md` for risk appetite, tolerance thresholds, acceptance authority, and GRC platform
2. Parse risk scenario to identify: threat source, asset/process at risk, potential impact
3. For `--type vendor`: invoke vendor risk assessment workflow with service/data access framing
4. For `--type operational` / `project` / `system`: invoke individual risk assessment workflow
5. Apply selected methodology:
   - `qualitative`: likelihood × impact matrix with 1-5 scales
   - `fair`: threat event frequency, vulnerability, loss magnitude estimation
6. Identify current controls and calculate residual risk
7. Recommend risk treatment (Accept / Mitigate / Transfer / Avoid)
8. If `--register`: format as risk register entry; if GRC platform connected, offer to create record

## Output

**Standard risk assessment includes:**
- Risk statement in structured format
- Inherent risk rating with rationale (qualitative or quantitative)
- Current controls assessment
- Residual risk rating
- Recommended treatment with specific mitigation actions
- Risk acceptance authority (from `security.local.md`)

**With `--register`:**
- Fully formatted risk register entry (Risk ID, owner, next review date, treatment plan)
- Ready for GRC platform import

**With `--methodology fair`:**
- Threat event frequency estimate
- Loss magnitude range (primary and secondary)
- Annualized loss expectancy range
- Sensitivity analysis (what changes the estimate most)

**Vendor assessment adds:**
- Vendor security posture evaluation
- Data and system access risk surface
- Contractual protection requirements
- Recommended vendor tier and review cadence

## When to Use This

- **New project or initiative:** Risk assessment before launch
- **Vendor onboarding:** Third-party risk assessment as part of procurement
- **Vulnerability exception:** Documenting the risk accepted when a patch is deferred
- **Board risk register:** Adding cyber risks to enterprise risk register with business framing
- **Architecture decision:** Risk trade-off analysis for security design choices
- **Regulatory change:** Assessing risk impact of new regulatory requirements
- **Post-incident:** Documenting the risk that materialized and its treatment going forward

## Dependencies

**Minimal (no MCP):** Fully functional from described risk scenarios — produces structured
assessment from natural language input.

**Recommended:**
1. GRC Platform — risk register CRUD; `--register` flag creates entries directly
2. Threat Intelligence — provides threat likelihood data for FAIR estimates
3. Documentation — pulls prior assessments for comparison

## Related

- **Skill:** `skills/risk-assessment/SKILL.md` (full documentation)
- **Command:** `/assess-compliance` — compliance gaps often become risk register entries
- **Command:** `/prep-report` — risk register summary feeds board and ELT security reports
- **Skill:** `skills/security-reporting/SKILL.md` — risk heat maps for board presentations
