# NorthStar Enterprise Threat Model

## Objective

Identify credible attack paths across the NorthStar Azure environment and map them to preventive, detective, and responsive security controls.

The threat model assumes that identities, workloads, credentials, network paths, and administrative interfaces may be targeted or compromised.

## Trust Boundaries

The architecture contains several important trust boundaries:

```text
Internet
   │
   ▼
[External Boundary]
   │
   ▼
Web Tier
   │
   ▼
[Workload Boundary]
   │
   ▼
Application / Data Resources

Users
   │
   ▼
[Identity Boundary]
   │
   ▼
Microsoft Entra ID
   │
   ▼
RBAC / ABAC
   │
   ▼
Azure Resources

Azure Resources
   │
   ▼
[Monitoring Boundary]
   │
   ▼
Log Analytics
   │
   ▼
Microsoft Sentinel
```

Crossing a trust boundary requires explicit security controls.

## Attack Path 1 — Compromised User Identity

### Scenario

An attacker obtains valid user credentials and attempts to access NorthStar resources.

### Risks

- Unauthorized resource access
- Data exposure
- Privilege escalation
- Administrative changes

### Preventive Controls

- MFA
- Security groups
- Least-privilege RBAC
- ABAC conditions
- Privileged-access design
- Identity lifecycle governance

### Detective Controls

- Identity and audit telemetry where available
- Azure Activity Log
- Microsoft Sentinel
- KQL detections

### Response

- Investigate identity activity
- Revoke unauthorized access
- Remove excessive permissions
- Rotate affected credentials where applicable
- Review related resource activity

---

## Attack Path 2 — Excessive or Misused Privileges

### Scenario

A compromised or legitimate identity attempts actions beyond its intended responsibilities.

### Risks

- Privilege escalation
- Unauthorized configuration changes
- Security-control modification
- Data access

### Preventive Controls

- Least-privilege RBAC
- Group-based authorization
- Resource scoping
- ABAC
- Privileged-access design

### Detective Controls

- Role-assignment monitoring
- Azure Activity Log
- Sentinel analytics
- Administrative activity investigation

### Response

- Review role assignments
- Remove unnecessary privilege
- Investigate related administrative operations
- Reassess authorization design

---

## Attack Path 3 — Internet-Facing Workload Compromise

### Scenario

An attacker exploits an externally accessible workload.

### Risks

- Workload compromise
- Lateral movement
- Credential theft
- Access to internal resources

### Preventive Controls

- Network segmentation
- NSGs
- Restricted inbound access
- Workload identities
- Least-privilege resource permissions
- Private-access architecture where appropriate

### Detective Controls

- Workload and Azure telemetry
- Centralized logging
- Sentinel detections

### Response

- Isolate affected resources
- Investigate related activity
- Revoke compromised access
- Rotate exposed secrets where required
- Remediate the exploited configuration or vulnerability

---

## Attack Path 4 — Secret or Credential Exposure

### Scenario

Application credentials, secrets, tokens, or keys are exposed through code, configuration, or operational processes.

### Risks

- Unauthorized workload impersonation
- Data access
- Resource manipulation
- Persistence

### Preventive Controls

- Managed identities
- Azure Key Vault architecture
- No secrets in source repositories
- Scoped RBAC
- Time-limited delegated access

### Detective Controls

- Access and administrative telemetry
- Azure Activity monitoring
- Sentinel investigation

### Response

- Revoke or rotate exposed credentials
- Investigate usage
- Remove unauthorized access
- Replace stored credentials with managed identities where possible

---

## Attack Path 5 — Security Control Tampering

### Scenario

An attacker attempts to weaken monitoring, policy, logging, or other defensive controls.

### Risks

- Reduced visibility
- Defense evasion
- Policy bypass
- Persistence

### Preventive Controls

- Least-privilege administration
- Azure Policy
- Separation of responsibilities
- Restricted security configuration access

### Detective Controls

- Azure Activity Log
- Diagnostic-setting monitoring
- Policy activity monitoring
- Sentinel analytics

### Response

- Restore security controls
- Investigate the initiating identity
- Review related changes
- Escalate if malicious activity is confirmed

---

## Attack Path 6 — Unauthorized Data Access

### Scenario

A user or workload attempts to access data outside its authorized scope.

### Risks

- Data disclosure
- Data modification
- Regulatory or contractual exposure

### Preventive Controls

- Data classification
- Storage RBAC
- ABAC
- Encryption
- Managed identities
- Private-access design
- Time-limited delegated access

### Detective Controls

- Resource and administrative telemetry
- Centralized monitoring
- Sentinel investigation

### Response

- Revoke unauthorized access
- Determine affected resources
- Investigate data-access scope
- Preserve evidence
- Escalate according to data sensitivity

## Defense-in-Depth Model

No individual security control is assumed to prevent every attack.

NorthStar combines:

```text
Identity Security
       +
Least Privilege
       +
Network Segmentation
       +
Data Protection
       +
Cloud Governance
       +
Security Monitoring
       +
Incident Response
       =
Defense in Depth
```

## Outcome

The threat model demonstrates how NorthStar security controls work together across attack paths.

Preventive controls reduce the probability or impact of compromise, detective controls provide visibility into suspicious activity, and response controls provide a structured mechanism for containment, remediation, and recovery.
