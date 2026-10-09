# TheRugbyPlaybook-Project

**The Rugby Playbook** is an AI-assisted digital rugby eBook publishing business that creates original illustrated rugby eBooks for three age groups: `3-6`, `7-12` and `12-plus`.

> Status: project foundation only. No external services are connected yet.

## Start here
- `CLAUDE.md`: business overview, tool responsibilities, approval and copyright rules (read first)
- `docs/workflow.md`: the book-production workflow
- `docs/naming-conventions.md`: product IDs, file names and publication states
- `docs/quality-control.md`: the quality checklist every book must pass

## Production workflow
```
brief → outline → page plan → content → illustration plan → assets → quality check → approval → final export
```

## Slash commands (Claude Code)
| Command | Purpose |
|---|---|
| `/create-book` | Start a new book: brief, outline and page plan |
| `/create-character` | Draft a new character profile for approval |
| `/create-illustration` | Write illustration plans and OpenArt prompts |
| `/build-pages` | Assemble page-by-page content ready for Canva |
| `/quality-check` | Run the quality checklist on a book |
| `/export-book` | Prepare an approved book for final export |

## Tool stack (connectors available; production setup not configured)
Claude Code (content and workflow) · OpenArt (illustrations) · Canva (design and PDF) · Base44 (storefront and access) · Stripe (payments)

## Rules
- Nothing is approved without the owner's explicit approval.
- All content is original. Competitor research informs general lessons only.
- Never commit secrets or `.env` files.
