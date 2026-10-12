# NorthStar Security Controls Matrix

## Objective

Map NorthStar security controls to their security function and clearly distinguish controls that were validated in the portfolio from target-state enterprise architecture recommendations.

## Control Status

- **Validated** — implemented and tested with recorded results in a NorthStar lab environment.
- **Implemented** — configured in the project or delivery platform with implementation evidence.
- **Authored** — version-controlled content exists but is not claimed as deployed.
- **Target State** — recommended enterprise control that forms part of the architecture but was not implemented and validated as a permanent NorthStar control.

## Security Controls

| Security Domain | Control | Function | Status |
|---|---|---|---|
| Identity | Microsoft Entra ID | Preventive | Validated |
| Identity | Security Groups | Preventive | Validated |
| Identity | Azure RBAC | Preventive | Validated |
| Identity | Azure ABAC | Preventive | Validated |
| Identity | MFA / Security Defaults | Preventive | Validated |
| Identity | Managed Identity | Preventive | Validated |
| Identity | Manual Identity Lifecycle Control | Preventive | Validated |
| Identity | Conditional Access | Preventive | Target State |
| Identity | Privileged Identity Management | Preventive | Target State |
| Identity | Emergency Access Design | Responsive | Target State |
| Network | Azure Virtual Network | Preventive | Validated |
| Network | Subnet Segmentation | Preventive | Validated in Lab |
| Network | Network Security Groups | Preventive | Validated |
| Network | Explicit Inbound Rules | Preventive | Validated |
| Network | Application Gateway WAF with OWASP CRS 3.2 | Preventive / Detective | Validated |
| Network | Restricted App Service ingress | Preventive | Validated |
| Network | Azure Bastion | Preventive | Target State |
| Network | Private Endpoints / Private Link | Preventive | Target State |
| Data | Data Classification | Preventive | Validated |
| Data | Azure Policy Tag Enforcement | Preventive | Validated |
| Data | Storage RBAC | Preventive | Validated |
| Data | Storage ABAC Condition | Preventive | Validated |
| Data | Time-Limited SAS | Preventive | Validated |
| Data | Azure Key Vault with scoped RBAC | Preventive | Validated |
| Data | Managed TLS certificate retrieval | Preventive | Validated |
| Data | Automated certificate renewal | Preventive | Target State |
| Governance | Azure Policy | Preventive / Detective | Validated |
| Governance | Policy Compliance | Detective | Validated |
| Governance | Policy Exception Design | Preventive | Target State |
| Infrastructure | Azure Bicep | Preventive | Validated |
| Infrastructure | Modular Terraform and remote state | Preventive | Validated |
| Secure Delivery | Terraform formatting and validation | Preventive | Implemented |
| Secure Delivery | Checkov infrastructure scanning | Preventive / Detective | Implemented |
| Secure Delivery | Policy-as-code gate | Preventive | Implemented |
| Secure Delivery | Protected pull-request workflow | Preventive | Implemented |
| Secure Delivery | Passwordless GitHub Actions OIDC | Preventive | Validated |
| Secure Delivery | Plan-only managed identity | Preventive | Validated |
| Monitoring | Azure Activity Log | Detective | Validated |
| Monitoring | Diagnostic Settings | Detective | Validated |
| Monitoring | Log Analytics | Detective | Validated |
| Monitoring | Microsoft Sentinel | Detective | Validated |
| Monitoring | KQL Detection | Detective | Validated |
| Monitoring | Scheduled Analytics Rule | Detective | Validated |
| Monitoring | Telemetry-based WAF detection tuning | Detective | Validated |
| Monitoring | Operational-state drift validation | Detective | Validated |
| Security Operations | Security Alert | Detective | Validated |
| Security Operations | Sentinel Incident | Detective / Responsive | Validated |
| Security Operations | Incident Investigation | Responsive | Validated |
| Security Operations | Incident Classification | Responsive | Validated |
| Security Operations | Incident Resolution | Responsive | Validated |
| Security Operations | Severity-based approval automation | Responsive | Validated |
| Security Operations | Managed-identity response playbook | Responsive | Validated |
| Security Operations | Destructive automated containment | Responsive | Target State |

## Defense-in-Depth Mapping

```text
PREVENT
Identity + RBAC + ABAC + MFA + NSGs + Policy + Data Controls
                         │
                         ▼
DETECT
Activity Logs + Log Analytics + KQL + Microsoft Sentinel
                         │
                         ▼
RESPOND
Investigation + Approval + Controlled Playbook + Classification
                         │
                         ▼
IMPROVE
Governance + Architecture + Detection Tuning
```

## Architectural Value

The control matrix prevents conceptual architecture from being confused with implemented capability.

NorthStar demonstrates validated controls where practical while documenting additional enterprise controls as target-state recommendations. The approval-gated playbook proves identity, authorization, orchestration and auditability; it does not claim automated destructive containment.

This distinction preserves technical accuracy while showing how the validated portfolio components can evolve into a broader enterprise cloud security architecture.
