# NorthStar Security Framework Crosswalk

## Purpose

Relate NorthStar controls to commonly used enterprise security frameworks without claiming certification or complete compliance. The mapping is architectural and evidence oriented; a formal assessment would require organizational scope, policy, operating evidence and independent review.

## Control Crosswalk

| NorthStar capability | NIST CSF 2.0 | NIST SP 800-207 principle | ITSG-33 family | Evidence status |
|---|---|---|---|---|
| Security ownership, risk and exceptions | Govern | Enterprise policies constrain access | PM / RA | Documented operating model |
| Asset and dependency inventory | Identify | Resources and subjects are explicitly known | CM / RA | Roadmap requirement |
| Entra authentication and MFA baseline | Protect | Authentication is dynamic and explicitly enforced | IA | Validated baseline |
| Group-based RBAC and ABAC | Protect | Least privilege and per-resource authorization | AC | Validated |
| Managed workload identities | Protect | No implicit trust based on location or ownership | IA / AC | Validated |
| Segmented VNet and NSGs | Protect | Network location does not grant trust | SC / AC | Validated |
| Application Gateway WAF | Protect / Detect | Continuous inspection of resource access | SC / SI | Validated in Detection mode |
| Key Vault and scoped access | Protect | Protect resources and credentials | SC / AC | Validated |
| Azure Policy and classification | Govern / Protect | Policy is consistently applied | CM / PL | Validated |
| Protected Terraform delivery and OIDC | Govern / Protect | Trust is evaluated for each workflow | CM / IA | Validated |
| Activity, WAF and diagnostic telemetry | Detect | Continuous diagnostics inform trust decisions | AU / SI | Validated |
| Sentinel and KQL analytics | Detect | Observe subjects, assets and access behavior | AU / SI | Validated |
| Approval-gated response playbook | Respond | Access and actions remain policy constrained | IR / AC | Validated non-destructive workflow |
| Expected-state validation | Identify / Detect | Reevaluate asset and control state | CA / CM | Validated |
| Continuity and recovery model | Recover | Restore resources to a trustworthy state | CP / IR | Documented target state |

## NIST CSF 2.0 Coverage

- **Govern:** architecture decisions, risk ownership, exceptions, policy and secure-delivery controls.
- **Identify:** inventory, dependencies, threat model, residual risk and expected-state assessment.
- **Protect:** identity, least privilege, segmentation, WAF, Key Vault and controlled delivery.
- **Detect:** centralized telemetry, Sentinel, KQL and drift validation.
- **Respond:** investigation, classification, approval tasks and controlled playbook execution.
- **Recover:** restoration sequencing, evidence preservation and post-recovery validation.

## Canadian Enterprise Context

The ITSG-33 references identify relevant control families, not assessed control implementation. Organizations applying ITSG-33 would still need to select control profiles, define tailoring, document control implementation statements, collect operating evidence and complete authorization activities appropriate to the system's business context.

## Boundary

This crosswalk demonstrates architectural literacy and traceability. It must not be represented as NIST certification, Government of Canada authorization or independent compliance attestation.
