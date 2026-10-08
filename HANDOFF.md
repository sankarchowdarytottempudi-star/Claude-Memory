# AROYA — Website UI/UX & Concierge Redesign: Handoff

_Last updated: 2026-10-08 (seeded from saved project notes; daily sync run same day found no further changes; refreshed daily ~11:00 IST)_

## 1. Who and what

- **Owner:** Sankar (Leela Sankar Chowdary Tottempudi). He has a finance background and is not hands-on with code, so give click-by-click steps for anything he must do himself.
- **Customer:** AROYA Cruises. The project now runs as a separate vendor engagement with **no link to royal-cyber-inc**.
- **Code repo:** `sankarchowdarytottempudi-star/Aroya_Concierge` (all work moves here).
- **UAT site:** app-uat.aroyacruise.com (also http://8.213.82.160/en). UAT is a replica of production.
- **Team as presented to the customer:** 4 people, 2 developers and 2 QA. QA-round status updates go to Fasih (Round 2 first, then later rounds).

## 2. Decisions already made (don't reopen)

- **Security / BFF:** all real AROYA API credentials, tokens and secrets live on a server-side broker (BFF). The browser only calls BFF APIs. UAT and production use the same broker setup. AROYA approved this on the condition that their details are never exposed.
- **Concierge design:** AROYA approved **Option 1 "Champagne"** (`AROYA-Concierge-1-Champagne.html`). The design files are on Sankar's PC in `Downloads\AROYA-Concierge-Designs`. The design goes to the IDE Claude to implement with fully working APIs.
- **Knowledge base:** stored in a GPU-based store that AROYA will provide. The infrastructure must support it, plus an agent that reads all conversations to give accurate answers.
- **Presentations for AROYA:** follow the customer's own theme (their "2025 Cruise Line Guest Digital Journey" deck) and improvise on it, not a generic look. Don't address the audience as "you/we"; name the parties instead (for example "AROYA", "RC team").

## 3. Concierge requirements (Sankar, 5 Oct 2026)

**Layout**
- Chat side is 40% of the screen; the stage is 60%. The stage stays **dark**.
- The stage is split 50/50 horizontally:
  - **Top half:** an auto-playing, modern, animated showcase of the chosen voyage's ports, their best places, specialities and images.
  - **Bottom half:** the working panel for whatever the guest is doing in the chat.

**Behaviour**
- The chat is good but **too slow**, and its AI answers are **not accurate enough**. Both need fixing.
- Preference words like "low budget cabin" lead to a direct suggestion ("this is our lowest cabin", changeable by the guest), not a picker.
- Whatever the chat shows (voyage, cabin, add-ons) also shows on the stage. Items can be removed from either side.
- From any step (for example Guests), the guest can go back to view or change an earlier choice such as the package.
- Saved travellers from earlier reservations (for example 13 of them) show on the stage to pick from. An edit icon expands a guest with prefilled details, and any single field can be changed.
- **Known defect:** logged-in guests are asked for their details again each time. Fix this by prefilling from the previous reservation.
- **Known defect:** booking used to reach payment but now fails when storing the reservation. Showing "reservation stored, reopen to pay" without a confirmed booking is wrong.

**Content and speed**
- Destination content comes from the CMS first. Where it's thin, a server-side background job, independent of the Concierge, gathers it from the web and open sources with AI and stores it.
- CMS data is cached in Redis and refreshed every 30 minutes. Images are cached for speed.

**Smart selling**
- Track guest price behaviour (voyage × cabin price-tier combinations) to recommend add-ons and shore excursions to similar guests.
- Offer a one-step suggestion: voyage + cabin + add-on + shore excursion.

**Testing**
- Testing must include looking at real screenshots in the browser and judging how the screen looks, not just checking the code.

## 4. Website UI/UX redesign (reservation site)

- Part of the same AROYA reservation website revamp; the Concierge panel sits inside it.
- _No separate website-level decisions recorded yet. The daily sync adds them here as they come up._

## 5. Open items

- [ ] Fix chat speed and answer accuracy.
- [ ] Fix the booking failure at the reservation-storing step.
- [ ] Prefill guest details for logged-in guests from their previous reservation.
- [ ] Build the 50/50 stage (port showcase on top, working panel below) on the Champagne design.
- [ ] CMS + background content job + Redis 30-minute cache.
- [ ] Saved-travellers picker with single-field edit.
- [ ] Back-navigation to earlier steps.
- [ ] Screenshot-based UI testing on UAT.

## 6. Next steps

1. Implement the Champagne design in `Aroya_Concierge` with working APIs through the BFF.
2. Fix the two known defects (booking store failure, guest re-entry) first, since they block real bookings.
3. Run screenshot-based tests on UAT, then send Fasih the next QA-round status.

## 7. Where things live

| Item | Location |
|---|---|
| Code | github.com/sankarchowdarytottempudi-star/Aroya_Concierge |
| Approved design file | Sankar's PC: `Downloads\AROYA-Concierge-Designs\AROYA-Concierge-1-Champagne.html` |
| UAT | app-uat.aroyacruise.com |
| Daily change log | `log/` in this repo |
