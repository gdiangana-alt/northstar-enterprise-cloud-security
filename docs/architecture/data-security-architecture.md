# NorthStar Data & Secrets Security Architecture

## Objective

Protect enterprise data, cryptographic material, application secrets, and storage resources throughout their lifecycle using classification, least-privilege access, encryption, centralized secrets management, and continuous monitoring.

## Data Security Architecture

```text
User / Workload Identity
          │
          ▼
 Authentication & Authorization
       RBAC / ABAC
          │
          ▼
   Data Classification
          │
          ▼
 ┌──────────────────────┐
 │   Azure Resources    │
 │ Storage / Workloads  │
 └──────────┬───────────┘
            │
     ┌──────┴──────┐
     ▼             ▼
 Encryption    Secrets / Keys
                   │
                   ▼
              Azure Key Vault
                   │
                   ▼
            Managed Identity
                   │
                   ▼
          Authorized Workload

Management Activity
        │
        ▼
Log Analytics / Sentinel
```

## Data Classification

NorthStar uses resource classification as a governance and security control.

The validated environment uses:

`DataClassification=Internal`

Azure Policy enforces the required classification value on applicable resources within the NorthStar environment.

Classification can be extended in an enterprise implementation to support categories such as:

- Public
- Internal
- Confidential
- Restricted

Security requirements should increase according to data sensitivity.

## Authorization

Access to Azure data resources is controlled independently of network connectivity.

NorthStar uses:

- Azure RBAC
- Security-group-based access
- Resource-level role assignments
- Azure ABAC conditions

The validated ABAC implementation restricts selected blob operations according to the target storage container.

## Encryption

Enterprise data should be encrypted both at rest and in transit.

The architecture requires:

- Azure service encryption for supported resources
- TLS for data in transit
- Secure key management
- Restricted access to cryptographic material
- Key rotation according to organizational requirements

Customer-managed keys may be introduced where regulatory, contractual, or risk requirements justify additional key control.

## Secrets Management

Application secrets should not be embedded in:

- Source code
- Deployment scripts
- Configuration files
- Container images
- Public repositories

The target architecture uses Azure Key Vault as the centralized service for managing:

- Secrets
- Cryptographic keys
- Certificates

Azure Key Vault is part of the target architecture and is not represented as an implemented NorthStar control unless separately validated.

## Workload Authentication

Managed identities are preferred over stored application credentials.

The intended flow is:

```text
Azure Workload
      ↓
Managed Identity
      ↓
Microsoft Entra ID
      ↓
Scoped RBAC Permission
      ↓
Key Vault / Storage / Azure Resource
```

This allows workloads to access authorized resources without storing long-lived credentials.

## Delegated Data Access

Where temporary delegated access is required, access should be:

- Resource specific
- Permission limited
- Time limited
- Revocable where supported
- Protected from public disclosure

NorthStar previously validated this principle using a read-only, time-limited SAS for a specific storage object.

SAS tokens and equivalent credentials must never be stored in public evidence or source repositories.

## Governance

Azure Policy provides centralized enforcement of data-classification requirements.

Enterprise policy design should also consider:

- Encryption requirements
- Public network access restrictions
- Approved deployment regions
- Required diagnostic settings
- Secure configuration baselines
- Private endpoint requirements for sensitive services

## Monitoring

Administrative changes affecting storage, access controls, policies, keys, secrets, and other protected resources should be logged and monitored.

Relevant activity can be centralized through Azure monitoring services and Microsoft Sentinel for detection and investigation.

## Design Principle

Data protection does not depend on a single perimeter.

NorthStar combines classification, identity-based authorization, encryption, workload identity, governance, secrets-management architecture, and monitoring to provide defense in depth around enterprise information.
