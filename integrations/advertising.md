# Integration: Advertising Platforms

> Never store credentials in this repo; use a gitignored `.env` file. A connection is not permission: every guarded action also needs the owner's explicit instruction.

## Connection status (verified 2026-10-09)
- **Available in Claude Code sessions:** TikTok for Business and Adspirer (Google, Meta, TikTok, LinkedIn, Amazon, ChatGPT ads). Neither has been audited, and which ad accounts are linked is unverified.
- **Guarded in `.claude/settings.json` (asks each time):** **every** tool on both servers, reads included.

## Role
Paid advertising to reach parents, coaches, schools and clubs. Strategy and rules are in `marketing/`.

## Platforms under consideration
| Platform | Status | Notes |
|---|---|---|
| TikTok for Business | Connector available, not audited | |
| Adspirer (multi-platform) | Connector available, not audited | |
| Others | `TO BE CONFIRMED` | |

## Rules
- No campaign is created, launched or edited, and no money is spent, without explicit owner approval of the creative, audience and budget.
- All spend must follow `marketing/budget-rules.md`.
- Ads aimed at children are subject to platform and legal restrictions. Target adults (parents, coaches) unless confirmed otherwise.
- Ad creative must follow the brand and originality rules.
