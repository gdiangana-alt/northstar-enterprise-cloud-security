# NorthStar Security Operating Model

## Objective

Define ownership and decision boundaries for operating the NorthStar target architecture. The model prevents security tooling from becoming ownerless and prevents automation from bypassing accountable human decisions.

## Core Roles

| Role | Primary accountability |
|---|---|
| Cloud platform owner | Landing-zone reliability, shared services, network and platform standards |
| Identity owner | Authentication, lifecycle, privileged access and identity risk |
| Application owner | Workload risk, data use, application recovery and remediation |
| Security engineering | Guardrails, detection architecture, response automation and assurance |
| SOC analyst | Alert triage, investigation, classification and evidence preservation |
| Incident commander | Severity, containment decision, coordination and business communication |
| Change approver | Business impact, implementation window and rollback authorization |
| Risk owner | Acceptance, funding and treatment of residual business risk |

## Responsibility Matrix

R = Responsible, A = Accountable, C = Consulted, I = Informed.

| Activity | Platform | Identity | App owner | Security engineering | SOC | Incident commander | Risk owner |
|---|---|---|---|---|---|---|---|
| Cloud security baseline | R | C | C | A | I | I | I |
| Privileged-access design | C | A/R | I | C | I | I | I |
| Network and WAF configuration | A/R | I | C | C | I | I | I |
| Detection development | C | C | C | A/R | C | I | I |
| Alert triage | I | C | C | C | A/R | I | I |
| Containment approval | C | C | C | C | R | A | I |
| Playbook execution | I | I | I | C | R | A | I |
| Exception approval | C | C | C | R | I | I | A |
| Recovery validation | R | C | A | C | I | C | I |
| Residual-risk acceptance | C | C | C | C | I | I | A/R |

## Detection Lifecycle

Every operational detection requires:

1. a documented threat or control-failure scenario;
2. an authoritative telemetry source;
3. an owner and review date;
4. severity and threshold rationale;
5. a positive test and a negative test;
6. investigation guidance and expected entities;
7. false-positive and exclusion documentation; and
8. a retirement or replacement decision when the signal is no longer useful.

## Incident Severity and Approval

Low-severity incidents may remain queued for routine triage unless additional context increases impact. Medium- and High-severity incidents enter the demonstrated approval workflow: they become Active, receive `ApprovalRequired`, and receive an approval task.

Approval must record:

- incident scope and supporting evidence;
- expected business impact;
- proposed action and minimum permissions;
- rollback or recovery method;
- approver identity; and
- completion result.

The current Logic App does not perform destructive containment. It records approved execution and adds `ResponseApproved`, proving the control path without creating avoidable operational risk.

## Change and Exception Management

Security changes should be version controlled and pass automated validation before implementation. Emergency changes still require retrospective review, evidence and an owner.

Exceptions must contain:

- affected control and scope;
- business justification;
- risk owner;
- compensating controls;
- expiry date; and
- closure or renewal decision.

## Evidence Standard

Evidence must establish what was expected, what actually occurred and who or what performed the action. Public evidence must exclude credentials, tokens, tenant/subscription identifiers, object identifiers, personal information and unnecessary resource IDs.

## Review Cadence

| Review | Minimum cadence |
|---|---|
| Critical incidents and failed automation | After each occurrence |
| Detection performance and false positives | Monthly |
| Privileged access and federated identity | Quarterly |
| Policy exceptions and risk register | Quarterly |
| Architecture and recovery exercises | At least annually and after material change |

## Operating Principle

Tools execute controls; accountable roles decide why the controls exist, when exceptions are justified and whether residual risk is acceptable.
