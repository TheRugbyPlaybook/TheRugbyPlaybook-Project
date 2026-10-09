# CLAUDE.md — The Rugby Playbook

This file tells Claude Code how to work in this repository. Read it at the start of every session.

## 1. The business

**The Rugby Playbook (TRP)** is an AI-assisted digital rugby eBook publishing business. We create original, illustrated rugby eBooks for three age groups. We sell them as digital products through an online storefront.

This repository is the **source of truth** for briefs, outlines, page plans, book text, character bibles, illustration prompts, brand rules, research notes, marketing plans and workflow documentation.

## 2. Tools and responsibilities

| Tool | Responsibility | Status |
|---|---|---|
| **Claude Code** | Content and workflow orchestration. Writes briefs, outlines, page plans, book text, character profiles, illustration prompts and quality-check reports. Keeps files organised, applies naming conventions and tracks publication state. | Active (this repo) |
| **OpenArt** | Generates illustrations from prompts and character reference sheets prepared in this repo. | Connector available (verified 2026-10-09). Plus plan. Production setup not configured. See `integrations/openart.md` |
| **Canva** | Page design, layout, brand templates and PDF export of the finished eBook. | Connector available (verified 2026-10-09). No Brand Kit yet. Production setup not configured. See `integrations/canva.md` |
| **Base44** | Digital storefront, product listings and customer access to purchased eBooks. | Connector available (verified 2026-10-09). An app named "The Rugby Playbook" already exists; its contents have not been reviewed. See `integrations/base44.md` |
| **Stripe** | Payment processing for eBook sales. | Connector available (verified 2026-10-09). ⚠️ **Live mode only, no test account.** Production setup not configured. See `integrations/stripe.md` |

TikTok for Business and Adspirer (advertising) connectors are also available. See `integrations/advertising.md`.

### Integration rules
- **A connection is not permission.** A working connector does not mean an action is approved, or that every feature is available on the current plan.
- Tools that write, spend credits or money, or publish are gated by ask-rules in `.claude/settings.json`. They also need the owner's explicit instruction for that specific action, and a permission prompt is not a substitute for that instruction.
- Check the OpenArt credit cost before any generation and tell the owner what it will cost.
- No Stripe write actions until a test environment exists and the owner says to proceed.
- Do **not** connect, authenticate, call or configure any external service unless the owner explicitly asks for it in that session. Read-only checks (account status, listings) are allowed when the owner asks for an audit.
- Do **not** create API keys, accounts, products, prices, payment links, ad campaigns or listings.
- Do **not** publish anything, or spend money (including generation credits), without explicit owner approval.
- Never claim an integration is connected or that an action happened in an external tool when it did not.
- Never commit secrets. Credentials belong in `.env` files, which are gitignored.

## 3. Age groups

| Code | Audience | Guide |
|---|---|---|
| `3-6` | Early years: read-aloud, picture-led | `age-groups/3-6.md` |
| `7-12` | Primary / junior players: early independent readers | `age-groups/7-12.md` |
| `12-plus` | Teen and older players: skills, tactics, mindset | `age-groups/12-plus.md` |

Every book, character and illustration belongs to exactly one age group. Files go in the matching `3-6/`, `7-12/` or `12-plus/` subfolder.

## 4. Book-production workflow

Every book follows these stages in order. Do not skip a stage.

```
brief → outline → page plan → content → illustration plan → assets → quality check → approval → final export
```

Details: `docs/workflow.md`. The slash commands in `.claude/commands/` and skills in `.claude/skills/` run these stages.

## 5. Product IDs and publication states

**Product ID format:** `TRP-<AGE>-<TITLE-SLUG>-v<N>`
- Example: `TRP-7-12-PASS-PERFECT-v1`
- `<AGE>` is `3-6`, `7-12` or `12-PLUS`
- `<TITLE-SLUG>` is UPPERCASE with words joined by hyphens
- `v<N>` goes up by one for each released revision

**Publication states:**

| State | Meaning |
|---|---|
| `DRAFT` | In production. Not approved. |
| `READY` | Passed quality check **and** approved by the owner. Ready to export or list. |
| `PUBLISHED` | Live for customers. |
| `ARCHIVED` | No longer sold. Kept for the record. |

Full rules: `docs/naming-conventions.md`.

## 6. Approval rule (non-negotiable)

**No book, character, illustration style or brand decision is approved without the owner's explicit approval.**
- Claude may draft, propose and recommend, but must never mark anything as approved, `READY` or `PUBLISHED` on its own.
- Approval must be recorded in the book's or character's file with the date and wording, e.g. `Approved by owner on YYYY-MM-DD`.
- Silence, an absence of objections or "looks fine so far" is **not** approval.
- If something is unclear, ask. Do not assume.

## 7. Quality standards

Every book must pass `docs/quality-control.md` before it is presented for approval. In summary:
- **Age-appropriate**: vocabulary, sentence length, concepts and page count match the age-group guide.
- **Rugby-accurate**: laws, terminology and techniques are correct, with player safety placed first (especially tackling, contact and scrums for younger ages).
- **Safe and inclusive**: positive messaging, mixed genders, abilities and backgrounds, and no harmful stereotypes.
- **Consistent**: characters match the character bible, visuals match the brand, and text matches the illustrations.
- **Clean**: no spelling or grammar errors, no placeholder text, no `TO BE CONFIRMED` left in final files.
- **Original**: passes the originality checks in section 8.

## 8. Original content and copyright rules

- All book text, characters, illustrations and layouts must be **original to The Rugby Playbook**.
- Competitor research (`research/`) may inform **general lessons only**: market gaps, pricing ranges, format ideas, age-group needs and what customers value.
- Competitor material must **never** be copied, paraphrased closely or imitated in:
  - book text, titles, storylines or catchphrases
  - character names, designs, personalities or likenesses
  - illustrations, art styles or prompts that reference a competitor's work or a named living artist
  - distinctive layouts, page designs, cover compositions or branding
- Do not use real players, teams, logos, kits, competition names or trademarks without written permission.
- Do not upload competitor images to OpenArt or any other tool as references.
- Research notes must record their source, and keep quotes short and clearly marked as quotes.
- If a draft looks too close to existing work, flag it and rewrite it. Do not ship it.

## 9. Undecided items

Brand colours, fonts, logo, characters, art style, pricing and other business decisions are **not yet decided**. They are marked `TO BE CONFIRMED` in the relevant files. Claude must not invent or assume these decisions. It may propose options, clearly labelled as proposals.

## 10. Repository map

| Path | Purpose |
|---|---|
| `.claude/commands/` | Slash commands for each production step |
| `.claude/skills/` | Reusable production skills |
| `brand/` | Brand bible, visual style, typography, colours |
| `characters/` | Character bible and per-age character files |
| `age-groups/` | Writing and design guides per age group |
| `books/` | One folder per book, by age group |
| `illustrations/` | Illustration plans, prompts and generated images, by age group |
| `integrations/` | External tool status and documentation |
| `assets/` | Logos, backgrounds, icons, reference images |
| `templates/` | Canva and page-layout templates |
| `research/` | Competitor and market research (general lessons only) |
| `marketing/` | Strategy, audiences, ad copy, experiments, budgets |
| `output/` | Exported drafts, final eBooks and previews |
| `docs/` | Workflow, quality control, naming conventions |

## 11. Working conventions
- Use British/NZ spelling (e.g. colour, organise) unless the owner decides otherwise. `TO BE CONFIRMED`
- Use Markdown for all source content.
- Never delete or overwrite existing work without asking. Create a new version instead.
- Keep every change traceable: one book per folder, and a status line at the top of every book file.
