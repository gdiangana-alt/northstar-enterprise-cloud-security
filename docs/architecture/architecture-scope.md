# NorthStar Enterprise Cloud Security — Architecture Scope

## Objective

Design an enterprise Azure security architecture that integrates the infrastructure, identity, governance, data protection, monitoring, detection, and incident-response capabilities developed across the NorthStar portfolio.

## Architecture Domains

The architecture covers six primary security domains:

1. Identity and Access Management
2. Network and Infrastructure Security
3. Data and Secrets Protection
4. Cloud Governance and Policy
5. Security Monitoring and Detection
6. Incident Response

## Design Principles

The NorthStar architecture follows these principles:

- Zero Trust
- Verify explicitly
- Least-privilege access
- Assume breach
- Defense in depth
- Network segmentation
- Centralized governance
- Secure workload identities
- Data classification and protection
- Continuous monitoring
- Detection and response
- Automation where appropriate

## Existing NorthStar Capabilities

The architecture integrates capabilities previously validated across the NorthStar portfolio:

### Infrastructure

- Azure virtual networking
- Subnet segmentation
- Network Security Groups
- Azure CLI
- Infrastructure as Code with Bicep
- Infrastructure troubleshooting

### Identity and Zero Trust

- Microsoft Entra ID
- Security groups
- Azure RBAC
- Azure ABAC
- MFA baseline controls
- Managed identities
- Azure Policy
- Identity lifecycle governance

### Security Operations

- Azure Activity Log
- Log Analytics
- Microsoft Sentinel
- KQL detection engineering
- Scheduled analytics rules
- Security alerts
- Incident investigation
- Incident classification and resolution

## Target Outcome

The final architecture will demonstrate how these capabilities operate together as a cohesive enterprise cloud-security system rather than as isolated Azure services.

The architecture will document security boundaries, trust relationships, attack paths, preventive controls, detective controls, response capabilities, architectural decisions, and implementation constraints.
