# NorthStar Enterprise Security Implementation Roadmap

## Purpose

Translate the validated NorthStar architecture into a risk-based enterprise adoption sequence. The roadmap preserves service continuity, limits privileged access and requires evidence before each maturity step is accepted.

## Prioritization Method

Work is ordered using four considerations:

- reduction of high-impact attack paths;
- dependencies required by later controls;
- operational and licensing constraints; and
- ability to validate, reverse and audit the change.

## Phase 0 — Discovery and Ownership

**Objective:** establish scope and accountability before technical enforcement.

| Deliverable | Acceptance criterion |
|---|---|
| Resource and identity inventory | Critical resources, owners, dependencies and data classifications are recorded |
| Privileged-access inventory | Direct, group, service-principal and emergency access are identified |
| Logging baseline | Required telemetry, retention and responsible owners are approved |
| Risk register | Risks have likelihood, impact, treatment, owner and review date |
| Exception process | Exceptions require justification, expiry and compensating controls |

## Phase 1 — Identity and Administrative Control

**Objective:** reduce the likelihood and impact of credential or privilege compromise.

- enforce phishing-resistant MFA for privileged roles where supported;
- implement Conditional Access using report-only evaluation before enforcement;
- introduce Privileged Identity Management for eligible elevation;
- establish emergency-access accounts with monitored use;
- automate joiner, mover and leaver controls;
- schedule access reviews for privileged and high-impact groups; and
- migrate remaining workload credentials to managed identities or governed secrets.

**Exit criteria:** no unexplained standing privileged access, emergency access is tested, and access revocation is demonstrably effective.

## Phase 2 — Network, Workload and Data Protection

**Objective:** restrict attack paths and protect public and internal workloads.

- maintain workload-tier segmentation and explicit NSG flows;
- use Application Gateway WAF as the controlled public entry point;
- tune managed rules against representative traffic before Prevention mode;
- remove unnecessary public endpoints through Private Link where justified;
- introduce Bastion or approved privileged remote-access paths;
- enforce Key Vault RBAC, soft delete, purge protection and rotation standards;
- automate certificate issuance, renewal and expiry monitoring; and
- apply Defender plans according to workload risk and cost.

**Exit criteria:** approved traffic flows are documented, public exposure is justified, secrets are governed and rollback has been tested.

## Phase 3 — Secure Delivery and Configuration Assurance

**Objective:** prevent unreviewed or noncompliant infrastructure change.

- standardize reusable Terraform/Bicep modules;
- require formatting, validation, security scanning and policy checks;
- use workload identity federation instead of stored CI/CD credentials;
- separate plan and deployment identities;
- protect production environments with reviewers and change windows;
- retain sanitized evidence while protecting raw plans and sensitive outputs; and
- run expected-state validation after approved changes.

**Exit criteria:** deployment cannot bypass required controls, identities hold only required permissions, and drift produces an actionable failure.

## Phase 4 — Detection and Incident Operations

**Objective:** provide reliable detection, triage and evidence preservation.

- onboard prioritized Azure, Entra, Defender, endpoint and application telemetry;
- assign owners and service-level objectives to each production detection;
- test detections with controlled events and negative cases;
- tune thresholds from baselines and document exclusions;
- map alerts to investigation steps and relevant ATT&CK context;
- monitor changes to logging, RBAC, policy, analytics and automation; and
- track false positives, mean time to triage and closure quality.

**Exit criteria:** high-priority detections are testable, owned, documented and linked to response procedures.

## Phase 5 — Approval-Gated Response and Recovery

**Objective:** automate safely without transferring unbounded authority to playbooks.

- preserve the approval task and `ApprovalRequired` label for consequential incidents;
- verify approver identity, business impact, scope and rollback before execution;
- grant each playbook a dedicated managed identity and minimum role;
- begin with evidence collection and reversible actions;
- require protected approval for account disablement, isolation or access revocation;
- record action, approver, outcome and recovery steps on the incident; and
- conduct tabletop and technical recovery exercises.

**Exit criteria:** automated actions are authorized, attributable, reversible and tested under failure conditions.

## Phase 6 — Continuous Assurance

**Objective:** keep the architecture effective as threats and services change.

- review risk and exceptions at defined intervals;
- monitor lifecycle and certificate deadlines;
- validate privileged access and federated credentials;
- measure control coverage and evidence freshness;
- reassess detection thresholds after material workload changes;
- test restoration of state, configuration and critical services; and
- update architecture decisions when constraints change.

## Success Measures

| Area | Example measure |
|---|---|
| Identity | Percentage of privileged access that is eligible rather than permanent |
| Exposure | Number of unjustified public endpoints |
| Delivery | Percentage of infrastructure changes merged through required gates |
| Detection | Tested high-priority detections with named owners |
| Response | Approval-to-action time and successful rollback rate |
| Assurance | Expected-state checks passing and exceptions within expiry |

## Sequencing Principle

Automation follows governance, identity and observability. A response action should not be automated until its authorization boundary, evidence requirements, failure behavior and rollback procedure are understood.
