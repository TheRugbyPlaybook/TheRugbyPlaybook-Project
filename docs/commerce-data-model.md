# Commerce data model (Base44)

> **Status: PROPOSAL — not built.** Part of `docs/migration/shopify-to-base44-stripe.md`. Creating these entities in Base44 is an external write and needs the owner's explicit approval.

## Principles
- **New entity names.** The existing Shopify-synced entities (`Product`, `GiftOrder` and others) are left untouched until Shopify is retired. The hourly Shopify sync deletes `Product` records, so nothing new goes in `Product`.
- **Money is stored as integers in minor units** (cents), with a currency code. Never as decimals.
- **Purchases keep a snapshot.** An order line records the title, price and book version as they were at purchase, so later catalogue changes do not rewrite history.
- **Admin-only by default.** Every commerce entity is readable and writable by `admin` only. Customers reach their own orders and downloads through backend functions, never through direct entity access.
- **Roles.** Base44 provides `admin` and `user` only (verified). Finer roles such as editor or support would need a custom field: `TO BE CONFIRMED`.
- **No card data** is ever stored. Stripe holds payment details.

## Catalogue

### `Book`
| Field | Notes |
|---|---|
| `product_id` | `TRP-<AGE>-<TITLE-SLUG>` (unique). See `docs/naming-conventions.md`. |
| `slug` | URL slug (unique). |
| `title`, `subtitle`, `description` | Listing copy from `listing.md`. |
| `age_group` | `3-6`, `7-12` or `12-plus`. |
| `learning_outcomes` | List, copied from the approved brief. |
| `cover_file`, `preview_files` | Public images only. |
| `current_version_id` | The `BookVersion` sold to new buyers. |
| `status` | `DRAFT` → `READY` → `PUBLISHED` → `ARCHIVED`. Only the owner sets `READY`, `PUBLISHED` or `ARCHIVED`. |
| `approved_by`, `approved_at` | Copied from the owner's approval in `status.md`. |

### `BookVersion`
| Field | Notes |
|---|---|
| `book_id`, `version` | e.g. `v1`. Unique together. |
| `private_file_ref` | Private storage reference. Never a public URL. |
| `sha256`, `bytes`, `page_count` | Must match the checksum recorded in the repo. |
| `qc_report_ref` | Repo commit of `quality-report.md`. |
| `status` | `DRAFT`, `RELEASED`, `WITHDRAWN`. |

### `Bundle` and `BundleItem`
- `Bundle`: `product_id` (unique), `slug`, `title`, `description`, `status` (same states as `Book`).
- `BundleItem`: `bundle_id`, `book_id`. Unique together.

### `Price`
| Field | Notes |
|---|---|
| `item_type`, `item_id` | `book` or `bundle`. |
| `currency` | ISO code, e.g. `NZD`. |
| `unit_amount` | Integer, minor units. |
| `stripe_product_id`, `stripe_price_id` | Set when created in Stripe (approval needed). |
| `livemode` | Test or live catalogue. |
| `active`, `valid_from`, `valid_to` | Only one active price per item and currency. |

## Orders and payments

### `Order`
| Field | Notes |
|---|---|
| `order_number` | Human-readable, unique. |
| `email` | Lower-cased. `user_id` if signed in. |
| `status` | See transitions below. |
| `currency`, `subtotal`, `tax`, `total` | Integers, minor units. |
| `stripe_checkout_session_id` | **Unique.** |
| `stripe_payment_intent_id` | |
| `livemode` | |
| `source` | `stripe` or `shopify_legacy`. |
| `created_at`, `paid_at`, `expires_at` | |

**Status transitions:**
- `pending` → `paid`, `failed` or `expired`
- `paid` → `partially_refunded`, `refunded` or `disputed`
- `partially_refunded` → `refunded`

No other transition is allowed. Every transition is written to `AuditLog`.

### `OrderItem`
`order_id`, `item_type`, `item_id`, `book_version_id` (for a book), `title_snapshot`, `unit_amount_snapshot`, `quantity`, `price_id_snapshot`.

### `PaymentEvent`
`stripe_event_id` (**unique**), `type`, `livemode`, `received_at`, `result` (`processed`, `duplicate`, `ignored`, `error`), `order_id`. Stores no card data and no full payload.

### `Refund`
`order_id`, `stripe_refund_id` (unique when present), `amount`, `reason`, `status` (`pending`, `succeeded`, `failed`), `idempotency_key` (unique), `initiated_by`.

## Access and delivery

### `Entitlement`
| Field | Notes |
|---|---|
| `email`, `user_id` | Owner of the entitlement. |
| `book_id` | A bundle purchase creates one entitlement per book. |
| `order_item_id` | Unique together with `book_id`. |
| `source` | `purchase`, `bundle`, `shopify_legacy`, `gift`, `manual`. |
| `status` | `active` or `revoked`. |
| `granted_at`, `revoked_at`, `revoke_reason` | |

### `DownloadToken`
| Field | Notes |
|---|---|
| `entitlement_id` | |
| `token_hash` | Hash only. The raw token is shown once, in the link. |
| `expires_at` | Short lifetime: `TO BE CONFIRMED`. |
| `max_uses`, `use_count`, `last_used_at` | |

A download is served only if the entitlement is `active`, the token has not expired and its uses are not exhausted. The backend function then issues a short-lived private-storage link (capability `TO BE CONFIRMED`).

## Customers and audit

### `Customer`
`email` (unique), `name`, `marketing_consent`, `consent_source`, `consent_at`. Marketing consent migrated from Shopify keeps its original source and date.

### `AuditLog`
`actor`, `action`, `entity`, `entity_id`, `summary`, `created_at`. Records are only ever added, never edited or deleted.
