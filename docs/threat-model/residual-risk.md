# NorthStar Residual Risk Assessment

## Objective

Identify security risks that remain after NorthStar preventive, detective, and responsive controls are applied.

Security architecture reduces risk but does not eliminate it. Residual risk must be understood, monitored, and addressed according to business impact and risk tolerance.

## Residual Risk Summary

| Risk | Existing Mitigation | Residual Risk | Target-State Improvement |
|---|---|---|---|
| Compromised user credentials | MFA, RBAC, security groups, monitoring | Medium | Conditional Access and risk-based authentication |
| Excessive administrative privilege | RBAC, least privilege, activity monitoring | Medium | Privileged Identity Management and time-limited elevation |
| Internet-facing workload compromise | NSGs and network segmentation | Medium | Private access, expanded segmentation and workload security controls |
| Secret or credential exposure | Managed identities and scoped permissions | Medium-Low | Azure Key Vault and automated secret rotation |
| Unauthorized data access | RBAC, ABAC, classification and encryption | Medium-Low | Private endpoints and enhanced data monitoring |
| Security-control modification | Azure Policy, RBAC and Activity Log monitoring | Medium | Dedicated privileged controls and additional tampering detections |
| Detection gaps | Activity Log, Log Analytics, Sentinel and KQL | Medium | Additional telemetry sources and expanded detection coverage |
| Manual incident response | Sentinel investigation and documented response workflow | Medium | SOAR automation and response playbooks |

## Identity Risk

Baseline MFA significantly improves identity security, but authentication context remains limited without premium identity controls.

Target-state improvements include:

- Conditional Access
- Risk-based authentication
- Privileged Identity Management
- Automated access reviews
- Automated lifecycle workflows

## Network Risk

NSGs and segmentation restrict connectivity but cannot independently determine whether an authenticated workload or identity is trustworthy.

Residual risks include:

- Application-layer vulnerabilities
- Compromised workloads
- Permitted-path abuse
- Misconfigured security rules

Network controls must therefore operate alongside identity, workload, data, and monitoring controls.

## Data Risk

RBAC, ABAC, classification, encryption, and controlled delegated access reduce unauthorized data exposure.

Residual risk remains from:

- Compromised authorized identities
- Incorrect permissions
- Credential leakage
- Application vulnerabilities
- Operational mistakes

Target-state Key Vault and private connectivity provide additional protection.

## Detection Risk

NorthStar validated an end-to-end Azure control-plane detection path.

This does not imply complete detection coverage across all enterprise attack techniques.

Additional production telemetry could include:

- Microsoft Entra sign-in and audit logs
- Workload security logs
- Network telemetry
- Endpoint telemetry
- Application logs
- Microsoft Defender security signals

Detection engineering should evolve as threats, workloads, and available telemetry change.

## Response Risk

The validated NorthStar incident workflow requires analyst investigation and decision-making.

Manual response introduces potential delays during high-impact incidents.

Target-state environments can reduce response time through carefully controlled automation and SOAR playbooks.

Automated response should include safeguards to prevent legitimate activity from being disrupted by false positives.

## Risk Treatment

Residual risks can be handled through:

- Mitigation
- Monitoring
- Transfer
- Acceptance
- Avoidance

Risk-treatment decisions should consider likelihood, business impact, cost, operational requirements, and organizational risk tolerance.

## Design Principle

A mature security architecture does not claim that its controls eliminate risk.

NorthStar identifies remaining exposure, documents control limitations, and defines target-state improvements that can reduce residual risk as the environment matures.
