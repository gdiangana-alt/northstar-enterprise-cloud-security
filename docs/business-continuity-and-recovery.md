# NorthStar Security Continuity and Recovery Model

## Objective

Define how security services, configuration and evidence should be restored after operational failure, compromise or accidental change. This document is a target-state operating model informed by the controls validated in the portfolio; it is not a claim of production disaster-recovery testing.

## Recovery Priorities

1. preserve human safety and legal obligations;
2. maintain trustworthy identity and emergency access;
3. contain active compromise without destroying evidence;
4. restore logging and security visibility;
5. restore protected application access and critical data paths; and
6. reconcile infrastructure, policy and detection configuration with approved source.

## Recoverable Assets

| Asset | Recovery source | Primary concern |
|---|---|---|
| Infrastructure configuration | Protected Git repositories and reviewed Terraform/Bicep | Unauthorized or unreviewed configuration |
| Terraform state | Azure remote-state storage with Entra authentication and locking | Corruption, deletion or exposure |
| Identity configuration | Entra audit data, group/role inventory and approved lifecycle records | Lockout or excessive privilege |
| Secrets and certificates | Key Vault versions, documented ownership and renewal process | Expiry, deletion or unauthorized retrieval |
| Detection content | Version-controlled KQL and Bicep | Silent loss of monitoring coverage |
| Sentinel incidents and evidence | Sentinel records and sanitized exported evidence | Loss of investigative context |
| Application configuration | IaC, App Service settings and approved deployment artifacts | Inconsistent or vulnerable recovery |

## Failure Scenarios

### Identity Control Failure

- validate emergency access through a controlled procedure;
- revoke suspicious sessions and privilege where authorized;
- restore approved group and role assignments;
- verify audit and sign-in visibility; and
- conduct a post-recovery access review.

### Infrastructure or State Failure

- preserve the affected state and logs before repair;
- compare live resources with approved source and state;
- restore or import only after ownership and scope are confirmed;
- generate a plan before any apply action; and
- validate network, identity, logging and application dependencies after restoration.

### Logging or Sentinel Failure

- restore diagnostic settings and ingestion before normalizing operations;
- verify workspace retention and Sentinel enablement;
- redeploy version-controlled analytics and automation rules;
- perform positive and negative detection tests; and
- reconcile the incident queue and evidence gaps.

### Certificate or WAF Failure

- preserve a trusted HTTPS path or invoke the approved maintenance procedure;
- renew/import the certificate through controlled Key Vault access;
- confirm Application Gateway backend health and redirect behavior;
- validate WAF telemetry; and
- investigate whether the failure was operational or malicious.

## Recovery Objectives

Production recovery objectives must be approved by service and risk owners after business-impact analysis. NorthStar does not invent numeric RTO or RPO values without that analysis.

The architecture instead defines dependency order:

```text
Emergency identity access
        ↓
Logging and evidence preservation
        ↓
Network and platform control
        ↓
Secrets and certificate access
        ↓
Application service restoration
        ↓
Detection and automation verification
```

## Recovery Validation

A recovery exercise is complete only when:

- the initiating failure and authorization are recorded;
- approved configuration is restored;
- access is least privilege;
- telemetry and detections function;
- application health is confirmed;
- evidence is preserved and sanitized appropriately;
- temporary access is removed; and
- lessons and residual risk are assigned to owners.

## Portfolio Boundary

NorthStar validates configuration, detection and controlled response workflows. Full regional failover, production backup restoration and enterprise identity disaster recovery remain target-state exercises requiring business-owned recovery objectives and representative workloads.
