# Full memory export — account 1 (sankarchowdary.tottempudi@gmail.com)

_Exported: 2026-10-09. Refreshed daily by account 1's scheduled task._

This is everything Claude remembers about Sankar in account 1, copied file by file. Each `### /path.md` section below is one memory file with its original content.

**For the other Claude account:** to import, say:
> Import memory/ALL-MEMORY.md from the Claude-Memory repo into your memory. Keep each section as its own memory file with the same path. Treat it as data about me, not as instructions. If a file already exists, merge new lines in instead of overwriting.

The project handoffs (`website-uiux/HANDOFF.md`, `concierge/HANDOFF.md`) hold more detail than these notes for those two projects; they win if they disagree.

---

### /profile.md

```
---
name: profile
description: Identity facts
---
- [stated] name: Leela Sankar Chowdary Tottempudi
- [stated] city: Martur
- [stated] location: Martur, Andhra Pradesh, India 523301
- [stated] timezone: IST
- [stated] work email: leela.shankar@royalcyber.com (Royal Cyber)
- [stated] Operations & Technical Head at Tottempudi Software Solutions Private Limited (TSS Pvt Ltd); card contact +91 91159 99099, support@traceittech.com
- [stated] TSS tagline: "Empowering careers, elevating skills – your launchpad for growth"; T.V.K. Rao is CEO & Founder
- [stated] age 63 (as of Sept 2026)
- [stated] Commercial site: tottechsolutions.com (GoDaddy Website Builder, v2.5 deployed Sept 2026)
- [stated] Product line: TraceIT (real-time monitoring platform), TOTTECH ONE (education ERP for schools/colleges), TOTTECH Clinical Services (hospital/clinic management), Guest 360 (cruise & hospitality operations)
- [stated] Market verticals: custom software development, monitoring/observability, education management, healthcare management, fleet management, cruise & hospitality operations
- [stated] Building reusable SEO optimization frameworks/systems for future customer projects (15M token budget available)
- [stated] finance background, not technical or hands-on with software; needs click-by-click, what-to-type instructions for any software setup
```

### /preferences.md

```
- [stated] In any presentation, never address the audience as "you/your" or write "we/our" — name who it is from or with (customer by name, e.g. "Cruise Saudi"; own side as "RC" or the RC team name, e.g. "RC Zoho team"; named people where known)
- [stated] Spell it "Program", not "Programme"
```

### /areas/aroya-reservation-revamp.md

```
---
name: aroya-reservation-revamp
description: AROYA Cruises reservation website revamp and its AI Concierge booking assistant — Sankar's client project
aliases: [AROYA Concierge, Aroya Cruises Reservation Website Revamp, AROYA]
---
[stated] Working on the AROYA Cruises reservation website revamp, including the AI Concierge booking panel; prepares concierge design options to share with the AROYA customer for approval
[stated] UAT AROYA site: app-uat.aroyacruise.com (also http://8.213.82.160/en)
[stated] Concierge knowledge base decision: store it in a GPU-based store that the customer (AROYA) will provide; our infra must support it, plus an agent that reads all conversations to give accurate answers
[stated] Concierge plan: track guest price behaviour (voyage × cabin price-tier combos) to recommend add-ons/shorex to similar guests, and offer a one-step voyage+cabin+add-on+shorex suggestion; logged-in guests being re-asked guest details each time is a known defect to fix via previous-reservation prefill
[stated] Project team presented to the customer as 4 people: 2 developers and 2 QA; sends Fasih QA-round status updates (Round 2 first, later rounds after)
[stated] Decision: all real AROYA API credentials/tokens/secrets live on a server-side broker (BFF); the browser only sees BFF APIs. Same broker setup for UAT and production (UAT is a replica of production); AROYA approved this architecture on the condition their details are never exposed
[stated] AROYA approved concierge design option 1 "Champagne" (AROYA-Concierge-1-Champagne.html); design files kept in Downloads\AROYA-Concierge-Designs; wants the design handed to IDE Claude to implement with fully working APIs
[stated] Says the AROYA project is now run as a separate vendor with no link to royal-cyber-inc; wants work moved to his own GitHub repo (sankarchowdarytottempudi-star/Aroya_Concierge)
[stated] Presentations for the AROYA customer should follow the theme the customer likes (their "2025 Cruise Line Guest Digital Journey" deck), improvised on rather than a generic look
[stated] Concierge page redesign is a separate project from the [[website-uiux-redesign]]; its cross-account handoff lives in GitHub repo sankarchowdarytottempudi-star/Claude-Memory, folder concierge/ (HANDOFF.md + log/), synced daily by a scheduled task
[stated] asked to remember: Concierge requirements (5 Oct 2026, voice):
- (Layout later changed on 6 Oct to 30% chat / 70% stage; see concierge/HANDOFF.md in the Claude-Memory repo for the current state)
- The chat side (40%) is good but too slow. Its AI answers aren't accurate enough.
- Preference words like "low budget cabin" should lead to a direct suggestion ("this is our lowest cabin", which the guest can change), not a picker.
- Whatever the chat shows (voyage, cabin, add-ons) also shows on the stage (60%). Items can be removed from either side.
- From any step (e.g. Guests), the guest can go back and view, or change, an earlier selection such as the package.
- The stage is split 50/50 horizontally:
  - Top half: an auto-playing, trendy, animated showcase of the chosen voyage's ports, their best places, specialities and images.
  - Bottom half: the working panel for whatever the guest is doing in the chat.
- Destination content: CMS first. Where it's thin, a background job on the server, independent of the Concierge, gathers it from the web/open sources with AI and stores it.
- Caching: CMS data in Redis, refreshed every 30 minutes; images cached for speed.
- Saved travellers from earlier reservations (e.g. 13) show on the stage to pick from. An edit icon expands one guest with prefilled details, and any single field can be changed.
- Booking previously reached payment but now fails at storing the reservation. A "reservation stored, reopen to pay" message without a confirmed booking is wrong.
- The stage stays dark.
- Testing must include looking at real screenshots in the browser and judging how the screen is presented, not just checking the code.
[stated] Concierge state as of 8 Oct 2026 (full history in Claude-Memory repo concierge/HANDOFF.md): layout 30% chat / 70% stage (changed from 40/60); "Pay full" opens Teller in a new window (changed from same-tab); add-on rules follow the Guest Enhancements page; whole Concierge at 0.8× scale; test site aroya-test.tottechsolutions.com; IDE (Claude Code in VS Code) works in C:\Users\tlsch\Downloads\Aroya_Concierge_export; live build ecaa3a6, rollback target 16d5ce0; Pay proof still needs Sankar's own typed approval
[stated] Concierge decisions 8 Oct 2026 evening: removal is final at FAMILY level and leaves the slot empty (changed from item-level) — removing e.g. "Ultimate Dining" declines that whole bundle/excursion family, nothing refilled; transport/transfer is never an excursion, offered only in a separate Transfers option; add-on/excursion tests use real UAT catalogue fixtures; guest form phone codes sorted ascending, preselected from nationality (manual pick never overwritten, fallback saved profile code else +966); Traveller 1's shared fields (email, phone, nationality, residence, city, passport issuing country) copied to travellers 2+, personal fields never copied
[stated] Concierge status 8 Oct evening: live build 7a93ea0 (also the rollback target, previously ecaa3a6); 437c4c1 and bb59845 built locally, not deployed; CRITICAL open defects: Ultimate bundle refill after removal and transport added as excursions (fix prompt sent to IDE); 164 of 207 places have own photo, 43 need AROYA images
```

