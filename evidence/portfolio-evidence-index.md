# NorthStar Portfolio Evidence Index

This index gives reviewers a direct path from each portfolio claim to public, sanitized implementation evidence. It separates validated work from target-state architecture and does not treat documentation alone as proof of deployment.

## Portfolio at a Glance

| # | Project | Primary capability | Status | Strongest evidence |
|---|---|---|---|---|
| 1 | [Azure Infrastructure & Network Security](https://github.com/gdiangana-alt/northstar-azure-lab) | Azure administration, networking, Bicep and troubleshooting | Validated | Bicep, CLI/Bash/PowerShell scripts, completion matrix and fault-remediation narrative |
| 2 | [Identity & Zero Trust](https://github.com/gdiangana-alt/northstar-identity-zero-trust) | Entra ID, RBAC/ABAC, managed identities and identity lifecycle | Validated | Terraform, control documentation, troubleshooting evidence and sanitized screenshots |
| 3 | [Security Operations](https://github.com/gdiangana-alt/northstar-azure-security-operations) | Sentinel, KQL, detection engineering and incident response | Validated | Detection/hunting queries, live validation, incident record, playbook and screenshots |
| 4 | [Secure Azure Landing Zone](https://github.com/gdiangana-alt/northstar-secure-azure-landing-zone) | Segmented Terraform foundation, WAF, TLS, Key Vault and monitoring | Validated lab implementation | Terraform modules, WAF/TLS validation and Sentinel case study |
| 5 | [Secure DevSecOps Pipeline](https://github.com/gdiangana-alt/northstar-secure-devsecops-pipeline) | Policy as code, security scanning, protected PRs and OIDC | Validated | GitHub Actions, Rego policy, remediation register and protected-gate screenshots |
| 6 | [Enterprise Cloud Security Architecture](https://github.com/gdiangana-alt/northstar-enterprise-cloud-security) | Zero Trust architecture, threat modeling, governance and residual risk | Documented architecture grounded in Projects 1–5 | Architecture decisions, threat model, controls matrix and residual-risk assessment |

## 1. Azure Infrastructure & Network Security

**Claims supported**

- Segmented Azure networking with subnet-level NSG controls.
- Repeatable infrastructure definition and deployment validation through Bicep.
- Structured diagnosis of an NSG rule-order failure affecting load-balancer health.
- Administrative automation through Azure CLI, Bash and PowerShell.

**Evidence paths**

- `bicep/main.bicep`
- `docs/architecture.md`
- `docs/troubleshooting.md`
- `docs/completion-matrix.md`
- `scripts/azure-cli/`
- `scripts/bash/vm-deployment.sh`
- `scripts/powershell/README.md`
- `evidence/README.md`

## 2. Identity & Zero Trust

**Claims supported**

- Group-based authorization using Azure RBAC and ABAC.
- Managed-identity implementation and least-privilege design.
- MFA/security-defaults and identity-lifecycle validation.
- Terraform quality and security checks for identity infrastructure.

**Evidence paths**

- `terraform/main.tf`
- `docs/architecture.md`
- `docs/terraform-identity-control.md`
- `docs/troubleshooting.md`
- `docs/completion-matrix.md`
- `.github/workflows/terraform-quality.yml`
- `.github/workflows/terraform-security.yml`
- `evidence/`

## 3. Security Operations

**Claims supported**

- Azure telemetry ingestion and Microsoft Sentinel analytics.
- KQL detection and threat-hunting content.
- Controlled-event validation and documented incident handling.
- A repeatable analyst response procedure for RBAC assignment alerts.

**Evidence paths**

- `analytics/detections/azure-role-assignment-created.kql`
- `analytics/hunting/application-gateway-waf-matches.kql`
- `analytics/hunting/failed-role-assignment-attempts.kql`
- `docs/sentinel-live-validation.md`
- `incidents/NS-IR-2026-001-failed-rbac-assignment-triage.md`
- `playbooks/azure-rbac-assignment-alert-response.md`
- `evidence/screenshots/`

## 4. Secure Azure Landing Zone

**Claims supported**

- Terraform-managed network, identity, governance, monitoring and web-front modules.
- Application Gateway WAF and diagnostic settings.
- Managed TLS certificate validation and documented WAF operations.
- Cost-conscious deployment and teardown decisions.

**Evidence paths**

- `main.tf`
- `modules/network/`
- `modules/identity/`
- `modules/governance/`
- `modules/monitoring/`
- `modules/webfront/`
- `docs/tls-and-waf-operational-validation.md`
- `docs/waf-log-validation.md`
- `docs/sentinel-incident-case-study.md`
- `docs/cost-control-and-teardown.md`

## 5. Secure DevSecOps Pipeline

**Claims supported**

- Terraform formatting and validation gates.
- Infrastructure security scanning and policy-as-code enforcement.
- Protected pull-request workflow and passwordless Azure OIDC planning.
- Documented remediation of security-scan findings.

**Evidence paths**

- `.github/workflows/terraform-quality.yml`
- `.github/workflows/terraform-security.yml`
- `.github/workflows/terraform-policy.yml`
- `.github/workflows/terraform-live-plan.yml`
- `policy/northstar.rego`
- `docs/checkov-remediation-register.md`
- `docs/pull-request-gate-validation.md`
- `docs/oidc-live-plan-control.md`
- `docs/evidence/screenshots/`

## 6. Enterprise Cloud Security Architecture

**Claims supported**

- A unified Zero Trust and defense-in-depth architecture.
- Explicit separation of validated controls and target-state recommendations.
- Threat scenarios mapped to preventive, detective and responsive controls.
- Documented architecture decisions, constraints and residual risks.

**Evidence paths**

- `docs/architecture/enterprise-architecture-diagram.md`
- `docs/architecture/architecture-decisions.md`
- `docs/threat-model/enterprise-threat-model.md`
- `docs/threat-model/residual-risk.md`
- `docs/security-controls/security-controls-matrix.md`
- `docs/governance/governance-framework.md`
- `docs/zero-trust/zero-trust-model.md`

## Evidence Boundaries

The following boundaries are deliberate:

- **PKI:** The portfolio demonstrates managed TLS certificate deployment and validation. It does not claim an enterprise certificate-authority or full PKI implementation.
- **WAF:** Architecture, configuration and operational validation are documented in the landing-zone project.
- **Bash and PowerShell:** Reusable administrative examples exist in the Azure infrastructure project.
- **SQL:** The current NorthStar architecture does not depend on a database workload, so SQL is not presented as validated project evidence.
- **Enterprise scale:** NorthStar is a controlled lab portfolio. Production-scale licensing, organizational processes and workload volume are represented as target-state considerations where appropriate.

## Publication Standard

Public evidence must exclude credentials, tokens, tenant IDs, subscription IDs, Entra object IDs, internal incident identifiers, temporary public addresses and other environment-specific identifiers. Deployment-specific values must be supplied through variables, environment configuration or documented placeholders.
