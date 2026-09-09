# NorthStar Enterprise Security Domains

## Overview

The NorthStar enterprise cloud-security architecture is organized into six security domains that work together to protect Azure resources, identities, workloads, data, and operations.

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
- Azure Key Vault architecture
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

## Architectural Relationship

The six domains operate as an integrated security model:

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
Monitoring & Detection
   ↓
Incident Response
