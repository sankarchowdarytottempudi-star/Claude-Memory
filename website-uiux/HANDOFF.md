# Project: Website UI/UX Redesign (TraceIT) — Handoff

> "Website UI/UX redesign" = the TraceIT (Pulsedeck) monitoring platform work. This is a **separate project** from the AROYA Concierge page redesign (see `../concierge/HANDOFF.md`). Record only this project's work here.


**Date:** 2026-10-08  
**Status:** Five coordinated changes batched for IDE deployment; awaiting IDE completion and 02:30 UTC 9 Oct backup verification

## Who / What

**Site:** TraceIT (Pulsedeck) — unified monitoring platform  
**Primary URLs:**
- https://bff-uat.aroyacruises.com/api/ (Aroya Cruise)
- https://mobileapp.aroyacruises.com/api/ (Cruise Saudi — same system, unified monitoring)

**Repository:** Core application  
**Contact:** Sankar (sankarchowdary.tottempudi@gmail.com)

---

## Decisions Made

### Email Alert Batching
- **Decision:** 1 email per 15 minutes max with summary format (not individual per alert)
- **Rationale:** 2,022 alerts/day to 7 people (290 each) triggered Microsoft 365 spam filter; batching reduces to ~100 emails/day while preserving all alert content
- **Implementation:** Separate no-reply@traceittech.com mailbox for account emails (invites, password resets)
- **Recipients:** phphanikrishna@gmail.com, pcr.242108@gmail.com, hb151214@gmail.com, michaelsam.dbi@gmail.com, sankarchowdary.tottempudi@gmail.com, fhussain@cruisesaudi.com
- **Teams channel:** Aroya Monitoring
- **Status:** DEPLOYED ✓

### Analytics Optimization
- **Phase 1:** page_views_30d_summary materialized view (daily roll-up) — 17.6s → 1.2s (14.6x improvement) ✓ DEPLOYED
- **Phase 2:** Top pages, Platform/device, Country summaries + Acquisition denormalization ✓ DEPLOYED
- **Phase 3:** Distinct-count roll-up deferred as "acceptable for now" (24-hour view 2s, 7-day cached 1.9s usable)
- **Pending:** Remove "By system" Analytics section (one database query reduction) — in batch deploy

