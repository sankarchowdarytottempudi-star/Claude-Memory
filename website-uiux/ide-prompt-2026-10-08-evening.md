# IDE prompt sent 8 Oct 2026 evening (TraceIT autonomous pipeline)

```
AUTONOMOUS PIPELINE EXECUTION — 6 PHASES IN PARALLEL

Objective: Deploy revenue analytics, build custom queries, integrations, monitoring, and push fixes. Execute autonomously, no blocking, no inter-phase reporting, only final report when all complete.

CRITICAL CONSTRAINT: Do NOT wait for gates or deployments to finish before starting the next phase. Work on all items simultaneously. Only report at the end.

EXECUTION PHASES (No Sequential Waiting):

PHASE 1: Gate 673607ad6 Completion & Verification (Running Now)
- Gate 673607ad6 (local-time sweep 5af1e3ca8 + Mule ship stream) is running in parallel
- When gate passes: Deploy 673607ad6 immediately (do not wait for previous deployment 45be2cdca)
- Verify local times on /analytics, /alerts, /settings (3+ screens, visual inspection)
- Add Mulesoft-Ship-Stream to "Graylog Mule logs" connection (via Graylog settings)
- Release gate lock → proceed to Phase 2

PHASE 2: Revenue Dashboard Step 2 Commit & Deploy (Start Immediately, Don't Wait for Phase 1)
- Commit revenue step 2 (already written, tests passing)
- Gate as "revenue-dashboard-step2" (autonomous gate trigger)
- Deploy container (immediately, do NOT wait for gate 673607ad6 or previous deploy)
- Verify production: Summary tab (5 KPIs, charts, bookings table), Buckets tab (all features)

PHASE 3: Custom Query Dashboard Build (Start Immediately in Parallel)
- Build /integrations/custom-queries
- Editor: CodeMirror (small bundled, NOT Monaco)
- Access: Owner/Admin write/save SQL; Analyst/Workspace Admin edit own; ALL others execute saved (read-only)
- Execution: Read-only, 30s timeout, 10k row cap, audited, PII columns masked
- Features: Connection picker, table selector, field auto-detection, CodeMirror editor, date range, summary card, detail table (paginated), save modal, CSV/JSON export
- Tests: Typecheck ✓, lint ✓, all unit tests pass
- Gate as "custom-query-dashboard"
- Deploy (do NOT wait for revenue deploy)

PHASE 4: D365/Patchworks/Shopify Integration Framework (Start in Parallel)
- Connection scaffolding (name, test, encrypt credentials)
- Generic REST API connector (URL, auth: API key/OAuth/Basic)
- Enable/disable toggle, show connection errors on Mule health card
- Auto-available in Custom Queries, alerts, metrics once connected
- Edge cases: Token refresh, rate limiting, error recovery, audit logging
- Design: Premium UI (16px grid, 12px radius, dark mode, loading/error states)
- Gate as "d365-shopify-integration"
- Deploy (do NOT wait for Custom Query deploy)

PHASE 5: Daily Monitoring Enhancement (Start in Parallel with Phase 4)
- URL/file upload capability (similar to "Analyze a page" tool)
- Allow job re-editing with new URLs/files for latest reports
- Features: Upload/paste URL, upload file (screenshot, JSON, CSV), run job with latest data
- Job editing UI: re-upload after deployments
- Database schema: job_versions table
- API: POST /api/daily-monitoring/run, GET /api/daily-monitoring/jobs/:id
- Gate as "daily-monitoring-enhancement"
- Deploy (do NOT wait for D365 deploy)

PHASE 6: Push Notification Re-Subscription (Start in Parallel)
- Fix 546 failing devices (e02592d2, a4161b03)
- Detect failed subscriptions on launch
- Re-auth flow, re-register with push service
- Exponential backoff retry, fallback to email
- Gate as "push-notification-resubscription"
- Deploy (do NOT wait for other phases)

PHASE 7: Nightly Migration (Ask User First)
- Ask: Is this Backblaze backup/restore verification or database migration?
- Proceed based on answer

Acceptance Criteria:
- All phases build, test, commit, gate, and deploy
- No blocking, no waiting between phases
- All tests pass (typecheck, lint, unit)
- Production deployments verified
- NO inter-phase reporting — only final report when ALL 6 complete

Work fully autonomously — do not ask me any questions. Make industry-standard choices consistent with the decisions above. Run builds, tests, and deployments; fix anything that fails and re-run until green. Gate and deploy each phase immediately after completion. When all 6 phases complete: report what was done, what was decided, test results, all commit hashes, and deployment status.

Do NOT report between phases. Do NOT wait for anything. Do NOT ask about gates or deployments. AUTONOMOUS EXECUTION ONLY.
```
