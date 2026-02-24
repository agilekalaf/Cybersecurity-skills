# /assess-compliance

Run a framework-based compliance assessment, gap analysis, or remediation roadmap against one or
more security frameworks. Loads the appropriate framework module(s) and produces a structured,
audit-ready output.

## Usage

```
/assess-compliance --framework nist-csf-2.0
/assess-compliance --framework iso-27001 --format gaps
/assess-compliance --framework nist-csf-2.0 --scope cloud-environment
/assess-compliance --framework nist-csf-2.0,soc2 --format roadmap
/assess-compliance --framework cmmc --format scorecard
/assess-compliance --framework nerc-cip --scope ot-environment
```

## What This Command Does

Invokes the compliance-assessment skill to evaluate current-state security controls against the
specified framework(s). Loads the relevant framework module from `frameworks/` for control
requirements and assessment criteria. Supports single-framework deep assessments and multi-framework
assessments that identify overlapping remediation opportunities.

## Parameters

| Parameter | Values | Default |
|-----------|--------|---------|
| `--framework` | `nist-csf-2.0`, `nist-800-53`, `iso-27001`, `nerc-cip`, `cmmc`, `soc2`, or comma-separated list | From `security.local.md` |
| `--format` | `scorecard`, `gaps`, `roadmap` | `scorecard` |
| `--scope` | `full`, `cloud-environment`, `ot-environment`, `specific-system:[name]`, custom | `full` |
| `--period` | Assessment period (for trend analysis) | Current |
| `--compare` | Date of prior assessment (enables trend reporting) | Not set |

## Workflow

1. Load `security.local.md` for configured frameworks, maturity targets, and tool stack
2. Load the specified framework module(s) from `frameworks/`
3. For `--format scorecard`: assess current maturity per function/domain and generate scores
4. For `--format gaps`: identify control gaps against framework requirements with risk ratings
5. For `--format roadmap`: prioritize gaps and produce time-phased remediation plan
6. For multi-framework: run cross-framework overlap analysis to identify shared remediations
7. For GRC platform connection: pull existing control assessments to accelerate scoring

## Output

**`--format scorecard`:**
- Overall maturity tier/level per function or domain
- Trend comparison if `--compare` is specified
- Key strengths and critical gaps summary
- Narrative for executive reporting

**`--format gaps`:**
- Structured gap table: control requirement, current state, gap, severity, remediation
- Sorted by gap severity (Critical first)
- Evidence requirements for each gap (supports audit preparation)

**`--format roadmap`:**
- Time-phased remediation plan (Phase 1: 0-3 months, Phase 2: 3-9 months, Phase 3: 9-18 months)
- Effort and cost framing per phase
- Multi-framework overlap analysis (if multiple frameworks specified)

## When to Use This

- **Annual compliance review:** Full scorecard against primary framework
- **Audit preparation:** Gap analysis 3-6 months before scheduled audit
- **New framework adoption:** Assess current state before committing to certification
- **Post-incident review:** Identify framework gaps exposed by a security incident
- **Board reporting:** Maturity scorecard as input to security-reporting skill
- **Budget justification:** Roadmap with effort framing to support security investment request

## Dependencies

**Minimal (no MCP):** Accepts manually provided control status descriptions and produces
assessment from that input. Useful when GRC platform is not connected.

**Recommended:**
1. GRC Platform — pulls existing control assessments; highest data quality
2. Documentation — retrieves policy evidence to assess control design
3. Ticketing — creates remediation tracking tickets from roadmap output

## Related

- **Skill:** `skills/compliance-assessment/SKILL.md` (full documentation)
- **Frameworks:** `frameworks/` directory — loaded automatically based on `--framework` parameter
- **Command:** `/prep-report` — uses scorecard output as input to security reports
- **Skill:** `skills/audit-support/SKILL.md` — audit preparation that follows gap analysis
