# NorthStar Network Security Architecture

## Objective

Design a segmented Azure network architecture that reduces external exposure, controls traffic between workload tiers, protects administrative access, and limits lateral movement.

## Network Architecture

```text
Internet
   │
   ▼
Application Gateway WAF
Dedicated WAF subnet
   │ HTTPS
   ▼
App Service
Direct ingress restricted to gateway path
   │ Managed identity
   ▼
Azure Key Vault

Segmented VNet
   ├── Management subnet
   ├── Web subnet
   ├── Application subnet
   └── Dedicated WAF subnet
            │
            ▼
Gateway diagnostics and Azure activity
            │
            ▼
Log Analytics → Microsoft Sentinel
```

## Segmentation Strategy

NorthStar separates workloads according to function and trust requirements.

### Web Tier

The public web path is fronted by Application Gateway WAF. The gateway uses OWASP Core Rule Set 3.2 in Detection mode, terminates trusted HTTPS and sends access, performance and firewall telemetry to Log Analytics.

Security controls include:

- Dedicated WAF subnet
- Network Security Group
- HTTP-to-HTTPS redirection
- Managed HTTPS certificate retrieved from Key Vault
- Default-deny behavior for unauthorized inbound traffic
- Restricted App Service direct ingress

### Application Tier

The landing-zone VNet includes a dedicated application subnet for tier separation. The validated web workload uses App Service with direct access restricted to the Application Gateway path rather than claiming that the service is hosted in the application subnet.

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

Application Gateway access, performance and WAF logs are centralized with Azure control-plane telemetry through Log Analytics and Microsoft Sentinel. WAF telemetry was used to tune a multi-signal high-confidence scanning detection.

## Design Principle

Network segmentation is one layer of defense rather than the primary trust mechanism.

NorthStar combines network controls with identity-based authorization, workload identities, centralized governance, data protection, and continuous security monitoring.
