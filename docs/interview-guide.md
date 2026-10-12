# NorthStar Enterprise Architecture — Interview Guide

## Thirty-Second Explanation

NorthStar is a six-project Azure security portfolio that I designed as one enterprise story rather than isolated labs. It connects least-privilege identity, segmented infrastructure, WAF and Key Vault protection, policy-governed Terraform delivery, Microsoft Sentinel detection and approval-gated SOAR. Every major claim links to sanitized evidence, and the architecture distinguishes what I validated hands-on from what I recommend as production target state.

## Two-Minute Technical Explanation

The public workload sits behind Application Gateway WAF and reaches an HTTPS-only App Service. The application and gateway use managed identities and scoped Key Vault access instead of embedded credentials. Human authorization is group based through Entra ID and Azure RBAC, with ABAC demonstrated for data access.

Terraform and Bicep provide repeatable configuration. GitHub pull requests require quality, security and policy checks, while a dedicated plan-only managed identity authenticates through OIDC and cannot deploy infrastructure. Azure Activity and WAF telemetry flow into Log Analytics and Sentinel. I tuned a noisy match-all WAF detection using 30 days of telemetry, replaced it with a multi-signal high-confidence rule and reconciled the legacy incident queue.

For response, Medium and High incidents are activated, labelled and assigned an approval task. After approval is recorded, a managed-identity Logic App can be invoked manually to add an audit comment and `ResponseApproved` label. It deliberately performs no destructive containment. That design proves orchestration and least privilege without pretending a lab should automatically disable identities or isolate workloads.

## Architecture Narrative

```text
Identity establishes trust
        ↓
Least privilege limits action
        ↓
Segmentation and WAF reduce exposure
        ↓
Policy and CI/CD govern change
        ↓
Telemetry makes activity observable
        ↓
Detection creates investigation context
        ↓
Approval gates consequential response
        ↓
Evidence supports assurance and improvement
```

## Strong Interview Topics

### Why approval-gated SOAR instead of full automation?

Containment can disrupt legitimate operations. I first automated preparation, attribution and evidence, then required human approval before response execution. Destructive actions would be added only after permissions, rollback, false-positive handling and business ownership were tested.

### How did you tune the WAF detection?

The initial rule created incidents from any WAF match and produced hundreds of low-value incidents. I analyzed 30 days of telemetry, measured five-minute client buckets and selected multiple behavioral signals—match volume, distinct rules and distinct paths. I validated historical positive results, confirmed a recent negative window, deployed the replacement disabled for configuration verification, enabled it and disabled the legacy rule.

### How is least privilege demonstrated?

Human roles are group based and resource scoped. Workloads use managed identities. The GitHub plan identity has only read and state permissions, while the Logic App has Microsoft Sentinel Responder at workspace scope. No long-lived Azure client secret is required for GitHub Actions.

### What failed, and what did you learn?

A mandatory classification policy initially blocked creation of an untagged managed identity. The corrected tagged deployment succeeded. A first playbook invocation also failed because the Sentinel service and operator lacked different required permissions. I diagnosed the two authorization boundaries, added the narrow roles, retested successfully and classified the generated incidents. Those failures became evidence about policy design, API validation and RBAC dependencies.

### What remains target state?

Conditional Access, PIM, access reviews, private endpoints, Bastion, WAF Prevention mode, automated certificate renewal, broader Defender/endpoint telemetry and destructive containment are not claimed as deployed. They are sequenced in the roadmap with prerequisites and validation requirements.

## Evidence to Mention

- six linked repositories with distinct implementation scope;
- protected pull-request gates and passwordless OIDC;
- live expected-state validation with sanitized JSON evidence;
- telemetry-based detection thresholds rather than arbitrary values;
- positive and negative automation tests;
- least-privilege managed-identity playbook execution; and
- explicit residual-risk and recovery documentation.

## Honest Scope Statement

NorthStar is controlled portfolio work, not employer production experience. It demonstrates hands-on implementation, troubleshooting and architectural judgment while clearly identifying licensing, scale and production-operating constraints.