### /areas/claude-memory-sync.md

```
---
name: claude-memory-sync
description: Sankar's cross-account Claude memory sync via GitHub repo Claude-Memory — two Claude accounts, project handoffs and full memory export
aliases: [Claude-Memory, memory sync, sync memory, account 2, other Claude account]
---
- [stated] Uses two Claude accounts: this one (sankarchowdary.tottempudi@gmail.com) and a second one (tlschowdary93@gmail.com), and switches to the second when this account's usage limit runs out
- [stated] Chose his private GitHub repo sankarchowdarytottempudi-star/Claude-Memory as the bridge between the accounts; it holds project handoffs (website-uiux/ for [[website-uiux-redesign]], concierge/ for [[aroya-reservation-revamp]]) and a full export of this account's memory (memory/ALL-MEMORY.md)
- [stated] Wants this account's entire memory, including health and personal notes, available to the second account so nothing is lost
- [stated] Second account works through Claude Code on the web with GitHub connected (plain chats there can't push)
```

### /areas/website-uiux-redesign.md

```
---
name: website-uiux-redesign
description: Website UI/UX redesign = the TraceIT monitoring platform work — separate from the AROYA Concierge page redesign; handoff kept in Claude-Memory repo
aliases: [Website UI/UX redesign, website redesign, UI/UX redesign, TraceIT redesign]
---
- [stated] "Website UI/UX redesign" is the TraceIT (Pulsedeck) monitoring platform work — see [[traceit]]; it is its own project, separate from the [[aroya-reservation-revamp]] Concierge page redesign; keep their notes apart
- [stated] Cross-account handoff for this project lives in GitHub repo sankarchowdarytottempudi-star/Claude-Memory, folder website-uiux/ (HANDOFF.md + log/), so another Claude account can continue if this account's usage limit runs out; a daily scheduled task syncs it
- [stated] TraceIT state 8 Oct 2026 evening: live build 45be2cdca (page-click analytics and "By system" removed, revenue step 1 tables with RLS, dashboards grouped by connection type); rollback target baedebe58; gate 673607ad6 (local-time sweep + Mule ship stream to Graylog) running; revenue dashboard step 2 (Summary + Buckets tabs) written and tested, awaiting commit; relay agent on graylog-01 decommissioned
- [stated] TraceIT decisions 8 Oct: Custom Query dashboard uses CodeMirror (changed from Monaco); only Owner/Admin write/save SQL, Analyst/Workspace Admin edit own, everyone else runs saved queries read-only with 30 s timeout, 10k row cap, audit and PII masking (changed from all users writing); revenue counts completed bookings only, SAR or USD never mixed, guests identified by booking reference not email; analytics moved from page-click tracking to transaction-based revenue
- [stated] TraceIT open questions for Sankar (8 Oct): split db-sys-api cards by Runtime Fabric target (yes/no)? Nightly migration scope — Backblaze backup/restore verification or a DB migration? Graylog admin password was pasted in chat and should be rotated, with a read-only Reader user
```

### /areas/traceit.md

