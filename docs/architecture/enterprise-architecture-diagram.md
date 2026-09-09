# NorthStar Enterprise Cloud Security Architecture

## Architecture Overview

The following diagram integrates the validated NorthStar security capabilities with clearly identified target-state enterprise controls.

```mermaid
flowchart TB

    Internet((Internet))
    Users[Enterprise Users]
    Admins[Cloud Administrators]

    subgraph Identity["Identity & Zero Trust"]
        Entra[Microsoft Entra ID]
        MFA[MFA / Security Defaults]
        Groups[Security Groups]
        AuthZ[Azure RBAC / ABAC]
        MI[Managed Identities]

        CA[Conditional Access<br/>Target State]
        PIM[Privileged Identity Management<br/>Target State]
    end

    subgraph Network["Azure Network Security"]
        VNet[NorthStar VNet]
        Web[Web Subnet]
        NSG[Network Security Group]

        App[Application Tier<br/>Target State]
        Mgmt[Management Tier<br/>Target State]
        Private[Private Endpoints / Bastion<br/>Target State]
    end

    subgraph Data["Data Protection"]
        Storage[Azure Storage]
        Classification[DataClassification = Internal]
        SAS[Time-Limited SAS]
        KV[Azure Key Vault<br/>Target State]
    end

    subgraph Governance["Governance"]
        Policy[Azure Policy]
        IaC[Azure Bicep]
        Guardrails[Security Guardrails]
    end

    subgraph SecOps["Security Operations"]
        Activity[Azure Activity Log]
        Diagnostics[Diagnostic Settings]
        LAW[Log Analytics]
        Sentinel[Microsoft Sentinel]
        KQL[KQL Analytics Rule]
        Incident[Alert / Incident]
        Response[Investigation & Response]
    end

    Internet --> Web
    Users --> Entra
    Admins --> Entra

    Entra --> MFA
    Entra -.-> CA
    Entra --> Groups
    Groups --> AuthZ
    Entra -.-> PIM

    AuthZ --> VNet
    AuthZ --> Storage
    MI --> Storage
    MI -.-> KV

    VNet --> Web
    Web --> NSG
    Web -.-> App
    Mgmt -.-> VNet
    Private -.-> VNet

    Storage --> Classification
    Storage --> SAS
    KV -.-> Storage

    Policy --> Classification
    Policy --> VNet
    Policy --> Storage
    IaC --> VNet
    Guardrails --> Policy

    VNet --> Activity
    Storage --> Activity
    Policy --> Activity
    AuthZ --> Activity

    Activity --> Diagnostics
    Diagnostics --> LAW
    LAW --> Sentinel
    Sentinel --> KQL
    KQL --> Incident
    Incident --> Response
```

## Diagram Legend

**Solid connections** represent controls or security flows validated within the NorthStar portfolio.

**Dashed connections** represent target-state enterprise capabilities that were not implemented as permanent NorthStar controls.

## Validated Architecture

The portfolio provides practical validation across the following security layers:

```text
Infrastructure
     ↓
Identity & Access
     ↓
Data Protection
     ↓
Cloud Governance
     ↓
Centralized Monitoring
     ↓
Detection Engineering
     ↓
Incident Response
```

## Target-State Extensions

The architecture identifies additional enterprise capabilities without presenting them as implemented lab components:

- Conditional Access
- Privileged Identity Management
- Azure Key Vault
- Expanded application and management segmentation
- Private Endpoints
- Azure Bastion

These controls represent the next maturity level for a production enterprise implementation.

## Architectural Principle

NorthStar combines preventive, detective, and responsive controls rather than relying on a single security boundary.

Identity establishes who or what may request access, authorization determines permitted actions, network controls restrict connectivity, governance establishes guardrails, data controls protect information, and Microsoft Sentinel provides centralized detection and response.
