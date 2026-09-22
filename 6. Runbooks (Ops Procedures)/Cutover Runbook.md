# Cutover Runbook — Project Xfusion Web

**Date:** 2026-10-04 (Saturday)
**Window:** 01:00 – 05:00 IST (4 hours)
**Rollback deadline:** 03:30 IST (if not passed, abort and revert)

## Pre-Cutover (T-24h, Friday)

| # | Step | Owner | Done |
|---|------|-------|------|
| P1 | Lower DNS TTL from 3600 → 300 seconds | Network | ☐ |
| P2 | Freeze all deployments & DB changes | Dev Lead | ☐ |
| P3 | Take final backup of on-prem SQL DB | DBA | ☐ |
| P4 | Verify DMS replication lag < 5s | DBA | ☐ |
| P5 | Notify stakeholders (email + Teams) | PM | ☐ |
| P6 | Confirm Azure resources are in "Ready" state | Infra | ☐ |

## Cutover Steps

| # | Time | Step | Owner | Duration | Actual |
|---|------|------|-------|----------|--------|
| 1 | 01:00 | Stop IIS app pool on on-prem (no new writes) | Dev | 2 min | |
| 2 | 01:05 | Wait for DMS final sync to complete (lag = 0) | DBA | ~10 min | |
| 3 | 01:15 | **Go/No-Go gate:** Confirm 0 pending transactions | DBA | 2 min | |
| 4 | 01:20 | Run validation: row count on-prem vs Azure (must match) | DBA | 5 min | |
| 5 | 01:30 | Switch DNS: CNAME `app.xfusion.com` → Azure Front Door IP | Network | 2 min | |
| 6 | 01:35 | Verify DNS propagation: `nslookup app.xfusion.com` from 3 locations | QA | 5 min | |
| 7 | 01:45 | Start Azure app (App Service / AKS) | Dev | 3 min | |
| 8 | 01:50 | Run smoke tests (login, create order, view dashboard) | QA | 15 min | |
| 9 | 02:10 | Monitor error rate for 10 min (must be < 0.1%) | DevOps | 10 min | |
| 10 | 02:20 | **Business sign-off** — notify stakeholders "Cutover complete" | PM | 5 min | |

## Rollback Trigger

> If ANY of the following is true at **03:30 IST**, execute Rollback Runbook:
> - P95 latency > 2× baseline for 5 consecutive minutes
> - Error rate > 1% for 3 consecutive minutes
> - Data integrity check fails (row count mismatch)
> - Any P0/P1 Sev alert fires

## Rollback Steps (if triggered)

| # | Step | Owner |
|---|------|-------|
| R1 | Stop Azure app | Dev |
| R2 | Revert DNS: CNAME back to on-prem IP | Network |
| R3 | `nslookup` to confirm propagation | QA |
| R4 | Start on-prem IIS app pool | Dev |
| R5 | Restore DB from pre-cutover backup (if delta writes occurred) | DBA |
| R6 | Smoke test on-prem | QA |
| R7 | Notify: "Rollback complete" | PM |   