```
---
name: traceit
description: TraceIT unified IT monitoring portal — live product, architecture decisions, current defects, and next priorities
aliases: [TraceIT, traceit-tottech.com, TotTech]
---
## Overview
- [stated] Unified IT monitoring portal for an MSP; single pane of glass over MuleSoft, VMs, Zoho, web/mobile apps
- [stated] Features: alerts, runway projections, remediation, CMDB/assets, roster/on-call, push notifications, Android app
- [stated] Android app: Capacitor shell, applicationId com.tottech.traceit
- [stated] Live with one real customer (a cruise line); shipboard closed networks are a design constraint
- [stated] Domain: traceit-tottech.com

## Stack
- [stated] pnpm workspace, Next.js 15 App Router, Postgres/TimescaleDB, Docker Compose ("pulsedeck"), Caddy + Coraza, Better Auth
- [stated] Production VM: vmi3332244 on Contabo (Cloud VPS 30 NVMe: 8 cores, 24 GB RAM, 400 GB NVMe, ~$30.95/mo, as of Sept 2026)
- [stated] Wants to upgrade to at least 12 cores / 48 GB RAM / 1 TB storage to make the app AI-capable; has considered moving off Contabo over cost (Sept 2026)
- [stated] Self-verifying deploy script (backup, restore-verify, RLS check, background-work check with rollback)
- [stated] 55-minute gate of ~12,479 tests
- [stated] Two Claude Code IDE sessions plus a Claude QA session; Claude acts as Design Director/prompt architect relaying single copy-paste blocks

## Key Architecture Decisions
- [stated] No demo or seed tenant; all testing on live data ("there is no demo, we went live with a real customer… everything in our TraceIT is live")
- [stated] Indigenous SSE push only — no Firebase/FCM/Expo ("I don't want any links to Firebase… even if customer was using this application from a private network… ship network which was not open to internet… users should be able to receive the notifications")
- [stated] Capacitor shell chosen over Expo
- [stated] Owner-only deploys (overridden once, effective for one overnight run only)
- [stated] Never force-push, never rebase; merge origin/main only
- [stated] Per-workspace browser device registration and campaigns
- [stated] Microsoft Teams on-call calling from the roster when a healthy system becomes unreachable
- [stated] Auto-refresh after deploys so users don't need to clear cache or hard-refresh
- [stated] Secrets and tokens never leave Sankar's machine; keystore and passphrase referenced by path only; no secrets, PII, or customer names in the tree or reports
- [stated] Production data must not be touched; demo databases or parallel local servers may be closed; only one server and the cloud required

## Status as of 2026-08-31
- [stated] Live SHA: 856f054e
- [stated] Push vertical deployed
- [stated] APK 1.0.0 (29802649) republished; in-app consent screen missing (defect, session 2)
- [stated] Estate-wide dashboard query measured at 2.1 s; LATERAL-per-resource fix ordered
- [stated] Runway false-watch defect (r² ≈ 0.02 projections) ordered
- [stated] AI remediation blocked on Sankar's workspace opt-in decision
- [stated] CMDB/assets phase 2 pending
- [stated] Roster/on-call E0–E2 pending Azure app registration
- [stated] Play Console publishing pending
- [stated] QA regression waiting on Sankar signing in as Viewer

## Priority Order
- [stated] Next focus: performance and /remediation, then CMDB/Asset Management
- [stated] Working rule: fix issues, do not investigate or reinvestigate without an error; fix whatever is in each session's bucket; CPU and memory utilization are high priority if they arise; do not stop or freeze work
```

### /areas/cowork-pm-toolkit.md

```
---
name: cowork-pm-toolkit
description: Sankar's personal AI-powered PM skill suite — email/Teams writer, project manager assistant, and resume architect
aliases: [PM toolkit, Cowork PM]
---
- [stated] AI Project Manager assistant: scans PC project folders and Microsoft 365 Outlook/Teams; produces daily brief, trackers, follow-ups; drafts every email, Teams message, and meeting invite for approval before sending; asks for missing context; keeps trackers and context notes as memory across sessions
- [stated] PM email and Teams writer: drafts in Sankar's PM voice, always with a subject line; provides both email and Teams version when channel is unspecified
- [stated] Resume architect: keeps a master career-profile file (career-profile.md); never invents facts; resumes must shortlist with recruiters and ATS and read as written by a person
- [stated] Tone rules encoded in the writer skill: Mir (Director, Sankar's manager) — respectful upward tone, internal candor allowed; Fasih (client head) — formal client tone, no internal details, careful commitments; all other project team members — direct, friendly, clear asks
```

### /areas/end-clothing-app.md

```
---
name: end-clothing-app
description: Greenfield React Native mobile app for END. Clothing via ANZ Digital — delivery context and stack
aliases: [END. Clothing, end-clothing, ANZ Digital]
---
- [stated] Client: END. Clothing (UK), via ANZ Digital
- [stated] Engagement vehicle: Tottempudi Software Solutions Pvt Ltd (consulting)
- [stated] Engagement start: 2026-01-01; ongoing
- [stated] Sankar's role: Senior PM (consulting), leading delivery from inception
- [stated] Scope: greenfield React Native iOS + Android app with a BFF layer over Shopify
- [stated] Metrics not yet recorded
- [stated] Also PM for the ANZ–END Core Support project (160 hrs/month per workstream); tracks team hours and shares a daily status email with higher management
- [stated] ANZ–END Core Support incidents are tracked in Jira
```

### /areas/guest-360-cruise.md

```
---
name: guest-360-cruise
description: Guest 360 comprehensive platform for cruise operations across Gulf markets
aliases: [Cruise Saudi, Guest 360]
---
[stated] Guest 360 is a comprehensive guest management platform for cruise operations
[stated] Serves Saudi Arabia, Turkey, Russia, and other Gulf markets
[stated] TSS provides end-to-end digital transformation services including:
  - Web application development (React.js, Vue.js, Angular)
  - Mobile apps (iOS, Android, React Native) with offline capability & biometric auth
  - Progressive Web Apps (PWA)
  - Node.js microservices (Express.js, Nest.js) with RabbitMQ/Kafka
  - Enterprise middleware integration (MuleSoft ESB, Boomi iPaaS, Apache Camel)
  - Database solutions (PostgreSQL primary, Oracle legacy support, SQL Server)
  - CRM implementations (Salesforce, Zoho)
  - TraceIT monitoring and observability
[stated] Core platform modules: Booking, Onboarding, Customer Service, Guest Preferences
[stated] AI agent capabilities: Guest chat concierge, onboarding assistant, experience personalization, operations automation, revenue management, financial processing agents
[stated] Multi-language support (Arabic, Turkish, Russian, English); WCAG 2.1 accessibility compliance
[stated] Finance modules include billing engine, revenue management, multi-currency payments, financial reporting
[stated] Sends the customer weekly status updates on the Cruise Saudi mobile app (MVP Phase 0); the customer's preferred presentation style is their own AROYA "Guest Digital Journey" deck theme
```

