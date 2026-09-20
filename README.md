## Azure migration plan for a typical on‑premises 3‑tier application (Web → App → Database). 

# Azure Migration – Design and Execution Phases
## 01 Scope Definition
Clarify what is being migrated and why.

- Identify the 3‑tier app (Web, App, DB)

- Define business drivers (scalability, cost, DR)

- Document current infra (servers, storage, network)

- Note compliance/security requirements
## 02. Requirements & Assessment

Understand the **technical and business needs** before designing the Azure solution.

### Key Activities

* Meet stakeholders:

  * IT
  * Business
  * Security
* Document:

  * SLA requirements
  * RPO (Recovery Point Objective)
  * RTO (Recovery Time Objective)
  * Availability / uptime goals
* Identify application dependencies:

  * Active Directory (AD)
  * DNS
  * External integrations
  * APIs and supporting services
* Capture current performance baselines:

  * CPU utilization
  * Memory utilization
  * Storage IOPS
  * Network throughput

---

## 03. High-Level Design (HLD)

Map the existing **on-premises application tiers** to appropriate Azure services.

| On-Prem Tier     | Azure Service Options                              |
| ---------------- | -------------------------------------------------- |
| Web Tier         | Azure App Service / Azure Front Door               |
| Application Tier | Azure Kubernetes Service (AKS) / Azure App Service |
| Database Tier    | Azure SQL Database / Azure SQL Managed Instance    |
| Networking       | Azure VNet / NSG / Azure Firewall                  |
| Identity         | Microsoft Entra ID integration                     |

### HLD Focus

* Define overall Azure architecture
* Identify major Azure services
* Define network topology
* Define security boundaries
* Define availability and DR architecture
* Define integration between application components

---

## 04. Low-Level Design (LLD)

Define the **detailed configuration and implementation parameters**.

### Networking

* VNet CIDR ranges
* Subnet design
* Network Security Groups (NSGs)
* Route tables / UDRs
* Azure Firewall configuration

### Compute

* VM sizes
* AKS node pools
* Auto-scaling configuration
* Availability requirements

### Storage

* Storage accounts
* Replication settings
* Performance tiers
* Backup requirements

### Identity & Access

* Microsoft Entra ID
* RBAC assignments
* Managed identities
* Least-privilege access

### Monitoring

* Log Analytics Workspace
* Azure Monitor
* Application Insights
* Alerts and dashboards

---

## 05. Migration Planning

Define **migration phases, tools, dependencies, and rollback strategies**.

### Key Activities

* Use **Azure Migrate** for:

  * Discovery
  * Dependency mapping
  * Assessment
  * Migration planning
* Select pilot workloads:

  * Prefer non-critical workloads initially
* Define migration strategy:

  * Big bang
  * Phased migration
  * Wave-based migration
* Create a rollback plan
* Define production cutover windows
* Identify migration dependencies and owners

### Migration Wave Example

```text
Wave 1 → Non-Critical Applications
Wave 2 → Supporting Applications
Wave 3 → Business-Critical Applications
Wave 4 → Mission-Critical / Core Systems
```

---

## 06. Execution

Execute the migration according to the approved migration plan.

### Infrastructure Migration

* Perform lift-and-shift migration of VMs using **Azure Migrate**
* Configure Azure networking and security
* Validate connectivity and dependencies

### Application Migration

* Refactor application workloads where required
* Move application tier to:

  * AKS
  * Azure App Service

### Database Migration

* Migrate databases using appropriate Azure migration tools
* Validate:

  * Schema
  * Data integrity
  * Connectivity
  * Performance

### Validation

Perform validation in the staging environment:

* Application functionality
* Database connectivity
* Performance
* Security
* Monitoring
* Backup and recovery

### Production Cutover

```text
Final Sync
    ↓
Freeze Source
    ↓
Perform Cutover
    ↓
Update DNS / Routing
    ↓
Start Azure Workloads
    ↓
Functional Validation
    ↓
Business Sign-Off
```

---

## 07. Post-Migration Management

Ensure the migrated environment remains **reliable, secure, cost-effective, and compliant**.

### Monitoring & Observability

* Azure Monitor
* Application Insights
* Log Analytics
* Alerts
* Dashboards

### Backup & Disaster Recovery

* Azure Backup
* Azure Site Recovery
* Validate RPO/RTO
* Perform periodic DR testing

### Cost Management

* Azure Cost Management
* Budgets and alerts
* Right-size resources
* Apply appropriate scaling policies
* Identify idle and underutilized resources

### Security & Governance

* Microsoft Defender for Cloud
* Azure Policy
* RBAC
* Security baselines
* Compliance monitoring

### Operations

Create and maintain operational runbooks for:

* Application restart
* VM/AKS operations
* Backup and restore
* DR/failover
* Incident response
* Monitoring and alert handling
* Scaling procedures

---

# Overall Azure Migration Flow

```text
Requirements & Assessment
          ↓
   High-Level Design
          ↓
    Low-Level Design
          ↓
   Migration Planning
          ↓
      Pilot/Wave
          ↓
      Migration
          ↓
     Validation
          ↓
   Production Cutover
          ↓
 Post-Migration Operations
          ↓
 Optimization & Governance
```
