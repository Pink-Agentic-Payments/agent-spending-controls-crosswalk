# Agent Spending Controls Crosswalk (2026)

Every payment provider and protocol that lets you cap what an AI agent can spend uses its own field names, units, and enforcement point — there is no shared standard. This crosswalk maps 14 providers/protocols (AP2, Stripe Issuing, Privacy.com, Lithic, AgentCard, Crossmint, Coinbase CDP, Circle, Tempo, Payman, Skyfire, x402, Visa Intelligent Commerce, Mastercard Agent Pay) to the exact field or setting they document for amount caps, allowlists, category blocks, and approval requirements, each with a quoted source.

Also available on Hugging Face: https://huggingface.co/datasets/Agentic-Payment/agent-spending-controls-crosswalk (with the dataset viewer).

## How to read the table

`crosswalk.csv` has one row per control (a provider may have several: a per-transaction cap, a merchant lock, an approval threshold, etc.). Columns:

- **control_type** — one of `amount_cap_per_tx`, `amount_cap_per_period`, `merchant_allowlist`, `category_block`, `single_use`, `human_approval`, `expiry`, `revocation`, `other`
- **field_or_setting** — the exact name as documented. Where a provider only describes a control in marketing language, with no API/schema field name published, this says `not documented` rather than guessing.
- **unit / period_options** — minor units (cents), major units, USDC, currency-agnostic, etc., and any interval choices (daily/weekly/monthly/…), as stated by the source.
- **enforcement_point** — where the cap is actually checked: authorization-time at the card network, onchain, API server-side, or client-side SDK/CLI.
- **evidence_url / verbatim_quote / accessed_date** — the exact source and quote, so you can verify it yourself.

## Summary: provider × control type

| Provider | Per-tx cap | Per-period cap | Merchant/recipient allowlist | Category block | Single-use | Human approval | Expiry | Revocation |
|---|---|---|---|---|---|---|---|---|
| AP2 | ✓ | ✓ | — | — | — | ✓ | — | — |
| Stripe Issuing | ✓ | ✓ | — | ✓ | — | — | — | — |
| Privacy.com | ✓ | ✓ | ✓ | — | ✓ | — | — | — |
| Lithic | — | ✓ | ✓ | ✓ | — | — | — | — |
| AgentCard | ✓ | ✓ | ✓ | — | ✓ | ✓ | — | — |
| Crossmint | — | — | — | — | — | — | — | ✓* |
| Coinbase CDP | ✓ | ✓ | — | — | — | — | — | — |
| Circle | ✓ | ✓ | ✓ | — | — | ✓ | — | — |
| Tempo | ✓ | ✓ | — | — | ✓ | — | ✓ | — |
| Payman | ✓ | ✓ | — | — | — | ✓ | — | — |
| Skyfire | ✓ | — | — | — | — | — | ✓ | — |
| x402 | ✓† | — | — | — | — | — | — | — |
| Visa Intelligent Commerce | — | — | — | — | — | — | — | — |
| Mastercard Agent Pay | — | — | — | — | — | — | — | — |

† x402: the `upto` scheme's authorized maximum is a per-request ceiling; `maxAmountRequired` (v1 `exact`) is a price set by the resource server, not a payer-side budget. Payer-side caps have to live in the client or wallet.

\* Crossmint's own docs describe allowances as "scoped, explicit, and revocable" but do not publish the specific field name for revocation on the page cited here — see `crosswalk.csv` notes.

Visa Intelligent Commerce and Mastercard Agent Pay are included because both are named agent-payment programs with public statements that spend limits exist, but as of 2026-09-29 neither had a public developer reference with a concrete field name for a spend-limit parameter — both rows are marked `not documented` rather than guessed.

## Gotchas

- **AP2's unit mismatch**: `amount_range.max` is documented in the schema as minor units ("cents"), but `budget.max` has no unit stated in its own schema text — the reference SDK's `BudgetEvaluator` multiplies `budget.max` by 100 to get minor units, implying `budget.max` is actually in **major** units. This is a live discrepancy across AP2's own schema files, not a crosswalk error. See `crosswalk.csv` rows 2 and the source repo (pinned commit `e1ea56d`).
- **Circle's monotonic rule**: Circle's CLI enforces `per-tx ≤ daily ≤ weekly ≤ monthly` — you cannot set a per-transaction cap higher than the daily cap, etc.
- **Circle's OTP handoff**: raising or resetting a Circle agent-wallet limit requires a human-entered OTP in an interactive terminal; the agent is explicitly instructed not to see or relay it.
- **x402's `amount` is phase-dependent** in the `upto` scheme: the same JSON field means "authorized maximum" at verification time and "actual amount to charge" at settlement time — read the phase, not just the field name.
- **"Not documented" is common** at the marketing layer: several programs (Coinbase CDP's TEE/enclave enforcement claims, Visa Intelligent Commerce, Mastercard Agent Pay) describe spend limits in prose without a public field-level schema. Don't assume a schema exists just because a blog post mentions "spending limits."

## Methodology

Rows were kept only when a provider's own documentation, spec, or reference SDK/API stated the control — no third-party blog posts or unverified aggregator pages were used as primary evidence. Every `verbatim_quote` was mechanically substring-matched (whitespace-normalized) against the text of its `evidence_url`, fetched on 2026-09-29: GitHub-hosted specs (AP2, x402, Circle's `circlefin/skills`) were fetched via `raw.githubusercontent.com` at a pinned commit SHA so the quotes stay reproducible even if the repo changes; JS-rendered documentation sites (docs.lithic.com, docs.skyfire.xyz, developers.circle.com, tempo.xyz, docs.cdp.coinbase.com, docs.crossmint.com) were rendered with Playwright/Chromium before extraction. Two official pages (`docs.paymanai.com`, `www.mastercard.com`) were unreachable directly at check time (a Cloudflare origin SSL error and Akamai bot-blocking, respectively) — for those two rows only, a Wayback Machine snapshot of the same official page is cited instead, and the substitution is disclosed in the row's `notes` column. See `quote-check.md` for the full pass/fail table (42/42 kept rows passed; 6 rows that failed the mechanical check were dropped rather than fixed by hand). A review pass on 2026-09-29 replaced the Stripe Issuing evidence with the spending-controls guide (https://docs.stripe.com/issuing/controls/spending-controls) and added a per_authorization row: 43 rows in total.

## Conflict of interest

Published by PinkWallet, which is building **Pink Agentic AI Payment** (early access). PinkWallet is not included in this dataset.

## Related PinkWallet datasets

- [agentic-payments-readiness](https://github.com/Pink-Agentic-Payments/agentic-payments-readiness)
- [awesome-agentic-payments](https://github.com/Pink-Agentic-Payments/awesome-agentic-payments)

## License

CC BY 4.0 — reuse with attribution.

## Corrections

Found a stale field name, a wrong unit, or a provider that's changed its docs? Open an issue with the URL and the exact quote you're disputing.