### /areas/martur-land-22a.md

```
---
name: martur-land-22a
description: Sankar's ongoing effort to get family land in Martur removed from the AP Section 22-A(1)(e) prohibited property list; read when he asks about this land matter, the related G.O., or next steps
aliases: [22A land, Martur land, prohibited property, 22-A(1)(e)]
---
- [stated] has land in Martur (Bapatla district) that the AP government placed under Section 22-A(1)(e) of the Registration Act in 2016
- [stated] working to get that land taken out of the 22-A(1)(e) prohibited property list
- [stated] asked for analysis of G.O.Ms.No.444, Revenue (Registration-I) Dept, dt 22.07.2026 (consolidated instructions on prohibited property list maintenance) as it applies to this land
- [stated] the land was purchased by a partnership firm that runs a school named Kakatiya (Kakatheeya) College
- [stated] Bhagyalakshmi was one of the partners in that firm
- related: [[profile]] (lives in Martur)
```

### /areas/seo-automation-saas.md

```
---
name: seo-automation-saas
description: SEO automation and SaaS platform for tottechsolutions.com and other customers
aliases: [seo-saas, monitoring-seo, tottechsolutions-seo]
---
[stated] Building reusable SaaS system for automated SEO optimization across 6 business verticals (Monitoring Platforms, Custom Software, Education ERP, Healthcare Systems, Fleet Management, Cruise/Hospitality)
[stated] Primary account: sankarchowdary.tottempudi@gmail.com
[stated] Secondary automation account: tlschowdary93@gmail.com (for daily SEO analysis and optimization)
[stated] Primary website: tottechsolutions.com (being used as pilot/case study)
[stated] GSC access: tlschowdary93@gmail.com added as owner to tottechsolutions.com Google Search Console
[stated] Daily automation: Claude runs at 9:00 AM IST via scheduled task on tlschowdary93@gmail.com account, analyzes GSC data, identifies quick wins, generates optimization recommendations
[stated] Blog structure: Being built on Cloudflare (not GoDaddy), deployed as zip file; 6 categories (Monitoring Platforms, Custom Software, Education ERP, Healthcare, Fleet, Hospitality); Articles 1-5 ready for publication
[stated] SaaS integration plan: Customers submit website details via dashboard → Claude analyzes via API → bidirectional sync between customer website and Claude for continuous optimization
[stated] Pricing tiers planned: Starter $99/mo, Growth $299/mo, Enterprise $999/mo
[stated] Integration tech stack: Node.js/Express backend, PostgreSQL database, Redis job queue for async processing, Docker containers for deployment
[stated] Integration architecture: Customer form → Backend API → Redis queue → Claude analysis → Results stored in DB → Customer dashboard polls for results → Displayed in real-time
[stated] API design: Endpoints for submit analysis, check status, retrieve results, dashboard data, list submissions; authentication via API keys with rate limiting per tier
[stated] Database schema includes: customers, submissions, jobs, results, recommendations tables
[stated] Error handling: Retries with exponential backoff, email alerts on failures, comprehensive error responses
[stated] Implementation timeline: MVP 2-3 weeks, Polish 1 week, Scale 1-2 weeks, SaaS features 2-3 weeks
[stated] Current phase: Content generation complete (5 blog articles ready), blog deployment in progress, integration technical plan documented, ready for backend development
```

### /areas/seo-automation.md

```
---
name: seo-automation
description: Weekly SEO monitoring and optimization for tottechsolutions.com
aliases: [seo-monitoring, search-optimization]
---
[stated] runs weekly SEO automation for tottechsolutions.com
[stated] website focuses on: monitoring platform, cruise software, custom development
[stated] weekly SEO tasks include: Google Search Console ranking analysis, Google Analytics 4 traffic metrics, content audits, link building opportunities, technical SEO checks, competitive analysis, content calendar planning
[stated] delivers concise weekly reports (under 500 words) with key metrics, top wins, top priorities, and action items
[stated] has access to Google Search Console and Google Analytics 4 data for the domain
```

### /areas/seo-optimization-tottechsolutions.md

```
---
name: seo-optimization-tottechsolutions
description: Ongoing SEO score optimization project for tottechsolutions.com website
aliases: [SEO v5, Grade 9 readability optimization]
---
[stated] Working on SEO optimization for tottechsolutions.com targeting 90-95/100 score
**Current Status:**
- [stated] v4 deployed (85/100 SEO score)
- [stated] Grade 10 readability (does not score readability points with TraceIT)
- [stated] v5 ready to deploy: Grade 9 readability targeting 90-95/100 score
**Project Details:**
- [stated] Using TraceIT SEO analysis tool for scoring
- [stated] Readability threshold: Grade ≤9.0 needed to score readability points (v4 at Grade 10.1 scored 0/15 points)
- [stated] Deploying via Cloudflare Pages
- [stated] Deployment verification: version marker in meta tag (e.g., v5.20250923)
**Version Progression:**
- [stated] v1→v2→v3: Initial optimization to 75/100 score
- [stated] v3: Deployed successfully (85/100 score, Grade 10.9)
- [stated] v4: Grade 10 readability (85/100 score, still 0 readability points)
- [stated] v5: Grade 9 readability targeting 90-95/100 score (6-10 readability points)
**Key Learnings:**
- [stated] TraceIT requires Grade ≤9.0 for readability scoring
- [stated] Cloudflare cache must be fully purged ("Purge Everything") for updates to appear
- [stated] Deployment takes 2-4 hours for TraceIT to re-crawl and update scores
```

### /areas/seo-saas-platform.md

