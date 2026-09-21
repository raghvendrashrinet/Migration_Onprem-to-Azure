## Low Level Design (LLD)
#### Networking

- VNet: 10.0.0.0/16

- Subnets:
  - Web: 10.0.1.0/24
  - App: 10.0.2.0/24
  - DB: 10.0.3.0/24

- NSGs:
  - Allow 443 inbound to Web
  - Restrict DB access to App subnet only

#### Compute
- AKS:
  - Node pools: system (2 nodes), app (4–10 nodes autoscale), batch (2 nodes)

- App Service:
  - Standard S1 plan, autoscale 2–5 instances

#### Database
- SQL MI: Business Critical tier, 4 vCores, geo‑replication enabled

#### Identity & Security
- Azure AD RBAC roles:
  - Reader, Contributor, Owner
- Key Vault for secrets management

#### Monitoring
- Azure Monitor + Application Insights
- Log Analytics Workspace (LAW)
- Alerts configured for CPU > 80%, DB latency > 200ms
