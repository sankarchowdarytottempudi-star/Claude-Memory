# IDE prompt — TraceIT Assistant: Conversation mode (15 Oct 2026)

Owner requirement (15 Oct): the TraceIT Assistant must work as an interactive, multi-turn conversation, the same way the booking concierge works: the user talks freely, follow-ups keep context, and the user can say "do what we discussed" and the assistant acts on the conversation.

Queue this AFTER release 1 (6fc6ba794) deploys and Train 2 is gated. Never on the production host while customers are on it. Each slice below gets its own gate, deploy and live checks. Never combine slices.

---

## Step 0 — Read before building (report before writing code)

Read the current Assistant code (UI, API route, prompt, tools, storage) and report in plain English:
- what it does today (single question/answer or multi-turn?)
- which model/provider it calls and how that is configured
- which TraceIT data it can reach and how screen access / RLS is enforced
- what is stored about conversations today

Do not assume any of this. Build on what exists; do not start a parallel assistant.

## Slice C1 — Conversation core

- Each user has conversations (threads). "New conversation" button; a list of past conversations to reopen and continue; delete own conversation.
- Multi-turn context: follow-ups resolve against earlier turns. Examples that must work:
  - "How is db-sys-api doing?" → "and yesterday?" → "only the ship cluster" → "compare with zoho-sys-api"
  - "What failed in check-in this week?" → "show me the worst booking" → "open its Graylog query"
- Replies stream token by token, with a Stop button. A typing indicator appears at once.
- Up to 3 suggested follow-up chips under each reply, never two of the same kind.
- Long conversations: summarise older turns on the server so context stays within the model limit; the user never sees a cut-off.
- Conversations are per user and per workspace, protected by RLS like all other data. Retention setting per workspace (default 90 days), audited deletes.

## Slice C2 — Grounded answers (live data only)

- Every figure in a reply comes from a tool call to TraceIT's own APIs, run as the signed-in user, so the user only ever hears about what their screens allow.
- Each figure carries a small source link that opens the exact screen, filter and time range it came from.
- Times in the viewer's browser time zone (same rule as the local-time sweep).
- If no data supports an answer, say so plainly and offer the nearest screen. Never estimate, never invent.
- Guest payloads / PII are never sent to the model. Mask before any model call.

## Slice C3 — Side panel ("stage")

- Chat on the left, a live panel on the right that shows what the conversation is about: the chart, table, alert list or log trace being discussed. It updates as the conversation moves.
- The user can click anything in the panel and the chat picks it up ("this one").
- Works on mobile: panel becomes a swipe-up sheet below 640 px.

## Slice C4 — Actions from the conversation

- The user can ask the assistant to act on what was discussed, e.g. "create an alert rule for that", "mute this for an hour", "open the Graylog query", "save this as a custom query", "export it".
- Read-only by default. Any change shows a confirmation card in the chat (what will change, for which system) and runs only after the user confirms. Role rules from Settings → Screen access apply. Every action audited.
- Never: deploys, deleting data, changing other users, paging the on-call roster, or anything the user's role cannot do on screen.

## Slice C5 — Knowledge and portable model setup

- Answer "how do I…" and "what does this alert mean" from TraceIT's own help and runbook content via a vector store (pgvector), with the source shown.
- Model provider and host are configuration, not code: one gateway setting switches between a hosted model, the planned self-hosted GPU VM, and a customer's on-prem install. No provider-specific code outside the gateway.
- Secrets only in the server environment. Nothing in git.

---

## Acceptance (each slice)

- Typecheck, lint and tests green; new tests for multi-turn follow-ups, RLS (user A cannot read user B's conversations or another workspace's data), PII masking, and the confirm-before-change rule.
- Live screenshots after deploy: desktop 1366×768 and 1920×1080, and a phone, dark and light. Judge the screenshots, not only the code.
- Time to first streamed token measured on the live site and reported (p50 and p95).
- Build behind a NEW flag that is off in production. The owner turns it on.
- Report in the owner's format: Done / In the gate / After the gate / Needs you.
