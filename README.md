# Agent Spending Controls Crosswalk (2026) — by Pink Agentic AI Payments

> [!NOTE]
> **Published by Pink Agentic AI Payments (by PinkWallet)** — the approval layer between AI agents and company money: plain-language rules, per-agent budgets and human approvals decide each payment before it executes. Agents connect via MCP or REST. **Try the free public sandbox:** https://agentic-sandbox.pinkwallet.com (test credentials, no real money moves) · Product: https://pinkwallet.com/agentic/ · Examples: https://github.com/Pink-Agentic-Payments/sandbox-examples
>
> As of v1.1.0, Pink is **included** as a row in `crosswalk.csv` and in the summary table below, under the same evidence rules as every other row (quoted, sourced, mechanically checked — see `quote-check.md`). Pink's rows are self-documented by the publisher, labeled as such, and scoped to its early-access public sandbox (production not yet available). See ["How Pink Agentic AI Payments compares"](#how-pink-agentic-ai-payments-compares) below.

Every payment provider and protocol that lets you cap what an AI agent can spend uses its own field names, units, and enforcement point — there is no shared standard. This crosswalk maps 14 providers/protocols (AP2, Stripe Issuing, Privacy.com, Lithic, AgentCard, Crossmint, Coinbase CDP, Circle, Tempo, Payman, Skyfire, x402, Visa Intelligent Commerce, Mastercard Agent Pay) + the publisher (Pink Agentic AI Payments) to the exact field or setting they document for amount caps, allowlists, category blocks, and approval requirements, each with a quoted source.

Also available on Hugging Face: https://huggingface.co/datasets/Agentic-Payment/agent-spending-controls-crosswalk (with the dataset viewer).

## How Pink Agentic AI Payments compares

Counted directly from the ✓ marks in the summary table below: Pink documents **7 of the 8** control types in this crosswalk (per-tx cap, per-period cap, merchant/recipient allowlist, category block, single-use, human approval, expiry); it does not document a separate call to revoke one already-issued credential (an agent can be paused, which is a different, agent-level control — see the `revocation` row for Pink in `crosswalk.csv`). Among the other 14 providers/protocols, the most any single one documents is **5** (AgentCard: per-tx cap, per-period cap, allowlist, single-use, human approval).

That is a count of breadth across this crosswalk's 8 categories, not a quality ranking — see "Where Pink is behind" below, and judge every row, including Pink's, by its own quoted source in `crosswalk.csv`.

**Depth the 8 columns don't capture.** These are specific things Pink's own docs describe, cited so you can check them yourself — not claims about what other providers lack:

