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
- Application Gateway WAF
- Restricted App Service ingress
- Workload identities
- Least-privilege resource permissions
- Private-access architecture where appropriate

### Detective Controls

- WAF, gateway, workload and Azure telemetry
- Centralized logging
- Tuned Sentinel detections

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
- Azure Key Vault with scoped RBAC
- Managed TLS certificate retrieval
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

---

## Attack Path 7 — CI/CD or Federated Identity Compromise

### Scenario

An attacker modifies infrastructure code or abuses a trusted automation workflow to access or change Azure resources.

### Risks

- Unauthorized infrastructure change
- Credential or state exposure
- Security-control weakening
- Persistence through trusted delivery paths

### Preventive Controls

- Protected branches and required pull-request checks
- Terraform validation, Checkov and policy-as-code
- GitHub OIDC instead of stored Azure client secrets
- Federated subject restricted to the approved repository and branch
- Plan-only identity without deployment permission
- Separate remote-state access scope

### Detective Controls

- GitHub workflow and branch-protection evidence
- Azure Activity Log
- Terraform expected-state validation
- Monitoring of federated credentials and role assignments

### Response

- Disable or remove the affected federated credential
- Revoke automation access and review workflow history
- Compare live state with approved source and remote state
- Investigate Azure activity performed by the identity
- Restore trusted configuration through protected change control

---

## Attack Path 8 — Unauthorized or Unsafe Response Automation

### Scenario

A playbook is invoked without adequate approval or receives permissions capable of disrupting legitimate services.

### Risks

- Account or workload outage
- Destruction or loss of evidence
- Excessive privilege through automation
- Unattributed containment activity

### Preventive Controls

- Severity-based approval task
- `ApprovalRequired` and `ResponseApproved` audit labels
- Manual invocation after recorded approval
- Dedicated managed identity
- Workspace-scoped Sentinel Responder role
- Non-destructive playbook actions

### Detective Controls

- Sentinel incident task, comment and label history
- Logic App run history
- Azure Activity Log
- Failed control-plane operation detection

### Response

- Disable the automation rule or Logic App
- Revoke the playbook identity's role assignment
- Preserve run history and incident evidence
- Reverse the action using its approved rollback procedure
- Investigate the approver, operator and triggering context

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
