---
name: humanmirror-verified-outcome
description: Get a measurable task done through HumanMirror Nexus on success-only billing — obtain a free trial key, quote the outcome for free, run it, and re-verify the result for free — over REST or the Nexus MCP server.
api: HumanMirror Nexus API / HumanMirror Outcome API
generated: '2026-09-19'
method: generated
source: openapi/humanmirror-fr-nexus-openapi.yml, openapi/humanmirror-fr-outcome-openapi.yml, mcp/humanmirror-fr-nexus-tools.json (live tools/list 2026-09-19), https://humanmirror.fr/connect/, https://humanmirror.fr/.well-known/nexus.json
operations:
  - POST /api/nexus/trial
  - GET /api/nexus/search
  - POST /api/outcome/quote/
  - POST /api/outcome/run/
  - POST /api/outcome/verify/
  - POST /api/nexus/call
---

# Run a verified outcome on success-only billing

The Nexus and Outcome contracts publish no `operationId`s, so steps cite `METHOD /path` exactly as they appear in `openapi/humanmirror-fr-nexus-openapi.yml` and `openapi/humanmirror-fr-outcome-openapi.yml`. The MCP twins are the six tools returned live by `https://humanmirror.fr/api/nexus/mcp/` (`outcome_quote`, `outcome_run`, `outcome_verify`, `nexus_search`, `magnet_resolve`, `nexus_call`).

## Before you start
- Credentials: `Authorization: Bearer hm_nexus_…`. One free trial per network origin every 90 days; buying more is `POST /api/nexus/checkout` (Stripe, 5 000 credits / 9.99 EUR) then `POST /api/nexus/claim`.
- Billing rule (nexus.json `model`): search is free, execution costs the declared per-tool credits, a failed execution is automatically refunded, and a verified outcome is charged **only on deterministic success**. Outcome = 5 credits.
- No idempotency key exists. `outcome_run` accepts an optional `contract_id` from the quote that must match the current `input`/`criteria`/`options` — use it so a retry cannot silently run a different job.

## Steps
1. **Get a key** — `POST /api/nexus/trial` (201 `Trial key created`; 409 `Trial already used` means this origin already had one — reuse the stored key).
2. **Find the capability (free)** — `GET /api/nexus/search?query=…` or MCP `nexus_search {query}`. If nothing fits, MCP `magnet_resolve {query}` (REST `POST /api/magnet/resolve`) records a sanitized capability gap instead of inventing a tool.
3. **Quote (free)** — `POST /api/outcome/quote/` with `{"objective": "…", "input": <json>, "criteria"?: {}}` (MCP `outcome_quote`). Read back the deterministic verifier, the selected internal tool, the credit cost and the `contract_id`.
4. **Run** — `POST /api/outcome/run/` with the same `input` plus `contract_id` (MCP `outcome_run`). Expect 200 with the result and a Trace receipt id; 401 `Invalid Nexus key`, 402 `Insufficient credits`, 429 `Rate limited` are the documented failures.
5. **Re-verify (free)** — `POST /api/outcome/verify/` with `{outcome_type, input, output}` (MCP `outcome_verify`) whenever you need to prove the result later without spending credits.
6. **Direct routing (optional)** — `POST /api/nexus/call` with `{"tool_id": "…", "input": …}` (MCP `nexus_call`) when you already know the catalog `tool_id`; 404 `Unknown tool` if not.

## Notes
- Smaller surfaces over the same key: `POST /api/one/run/` / MCP `humanmirror_do` (one tool, 6 credits, `dry_run: true` quotes free) and `POST /api/flow/run/` / MCP `humanmirror_flow` (2–3 step mission, 12 credits). Both refund on failure.
- USDC twin: the same outcome is sold pay-per-call as `humanmirrorX402Outcome` (`POST /api/x402/outcome/`) in the x402 contract.
