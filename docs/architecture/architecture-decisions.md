# NorthStar Architecture Decisions & Constraints

## Objective

Document the major security architecture decisions, implementation constraints, trade-offs, and target-state capabilities within the NorthStar enterprise cloud security architecture.

## Decision 1 — Identity as the Primary Security Boundary

### Decision

NorthStar treats identity and authorization as the primary access-control layer rather than assuming that resources inside an Azure virtual network are trusted.

### Rationale

Modern cloud resources can be accessed through multiple network paths and service interfaces.

NorthStar therefore combines:

- Microsoft Entra ID
- MFA
- Azure RBAC
- Azure ABAC
- Managed identities
- Identity lifecycle controls

Network security remains an additional defense layer rather than the sole trust boundary.

---

## Decision 2 — Group-Based Authorization

### Decision

Human access should be assigned through security groups wherever practical rather than through repeated direct user assignments.

### Rationale

Group-based authorization improves:

- Access administration
- Role consistency
- Lifecycle management
- Auditability
- Least-privilege review

---

## Decision 3 — Managed Identities for Workloads

### Decision

Azure workloads should use managed identities when supported.

### Rationale

Managed identities reduce dependence on long-lived application credentials and eliminate the need to embed supported Azure authentication secrets in source code or configuration.

The NorthStar portfolio validated a user-assigned managed identity with scoped Azure RBAC permissions.

---

## Decision 4 — Segmented Network Architecture

### Decision

Workload tiers should be separated according to function and trust requirements.

### Rationale

Segmentation reduces unnecessary connectivity and limits potential lateral movement.

The permanent NorthStar environment validated VNet, subnet, and NSG controls. Additional application and management segmentation represents target-state architecture where not present in the permanent environment.

---

## Decision 5 — Centralized Governance

### Decision

Security requirements should be enforced centrally where practical rather than depending entirely on manual administrator behavior.

### Rationale

Azure Policy provides consistent governance and compliance assessment.

NorthStar validated mandatory resource classification through policy enforcement.

The Sentinel deployment also demonstrated that governance controls require carefully designed scope and exception handling to avoid disrupting legitimate Azure platform operations.

---

## Decision 6 — Centralized Security Monitoring

### Decision

Security-relevant Azure control-plane telemetry should be centralized for analysis and detection.

### Rationale

NorthStar uses:

```text
Azure Activity Log
        ↓
Diagnostic Settings
        ↓
Log Analytics
        ↓
Microsoft Sentinel
        ↓
KQL Detection
        ↓
Alert / Incident
```

This provides an end-to-end security operations path from cloud activity to investigation and response.

---

## Decision 7 — Detection Requires Analyst Context

### Decision

A detection is treated as a security signal rather than automatic proof of malicious activity.

### Rationale

NorthStar validated this principle through a controlled Azure operation that generated a legitimate Sentinel alert and incident.

Investigation determined that the activity was authorized security testing, demonstrating the importance of analyst context and incident classification.

---

## Decision 8 — Separate Validated Controls from Target State

### Decision

NorthStar explicitly distinguishes implemented or validated controls from architectural recommendations.

### Rationale

Enterprise architectures frequently include capabilities that cannot or should not be reproduced in a small portfolio environment.

The security controls matrix therefore identifies controls as:

- Validated
- Validated in Lab
- Target State

This prevents architectural recommendations from being presented as production implementation experience.

---

## Platform and Licensing Constraints

The NorthStar environment uses Microsoft Entra ID Free capabilities.

As a result, premium identity capabilities such as Conditional Access and Privileged Identity Management are documented as target-state controls rather than implemented features.

Where appropriate, Security Defaults provides the validated baseline MFA protection.

---

## Cost and Lab Constraints

NorthStar is a portfolio and laboratory environment rather than a continuously operating production platform.

Architecture decisions therefore prioritize:

- Low-cost validation
- Reusable Azure resources
- Controlled testing
- Documentation of enterprise target state
- Avoidance of unnecessary persistent compute resources

Some infrastructure capabilities were validated in temporary lab environments rather than maintained permanently.

---

## Security Tooling vs Governance

Security tooling may create platform-managed resources that interact unexpectedly with broad governance policies.

NorthStar encountered this when mandatory tag enforcement interfered with Microsoft Sentinel enablement.

The experience demonstrates why enterprise policy architecture requires:

- Testing
- Scope analysis
- Controlled exemptions
- Platform-service awareness
- Change management

---

## Architecture Limitation

NorthStar does not represent a production enterprise deployment.

It demonstrates security architecture principles and validated Azure controls using a controlled portfolio environment.

Capabilities documented as target state should not be interpreted as deployed production services.

## Design Principle

A credible security architecture documents not only its controls, but also its assumptions, constraints, trade-offs, implementation status, and operational consequences.
