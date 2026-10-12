# NorthStar Security Operations Architecture

## Objective

Provide centralized security visibility, detection, investigation, and incident-response capabilities across the NorthStar Azure environment.

The architecture integrates cloud telemetry with Microsoft Sentinel so that preventive security controls are supported by continuous monitoring and response.

## Security Operations Flow

```text
Azure Environment
       │
       ├── Identity Activity
       ├── Administrative Activity
       ├── Resource Changes
       ├── Policy Activity
       ├── WAF and Gateway Activity
       └── Security Telemetry
                    │
                    ▼
             Azure Monitoring
                    │
                    ▼
           Log Analytics Workspace
                    │
                    ▼
             Microsoft Sentinel
                    │
          ┌─────────┴─────────┐
          ▼                   ▼
     KQL Analysis       Analytics Rules
          │                   │
          └─────────┬─────────┘
                    ▼
              Security Alert
                    │
                    ▼
             Sentinel Incident
                    │
                    ▼
          Analyst Investigation
                    │
                    ▼
     Approval Task for Medium / High
                    │
                    ▼
      Approved Playbook or Manual Action
                    │
                    ▼
       Classification and Resolution
```

## Telemetry Collection

Security monitoring depends on reliable telemetry.

NorthStar uses Azure Activity Log to provide visibility into Azure control-plane operations.

A subscription-level diagnostic setting streams relevant activity to the centralized Log Analytics workspace.

Enterprise monitoring should additionally incorporate workload, identity, network, application, and security-product telemetry according to risk and operational requirements.

## Centralized Logging

`NorthStar-SOC-Workspace` provides the validated Log Analytics foundation for security telemetry.

Centralized logging enables:

- Security investigation
- Historical analysis
- Detection engineering
- Activity correlation
- Operational troubleshooting

## Detection Engineering

Microsoft Sentinel provides the SIEM layer.

KQL is used to transform collected telemetry into security detections.

NorthStar validated this process through failed Azure control-plane detection and Application Gateway WAF analytics. The original match-all WAF rule generated excessive Low-severity incidents. Thirty days of telemetry were analyzed to establish client-level five-minute baselines, and the rule was replaced with a multi-signal detection using event volume, distinct rules and distinct request paths.

The replacement was validated against historical qualifying activity, deployed disabled for configuration verification, enabled after validation and monitored with a recent negative-test window. The legacy rule was disabled rather than deleted, preserving an auditable rollback path.

## Alerting

Scheduled analytics rules evaluate security telemetry for defined conditions.

When detection criteria are satisfied, Sentinel generates security alerts containing context for analyst review.

Detection severity should reflect potential security impact rather than automatically treating every matching event as malicious.

## Incident Management

Sentinel can convert qualifying alerts into incidents.

The NorthStar incident-response workflow includes:

1. Detection
2. Alert generation
3. Incident creation
4. Triage
5. Investigation
6. Context validation
7. Classification
8. Response decision
9. Resolution
10. Documentation

## Detection Context

A detection represents a signal requiring interpretation.

Analysts should correlate alerts with:

- Identity activity
- Administrative context
- Target resources
- Related events
- Change activity
- Known security testing
- Expected operational behavior

NorthStar validated this principle when a correctly detected control-plane failure was investigated and classified as authorized security testing.

## MITRE ATT&CK

MITRE ATT&CK provides a framework for relating detections to potential adversary behaviors.

ATT&CK mappings should provide investigation context and should not be interpreted as proof that an adversary technique occurred.

## Approval-Gated Response

Medium- and High-severity incidents enter a Sentinel automation rule that:

- changes the incident to Active;
- adds `ApprovalRequired`; and
- creates a task requiring review of scope, evidence, business impact, approver identity and rollback.

After approval is recorded, the managed-identity Logic App can be invoked manually. The validated playbook adds an audit comment and `ResponseApproved` label. It performs no destructive containment.

Potential enterprise response actions may include:

- Identity containment
- Access revocation
- Privilege reduction
- Resource isolation
- Configuration rollback
- Credential or secret rotation
- Evidence preservation
- Escalation
- Detection tuning
- Incident resolution

Consequential actions should be added only after least-privilege permissions, false-positive handling, failure behavior and rollback are tested.

## Operational Assurance

The PowerShell operational validator compares live Azure and Sentinel state with a version-controlled YAML manifest. It checks subscription and workspace configuration, Sentinel enablement, and required analytics-rule properties. A detected mismatch returns a non-zero exit code, and successful runs produce sanitized JSON evidence through GitHub Actions using OIDC.

## Governance Integration

Security operations also monitor the effectiveness and impact of governance controls.

Policy violations, role changes, diagnostic-setting modifications, and other security-relevant administrative operations can provide useful detection signals.

This creates a feedback loop:

```text
Security Architecture
        ↓
Preventive Controls
        ↓
Operational Activity
        ↓
Monitoring & Detection
        ↓
Investigation
        ↓
Security Findings
        ↓
Architecture / Control Improvement
```

## Design Principle

NorthStar treats monitoring and incident response as architectural requirements rather than capabilities added after deployment.

Preventive controls reduce risk, but centralized telemetry, detection engineering, investigation, and response provide visibility when controls fail, are bypassed, or generate unexpected security events.
