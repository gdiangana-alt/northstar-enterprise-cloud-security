# NorthStar Enterprise Cloud Security — Executive Architecture Brief

## Executive Summary

NorthStar is a controlled Azure security portfolio that demonstrates how infrastructure, identity, governance, secure delivery and security operations can operate as one defensible system. The architecture is grounded in six public projects and separates live validation from production recommendations.

The implemented environment uses segmented Azure networking, Application Gateway WAF, App Service, Microsoft Entra ID, group-based RBAC, managed identities, Azure Key Vault, Azure Policy, Log Analytics, Microsoft Sentinel, GitHub Actions and Terraform. Security-relevant changes are validated through protected delivery gates, centralized telemetry and evidence-producing operational checks.

The operating model assumes that preventive controls will sometimes fail. Detection and response are therefore first-class architecture requirements. Microsoft Sentinel receives Azure control-plane and WAF telemetry, tuned analytics reduce alert noise, and Medium- or High-severity incidents enter an approval workflow before the managed-identity response playbook may be invoked. The demonstrated playbook records authorized execution without performing destructive containment.

## Business Problem

Cloud environments become difficult to defend when identity, infrastructure, delivery and security operations are designed independently. Typical consequences include excessive privilege, inconsistent configuration, unmonitored changes, alert fatigue and automated response without adequate safeguards.

NorthStar addresses that problem through five architectural outcomes:

1. identity and managed workload credentials replace implicit network trust;
2. segmented infrastructure and WAF controls reduce exposed attack paths;
3. policy and protected infrastructure-as-code delivery create repeatable guardrails;
4. centralized telemetry and tuned detections convert activity into actionable incidents; and
5. approval-gated automation improves response consistency while preserving human accountability.

## Architecture Outcomes

| Outcome | Implemented evidence | Enterprise value |
|---|---|---|
| Least-privilege access | Entra groups, scoped RBAC/ABAC, managed identities | Reduces standing privilege and credential exposure |
| Protected application delivery | Segmented VNet, dedicated WAF subnet, Application Gateway WAF, HTTPS-only App Service | Reduces direct exposure and creates inspection telemetry |
| Governed cloud configuration | Azure Policy, Terraform/Bicep, protected pull requests, Checkov and policy-as-code | Makes security requirements repeatable and reviewable |
| Central detection and investigation | Log Analytics, Sentinel, KQL analytics, WAF and control-plane telemetry | Provides evidence for triage and incident decisions |
| Controlled automation | Severity-based automation rule, approval task, managed-identity Logic App | Prevents unapproved containment while proving safe orchestration |
| Continuous assurance | Ten expected-versus-actual operational checks with sanitized evidence | Detects drift and supports auditability |

## Key Architecture Decisions

- Identity is treated as the primary security boundary.
- Human access is group based and scoped to the smallest practical resource boundary.
- Azure workloads use managed identities instead of stored application credentials where supported.
- Internet traffic reaches the application through Application Gateway WAF rather than direct public application access.
- Terraform changes pass formatting, security scanning, policy and pull-request controls before merge.
- GitHub Actions uses short-lived OIDC authentication; the demonstrated live workflow is plan-only.
- Sentinel detections are tuned from observed telemetry rather than arbitrary thresholds.
- Response automation prepares and records action, but destructive containment requires explicit approval and remains outside the demonstrated playbook.

## Material Residual Risks

| Residual risk | Current treatment | Recommended progression |
|---|---|---|
| Compromised privileged identity | MFA baseline, scoped RBAC and monitoring | Conditional Access, PIM, risk-based identity protection and access reviews |
| Public workload exploitation | WAF Detection mode, restricted backend access and telemetry | Tune exclusions, validate Prevention mode and add workload/endpoint protection |
| Certificate renewal failure | Key Vault-backed certificate and documented renewal date | Automate DNS validation, renewal and expiry alerting |
| Incomplete telemetry coverage | Azure Activity and WAF telemetry in Sentinel | Add Entra, endpoint, application and Defender signals based on risk |
| Response delay | Approval task and non-destructive response playbook | Add tested, reversible containment actions with protected approval paths |
| Recovery uncertainty | Version control, remote state, evidence and documented procedures | Formalize recovery objectives and regularly test restore and redeployment |

## Investment Priorities

1. Complete premium identity controls for privileged and risky access.
2. Automate certificate lifecycle management before production use.
3. Expand telemetry coverage and detection-as-code validation.
4. Test WAF Prevention mode using an approved tuning and rollback plan.
5. Build reversible containment actions behind the existing approval gate.
6. Establish tested recovery objectives for identity, state, logging and application services.

## Decision Statement

The NorthStar architecture is suitable as a validated portfolio reference, not as a claim of production operation. Its strongest value is the traceable connection between design decisions, deployed controls, operational evidence and explicitly documented residual risk.
