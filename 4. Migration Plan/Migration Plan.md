## 4. Migration Plan
#### Phase 1: Assessment
 - Use Azure Migrate to discover VMs, apps, DBs
 - Dependency mapping

#### Phase 2: Pilot Migration
 - Migrate non‑critical web app to App Service
 - Validate connectivity, performance

#### Phase 3: Database Migration
 - Use Azure Database Migration Service (DMS)
 - Migrate SQL Server → SQL MI
 - Validate schema, data integrity

#### Phase 4: App Tier Migration
 - Containerize .NET services
 - Deploy to AKS
 - Configure CI/CD pipelines (Azure DevOps/GitHub Actions)

#### Phase 5: Cutover
 - Switch DNS to Azure Front Door
 - Monitor traffic and performance

#### Phase 6: Post‑Migration Optimization
 - Cost optimization (Azure Advisor)
 - Security hardening (Defender for Cloud)
 - Backup & DR setup (Azure Site Recovery)
