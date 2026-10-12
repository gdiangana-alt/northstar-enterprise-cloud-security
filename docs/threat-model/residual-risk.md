# NorthStar Residual Risk Assessment

## Objective

Identify security risks that remain after NorthStar preventive, detective, and responsive controls are applied.

Security architecture reduces risk but does not eliminate it. Residual risk must be understood, monitored, and addressed according to business impact and risk tolerance.

## Residual Risk Summary

| Risk | Existing Mitigation | Residual Risk | Target-State Improvement |
|---|---|---|---|
| Compromised user credentials | MFA, RBAC, security groups, monitoring | Medium | Conditional Access and risk-based authentication |
| Excessive administrative privilege | RBAC, least privilege, activity monitoring | Medium | Privileged Identity Management and time-limited elevation |
| Internet-facing workload compromise | Segmentation, restricted backend ingress, WAF Detection mode and telemetry | Medium | Tuned Prevention mode, workload protection and private access where justified |
| Secret or credential exposure | Managed identities, scoped permissions and Key Vault | Medium-Low | Automated rotation, certificate renewal and secret-lifecycle monitoring |
| Unauthorized data access | RBAC, ABAC, classification and encryption | Medium-Low | Private endpoints and enhanced data monitoring |
| Security-control modification | Azure Policy, RBAC and Activity Log monitoring | Medium | Dedicated privileged controls and additional tampering detections |
| Detection gaps | Activity Log, Log Analytics, Sentinel and KQL | Medium | Additional telemetry sources and expanded detection coverage |
| Delayed or unsafe response | Approval automation and non-destructive managed-identity playbook | Medium-Low | Tested reversible containment actions with protected approvals |
| Certificate expiry | Key Vault-backed TLS and documented renewal procedure | Medium | Automated issuance, renewal and expiry alerting |

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

Key Vault and managed identities reduce stored-credential exposure. Private connectivity, automated rotation and certificate-lifecycle monitoring provide additional protection.

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

The validated NorthStar incident workflow requires analyst investigation and approval before consequential response.

Approval and manual invocation can still introduce delays during high-impact incidents.

NorthStar validates severity-based automation and a non-destructive managed-identity playbook. This reduces preparation and documentation delay without granting the playbook authority to disable identities or isolate workloads.

Future containment automation should be reversible, separately authorized, least privilege and tested against false positives and partial failure.

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
