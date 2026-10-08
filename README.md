# Claude-Memory — handoff between Claude accounts

This repo carries the working context for two pieces of AROYA work so a **different Claude account** can pick up where the current one stopped (for example, when the current account's usage limit runs out).

- **Website UI/UX redesign**: the AROYA Cruises reservation website revamp
- **Concierge page redesign**: the AI Concierge booking panel

A scheduled task in the main account refreshes these files every day at about 11:00 AM IST.

## Files

| File | What it holds |
|---|---|
| `HANDOFF.md` | The current state: decisions, requirements, open items, and the next steps. **Read this first.** |
| `log/YYYY-MM-DD.md` | One short entry per day listing what changed. |

## How to continue in the other Claude account

1. Sign in to the other Claude account.
2. Open a new chat, or a Claude Code session with this repo attached.
3. Paste this message:

   > Read HANDOFF.md in github.com/sankarchowdarytottempudi-star/Claude-Memory and continue the AROYA Website UI/UX and Concierge redesign work from the "Next steps" section. Ask me only for business decisions.

4. When work happens in the other account, ask it to update `HANDOFF.md` and add a `log/` entry before you stop. That keeps both accounts in sync.

## Rules

- Never put passwords, API keys, tokens or AROYA credentials in this repo.
- Keep the repo **private**.
