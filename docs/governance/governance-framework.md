# NorthStar Enterprise Cloud Governance Framework

## Objective

Establish centralized security guardrails that ensure Azure resources are deployed, configured, classified, monitored, and operated according to NorthStar enterprise security requirements.

Governance complements technical security controls by defining requirements that apply consistently across the cloud environment.

## Governance Model

```text
Enterprise Security Requirements
              │
              ▼
       Governance Standards
              │
              ▼
         Azure Policy
              │
       ┌──────┴──────┐
       ▼             ▼
   Prevent         Audit
       │             │
       ▼             ▼
Azure Resources → Compliance State
       │
       ▼
Logging & Monitoring
       │
       ▼
Microsoft Sentinel
```

## Resource Classification

NorthStar requires applicable resources to carry:

`DataClassification=Internal`

The control was validated using Azure Policy.

A noncompliant resource operation was denied until the required classification tag was supplied.

This demonstrates preventive governance rather than relying solely on administrator compliance.

## Policy Enforcement

Azure Policy provides centralized enforcement and assessment.

NorthStar governance uses policy controls to support:

- Required resource metadata
- Data classification
- Secure configuration
- Deployment standards
- Compliance visibility

Enterprise policy design should use appropriate effects according to risk:

- Audit
- Deny
- Modify
- DeployIfNotExists

## Policy Scope

Policies should be assigned at the highest appropriate scope while avoiding unnecessary impact on platform-managed resources.

Potential scopes include:

```text
Management Group
      ↓
Subscription
      ↓
Resource Group
      ↓
Resource
```

Broader scope provides consistency but requires stronger testing and exception management.

## Exception Management

Security policies must account for legitimate platform requirements.

During the NorthStar Sentinel deployment, a mandatory tagging policy prevented creation of a Sentinel-managed resource that could not satisfy the tagging requirement.

This demonstrated the risk of applying blanket deny controls without considering Azure platform behavior.

A production governance model should use documented:

- Policy exclusions
- Exemptions
- Appropriate assignment scopes
- Service-specific policy design
- Approval processes
- Periodic exception reviews

Temporary disabling of enforcement should not be the standard production exception mechanism.

## Security Baselines

Enterprise Azure resources should follow defined security baselines covering areas such as:

- Identity and access
- Network exposure
- Encryption
- Logging
- Monitoring
- Resource classification
- Public endpoint restrictions
- Administrative access
- Secrets management

## Logging Requirements

Security-relevant Azure resources should provide sufficient telemetry for centralized monitoring.

The architecture includes:

- Azure Activity Log
- Diagnostic settings
- Log Analytics
- Microsoft Sentinel

Logging requirements should be incorporated into governance so that security monitoring is not dependent on manual configuration.

## Least-Privilege Governance

Authorization should follow:

- Minimum required privilege
- Appropriate resource scope
- Group-based assignment where practical
- Separation of administrative responsibilities
- Regular access reassessment

Privileged access should receive additional controls and monitoring.

## Infrastructure as Code

Infrastructure as Code improves governance by making infrastructure configuration:

- Repeatable
- Reviewable
- Version controlled
- Testable
- Documented

NorthStar previously validated Azure Bicep as part of its infrastructure implementation.

Enterprise environments should integrate IaC with security validation and deployment controls.

## Governance Monitoring

Governance does not end when a policy is assigned.

Organizations should monitor:

- Compliance state
- Policy failures
- Exceptions
- Role changes
- Resource configuration changes
- Logging configuration
- Security-control drift

Relevant activity should feed centralized security monitoring where appropriate.

## Design Principle

NorthStar treats governance as an architectural security layer.

Identity, network, data, and monitoring controls protect individual resources, while governance establishes consistent security requirements across the enterprise cloud environment.
