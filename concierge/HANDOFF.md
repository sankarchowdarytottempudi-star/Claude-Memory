# Project: AROYA Concierge Page Redesign — Handoff

_Last updated: 2026-10-08 evening (account 1 sync: 8 Oct afternoon → evening; earlier: full history upload 28 Sep – 8 Oct)_

> This is a **separate project** from the Website UI/UX redesign (see `../website-uiux/HANDOFF.md`). Record only Concierge work here.

## 0. How the work is run (read first)

- **Roles:** Sankar ferries prompts between the "architect" Claude chat (writes IDE prompts, emails and decisions) and the **IDE agent (Claude Code in VS Code on Sankar's PC)**, which writes the code, tests and deploys.
- **IDE working folder:** `C:\Users\tlsch\Downloads\Aroya_Concierge_export` (clean export, no old history). Old folders are read-only reference.
- **Long prompts:** save them as `.md` files (in Downloads or `docs/qa/` in the repo) and send the IDE a one-liner like "Read <path> and execute it". Never attach the big design HTML (`docs/design/aroya-concierge-design-v12.html`, 2.8 MB); it caused "prompt too long". Use `aroya-concierge-design-v12-code-only.html`.
- **IDE status format:** every IDE update starts with "Live now / Deploying / Last rollback".
- **Approvals the IDE needs typed by Sankar himself:** the IDE ignores pasted approvals for deploys, UAT writes and server jobs. Sankar must type a short line himself, e.g. "confirmed: deploy <build> + run the content job".
- **Customer emails (Fasih):** never mention AI, the IDE, Claude, commit hashes or infrastructure. Use "in progress / completed / next steps / inputs needed".

## 1. Who and what

- **Owner:** Sankar (Leela Sankar Chowdary Tottempudi). He has a finance background and is not hands-on with code, so give click-by-click steps for anything he must do himself.
- **Customer:** AROYA Cruises. The work runs as a separate vendor engagement with **no link to royal-cyber-inc**. Client head: Fasih.
- **What it is:** the AI Concierge booking panel. A guest chats to choose a voyage, cabin, add-ons and shore excursions, and books.
- **Code repo:** `sankarchowdarytottempudi-star/Aroya_Concierge` (private). Branches: `main` and `concierge-intelligence`; both are pushed.
- **Test site (ours):** https://aroya-test.tottechsolutions.com, on a VM with Caddy + Docker, SSH key only, and a red "Test environment" banner.
- **AROYA UAT booking system:** Seaware/Versonix GraphQL via MuleSoft. AROYA UAT site: app-uat.aroyacruise.com. UAT is a replica of production.
- **Team as presented to the customer:** 2 developers and 2 QA.

## 2. Decisions already made (don't reopen)

**Security / architecture**
- The BFF broker holds all AROYA credentials (root-only env file on the VM). The browser only calls `/bff/v1/...`. UAT and production use the same broker setup. AROYA approved this on the condition that their details are never exposed.
- Secrets are never pasted in chat, prompts or the repo; Sankar enters them on the server himself. gitleaks and the large-file guard run before every push. Push only to the private repo; never rewrite or roll back the old royal-cyber repo.
- Never touch AROYA production.

**Design**
- AROYA approved design direction "Champagne". The build is the **v12 "Champagne · Cinema"** design (flag `conciergeFlags.designV12`, ON on the test site) with AROYA branding: Krub font, navy #003083, sea blue #0090D0, teal #1CA8C8. The stage (right side) is always **dark** (a light stage was tried and Sankar rejected it).
- **Layout: 30% chat / 70% stage** (changed from 40/60 on 6 Oct).
  - Chat column: min 400 px, max 520 px.
  - The top header (logo, New conversation, account, close, "⋯" menu with sound/theme/language) sits only above the chat column.
  - The stage is full window height. No Trip…Pay step bar on the stage.
  - The total line ("SAR x · 2A 1C · Breakup ›") sits in the chat column above the message box.
- **Stage top:** an auto-playing destination showcase for the chosen voyage. Each port shows a description, a "Why visit" line and best places with photos, and stays readable on any image. When a section is active, it shrinks to a strip that still shows the port, "Why visit" and "More about <port>".
- **Stage bottom:** a fixed "journey board" that **never scrolls**, with 8 parts: Voyage, Cabin, Guests (double width), Add-ons, Excursions, Price breakup (double width).
  - The current step's part is large; the others are compact tiles.
  - No ‹ › arrows are needed to see content. Guests show a card list on the left and a form on the right; add-ons and excursions show a grid with tabs.
- **Sizing:** the whole Concierge is at **0.8× scale**: one token `--concierge-scale: 0.8` for both sides. Sankar found 80% browser zoom fitted best.
- **Payment:** payment options only in the chat. "Pay full" opens the payment provider (Teller) in a **new window** (changed from same-tab on 6 Oct). Confirmation shows only when the broker confirms payment, then the full-width booking summary on the stage.

**Behaviour rules**
- Nothing paid is added without the guest confirming in chat, with names and prices.
- An explicit removal is final: removed items are never re-added. Recommendations never auto-apply.
- **Removal is final at family level, and removing leaves the slot empty** (changed from item-level "removal is final" on 8 Oct, after the Ultimate refill bug): removing e.g. "Ultimate Dining" declines that whole bundle/excursion family for that guest; nothing of the same family is added in its place.
- **Transport/transfer is never an excursion** (8 Oct): classified by the catalogue type code and offered only in a separate Transfers option.
- **Test fixtures use real catalogue data** (8 Oct): add-on/excursion tests run on a fixture taken from the real UAT catalogue, not invented items.
- **Add-on rules = the existing Guest Enhancements page** (changed 6 Oct; the earlier "one package per guest" rule was wrong and is removed). The guest chooses which guest each add-on is for ("For everyone / Specific guests"). Only bundles that page applies to everyone (e.g. the drinks package) go to all. Age rules apply (spa 18+).
- Suggestions: at most 3, one per category, never two of a kind, never transport/transfer offered as an experience. No two overlapping excursions for one guest ("Replace it?").
- Booked excursions can't be removed online (no Seaware remove call) and show a "contact AROYA" note.
- "Low budget cabin" and similar words lead to one direct recommendation (lowest price) with the option to change it.
- A party size stated in words beats the model's guess (e.g. "my wife, me and my son" = 2 adults + 1 child).
- One Seaware session per booking; a lost session gives "Your session timed out. Let's re-check your cabin."
- After a reservation exists, name, DOB and passport are locked (Seaware adds a guest on update instead of replacing). Contact details can be edited, with an "Also update my saved profile" tick box.
- Destination content: CMS first, then curated/stored guides, then a branded fallback. Nothing is generated live during a guest session. Photos come only from Wikimedia/Wikipedia with CC0, public domain, CC BY or CC BY-SA licences, with attribution, and stay marked "auto" until AROYA approves.
- **Guest form phone codes** (8 Oct):
  - the code list is sorted ascending numerically (master-data list and fallback list);
  - the code is preselected from the guest's nationality; a manual pick is never overwritten; fallback = the saved profile's code, else +966; the picker is searchable.
- **Copy Traveller 1's details to other travellers** (8 Oct): shared fields (email, phone code + mobile, nationality, country of residence, city, passport issuing country) are prefilled for travellers 2+, editable, with a "Same as Traveller 1" note. Personal fields (title, names, gender, DOB, passport number/expiry) are never copied. If Seaware requires a field to be unique per guest, follow the regular booking flow's rule.
- **Guest form layout** (8 Oct): email/phone fields show in full (no clipped "+966"); "Call AROYA" and "WhatsApp AROYA" are two side-by-side buttons (no "·" line).
- The opening options always show on open and after New conversation: "Guide me / I know what I want", then "Sign in / Continue as a guest".

**Deploy / test process (agreed)**
- Every deploy runs from a clean copy of the commit, with a committed test manifest (`deploy/test-vm/live-manifest.json`) and a pre-deploy security dry run.
- Blocking checks: build/deploy, bundle scans (0 credentials), security-verify 0 FAIL, the end-to-end journey to Pay (mocks) and to Hold (live), and chat smoke. Everything else is report-only.
- Any blocking failure leads to an automatic rollback. Rollback first re-locks payment to runner-only.
- The IDE must look at live screenshots (EN + AR, 1366×768, 1920×1080, iPhone) and fix forward. Testing is never code-only.
- Real UAT writes only with Sankar's typed approval, one booking at a time, no second attempt.
- Test route: **Mediterranean from Alexandria, November 2026 (10 Nov sailing)**. The Jeddah Red Sea sailings have no prices on UAT.

## 3. What is built and where (as of 8 Oct evening)

- **Live on the test site:** build **20261008-133819-7a93ea0** (commit 7a93ea0), deployed 8 Oct after Sankar typed "confirmed: deploy 7a93ea0 + rerun the content job". All checks green:
  - security-verify 52 pass / 0 fail / 5 warnings
  - bundle scans 0
  - smoke green
  - first-load matrix 60 passed
  - Hold journey passed
  - self-QA EN / AR / WebKit / iPhone / iPad passed
- **Rollback target: 7a93ea0** (target committed as 809acea). Previous good build: ecaa3a6 (target committed as 9daf566), which went green on 8 Oct and replaced 16d5ce0.
- **7a93ea0 adds (on top of ecaa3a6):**
  - email/phone fields shown in full; "+966" not clipped
  - Call / WhatsApp as two side-by-side buttons
  - the last English lines on the Arabic screen translated (reservation created, extras question, welcome back)
  - new test `e2e/v12-contact-form.mock.spec.js` (1366×768 and 1920×1080, EN + AR; fails on field overflow, a clipped code, button layout, or codes out of order)
- **ecaa3a6 contains:**
  - the 0.8× scale
  - destination info always showing (11 test-sailing ports covered EN + AR)
  - the non-scrolling board
  - guest cards restored
  - the banner and "From SAR x" fixes
  - 30 more Arabic Concierge lines
  - place-photo support
  - the Kusadasi KUS/KAS mapping by sailing code
  - an unsaved guest form that stays open while the reservation is being created
- **Local, not deployed yet:**
  - **437c4c1:** phone codes sorted ascending numerically.
  - **bb59845:** nationality-based code preselect + Traveller 1 shared-details copy. The full mocked set was running at the last IDE report.
  - **Ultimate refill / transport fix:** prompt sent to the IDE; not yet coded or reported.
- **Earlier work, all in the code:**
  - **v5c/v5d/v5e:** the 30/70 layout, board, payment new window, add-on rules, edit-guest prefill, dedupe of saved travellers, header in the chat column.
  - **Fix pass on 7–8 Oct:**
    - removals are final
    - suggestions de-duplicated
    - excursion conflict check
    - opening options restored
    - 13-inch layout
    - the "⋯" menu fix
    - promo-0 fare fix ("Cruise Only")
  - **Payment guards in the broker (security-verify P1–P5):**
    - own booking only
    - test mode forced
    - rate limits 5 per session and 20 per IP per hour
    - audit log
    - refused outside UAT
- **Content job:** built, with photo fetching (Wikipedia lead image, then Wikimedia Commons search; CC0/PD/CC BY/CC BY-SA with attribution; status "auto"). Ran on the VM after ecaa3a6, then reran after 7a93ea0 at a 2.5 s request pace:
  - **164 of 207 places now have their own photo** (162 → 164 on the rerun; ITCAG and OMMCT improved). The other **43 show the port photo**. Throttling is not the cause: these need AROYA's images.
  - Backup before the rerun: `/opt/aroya-broker/backups/destinations-before-rerun-20261008.tgz` (on the VM).
  - The nightly schedule is still OFF.
- **Redis:** OFF until Sankar sets a password on the VM (steps in `docs/production/redis-secret-steps.md`). The broker uses its in-memory cache meanwhile, so guests lose their session on each deploy. The old Redis was internal-only, never exposed.
- **Useful repo docs:**
  - `docs/concierge/aroya-inputs-needed.md`
  - `docs/concierge/addon-rules.md`
  - `docs/concierge/rca-session-context.md`
  - `docs/concierge/master-data-gaps.md`
  - `docs/qa/` (prompts, run logs, visual reviews)
  - `docs/production/runbook.md`
- **Screenshots** (Sankar's PC): `Downloads\AROYA_Concierge_Test_Deliverables\screens\...` (v5e, v5h, zoom80-baseline).
- **Tests at last report:** 1,894+ unit tests pass; broker 123–133 pass; security-verify 52 pass / 0 fail / 5 warnings on 7a93ea0; the mocked blocking set was green on 7a93ea0 and was running on bb59845.

## 4. API / BFF status

- BFF broker live with the payment guards above. The payment page is open to plain visitors on the test site only, guarded; `patches/pay-testers.patch` is obsolete and unapplied.
- **UAT bookings:**
  - 23693 is CANCELLED (verified)
  - -27480779 is a temporary booking that expires on its own
  - 23574 was cancelled earlier by AROYA
  - Stored holds (OFFER) do NOT expire on their own (asked AROYA to confirm).
- **Pay proof** (one real booking → Teller window shows the TEST notice → no card → cancel): **NOT done yet.** Needs Sankar's own typed approval, e.g. "approved: 1 booking on <build> for the Pay proof". If the TEST notice is missing, the fail-safe re-locks payment.
- Seaware has no call to remove an excursion or to update an existing guest's identity (asked AROYA).

## 5. Known defects / gaps

**Open: CRITICAL (found by Sankar, 8 Oct)**
- **Ultimate bundle refill:** removing "Ultimate Dining" adds another "Ultimate" bundle in its place; the same refill happens for excursions. Breaks "removals are final". Fix prompt sent: reproduce on live, family-level declined list, no refill, real-catalogue fixture tests, live screenshots.
- **Transport added as excursions:** transfer/transport items still appear and get added as excursions. Fix prompt sent: classify by type code into a separate Transfers option.

**Open: other**
- 43 of 207 places have no own photo (the port photo shows); needs AROYA images. Some auto matches are weak (e.g. a painting for the Palace of the Grand Master).
- The Arabic review of destination text needs a native reviewer.
- "Total so far" shows "From SAR x" until priced. Verify on the live site.
- No "with flights" journey testable (the Mediterranean sailing sells no flight fare on UAT).
- Classic booking promo-0 fix: confirm it shipped.
- Reply speed: the true send-to-reply time was never measured on the live site (the "0.1 s" figure was server-only).
- Holdout accuracy: v5 scored 91.7% (target 95%); holdout-v6 is planned.

**Fixed on 8 Oct (live in 7a93ea0)**
- Guest form email/phone fields cut off text and clipped "+966" → fixed.
- "Call AROYA · WhatsApp AROYA" stacked awkwardly → two side-by-side buttons.
- English lines left on the Arabic screen (reservation created, extras question, welcome back) → translated.
- Guest form closed while the reservation was being created, losing unsaved input → stays open (ecaa3a6).
- Kusadasi KUS vs KAS mix-up → mapped by sailing code (ecaa3a6).

**Fixed locally (not deployed)**
- Phone codes not in order → sorted ascending (437c4c1).

## 6. AROYA inputs needed (send via Fasih)

1. Do stored holds on UAT expire on their own, or need a manual cancel?
2. Can inventory be loaded for the Jeddah Red Sea sailings (30 Sep / 3 Oct 2027 show no prices)?
3. Is there a call to update an existing guest's name/DOB/passport after booking?
4. Is there a call to remove an excursion from a booking?
5. Remove the blank "test" and "hey" add-ons from the CMS.
6. Images for add-ons and excursions, and approved images for the **43 places** that have no own photo (list to be sent with the next IDE report).
7. Vector logo, final Arabic font and brand pattern files.
8. A native Arabic reviewer for destination descriptions, and approval of the auto-sourced photos/guides.
9. Kusadasi port code (KUS vs KAS) confirmation.
10. Confirmation that the 14 old credentials were rotated.

## 7. Open items

- [x] Chat/stage layout (30/70, board, showcase)
- [x] Fix the booking failure at the reservation-storing step
- [x] Prefill guest details / saved-travellers picker with single-field edit
- [x] Back-navigation (look-back via board tiles)
- [x] Screenshot-based UI testing (live screenshots each deploy)
- [x] ecaa3a6 live checks → rollback target moved → content job run once
- [x] Guest form field width + Call/WhatsApp buttons (7a93ea0, live)
- [x] Content rerun (164/207)
- [ ] **CRITICAL: Ultimate bundle / excursion refill after removal + transport as excursions** (prompt sent)
- [ ] Phone code sort (437c4c1) + nationality preselect + Traveller 1 copy (bb59845): mocked set → "Ready to ship" → Sankar types the deploy approval
- [ ] 43-places list to AROYA for images
- [ ] Arabic live screenshots past extras
- [ ] Pay proof (needs Sankar's typed approval)
- [ ] Redis password (Sankar on the VM) → turn Redis on
- [ ] Content job nightly schedule + AROYA approval of auto content
- [ ] Honest live speed measurement; holdout-v6
- [ ] Updated customer test script docx; journey video
- [ ] Smart-selling (price-behaviour recommendations) — not started

## 8. Next steps (exact)

1. Wait for the IDE's "Ready to ship" report on bb59845. It must also include the **Ultimate refill + transport fix** (with real-catalogue fixture tests and live screenshots) and the **43-places list**. If the refill fix is missing, send it back before deploying.
2. Sankar types the approval himself: `confirmed: deploy <build>` (the build number is in the IDE's "Ready to ship" line).
3. After it is live and green, Sankar tests:
   - add Ultimate Dining → remove it → nothing replaces it; repeat for an excursion
   - no transport/transfer items in Excursions; they show under Transfers only
   - Guests: the phone code follows nationality; a manual pick stays; codes are in ascending order
   - Traveller 2+ get Traveller 1's email/phone/nationality/residence/city/issuing country with a "Same as Traveller 1" note, editable; names, DOB, gender and passport are blank
   - EN + AR, 13-inch laptop at 100% zoom, stop before Hold/Pay
4. Send Fasih the progress email (drafted in the architect chat). Once bb59845 is live, move the nationality/copy items from "In progress" to "Completed". Include the 43 photos and Kusadasi in the inputs.
5. Optional: the Pay proof (Sankar types "approved: 1 booking on <build> for the Pay proof").
6. Sankar: set the Redis password on the VM (`docs/production/redis-secret-steps.md`), then the IDE turns Redis on.
7. Later: content job nightly schedule (after AROYA approves the auto content), honest live speed measurement, holdout-v6, customer test script docx, journey video.

## 9. Where things live

| Item | Location |
|---|---|
| Code | github.com/sankarchowdarytottempudi-star/Aroya_Concierge (`main`, `concierge-intelligence`) |
| IDE working copy | Sankar's PC: `C:\Users\tlsch\Downloads\Aroya_Concierge_export` |
| Design files | repo `docs/design/` (v12; use the code-only HTML); Sankar's PC `Downloads\AROYA-Concierge-Designs` |
| Designer brief | Claude Docs artifact "AROYA Concierge — Design Requirements" |
| Test site | https://aroya-test.tottechsolutions.com |
| AROYA UAT | app-uat.aroyacruise.com |
| Test screenshots | Sankar's PC: `Downloads\AROYA_Concierge_Test_Deliverables\screens\` |
| Daily change log | `concierge/log/` in this repo |
