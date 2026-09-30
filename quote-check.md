# Quote-check: Agent Spending Controls Crosswalk

Mechanical substring check (whitespace-normalized) of every `verbatim_quote` against its fetched `evidence_url`, run on 2026-09-29. JS-rendered pages (docs.lithic.com, docs.cdp.coinbase.com's app shell, docs.skyfire.xyz, developers.circle.com, tempo.xyz, docs.crossmint.com) were rendered with Playwright (Chromium); GitHub-hosted files (AP2, x402, circlefin/skills) were fetched via `raw.githubusercontent.com` at a pinned commit SHA.

**Result: 42/48 quotes passed.** Rows that failed were dropped from `crosswalk.csv` (kept rows: 42).

| # | Provider | Evidence URL | Result |
|---|---|---|---|
| 1 | AP2 (Agent Payments Protocol) | https://raw.githubusercontent.com/google-agentic-commerce/AP2/e1ea56db72a6385bce3e5c1112b3a56ce60acb43/code/sdk/schemas/ap2/open_payment_mandate.json | PASS |
| 2 | AP2 (Agent Payments Protocol) | https://raw.githubusercontent.com/google-agentic-commerce/AP2/e1ea56db72a6385bce3e5c1112b3a56ce60acb43/code/sdk/schemas/ap2/open_payment_mandate.json | PASS |
| 3 | AP2 (Agent Payments Protocol) | https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol | PASS |
| 4 | AP2 (Agent Payments Protocol) | https://raw.githubusercontent.com/google-agentic-commerce/AP2/e1ea56db72a6385bce3e5c1112b3a56ce60acb43/code/sdk/python/ap2/sdk/constraints.py | PASS |
| 5 | Stripe | https://docs.stripe.com/api/issuing/cards/object | PASS |
| 6 | Stripe | https://docs.stripe.com/api/issuing/cards/object | PASS |
| 7 | Stripe | https://docs.stripe.com/issuing | PASS |
| 8 | Privacy.com | https://developers.privacy.com/docs/cards | PASS |
| 9 | Privacy.com | https://developers.privacy.com/docs/cards | PASS |
| 10 | Privacy.com | https://developers.privacy.com/docs/cards | PASS |
| 11 | Privacy.com | https://developers.privacy.com/docs/cards | PASS |
| 12 | Lithic | https://docs.lithic.com/docs/spend-limits | PASS |
| 13 | Lithic | https://docs.lithic.com/docs/spend-limits | PASS |
| 14 | Lithic | https://docs.lithic.com/docs/velocity-limit-rules | PASS |
| 15 | Lithic | https://docs.lithic.com/docs/velocity-limit-rules | PASS |
| 16 | Lithic | https://docs.lithic.com/docs/velocity-limit-rules | PASS |
| 17 | Lithic | https://docs.lithic.com/docs/authorization-rules-v2 | PASS |
| 18 | Lithic | https://docs.lithic.com/docs/authorization-rules-v2 | PASS |
| 19 | AgentCard | https://docs.agentcard.sh/api-reference/cards/create | FAIL |
| 20 | AgentCard | https://docs.agentcard.sh/issuing/issuing-a-card | FAIL |
| 21 | AgentCard | https://docs.agentcard.sh/issuing/issuing-a-card | FAIL |
| 22 | AgentCard | https://docs.agentcard.sh/api-reference/cards/create | FAIL |
| 23 | AgentCard | https://docs.agentcard.sh/tools/cli/cards-set-limit | PASS |
| 24 | Crossmint | https://docs.crossmint.com/agents/overview | PASS |
| 25 | Crossmint | https://docs.crossmint.com/agents/overview | PASS |
| 26 | Coinbase | https://docs.cdp.coinbase.com/agentic-wallet/mcp/faq | PASS |
| 27 | Coinbase | https://docs.cdp.coinbase.com/agentic-wallet/mcp/faq | PASS |
| 28 | Coinbase | https://docs.cdp.coinbase.com/agentic-wallet/mcp/faq | PASS |
| 29 | Circle | https://raw.githubusercontent.com/circlefin/skills/58ab8648bb1ae9d037a3bf5197ad3bb01262f5b1/plugins/circle/skills/agent-wallet-policy/SKILL.md | FAIL |
| 30 | Circle | https://raw.githubusercontent.com/circlefin/skills/58ab8648bb1ae9d037a3bf5197ad3bb01262f5b1/plugins/circle/skills/agent-wallet-policy/SKILL.md | PASS |
| 31 | Circle | https://raw.githubusercontent.com/circlefin/skills/58ab8648bb1ae9d037a3bf5197ad3bb01262f5b1/plugins/circle/skills/agent-wallet-policy/SKILL.md | PASS |
| 32 | Circle | https://raw.githubusercontent.com/circlefin/skills/58ab8648bb1ae9d037a3bf5197ad3bb01262f5b1/plugins/circle/skills/agent-wallet-policy/SKILL.md | PASS |
| 33 | Circle | https://developers.circle.com/agent-stack/agent-wallets | PASS |
| 34 | Tempo | https://tempo.xyz/developers/docs/wallet/use-with-agents | PASS |
| 35 | Tempo | https://tempo.xyz/developers/docs/protocol/transactions/AccountKeychain | PASS |
| 36 | Tempo | https://tempo.xyz/developers/docs/protocol/transactions/AccountKeychain | FAIL |
| 37 | Tempo | https://tempo.xyz/developers/docs/protocol/transactions/AccountKeychain | PASS |
| 38 | Payman | http://web.archive.org/web/20251118161108/https://docs.paymanai.com/dashboard-guide/policies | PASS |
| 39 | Payman | http://web.archive.org/web/20251118161108/https://docs.paymanai.com/dashboard-guide/policies | PASS |
| 40 | Payman | http://web.archive.org/web/20251118161108/https://docs.paymanai.com/dashboard-guide/policies | PASS |
| 41 | Skyfire | https://docs.skyfire.xyz/docs/pay-token | PASS |
| 42 | Skyfire | https://docs.skyfire.xyz/docs/pay-token | PASS |
| 43 | Skyfire | https://docs.skyfire.xyz/docs/common-token-claims | PASS |
| 44 | x402 | https://raw.githubusercontent.com/coinbase/x402/dd927a26cfefc98c24b3ec38b3a8f204dad0c60d/specs/transports-v1/http.md | PASS |
| 45 | x402 | https://raw.githubusercontent.com/coinbase/x402/dd927a26cfefc98c24b3ec38b3a8f204dad0c60d/specs/schemes/upto/scheme_upto.md | PASS |
| 46 | x402 | https://raw.githubusercontent.com/coinbase/x402/dd927a26cfefc98c24b3ec38b3a8f204dad0c60d/specs/schemes/upto/scheme_upto.md | PASS |
| 47 | Visa | https://developer.visa.com/use-cases/visa-intelligent-commerce-for-agents | PASS |
| 48 | Mastercard | http://web.archive.org/web/20260918180921/https://www.mastercard.com/us/en/business/artificial-intelligence/mastercard-agent-pay/agent-pay-for-machines.html | PASS |

## Review additions (2026-09-29)
- Stripe amount_cap_per_period: evidence → https://docs.stripe.com/issuing/controls/spending-controls, quote "Spending limit rules limit the total amount of spending for categories over intervals of time." PASS (the fetched page text).
- Stripe amount_cap_per_tx (new): quote "spending_controls[spending_limits][0][interval]=per_authorization" PASS (the raw page source, cURL example).
- x402 maxAmountRequired: control_type changed to `other` (a server-declared price, not a payer-side limit).
