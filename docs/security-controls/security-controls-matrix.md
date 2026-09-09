# NorthStar Security Controls Matrix

## Objective

Map NorthStar security controls to their security function and clearly distinguish controls that were validated in the portfolio from target-state enterprise architecture recommendations.

## Control Status

- **Validated** — implemented and tested within the NorthStar portfolio or its documented Azure lab environments.
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
| Network | Azure Bastion | Preventive | Target State |
| Network | Private Endpoints / Private Link | Preventive | Target State |
| Data | Data Classification | Preventive | Validated |
| Data | Azure Policy Tag Enforcement | Preventive | Validated |
| Data | Storage RBAC | Preventive | Validated |
| Data | Storage ABAC Condition | Preventive | Validated |
| Data | Time-Limited SAS | Preventive | Validated |
| Data | Azure Key Vault | Preventive | Target State |
| Governance | Azure Policy | Preventive / Detective | Validated |
| Governance | Policy Compliance | Detective | Validated |
| Governance | Policy Exception Design | Preventive | Target State |
| Infrastructure | Azure Bicep | Preventive | Validated |
| Monitoring | Azure Activity Log | Detective | Validated |
| Monitoring | Diagnostic Settings | Detective | Validated |
| Monitoring | Log Analytics | Detective | Validated |
| Monitoring | Microsoft Sentinel | Detective | Validated |
| Monitoring | KQL Detection | Detective | Validated |
| Monitoring | Scheduled Analytics Rule | Detective | Validated |
| Security Operations | Security Alert | Detective | Validated |
| Security Operations | Sentinel Incident | Detective / Responsive | Validated |
| Security Operations | Incident Investigation | Responsive | Validated |
| Security Operations | Incident Classification | Responsive | Validated |
| Security Operations | Incident Resolution | Responsive | Validated |
| Security Operations | Automated SOAR Response | Responsive | Target State |

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
Investigation + Classification + Containment + Remediation
                         │
                         ▼
IMPROVE
Governance + Architecture + Detection Tuning
```

## Architectural Value

The control matrix prevents conceptual architecture from being confused with implemented capability.

NorthStar demonstrates validated controls where practical while documenting additional enterprise controls as target-state recommendations.

This distinction preserves technical accuracy while showing how the validated portfolio components can evolve into a broader enterprise cloud security architecture.
