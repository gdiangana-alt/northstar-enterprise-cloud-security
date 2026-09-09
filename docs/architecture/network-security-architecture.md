# NorthStar Network Security Architecture

## Objective

Design a segmented Azure network architecture that reduces external exposure, controls traffic between workload tiers, protects administrative access, and limits lateral movement.

## Network Architecture

```text
                         Internet
                            │
                            ▼
                  Controlled Ingress
                            │
                            ▼
                    ┌───────────────┐
                    │  Web Subnet   │
                    │ 10.0.1.0/24   │
                    └───────┬───────┘
                            │
                     Explicit Access
                            │
                            ▼
                    ┌───────────────┐
                    │  App Subnet   │
                    │ Application   │
                    │    Tier       │
                    └───────┬───────┘
                            │
                     Restricted Access
                            │
                            ▼
                    Internal Resources

              ┌───────────────────────────┐
              │   Management Subnet       │
              │ Administrative Services   │
              └───────────────────────────┘

All tiers
   │
   ▼
Azure Activity / Security Telemetry
   │
   ▼
Log Analytics → Microsoft Sentinel
```

## Segmentation Strategy

NorthStar separates workloads according to function and trust requirements.

### Web Tier

The web tier represents services requiring controlled external connectivity.

Security controls include:

- Dedicated subnet
- Network Security Group
- Explicit HTTP/HTTPS rules where required
- Default-deny behavior for unauthorized inbound traffic
- No assumption of trust for downstream application resources

### Application Tier

The application tier is isolated from direct Internet exposure.

Access should originate only from explicitly authorized services or network segments.

Security controls include:

- Dedicated application subnet
- Network Security Group
- Restricted inbound traffic
- Explicit communication paths from approved upstream services
- Workload identity for Azure resource access

### Management Tier

Administrative services are logically separated from application workloads.

Security controls include:

- Dedicated management subnet
- Restricted administrative access
- Least-privilege authorization
- No unnecessary public exposure
- Administrative activity monitoring

## Network Security Groups

NSGs provide subnet and network-interface traffic filtering.

NorthStar uses explicit security rules combined with Azure default-deny behavior to limit unnecessary connectivity.

Rules should follow:

- Least privilege
- Explicit source and destination requirements
- Required protocols and ports only
- Documented business or technical purpose
- Regular review of obsolete access

## Administrative Access

Production administrative access should not depend on unrestricted public SSH or RDP exposure.

Preferred architecture includes controlled management mechanisms such as:

- Azure Bastion
- Private connectivity
- Just-in-time administrative access
- Privileged identity controls

These controls are architectural recommendations and are not represented as implemented NorthStar components unless separately validated.

## Private Access Strategy

Where supported by workload requirements, Azure services should use private connectivity rather than public endpoints.

Potential controls include:

- Azure Private Link
- Private Endpoints
- Private DNS
- Public network access restrictions

These capabilities form part of the target enterprise architecture and should be deployed according to workload requirements.

## East-West Traffic

Communication between internal workload tiers is explicitly controlled.

A resource residing inside the Azure virtual network is not automatically considered trusted.

Traffic between web, application, management, and data resources should be permitted only where required.

## Monitoring

Network and resource-management activity feeds the broader NorthStar security operations architecture.

Relevant telemetry is centralized through Azure monitoring services and Microsoft Sentinel to support detection and investigation.

## Design Principle

Network segmentation is one layer of defense rather than the primary trust mechanism.

NorthStar combines network controls with identity-based authorization, workload identities, centralized governance, data protection, and continuous security monitoring.
