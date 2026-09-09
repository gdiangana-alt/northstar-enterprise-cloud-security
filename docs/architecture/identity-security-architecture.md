# NorthStar Identity Security Architecture

## Objective

Design identity as the primary security control plane for human users, administrators, applications, and Azure workloads.

The architecture applies Zero Trust and least-privilege principles so that network location alone never grants access to NorthStar resources.

## Identity Architecture

```text
                    Microsoft Entra ID
                           │
             ┌─────────────┴─────────────┐
             │                           │
        Human Identities            Workload Identities
             │                           │
      Users / Groups              Managed Identities
             │                           │
             ▼                           ▼
      Authentication                Authentication
       MFA Baseline                 Without Embedded
        Controls                      Credentials
             │                           │
             └─────────────┬─────────────┘
                           ▼
                     Authorization
                     RBAC / ABAC
                           │
                           ▼
                    Azure Resources
                           │
                           ▼
                    Audit / Activity
                           │
                           ▼
               Log Analytics / Sentinel
```

## Human Identity Security

NorthStar uses Microsoft Entra ID as the centralized identity platform.

Access is organized through security groups representing business and technical functions rather than assigning broad permissions directly to individual users wherever practical.

The validated NorthStar model includes:

- Cloud administrators
- Security analysts
- Application developers
- Standard employees

## Authentication

Baseline authentication protection is provided through Microsoft Entra Security Defaults and Microsoft Authenticator.

The target enterprise architecture extends this model with risk- and context-aware access controls where appropriate licensing is available.

Potential enterprise controls include:

- Conditional Access
- Authentication strength requirements
- Sign-in risk evaluation
- User risk evaluation
- Location and device context

These are architectural recommendations and are not represented as implemented controls unless separately validated.

## Authorization

Azure authorization follows least privilege.

NorthStar uses:

- Azure RBAC for role-based permissions
- Security-group-based assignments
- Resource and resource-group scoping
- Azure ABAC conditions where additional resource attributes are required

Permissions should be granted at the narrowest practical scope.

## Privileged Access

Administrative access receives stronger controls than standard user access.

The target architecture includes:

- Dedicated administrative identities
- Minimal standing privilege
- Privileged Identity Management where licensing permits
- Time-limited privilege elevation
- Approval and audit requirements for sensitive roles
- Separate administrative and standard-user activity

## Emergency Access

The enterprise design includes emergency-access accounts for recovery from identity-control failures.

Emergency accounts should:

- Be tightly controlled
- Be excluded only from controls necessary to preserve emergency access
- Use strong authentication
- Avoid routine administrative use
- Be continuously monitored
- Generate alerts when used
- Be regularly tested

This is an architectural design requirement rather than a claim that production break-glass accounts were deployed in the NorthStar lab.

## Workload Identity

Applications and Azure services should authenticate through managed identities whenever supported.

This reduces reliance on:

- Embedded passwords
- Stored application credentials
- Long-lived secrets
- Manually distributed service credentials

Managed identities receive only the Azure roles required by their workload.

## Identity Lifecycle

Access should change with the user's organizational lifecycle.

The architecture supports:

```text
Joiner → Access Provisioning
Mover  → Access Reassessment
Leaver → Access Removal
```

NorthStar previously validated a manual leaver scenario by removing a user from an access group while retaining the identity for lifecycle and audit purposes.

Enterprise implementations can extend this with automated lifecycle workflows and access reviews where licensing supports them.

## Monitoring

Identity and authorization activity should be centrally observable.

Relevant telemetry includes:

- Sign-in activity
- Audit events
- Group membership changes
- Role assignments
- Privileged operations
- Resource-management activity

Available telemetry should feed centralized monitoring and Microsoft Sentinel for investigation and detection.

## Design Principle

Identity is treated as a security boundary independent of network location.

A user or workload must be authenticated, explicitly authorized, appropriately scoped, governed throughout its lifecycle, and monitored after access is granted.
