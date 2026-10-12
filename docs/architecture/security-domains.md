# NorthStar Enterprise Security Domains

## Overview

The NorthStar enterprise cloud-security architecture is organized into eight security domains that work together to protect Azure resources, identities, workloads, data, delivery and operations.

## 1. Identity and Access Management

### Objective

Ensure that users, groups, applications, and workloads receive only the access required to perform approved functions.

### Controls

- Microsoft Entra ID
- Security groups
- Azure RBAC
- Azure ABAC
- MFA baseline controls
- Managed identities
- Least-privilege role assignments
- Identity lifecycle governance
- Break-glass account design
- Privileged access concepts

## 2. Network and Infrastructure Security

### Objective

Reduce attack surface and limit lateral movement through segmentation and controlled connectivity.

### Controls

- Azure Virtual Network
- Segmented subnets
- Network Security Groups
- Application Gateway WAF
- Restricted App Service ingress
- Restricted inbound access
- Internal traffic controls
- Secure management paths
- Private-access architecture concepts
- Infrastructure as Code
- Network troubleshooting and validation

## 3. Data and Secrets Protection

### Objective

Protect sensitive information throughout its lifecycle.

### Controls

- Data classification
- Azure Policy enforcement
- Storage access controls
- Encryption at rest
- Encryption in transit
- Azure Key Vault with scoped managed-identity access
- Secrets-management principles
- Managed identities for workload authentication
- Time-limited delegated access where appropriate

## 4. Cloud Governance and Policy

### Objective

Apply consistent enterprise security requirements across Azure resources.

### Controls

- Azure Policy
- Mandatory resource classification
- Security baselines
- Resource tagging
- Least-privilege governance
- Deployment guardrails
- Policy scope and exclusion design
- Auditability
- Architecture standards

## 5. Security Monitoring and Detection

### Objective

Provide centralized visibility into cloud activity and detect potentially suspicious behavior.

### Controls

- Azure Activity Log
- Log Analytics
- Microsoft Sentinel
- KQL
- Scheduled analytics rules
- Security alerts
- Detection engineering
- MITRE ATT&CK context
- Continuous monitoring

## 6. Incident Response

### Objective

Ensure detected security events can be investigated, classified, contained, remediated, and resolved.

### Controls

- Sentinel incident creation
- Alert triage
- Investigation
- Context validation
- Incident classification
- Containment decision-making
- Remediation
- Resolution
- Incident documentation

## 7. Secure Infrastructure Delivery

### Objective

Ensure infrastructure changes are reviewed, tested, policy compliant and authenticated without stored cloud credentials.

### Controls

- Terraform and Bicep
- Protected pull requests
- Formatting and validation
- Checkov security scanning
- Policy-as-code
- GitHub Actions OIDC
- Plan-only managed identity
- Sanitized workflow evidence

## 8. Continuity and Recovery

### Objective

Restore trustworthy identity, security visibility, infrastructure and application service after failure or compromise.

### Controls

- Version-controlled infrastructure and detection content
- Remote state with authentication and locking
- Emergency-access design
- Key Vault versioning and recovery capabilities
- Certificate renewal procedure
- Evidence preservation
- Recovery sequencing and validation criteria

## Architectural Relationship

The eight domains operate as an integrated security model:

```text
Identity
   ↓
Access Control
   ↓
Network & Infrastructure
   ↓
Data & Workloads
   ↓
Governance
   ↓
Secure Delivery
   ↓
Monitoring & Detection
   ↓
Incident Response
   ↓
Continuity & Recovery
```