- **Company-wide daily ceiling across all agents**, checked as a circuit breaker before any rule runs: "Company daily ceiling. All agents together, per day." ([policy-rules-reference](https://pinkwallet.com/agentic/developers/policy-rules-reference/))
- **Ordered rules with a default-block fallback**: breakers first, then rules top to bottom, first match wins, and anything no rule covers is blocked by default. ([policy-rules-reference](https://pinkwallet.com/agentic/developers/policy-rules-reference/))
- **n-of-m group approvers** for a single rule, e.g. a documented example rule requiring 2 of 3 executives above $50,000: `"approvers": {"group": "g_exec", "n": 2}`. ([policy-rules-reference](https://pinkwallet.com/agentic/developers/policy-rules-reference/))
- **Payee-bank-change and duplicate-invoice fraud signals** evaluated on every request regardless of amount, via `requires`/`absent` evidence flags `payeeChanged` and `dupInvoice`. ([security-model](https://pinkwallet.com/agentic/developers/security-model/), [policy-rules-reference](https://pinkwallet.com/agentic/developers/policy-rules-reference/))

**Where Pink is behind.** Pink is **early access**: production is explicitly not available yet ("Sandbox live... Production is not yet available" appears across the developer docs), credentials are test values (a 4111 1111 test-range card BIN, sandbox bank-transfer references), and evidence flags like `po`/`scan` are self-asserted by the calling agent in the sandbox rather than verified against a connected ERP/warehouse system. Pink does not document a per-credential revocation call (see `revocation` row above) — only agent-level pause.

## How to read the table

`crosswalk.csv` has one row per control (a provider may have several: a per-transaction cap, a merchant lock, an approval threshold, etc.). Columns:

- **control_type** — one of `amount_cap_per_tx`, `amount_cap_per_period`, `merchant_allowlist`, `category_block`, `single_use`, `human_approval`, `expiry`, `revocation`, `other`
- **field_or_setting** — the exact name as documented. Where a provider only describes a control in marketing language, with no API/schema field name published, this says `not documented` rather than guessing.
- **unit / period_options** — minor units (cents), major units, USDC, currency-agnostic, etc., and any interval choices (daily/weekly/monthly/…), as stated by the source.
- **enforcement_point** — where the cap is actually checked: authorization-time at the card network, onchain, API server-side, or client-side SDK/CLI.
- **evidence_url / verbatim_quote / accessed_date** — the exact source and quote, so you can verify it yourself.

## Summary: provider × control type

14 providers/protocols + the publisher (Pink Agentic AI Payments).

| Provider | Per-tx cap | Per-period cap | Merchant/recipient allowlist | Category block | Single-use | Human approval | Expiry | Revocation |
|---|---|---|---|---|---|---|---|---|
| **Pink Agentic AI Payments** (publisher; self-documented; sandbox stage) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | — |
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

### How Pink does it, per control type

Sourced from [policy-rules-reference](https://pinkwallet.com/agentic/developers/policy-rules-reference/) and [security-model](https://pinkwallet.com/agentic/developers/security-model/), consistent with Pink's row in the table above:

| Control type | Pink | How |
|---|---|---|
| Per-tx cap | ✓ | A rule's `amount.max` with `window: "tx"` — e.g. a per-payment cap on an agent. |
| Per-period cap | ✓ | Per-agent monthly budget, plus a company-wide daily ceiling checked across all agents before any rule runs. |
| Merchant/recipient allowlist | ✓ | The rule `payee` field: `any` \| `approved` \| `new` \| `cat:<category>` \| an explicit list. |
| Category block | ✓ | A `cat:blocked` payee match with `action: "block"` — e.g. the documented rule "Never: gift cards, cash-like, crypto." |
| Single-use | ✓ | Approved payments return a single-use virtual card or bank-transfer credential locked to the payee and the amount. |
| Human approval | ✓ | An `action: "ask"` rule with named approvers or an n-of-m quorum (e.g. "2 of 3 executives" over $50,000). |
| Expiry | ✓ | Issued credentials expire 15 minutes after issue. |
| Revocation | — | Not documented as a separate per-credential revoke call; Pink documents pausing the agent itself, which is a different, agent-level control (see "Where Pink is behind" above). |

## Try Pink Agentic AI Payments in 2 minutes

Create a free sandbox workspace with one call, no sales contact:

```
curl -X POST https://agentic-sandbox.pinkwallet.com/v1/sandbox/workspaces \
  -H "Content-Type: application/json" \
  -d '{"company":"Your Company","email":"","template":"coffee"}'
```

This report's companion dataset, [agentic-payments-readiness](https://github.com/Pink-Agentic-Payments/agentic-payments-readiness#try-pink-agentic-ai-payments-in-2-minutes), ran this live on 2026-10-02 and documents the full walkthrough: connecting an agent via MCP, and the three real decision outcomes (`allowed` / `pending_human` / `blocked`) with trimmed sandbox responses. Sandbox, test credentials, no real money moves — production is not yet available.

## How Pink decides a payment

Quoted from [policy-rules-reference](https://pinkwallet.com/agentic/developers/policy-rules-reference/): "A policy is an ordered list of rules plus three circuit breakers. Every payment request is checked the same way: breakers first, then rules top to bottom, first match decides, and anything no rule covers is blocked."

1. Agent registered?
2. Agent active (not paused)?
3. Monthly budget not exceeded?
4. Company daily ceiling not exceeded (all agents together)?
5. Vault balance sufficient?
6. Rules, top to bottom — first match wins.
7. Default: block.

## Pink console (sample data)

![Policy rules editor](https://pinkwallet.com/agentic/img/console-policies.webp)
*Policy rules editor, shown in evaluation order (Pink console, sample data).*

![Pending approvals queue](https://pinkwallet.com/agentic/img/console-approvals.webp)
*Pending "ask a person" approvals (Pink console, sample data).*

## Gotchas

- **AP2's unit mismatch**: `amount_range.max` is documented in the schema as minor units ("cents"), but `budget.max` has no unit stated in its own schema text — the reference SDK's `BudgetEvaluator` multiplies `budget.max` by 100 to get minor units, implying `budget.max` is actually in **major** units. This is a live discrepancy across AP2's own schema files, not a crosswalk error. See `crosswalk.csv` rows 2 and the source repo (pinned commit `e1ea56d`).
- **Circle's monotonic rule**: Circle's CLI enforces `per-tx ≤ daily ≤ weekly ≤ monthly` — you cannot set a per-transaction cap higher than the daily cap, etc.
- **Circle's OTP handoff**: raising or resetting a Circle agent-wallet limit requires a human-entered OTP in an interactive terminal; the agent is explicitly instructed not to see or relay it.
- **x402's `amount` is phase-dependent** in the `upto` scheme: the same JSON field means "authorized maximum" at verification time and "actual amount to charge" at settlement time — read the phase, not just the field name.
- **"Not documented" is common** at the marketing layer: several programs (Coinbase CDP's TEE/enclave enforcement claims, Visa Intelligent Commerce, Mastercard Agent Pay) describe spend limits in prose without a public field-level schema. Don't assume a schema exists just because a blog post mentions "spending limits."

## Methodology

Rows were kept only when a provider's own documentation, spec, or reference SDK/API stated the control — no third-party blog posts or unverified aggregator pages were used as primary evidence. Every `verbatim_quote` was mechanically substring-matched (whitespace-normalized) against the text of its `evidence_url`, fetched on 2026-09-29: GitHub-hosted specs (AP2, x402, Circle's `circlefin/skills`) were fetched via `raw.githubusercontent.com` at a pinned commit SHA so the quotes stay reproducible even if the repo changes; JS-rendered documentation sites (docs.lithic.com, docs.skyfire.xyz, developers.circle.com, tempo.xyz, docs.cdp.coinbase.com, docs.crossmint.com) were rendered with Playwright/Chromium before extraction. Two official pages (`docs.paymanai.com`, `www.mastercard.com`) were unreachable directly at check time (a Cloudflare origin SSL error and Akamai bot-blocking, respectively) — for those two rows only, a Wayback Machine snapshot of the same official page is cited instead, and the substitution is disclosed in the row's `notes` column. See `quote-check.md` for the full pass/fail table (42/42 kept rows passed; 6 rows that failed the mechanical check were dropped rather than fixed by hand). A review pass on 2026-09-29 replaced the Stripe Issuing evidence with the spending-controls guide (https://docs.stripe.com/issuing/controls/spending-controls) and added a per_authorization row: 43 rows in total. In v1.1.0 (2026-10-02), 8 rows for the publisher, Pink Agentic AI Payments, were added under the same rules — fetched live, mechanically quote-checked (8/8 passed, see `quote-check.md`), and labeled self-documented in `notes`: 51 rows in total.

## Conflict of interest

Published by Pink Agentic AI Payments (by PinkWallet, early access) — see the note at the top of this README. Pink **is included** in `crosswalk.csv` as of v1.1.0, under the same evidence rules as every other row: self-documented by the publisher, quoted, sourced, and mechanically quote-checked (see `quote-check.md`), with `notes` on every Pink row stating "Publisher (PinkWallet), self-documented."

Try the free public sandbox (test credentials, no real money moves): https://agentic-sandbox.pinkwallet.com

## Related PinkWallet datasets

- [agentic-ai-payments](https://github.com/Pink-Agentic-Payments/agentic-ai-payments) — an open developer guide to agentic AI payments, including this crosswalk's control types
- [agentic-payments-readiness](https://github.com/Pink-Agentic-Payments/agentic-payments-readiness)
- [awesome-agentic-payments](https://github.com/Pink-Agentic-Payments/awesome-agentic-payments)

## License

CC BY 4.0 — reuse with attribution.

## Corrections

Found a stale field name, a wrong unit, or a provider that's changed its docs? Open an issue with the URL and the exact quote you're disputing.

## Changelog

- **v1.2.0 (2026-10-02):** expanded publisher (Pink) sections — a "How Pink does it" note per control type under the summary table, a 2-minute trial block, the decision order, and 2 console screenshots. No data changes for other providers.
- **v1.1.0 (2026-10-02):** added the publisher (Pink Agentic AI Payments) under the same evidence rules; title updated; no other rows changed.
- **v1.0.0 (2026-09-29):** initial release, 43 rows across 14 providers/protocols.