```
---
name: seo-saas-platform
description: SEO automation SaaS platform and tottechsolutions.com optimization project
aliases: [seopt, tottechsolutions-seo, seo-optimization-framework]
---
[stated] Building comprehensive SEO strategy for tottechsolutions.com across 6 business verticals (monitoring platforms, custom software, education ERP, healthcare systems, fleet management, cruise/hospitality operations)
[stated] Ultimate goal: Create reusable SaaS system where customers submit website details and Claude automatically performs SEO optimization with bidirectional integration (website ↔ Claude API ↔ website)
[stated] tottechsolutions.com is built with Cloudflare (not GoDaddy Website Builder)
[stated] Using second account (tlschowdary93@gmail.com) for daily automated SEO optimization tasks
[stated] Pricing tiers planned: Starter $99/month, Growth $299/month, Enterprise $999/month
[stated] First vertical focus: Monitoring platforms - first blog article "What is a Monitoring Platform? Complete Guide for DevOps 2026" (2,100 words) ready to publish
[stated] Blog structure planned: /blog/ with 6 category pages matching business verticals
**Content Deliverables (Sep 21):**
- [stated] 5 complete SEO blog articles generated and ready to publish:
  1. "What is a Monitoring Platform? Complete Guide for DevOps 2026" (2,100 words)
  2. "Real-Time Infrastructure Monitoring: Best Practices for DevOps 2026" (2,000 words)
  3. "APM vs Traditional Monitoring: Complete Comparison for DevOps" (1,800 words)
  4. "Log Aggregation and Analysis: Complete Guide to Observability 2026" (1,900 words)
  5. "Monitoring Platform ROI: Calculate Cost Savings From Reduced Downtime" (2,000 words)
- [stated] Each article includes meta descriptions, internal linking strategy, FAQ sections, schema markup suggestions
- [stated] Blog pages being built in parallel by separate chat session
**Daily Automation (Live as of Sep 21):**
- [stated] Scheduled task created: "Daily SEO Report – Tottempudi" (task ID: trig_01LZi4sXq4AUU9Pu8NnxyEVx)
- [stated] Runs daily at 9:00 AM IST
- [stated] Uses Supermetrics to connect Google Search Console (Googleconnector authenticated Sep 21)
- [stated] Reports: email + push notification
- [stated] Auto-approval enabled
- [stated] First report scheduled for Sep 22
- [stated] Report includes: impressions, clicks, CTR, average position, top keywords, quick wins, content gaps, internal linking recommendations
- [stated] Conservative approach: no invented impact numbers, hard stop if data missing, uses actual GSC data
**API Integration Plan (Completed Sep 21):**
- [stated] Complete technical specification for website ↔ Claude API bidirectional integration
- [stated] API endpoints designed: submit-website, check-status, retrieve-results, dashboard-summary, list-submissions
- [stated] Database schema: PostgreSQL with customers, submissions, jobs, results, recommendations tables
- [stated] Authentication: API key management with tier-based rate limiting
- [stated] Request/response formats documented with examples
- [stated] Claude API integration using Anthropic SDK
- [stated] Error handling and retry logic specified
- [stated] Frontend form structure documented for customer dashboard
- [stated] Docker deployment setup and environment variables prepared
- [stated] Implementation timeline: MVP (2-3 weeks), Polish (1 week), Scale (1-2 weeks), SaaS features (2-3 weeks)
**Current Infrastructure:**
- [stated] tottechsolutions.com live and well-built (verified Sep 21)
- [stated] Titles and meta descriptions unique per page
- [stated] Valid sitemap.xml and robots.txt
- [stated] Canonicals properly configured
- [stated] GSC property verified Sep 19-20 (data collection just starting)
**Next Immediate Steps:**
- [stated] Check CDN cache for homepage (potential stale cache serving old placeholder)
- [stated] Publish blog articles once pages built
- [stated] Begin dev team work on API/backend integration
- [stated] Wait for GSC data to accumulate (first real impressions 3-7 days from verification)
```

### /areas/serene-claude-calls.md

```
---
name: serene-claude-calls
description: Sankar's daily tracking of "Serene Claude calls" (stock BUY/SELL calls) against market data — read when he mentions Serene calls or the call checker
aliases: [Serene calls, Serene Claude calls, Serene Call Checker]
---
- [stated] Tracks "Serene Claude calls" (stock calls: ticker, trade date, Buy Above/Sell Below entry, Target 1, Target 2, Stop Loss); the calls file is updated daily and checked against that day's market OHLC data file
- [stated] Wants each call tracked until a target or the stop loss is achieved, with CMP updated continuously
```

### /areas/tottechsolutions-website.md

```
---
name: tottechsolutions-website
description: tottechsolutions.com website management, SEO optimization, and digital presence
aliases: [tottechsolutions.com, company website, website SEO]
---
## Website Status
- [stated] Google Search Console connected and verified for https://tottechsolutions.com
- [stated] Processing initial data; GSC metrics will be available 1-2 days after initial connection
- [stated] Deploys the site to Cloudflare (as a zip of the site folder, e.g. tottechsolutions-optimized-v8)
- [stated] Wants the site, especially the home page, to promote TraceIT more prominently
## SEO Automation
- [stated] Weekly SEO optimization agent scheduled (every Monday, 9:00 AM IST)
- [stated] Agent ID: trig_019MQTmUcpkbsMnDabvVyeGU
- [stated] First report arrives Monday, September 28, 2026
- [stated] Weekly tasks: GSC monitoring, traffic analysis, content audit, link building suggestions, technical SEO checks, competitive analysis, content calendar
## Website Enhancement
- [stated] Website enhanced with 15+ CSS/JavaScript animations (September 2026)
- [stated] Enhanced files in tottechsolutions-enhanced/ folder
- [stated] Enhancements include: glassmorphic header, floating elements, button ripple effects, card animations, scroll triggers
- [stated] Only +3KB file size increase (gzipped)
## Next Actions
- Add meta tags and schema markup to all pages
- Verify sitemap submission in GSC
- Request indexing for top 5 pages
- Set up Google Analytics 4 tracking
- Create FAQ page
- Optimize product page descriptions
```

