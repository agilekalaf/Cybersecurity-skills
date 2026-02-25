---
name: security-architecture-review
description: >
  Security architecture review, design review, architecture assessment, secure design,
  threat modeling, cloud security review, zero trust assessment, network architecture review,
  security design patterns, reference architecture, cloud posture assessment, CSPM findings review,
  secure by design, AWS security review, Azure security review, GCP security architecture,
  Kubernetes security review, API security review, application security architecture,
  microservices security, "review this architecture", "is this design secure", design threat model,
  infrastructure security review, secure SDLC architecture, DevSecOps architecture.
---

# Security Architecture Review

This skill evaluates proposed or existing system architectures, infrastructure designs, and cloud
configurations against security reference patterns and zero trust principles. It identifies
architectural risks, recommends design changes, assesses compensating controls, and produces
structured findings that can be tracked through remediation. It works at the design stage (where
security is cheapest to implement) and at the assessment stage (evaluating what's already built).

> **Philosophy: People Led, AI Driven (PLAID)**
>
> Architecture decisions have long lives and broad consequences. A design flaw embedded in production
> infrastructure today may persist for years and cost far more to remediate than it would have cost to
> fix on the whiteboard. This skill provides systematic security evaluation at design time so that
> architects and security teams can make better decisions faster. But AI analysis of architecture
> has real limits: it cannot see what documentation doesn't capture, it cannot test runtime behavior,
> and it cannot assess the human processes around a system. Architecture review findings are inputs
> to human architectural decisions — the security architect and engineering team determine what
> changes to make and how.

---

## Before You Begin

Load your `security.local.md` to calibrate this skill. Key fields used:

- **Cloud providers** — focuses review on the relevant cloud security model (Azure, AWS, GCP)
- **CSPM platform** — enables pull of existing cloud posture findings
- **Active compliance frameworks** — many frameworks (NIST CSF, FedRAMP, NERC CIP) have architectural requirements
- **Zero trust maturity target** — calibrates recommendations against your adoption stage

---

## Roles This Skill Serves

**Primary:** Security Architecture & Engineering, Application Security

**Also useful for:**
- GRC: architectural control evidence for compliance assessments
- Security Leadership: understanding architectural risk at program level
- Incident Response: post-incident architectural gap identification

---

## Workflow 1: Design Review (Pre-Build)

Use when evaluating a proposed architecture or design document before implementation.
This is the highest-value stage — catching flaws before they're built is dramatically cheaper.

### Inputs for design review

```
Design artifact:     [Architecture diagram (describe or paste) | Design document | RFC/ADR text]
System description:  [What does this system do? What data does it process?]
Data classification: [What's the most sensitive data this system touches?]
User population:     [Internal users | External/customer-facing | Both | Machine-to-machine]
Integration points:  [What systems does this connect to?]
Deployment target:   [Cloud provider | On-premises | Hybrid | Edge]
Compliance scope:    [Is this system in-scope for any compliance frameworks?]
Prior review:        [Has this design been reviewed before? Any known concerns?]
```

### Design review findings template

```markdown
## Security Architecture Review: [System Name]
**Review date:** [Date]
**Review type:** [Design review | Existing system | Cloud posture | Threat model]
**Reviewer:** [Name — human sign-off required]
**Artifact reviewed:** [Document name/version or description]

### System Summary
[2-3 sentences: what this system does, who uses it, what data it processes]

### Security Design Evaluation

#### Trust boundary analysis
| Boundary | From | To | Authentication | Authorization | Encryption | Finding |
|----------|------|----|---------------|---------------|------------|---------|
| [Boundary name] | [Component A] | [Component B] | [Method] | [Method] | [TLS/None] | [OK/Gap] |

#### Identity and access design
- Authentication mechanism: [Assessment]
- Authorization model: [RBAC / ABAC / other — assessment]
- Privileged access: [How are admin functions protected?]
- Service-to-service authentication: [mTLS / managed identity / API key — assessment]
- Finding: [OK / Concern / Risk]

#### Network security design
- Network segmentation: [Assessment]
- Exposure: [What's internet-facing? Is that necessary?]
- Ingress controls: [WAF / API gateway / load balancer — assessment]
- Egress controls: [Are outbound connections controlled?]
- Finding: [OK / Concern / Risk]

#### Data protection design
- Data at rest: [Encryption standard, key management — assessment]
- Data in transit: [TLS version, certificate management — assessment]
- Data classification enforcement: [How is sensitive data identified and protected?]
- Backup and recovery: [Assessment]
- Finding: [OK / Concern / Risk]

#### Logging and monitoring design
- Audit logging: [What events are logged?]
- Log retention: [Meets compliance requirements?]
- Detection coverage: [Will the SIEM see what it needs to?]
- Finding: [OK / Concern / Risk]

### Findings Summary

| ID | Finding | Severity | Category | Remediation | Effort |
|----|---------|----------|----------|-------------|--------|
| AR-001 | [Finding description] | [Critical/High/Medium/Low/Informational] | [Identity/Network/Data/Logging/Supply Chain] | [Recommended change] | [Low/Med/High] |

### Recommended design changes
[Prioritized list of specific, actionable changes to the design]

### Approval recommendation
**Overall risk rating:** [Critical | High | Medium | Low | Acceptable]
**Recommendation:** [Approve | Approve with conditions | Revise and re-review | Do not proceed]
**Conditions (if applicable):** [List conditions that must be met before deployment]
**Sign-off required from:** [Security Architecture lead / CISO — per security.local.md]
```

---

## Workflow 2: Zero Trust Maturity Assessment

Use to evaluate an organization's or system's progress against zero trust architectural principles.

### Zero trust pillars assessment

| Pillar | Current state | Target state | Gap | Priority |
|--------|-------------|-------------|-----|----------|
| **Identity** — verify every user and device | [Assessment] | [Target] | [Gap] | [High/Med/Low] |
| **Device** — validate device health | [Assessment] | [Target] | [Gap] | |
| **Network** — micro-segment, assume breach | [Assessment] | [Target] | [Gap] | |
| **Application** — authenticate at app layer | [Assessment] | [Target] | [Gap] | |
| **Data** — protect and classify data | [Assessment] | [Target] | [Gap] | |
| **Visibility** — log everything, detect anomalies | [Assessment] | [Target] | [Gap] | |
| **Automation** — automated policy enforcement | [Assessment] | [Target] | [Gap] | |

### Zero trust maturity levels

| Level | Description |
|-------|-------------|
| **Traditional** | Perimeter-based; implicit trust inside the network |
| **Initial** | Zero trust projects begun; MFA enforced for some users; some segmentation |
| **Advanced** | Identity-centric; device health checks; application-layer auth; automated responses |
| **Optimal** | Full zero trust; continuous validation; automated enforcement; behavioral analytics |

---

## Workflow 3: Cloud Security Posture Review

Use to assess cloud environment configuration against security best practices and compliance
requirements. Works with CSPM platform output (Defender for Cloud, Prisma, Wiz) when connected.

### Cloud posture review areas

| Area | Key checks | Common findings |
|------|-----------|----------------|
| **Identity & IAM** | Over-permissive roles, console access without MFA, key rotation | Wildcard permissions, long-lived credentials |
| **Storage** | Public bucket exposure, encryption at rest, access logging | Public S3/blobs, unencrypted storage |
| **Compute** | OS patch status, instance metadata exposure, public IPs | Unpatched instances, overly broad security groups |
| **Network** | Security group rules, VPC/VNET configuration, exposed management ports | SSH/RDP from 0.0.0.0/0, flat networks |
| **Logging** | CloudTrail/Activity Log enabled, log retention, SIEM integration | Missing audit logs, short retention |
| **Secrets management** | Secrets in code, key vault usage, rotation | Hardcoded credentials, no rotation |
| **Kubernetes / containers** | Pod security, image scanning, RBAC | Privileged containers, public dashboards |

---

## Working with Tools

### MCP connectors this skill uses

| Connector | Used for | Priority |
|-----------|----------|----------|
| **Cloud Security / CSPM** (Defender for Cloud, Prisma Cloud, Wiz) | Pull existing cloud posture findings, configuration data | High for cloud reviews |
| **Documentation** (SharePoint, Confluence) | Retrieve architecture diagrams, design documents | High |
| **Vulnerability Scanner** | Application-layer vulnerability findings for in-scope systems | Medium |
| **SIEM** | Validate logging coverage for reviewed systems | Medium |

### Graceful degradation

Without CSPM connectivity, provide a description of the architecture, exported CSPM findings, or
paste relevant configuration excerpts. The skill will analyze from provided materials and note
what a CSPM-connected review would add.

---

## What This Skill Does NOT Do

- **Does not perform penetration testing or active exploitation.** Architecture review is analytical, not adversarial. Use qualified penetration testers for runtime testing.
- **Does not review application source code.** Code-level security review is performed in the application security context; this skill reviews architecture and design.
- **Does not produce FedRAMP, PCI, or similar compliance certifications.** Formal compliance certifications require accredited assessors.
- **Does not cover OT/ICS/SCADA architecture.** Industrial control system architecture has specialized requirements not addressed here.
- **Does not guarantee designs are vulnerability-free.** Review quality is bounded by the completeness and accuracy of the materials provided.
- **Does not approve deployments autonomously.** Architecture review sign-off requires a human security architect or CISO per your governance process.
