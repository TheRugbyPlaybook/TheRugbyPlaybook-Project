# Naming Conventions

## Product IDs
Format: `TRP-<AGE>-<TITLE-SLUG>-v<N>`

| Part | Values | Example |
|---|---|---|
| `TRP` | Fixed brand prefix | `TRP` |
| `<AGE>` | `3-6`, `7-12`, `12-PLUS` | `7-12` |
| `<TITLE-SLUG>` | UPPERCASE, hyphen-separated, short | `PASS-PERFECT` |
| `v<N>` | Version number, starting at 1 | `v1` |

Examples: `TRP-3-6-<SLUG>-v1`, `TRP-7-12-PASS-PERFECT-v1`, `TRP-12-PLUS-<SLUG>-v1`

Rules:
- Product IDs are unique and never reused, even for archived books.
- A new version is a new ID (`-v2`) with its own folder.
- The product ID is the shared reference across this repo, Canva, Base44 and Stripe.

## Publication states
| State | Meaning | Set by |
|---|---|---|
| `DRAFT` | In production | Claude / owner |
| `READY` | QC passed and owner approved | Owner only |
| `PUBLISHED` | Live for customers | Owner only |
| `ARCHIVED` | Withdrawn, kept for the record | Owner only |

## Folders
| Item | Path |
|---|---|
| Book | `books/<age>/<PRODUCT-ID>/` |
| Character | `characters/<age>/<character-slug>.md` |
| Illustrations | `illustrations/<age>/<PRODUCT-ID>/` |
| Final eBook | `output/final/<PRODUCT-ID>.pdf` |
| Draft export | `output/drafts/<PRODUCT-ID>-draft-YYYYMMDD.pdf` |
| Preview | `output/previews/<PRODUCT-ID>-preview-<NN>.png` |

`<age>` folder names are lowercase: `3-6`, `7-12`, `12-plus`.

## Image IDs
Format: `<PRODUCT-ID>-P<NN>-<LETTER>`, e.g. `TRP-7-12-PASS-PERFECT-v1-P03-A` (page 3, first image). Cover: `<PRODUCT-ID>-COVER`.

## General file rules
- Markdown source files: lowercase, hyphen-separated (`page-plan.md`).
- No spaces or special characters in file names.
- Dates as `YYYY-MM-DD` (in file names: `YYYYMMDD`).