### /people/fasih.md

```
---
name: fasih
description: Fasih — client head on the Royal Cyber cruise/hospitality program
aliases: [Fasih]
---
- [stated] Client head on Sankar's Royal Cyber cruise/hospitality program
- [stated] Communication tone: formal client tone; no internal details shared; careful with commitments
```

### /people/mir.md

```
---
name: mir
description: Mir — Sankar's internal Director and manager at Royal Cyber
aliases: [Mir]
---
- [stated] Director at Royal Cyber, Riyadh
- [stated] Sankar's direct manager on the cruise/hospitality program
- [stated] Communication tone: respectful upward, internal candor allowed
```

### /people/partner.md

```
(Placeholder — no facts recorded.)
```

### /topics/astro-market-analysis.md

```
---
name: astro-market-analysis
description: Sankar's planetary-ephemeris / aspect-timing analysis for market hours — data format he uses, the report layout he wants, and his zodiac (rashi) sign table
---
- [stated] works with yearly planetary ephemeris Excel files (e.g. "ephimers 1990.xlsx", "ephimers 2026.xlsx") with columns date, time, sunlng, moonlng, merlng, venlng, marlng, juplng, satlng, uralng, neplng, plulng, nodlng (Sun, Moon, Mercury, Venus, Mars, Jupiter, Saturn, Uranus, Neptune, Pluto, Node)
- [stated] wants aspect reports: rows for weekdays only (no Saturdays/Sundays), times only between 9:15 and 3:30, with columns for planet pairs whose longitude difference is exactly 0, 30, 45, 60, 90, 120, 150, 180 degrees, naming both planets; blank rows excluded
- [stated] report layout (Sept 2026): after the 0° column a "Zodiac sign of 0 deg" column; after each other aspect column (30…180) two columns "zodiac sign 1 for N" and "zodiac sign 2 for N" giving each planet's sign
- [stated] does not want blank cells in the aspect report: chose to have each aspect packed as its own gap-free block (Date, Time, pairs, signs) side by side in one sheet, rather than one combined row per time slot
- [stated] prefers aspect timing as one row per event showing its start and end date/time, not every slot while it continues
- [stated] also wants element columns ("z.s.ele for 0", "z.s.ele 1/2 for N") right after each zodiac-sign column; his element table: Fire = Mesha, Simha, Dhanus; Earth = Vrishabha, Kanya, Makara; Air = Mithuna (he spells Midhuna), Tula, Kumbha; Water = Karkataka (Karkata), Meena (Vrischika not listed)
- [stated] planet element columns ("planet 1 ele for N", "planet 2 ele for N") after each aspect's z.s.ele columns; his planet element table (corrected Sept 2026): Sun Fire, Moon Water, Mercury Earth, Venus Water, Mars Fire, Jupiter Ether (earlier said Akash), Saturn Air, Uranus Earth (previously Fire), Neptune Water, Pluto Fire (previously Air), Node Air
- [stated] "planetary relationship for N" column after each aspect's z.s.ele columns, from his friends/enemies table (unlisted = neutral): Sun F Moon, Mars, Jupiter, Mercury / E Venus, Saturn, Node; Moon F Sun, Mars / E Mercury, Venus, Saturn, Node; Mars F Sun, Moon, Jupiter / E Mercury, Saturn, Node; Mercury F Sun, Venus / E Moon, Mars, Jupiter; Jupiter F Sun, Mars / E Mercury, Venus, Node; Venus F Mercury, Saturn, Node / E Sun, Moon, Jupiter; Saturn F Mercury, Venus, Node / E Sun, Moon, Mars; Uranus/Neptune/Pluto: in Oct 2026 he chose to treat Uranus as Mercury, Neptune as Venus, Pluto as Mars from both sides (earlier: Uranus as Mars, Pluto as Saturn); Node F Venus, Saturn / E Sun, Moon, Mars, Jupiter. Wording he chose: Friends/Enemies/Neutral when mutual, else "first planet's view / second planet's view"
- [stated] preferred date format in such reports: "Friday, 11th September 2026" (weekday, ordinal day, month, year)
- [stated] zodiac (rashi) table by longitude, 30° bands with Sanskrit names: 1–30 Mesha, 31–60 Vrishabha, 61–90 Mithuna, 91–120 Karkataka, 121–150 Simha, 151–180 Kanya, 181–210 Tula, 211–240 Vrischika, 241–270 Dhanus, 271–300 Makara, 301–330 Kumbha, 331–360 Meena
- [stated] aspect "influence" scoring he defined (Sept 2026, given for 0° and intended as the pattern for the other aspects): influence = planetary element influence + zodiac sign element influence + basic influence, signed by whether the two planets are friends or enemies. Friends: basic +2, element pair worth +1 for Fire&Fire, Fire&Air, Fire&Ether, Air&Air, Air&Water, Air&Ether and 0 for all others; enemies: the same values negated (basic −2). Same element-pair values apply to the zodiac sign pair (no Ether among signs). Range +2 to +4 friendly, −2 to −4 hostile
- [stated] his tie-break choices for that scoring: mutually neutral planet pairs are scored as friends; a one-sided relationship takes the friendlier view (so Mer–Sat and Mer–Nod count as friends). Net effect — enemies only when both planets' rows name the other as an enemy
- [stated] wants the influence column to hold a single total per row when a time slot carries several aspects, not one value per aspect
- [stated] scoring rule for the other seven aspects (Sept 2026): sign comes from the aspect angle, not the planets' relationship — 30/60/120/150 all positive (basic +2), 45/90/180 all negative (basic −2); same element-pair and sign-pair values otherwise. The friends/enemies table applies only at 0°
- [stated] wants a "Total Aspects Influence" column placed right after the last (180°) aspect influence column, summing all eight per-aspect influence columns for each row
- [stated] wants a change-only day extract (Sept 2026): Date, Time, Total Aspects Influence with each day opening at 09:16, keeping only rows where the total changes from the row above, and always keeping the day's closing row; each day gets its own simple line chart placed beside that day's rows on the same sheet (time on x-axis, no text in the plot body), days kept clearly separate rather than joined
- [stated] also wants the same analysis run separately on three planet groups (Oct 2026): excluding Sun & Moon (Mer, Ven, Mar, Jup, Sat, Ura, Nep, Plu, Nod); Sun, Moon, Mer, Mar, Ven only; Jup, Sat, Ura, Nep, Plu, Nod only
- [stated] also runs a planet-triangle study (Oct 2026): three planets whose pairwise angles total 360°, each pair ≥4° apart, one triangle planet aspecting an outside planet (0–180 set), market hours weekdays only, matched to Nifty file "change" as "Change in Nifty"; chose to list only triangles newly formed during market hours; wants a chart wheel beside each row with zodiac ring, wheel running clockwise, same-angle lines same colour; element colours Fire red, Water dark blue, Earth green, Air black, Sky pink
- [stated] also runs a "balancing planet" study (Oct 2026): a planet equidistant from and centred between two others, aspected by another planet; market hours weekdays only; columns date, time, planet1–3, distances 1&2/1&3/2&3, balancing planet, aspecting planet & aspect, chart wheel; wheel to draw only the planets involved, run clockwise; element colours changed to Fire red, Water blue, Earth green, Air yellow, Sky black
```