### Canary Health Check
- **Root causes identified:** Missing Origin header (https://traceit-tottech.com) + malformed request body (platform field missing)
- **Fix:** Added Origin header, fixed request body
- **Result:** Canary → ingest 202 OK ✓ DEPLOYED
- **Commit:** 24b12a4e6

### Nightly Backup Offsite
- **Problem:** Deploy backups stream to Backblaze; nightly backups local-only
- **Root cause:** curl 7.81 can't sign streamed uploads; nightly container lacks Python
- **Decision:** Python streaming uploader (1 MiB blocks, SHA-256 verification, environment-only credentials)
- **Implementation:** `/scripts/backup-offsite-put.py` (new); nightly postgres:16-alpine container modified to include Python 3
- **Performance:** ~13 minutes per 1.4 GB dump; memory <21 MB peak
- **Gate:** f1adf61ec PASSED; deployment in progress
- **Credentials:** BACKUP_S3_* environment variables (mapped from existing B2_* in .env)
- **Status:** Awaiting docker-compose.yml fix + environment variable mapping + 02:30 UTC 9 Oct verification

### Aroya Cruise / Cruise Saudi Unification
- **Decision:** Same system, no differentiation in monitoring
- **Implementation:** Unified API monitoring with shared alert routing and dashboards
- **Status:** CONFIGURED ✓

### Mobile Responsive Design
- **Breakpoints:** 390px-900px+ (mobile-first, desktop excellence)
- **Table-to-card:** Below 640px (one row per card, scrollable content)
- **Engagement list:** Becomes paginated (25 items/page) with "Sort by" menu
- **Android:** Opaque status bar strip with --safe-area-inset-top for notch handling
- **Licensing timeline:** Date markers below to avoid label overlap at any width
- **Status:** DEPLOYED ✓

---

## Requirements & Design Choices

### Five Coordinated Changes (Batched for One IDE Deployment)

#### 1. Fix docker-compose.yml Backup Service
- **Issue:** YAML syntax errors; manual text-based fixes failed
- **Fix:** Replace malformed backup service with clean YAML
  - Image: postgres:16-alpine
  - Container: pulsedeck-backup
  - Environment: BACKUP_S3_BUCKET, BACKUP_S3_KEY_ID, BACKUP_S3_SECRET_KEY, BACKUP_S3_ENDPOINT, BACKUP_S3_REGION, BACKUP_PASSPHRASE, POSTGRES_HOST, POSTGRES_USER, POSTGRES_PASSWORD, POSTGRES_DB
  - Depends on: postgres
  - Entrypoint: `sh -c "apk add --no-cache python3 py3-pip openssl && pip install --no-cache-dir requests && while true; do sleep 60; done"`
- **Validation:** `docker compose config` passes

#### 2. Remove Analytics "By System" Section
- **Scope:** Delete entire "By system" card (heading, table, all rows)
- **Benefit:** One database query reduction per Analytics load
- **UX:** Page loads clean; section gone; no console errors

#### 3. Add Backup Streaming Script
- **File:** `/opt/traceit/scripts/backup-offsite-put.py`
- **Specs:**
  - Python streaming uploader for Backblaze B2
  - 1 MiB block streaming with SHA-256 verification
  - Credentials from environment (BACKUP_S3_*) only
  - Upload: `s3://traceit-pg-backups/<timestamp>-<dbname>.enc`
  - Memory peak <256 MiB on typical 1.4 GB dumps
  - Logs success/failure with error details

#### 4. D365/Patchworks/Shopify Monitoring Integration Framework
- **Scope:** Monitoring-only (read-only, no destructive operations)
- **Role-based:** Owner, Workspace Admin, Admin only configure
- **Features:**
  - Dashboards: KPI cards per integration
  - Screens: Setup UI + monitoring view
  - Alerts: Real-time anomalies (sales drop, sync failures, error rates)
  - Health checks: Connectivity, API quota monitoring
- **Reference integrations:**
  - D365: OAuth, sales/revenue metrics
  - Patchworks: API key, workflow/sync status, error rate
  - Shopify: OAuth, order events, store health
- **Performance:** Pre-aggregate (materialized views, daily roll-ups, 5-min bucketing); dashboards <2s
- **Extensibility:** New integration type <5 code changes
- **Schema:** integrations table (metadata), external_events table (metrics), materialized views (KPIs)

#### 5. Daily Monitoring Input Methods
- **Three inputs:** URL, Paste text, Upload file (matching "Analyze a page" UX)
- **Edit capability:** Re-upload/re-paste latest after deployments (re-runs report with latest input)
- **UX:** Edit button visible; seamless re-upload flow; reports reflect current input

---

## What Is Built & Where

### Completed & Deployed
- **Email batching:** Alert routing pipeline (no-reply@traceittech.com separation)
- **Analytics Phase 1-2:** Materialized views, pre-aggregated summary tables
  - `page_views_30d_summary`
  - `analytics_visits_summary` (5-min bucketing, 30-min backfill)
  - `top_pages_summary`, `platform_device_summary`, `country_summary`
  - Acquisition denormalization
- **Canary health check:** Origin header + request body fix (commit 24b12a4e6)
- **Mobile responsive:** CSS grid/flexbox, table-to-card conversion, Android safe-area handling
- **Backup script:** `/scripts/backup-offsite-put.py` (streaming uploader, Python standard library)

### In Progress (Batch IDE Deployment)
- docker-compose.yml backup service (fix)
- Analytics "By system" removal
- D365/Patchworks/Shopify integration framework
- Daily monitoring input methods

### File Locations
- **Docker:** `/opt/traceit/docker-compose.yml` (needs backup service fix)
- **Backup script:** `/opt/traceit/scripts/backup-offsite-put.py`
- **Environment:** `/opt/traceit/.env` (contains B2_* and will receive BACKUP_S3_* vars)
- **Database:** Materialized views in PostgreSQL (timescaledb)
- **App code:** Repository root (Rails/Node/React stack)

---

## Known Defects

1. **Browser push subscriptions:** 546 failures on devices e02592d2, a4161b03 (deferred follow-up)
2. **Alert routing:** Old royalcyber.com address in config (deferred cleanup)
3. **iOS builds:** No Mac available; web-only delivery for now
4. **Analytics Phase 3:** Distinct-count roll-up deferred as "acceptable for now"

---

## Open Items

### Immediate (Next Session)
1. **IDE completes five-change batch:** Monitor completion and commit hashes
2. **Nightly backup verification:** 02:30 UTC 9 Oct
   - Check: `docker-compose logs backup --tail 100`
   - Verify: Dump encrypted, uploaded to Backblaze, file size correct, no credential errors
   - Report: "Nightly backup verified"

### Follow-up (After Batch Deploys)
1. Browser push re-subscription (devices e02592d2, a4161b03)
2. Remove royalcyber.com from alert routing
3. Phase 3 analytics optimization (if priority raised)

---

## Exact Next Steps

### For New Claude Session (If Limit Exhausted)

1. **Read this handoff** (you're doing it now)
2. **Pass IDE prompt** to Claude Code or IDE agent:

```
Build and deploy these five coordinated changes in one push:

FIX DOCKER-COMPOSE.YML BACKUP SERVICE
Image: postgres:16-alpine, container: pulsedeck-backup
Environment: BACKUP_S3_BUCKET, BACKUP_S3_KEY_ID, BACKUP_S3_SECRET_KEY, BACKUP_S3_ENDPOINT, BACKUP_S3_REGION, BACKUP_PASSPHRASE, POSTGRES_HOST, POSTGRES_USER, POSTGRES_PASSWORD, POSTGRES_DB
Depends on: postgres
Entrypoint: sh -c "apk add --no-cache python3 py3-pip openssl && pip install --no-cache-dir requests && while true; do sleep 60; done"
Validate: docker compose config passes
REMOVE ANALYTICS "BY SYSTEM" SECTION
Delete entire card (heading, table, all rows)
Benefit: one database query reduction per load
ADD BACKUP STREAMING SCRIPT
File: /opt/traceit/scripts/backup-offsite-put.py
Python streaming uploader for Backblaze B2
1 MiB blocks, SHA-256 verification, environment-only credentials
Upload: s3://traceit-pg-backups/<timestamp>-<dbname>.enc
Memory peak <256 MiB
D365/PATCHWORKS/SHOPIFY MONITORING FRAMEWORK
Monitoring-only (read-only), role-based (Owner/Admin/Workspace Admin)
Dashboards, Screens, Alerts, Health checks
Reference integrations: D365 (OAuth, sales/revenue), Patchworks (API key, sync), Shopify (OAuth, orders)
Pre-aggregate: materialized views, daily roll-ups, 5-min bucketing
Dashboard queries <2 seconds
New integration type: <5 code changes
DAILY MONITORING INPUT METHODS
Three inputs: URL, Paste text, Upload file (matching "Analyze a page" UX)
Edit capability: re-upload/re-paste after deployments
Reports reflect latest input

Acceptance: All five working, tests green, lint clean, conventional commits, push to main.
Do not ask questions — make architectural choices, build, test, commit, push. Report: what done, decisions, test results, commit hashes.
```

3. **After IDE completes:** Await commit hashes and verify

4. **Monitor 02:30 UTC 9 Oct backup run:**
```bash
   docker-compose logs backup --tail 100
```
   Confirm: dump encrypted, uploaded to Backblaze, file size correct, no errors

5. **Follow-up items:** Browser push re-subscription, royalcyber.com cleanup (after batch deploys successfully)

---

## Environment Variables

Values live only in `/opt/traceit/.env` on the server. They are **never** recorded in this repo.

**Existing in .env:** `B2_BUCKET`, `B2_KEY_ID`, `B2_APPLICATION_KEY`, `B2_ENDPOINT`, `BACKUP_PASSPHRASE`

**To add (map from the B2_* values):**

| New variable | Takes its value from |
|---|---|
| `BACKUP_S3_BUCKET` | `B2_BUCKET` (bucket: traceit-pg-backups) |
| `BACKUP_S3_KEY_ID` | `B2_KEY_ID` |
| `BACKUP_S3_SECRET_KEY` | `B2_APPLICATION_KEY` |
| `BACKUP_S3_ENDPOINT` | `B2_ENDPOINT` (s3.us-east-005.backblazeb2.com) |
| `BACKUP_S3_REGION` | `us-east-005` |

> Security note (2026-10-08): the B2 key and backup passphrase were pasted into a chat. Rotate them and update `.env`.

---

## Contact & Escalation

**Owner:** Sankar (sankarchowdary.tottempudi@gmail.com)  
**Alert emails:** 6 recipients (see "Email Alert Batching" decision)  
**Teams:** Aroya Monitoring channel  
**Credentials:** Stored in environment only; no hardcoded keys in repo

---

## Session Summary

**Session date:** 2026-10-08  
**Work completed:** Email batching (deployed), Analytics Phase 1-2 (deployed), Canary fix (deployed), Mobile responsive (deployed), Backup script created, Nightly backup config passed gate f1adf61ec  
**Work batched for IDE:** Five coordinated changes (docker-compose fix, Analytics cleanup, integrations, daily monitoring)  
**Blockers:** docker-compose.yml YAML syntax errors (pivoted to IDE); awaiting IDE completion  
**Critical monitoring:** 02:30 UTC 9 Oct nightly backup run verification

---
