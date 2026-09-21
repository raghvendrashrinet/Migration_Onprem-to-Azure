## Architecture Mapping

- Web Tier → Azure App Service behind Azure Front Door (global load balancing)

- App Tier → Azure Kubernetes Service (AKS) with autoscaling

- Database Tier → Azure SQL Managed Instance with geo‑replication

- Networking → Hub‑spoke VNets, NSGs, Azure Firewall

- Identity → Azure AD + RBAC

#### Diagram (conceptual)

- Users → Front Door → App Service → AKS → SQL MI

- Monitoring via Azure Monitor + Log Analytics

- Security via Defender for Cloud