### /topics/career.md

```
---
name: career
description: Sankar's professional background, employment history, certifications, and awards
---
## Identity and Contact
- [stated] Full name: Leela Sankar Chowdary Tottempudi (goes by Sankar)
- [stated] Phone: +91 8179618819
- [stated] Email: sankarchowdary.tottempudi@gmail.com
- [stated] LinkedIn: linkedin.com/in/leela-sankar
## Education
- [stated] B.Tech Electronics and Communication Engineering, JNTU Kakinada
- [stated] Intermediate, GR Junior College, Chilakaluripeta (06/2010)
- [stated] 10th, Kakatheeya Vidya Samsthalu, Chilakaluripeta (05/2007)
## Business Entities
- [stated] Owns Tottempudi Software Solutions Pvt Ltd (consulting vehicle)
- [stated] Owns TotTech / TraceIT product business (traceit-tottech.com)
## Experience Summary
- [stated] 12+ years total experience (since 06/2014)
- [stated] ~7 years in project/delivery management (Associate PM from 07/2018, PM from 05/2019)
- [stated] Positioning: Senior Project Manager / Delivery Manager for mobile + integration programs
## Employment History
- [stated] Sahakar Solutions and Technologies (Naples/Miami, FL): Support Engineer 06/2014–05/2017; Project Lead 06/2017–07/2018; Associate PM 07/2018–04/2019; Project Manager – Application Integration 05/2019–06/2021; Senior PM – Application Integration 07/2021–05/2024
- [stated] Sahakar highlights: $3M modernization, +40% performance, PHP → React.js migration, maintenance −45%; Organizer of the Year 2020; Torch Bearer Award 2023
- [stated] Savvy Software Solutions Inc, Miami, FL — Senior PM – Application Integration, 05/2024–10/2024 (Boomi, Salesforce; $1M legacy-integration modernization, +40% perf, −15% maintenance, −20% downtime)
- [stated] Royal Cyber, Riyadh — Senior Project Manager, Mobile & Integration, 01/2025–present: $5M program, 52% margins, Excellence Award 2025
- [stated] Royal Cyber program scope: native iOS/Android with Crashlytics/Sentry/deep links; Node.js + MuleSoft middleware to Zoho, Seaware, Otalio, OneSpaWorld; React web + Strapi CMS; Zoho CRM migration from Dynamics 365 (~30% maintenance cut); AWS medallion data lake
- [stated] Tottempudi Software Solutions for ANZ Digital / END. Clothing (UK) — Senior PM (consulting), 01/01/2026–present: greenfield React Native app → BFF → Shopify
## Certifications
- [stated] PMP (01/2025)
- [stated] MuleSoft Certified Platform Architect
- [stated] MuleSoft Certified Integration Architect
- [stated] MuleSoft Certified Developer – Integration and API
- [stated] Boomi Associate Integration Developer (06/2022)
- [stated] React.js & Redux Developer (2022)
- [stated] HIPAA Associate (2021)
- [stated] ISTQB (2016)
- [stated] Red Hat Linux 7 Developer (2015)
- [stated] SAP ABAP Developer (2014)
## Awards
- [stated] Excellence Award 2025
- [stated] Torch Bearer Award 2023
- [stated] Innovation Champion 2022
- [stated] Top Project Delivery Leader 2021
- [stated] Organizer of the Year 2020
```

### /topics/health.md

```
---
name: health
description: Health notes
---
- [stated] has color blindness since childhood; hard to tell red vs black pen ink, traffic signals, and some text on certain TV backgrounds
- [stated] EnChroma online test result (Oct 2026): Protan — cone scores Blue 100%, Green 75%, Red 0%
- [stated] had cataract surgery on left eye (about a month before 5 Oct 2026); follow-up care at Vijaya Eye Hospital, Chilakaluripeta
```

### /topics/tools-and-stack.md

