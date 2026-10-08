# Claude-Memory — handoff between Claude accounts

This repo carries the working context for **separate projects** so a **different Claude account** can pick up where the current one stopped (for example, when the current account's usage limit runs out).

| Project | Folder |
|---|---|
| Website UI/UX redesign (TraceIT monitoring platform) | `website-uiux/` |
| AROYA Concierge page redesign | `concierge/` |
| Full memory of account 1 (all notes, both accounts can import) | `memory/ALL-MEMORY.md` |

Each folder has its own `HANDOFF.md` (current state: decisions, requirements, open items, next steps) and its own `log/YYYY-MM-DD.md` (what changed each day). The two projects are kept apart: never mix their notes.

A scheduled task in the main account refreshes both folders every day at about 10:50 AM IST.

## How to continue in the other Claude account

1. Sign in to the other Claude account.
2. Open a new chat, or a Claude Code session with this repo attached.
3. Paste the line for the project you want to continue:

   **Website UI/UX redesign**
   > Read website-uiux/HANDOFF.md in github.com/sankarchowdarytottempudi-star/Claude-Memory and continue the Website UI/UX redesign from its "Next steps" section. Ask me only for business decisions.

   **Concierge page redesign**
   > Read concierge/HANDOFF.md in github.com/sankarchowdarytottempudi-star/Claude-Memory and continue the AROYA Concierge page redesign from its "Next steps" section. Ask me only for business decisions.

4. Before you stop in the other account, ask it to update that project's `HANDOFF.md` and add a `log/` entry in the same folder. That keeps both accounts in sync.

## Rules

- Never put passwords, API keys, tokens or customer credentials in this repo.
- Keep the repo **private**.
