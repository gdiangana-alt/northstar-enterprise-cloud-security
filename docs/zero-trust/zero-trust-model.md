# NorthStar Zero Trust Architecture Model

## Objective

Apply Zero Trust principles across identities, workloads, networks, data, governance, and monitoring within the NorthStar Azure environment.

The model assumes that no user, device, workload, network location, or administrative action should be trusted automatically.

## Core Principles

### Verify Explicitly

Access decisions should consider identity, authentication strength, authorization, resource sensitivity, and activity context.

NorthStar uses:

- Microsoft Entra ID
- MFA baseline controls
- Azure RBAC
- Azure ABAC
- Security groups
- Activity logging
- Sentinel monitoring

### Use Least Privilege

Access is limited to the minimum permissions required for approved business or technical functions.

NorthStar implements:

- Group-based access
- Scoped Azure RBAC assignments
- ABAC conditions
- Managed identities for workloads
- Separation of administrative and standard access
- Identity lifecycle controls

### Assume Breach

The architecture assumes that credentials, sessions, workloads, or network paths may eventually be compromised.

Controls therefore focus on limiting blast radius and increasing visibility.

NorthStar implements:

- Network segmentation
- Restricted inbound access
- Resource-level authorization
- Centralized logging
- KQL detections
- Sentinel alerts
- Incident investigation and response

## Identity Layer

Human and workload identities are treated as primary security boundaries.

Controls include:

- Microsoft Entra ID
- Security groups
- MFA
- Azure RBAC
- Azure ABAC
- Managed identities
- Lifecycle governance
- Break-glass account design
- Privileged access concepts

## Network Layer

Network location alone does not establish trust.

Controls include:

- Segmented Azure subnets
- Network Security Groups
- Restricted management access
- Controlled east-west traffic
- Private-access design concepts
- Explicit network rules

## Workload Layer

Applications and services should authenticate using workload identities rather than embedded credentials.

Controls include:

- User-assigned managed identities
- Scoped role assignments
- Secrets-management architecture
- Resource-level permissions
- Monitoring of management activity

## Data Layer

Access to data is governed independently of network access.

Controls include:

- Data classification
- Azure Policy enforcement
- Storage RBAC
- ABAC conditions
- Encryption
- Time-limited delegated access
- Secrets and key-management design

## Governance Layer

Security controls are reinforced centrally rather than relying entirely on individual administrators.

Controls include:

- Azure Policy
- Mandatory classification requirements
- Security baselines
- Deployment guardrails
- Resource tagging
- Policy scope and exclusion design

## Monitoring Layer

Trust decisions and administrative activity are continuously observable.

Controls include:

- Azure Activity Log
- Log Analytics
- Microsoft Sentinel
- KQL
- Scheduled analytics rules
- Alerts
- Incidents
- Investigation and classification

## Zero Trust Flow

```text
User / Workload
       ↓
Identity Verification
       ↓
Authentication Controls
       ↓
Authorization
   RBAC / ABAC
       ↓
Network Controls
       ↓
Azure Resource / Data
       ↓
Activity Logging
       ↓
Microsoft Sentinel
       ↓
Detection & Investigation
       ↓
Response