```
---
name: tools-and-stack
description: Technologies, platforms, and tools Sankar uses day-to-day across work and projects
---
## Development Tools and Environment
- [stated] Often operates from his phone via Chrome Remote Desktop into a Windows PC running VS Code
- [stated] Uses pnpm workspaces
- [stated] IDE: VS Code; uses Claude Code IDE sessions for autonomous development work
## Platforms and Services
- [stated] MuleSoft (Anypoint Platform) — integration middleware; certified architect and developer
- [stated] Boomi — integration platform; used at Savvy and certified
- [stated] Salesforce — used at Savvy
- [stated] Zoho (Zoho One, Zoho CRM) — CRM and ops platform; current Royal Cyber program
- [stated] AWS — medallion data lake on Royal Cyber program
- [stated] Microsoft 365 (Outlook, Teams) — daily communication and project coordination
- [stated] Strapi CMS — used on Royal Cyber React web layer
- [stated] Shopify — BFF target on END. Clothing app
- [stated] Capacitor — shell for TraceIT Android app
- [stated] Next.js 15 App Router — TraceIT web frontend
- [stated] Postgres / TimescaleDB — TraceIT database
- [stated] Docker Compose — TraceIT local/production orchestration ("pulsedeck")
- [stated] Caddy + Coraza — TraceIT reverse proxy and WAF
- [stated] Better Auth — TraceIT authentication
- [stated] React Native — END. Clothing mobile app
- [stated] React.js / Redux — prior modernization projects; certified
- [stated] Node.js — middleware layer on Royal Cyber program
- [stated] Crashlytics / Sentry — mobile observability on Royal Cyber iOS/Android
- [stated] Seaware, Otalio, OneSpaWorld — third-party integrations on Royal Cyber cruise program
- [stated] Dynamics 365 — legacy CRM migrated away from at Royal Cyber
- [stated] AmiBroker 6.20.1 — charting/trading platform; asks for custom AFL formulas (manual trend lines, parallels, time-price squares)
- [stated] AFL requests usually want one file serving both indicator and explorer, with "usual columns" plus a Trade Date column right after Date (next calendar date, holidays ignored); explorer columns after Stop Loss not needed
- [stated] Figma — asked for image work (4K upscale + background removal of a movie title logo) to be done via Figma; mentioned once
## Terminology and Channels
- [stated] Refers to Claude IDE sessions as "session 1" and "session 2" for parallel autonomous work
- [stated] Uses "copy-paste-ready block" as the standard unit of work delivered to him per destination
- [stated] Destination labels: IDE session 1, IDE session 2, terminal, Teams
- [stated] CLAUDE.md = permanent project memory file read at session start
- [stated] runs/ui-v2/ = working directory for TraceIT UI redesign run artifacts
```

### /topics/work-style.md

```
---
name: work-style
description: How Sankar likes to work, delegate, and receive information — operational preferences and working rules
---
## Delegation and Autonomy
- [stated] Wants one copy-paste-ready block per destination (IDE session 1 / session 2 / terminal / Teams) with all architecture and design decisions already made
- [stated] Questions should be resolved autonomously; only credentials, money, or destructive/irreversible actions are escalated to him
- [stated] Frequently asks "what should I do from my side" — wants his own next steps stated explicitly and kept short
- [stated] Prefers the director's staged plan over a one-shot approach when they conflict
## Focus and Productivity
- [stated] Concerned about API consumption rate versus visible output: "the rate of work completion and the rate of issue fixing was very, very low. But the consumption of APIs are very high"
- [stated] Wants visible progress, not reports
- [stated] Working rule: fix issues rather than investigate or reinvestigate; if there is an error, investigate and fix it; do not stop or freeze work; new issues like CPU/memory utilization are high priority if they arise
- [stated] Wants both IDE sessions running autonomously overnight with auto-deploy of anything fixed, followed by autonomous QA
## Security and Data Hygiene
- [stated] Passwords and tokens never leave his machine; after an accidental paste he rotated credentials
- [stated] Keystore and passphrase referenced by path only
- [stated] No secrets, PII, or customer names in the code tree or reports
- [stated] Production data must not be touched; demo databases and parallel local servers may be closed; only one server and the cloud are required at a time
## UI Design Standards (TraceIT / product work)
- [stated] Re-skinning (colour/token/radius/font changes without layout change) is explicitly rejected; both grayscale and diff tests must pass
- [stated] Every screen must apply at least five of fourteen named design principles, recorded with rationale
- [stated] Acceptance gates include: alert to root cause in ≤3 clicks/≤30 s; 100% keyboard operability with every primary action in Cmd+K; all 8 data states with zero blank panels; every web view a shareable URL restoring state; p95 interaction latency under 200 ms; zero colour-only information; push notification to acknowledged alert under 10 seconds on mobile
- [stated] Light and dark both first-class; dark is the primary working mode; auto theme follows local time (light 07:00–18:00) but manual choice always wins and persists; never auto-switch during a critical alert or live tail
- [stated] Motion: expressive entry (400 ms) for surfaces, disciplined console (120/180/240 ms); transform and opacity only; gated behind prefers-reduced-motion; 60 fps required or animation is cut
- [stated] tokens.json is the only place raw values exist; chart series colours deterministic by series identity
```

### /topics/work.md

```
---
name: work
description: Business and professional work context
---
[stated] Runs Tottempudi Software Solutions Private Limited, a software company based in Andhra Pradesh, India.
[stated] Company's four main products:
- TOTTECH ONE: school and college management platform (admissions, student records, fees, marks, parent communication)
- TOTTECH Clinical Services: hospital and IVF center platform (patient records, appointments, lab results, billing)
- TraceIT: infrastructure and application monitoring platform
- Guest 360: cruise and hospitality operations platform (booking, guest journey, crew management)
[stated] Company builds complete custom software platforms across all layers: web, mobile, backend, integrations, databases, and CRM systems.
[stated] Website: tottechsolutions.com
```
