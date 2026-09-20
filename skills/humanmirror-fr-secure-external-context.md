---
name: humanmirror-secure-external-context
description: Put HumanMirror's security stack between untrusted external content and an agent action — quarantine prompt injection, scan for leaked secrets, preflight the proposed tool call, then bind the result to an execution receipt — paying per call in USDC over x402.
api: HumanMirror x402 API / HumanMirror Sanitize Shield
generated: '2026-09-19'
method: generated
source: openapi/humanmirror-fr-x402-openapi.yml, openapi/humanmirror-fr-sanitize-shield-openapi.yml, https://humanmirror.fr/index.html.md ("Recommended security policy"), live 402 probe 2026-09-19
operations:
  - discoverSanitizeShield
  - sanitizeShield
  - humanmirrorX402SecretScanning
  - humanmirrorX402SafePreflight
  - humanmirrorX402ExecutionReceipt
---

# Secure external context before an agent acts

HumanMirror's own recommended order (index.html.md) is: untrusted context -> Sanitize Shield; code/config/logs/tool output -> Secret Scanning; proposed command or tool call -> Safe Preflight; successful action -> Execution Receipt. Every operation below is a real operationId in `openapi/`.

## Before you start
- Base URL is `https://humanmirror.fr`. There is no sandbox: the free quota calls and the paid calls both run in production (`sandbox/humanmirror-fr-sandbox.yml`).
- Paid routes use **x402 v2**: the first call without a `PAYMENT-SIGNATURE` header returns **402** with a `PAYMENT-REQUIRED` header (base64 JSON: `accepts[].amount`, `payTo`, `network eip155:8453`, USDC asset). Authorize exactly that amount (EIP-3009) and retry with `PAYMENT-SIGNATURE`. Settlement happens only after success; **422 settles nothing**.
- Errors are `{error, code, retryable}` (`errors/humanmirror-fr-problem-types.yml`). There is **no idempotency key** — do not blindly retry a paid POST after a timeout without checking the receipt (`conventions/humanmirror-fr-conventions.yml`).

## Steps
1. **Read the free contract** — `GET /api/v1/sanitize/shield/` (`discoverSanitizeShield`). Returns `max_input_bytes` (65536), `test_quota {calls: 3, window_hours: 24}` and the Enterprise-pass terms. Respect `x-humanmirror-free-quota: 3;w=86400`.
2. **Quarantine the external content** — `POST /api/v1/sanitize/shield/` (`sanitizeShield`) with `{"input": <bounded text or JSON>}`. Free for 3 calls/24h, then 0.001 USDC. Expect a verdict `CLEAN | REVIEW | QUARANTINED` and a signed Cleanliness Proof. Stop on `QUARANTINED`.
3. **Scan what you are about to send or commit** — `POST /api/x402/secret-scanning/` (`humanmirrorX402SecretScanning`), body `{"input": ..., "criteria"?: {}, "options"?: {}}`. 0.010 USDC. A secret-bearing payload must not leave the boundary.
4. **Preflight the action** — `POST /api/x402/safe-preflight/` (`humanmirrorX402SafePreflight`) with the proposed command or tool call. 0.010 USDC. Proceed only within the declared risk limit.
5. **Bind the outcome** — after the action succeeds, `POST /api/x402/execution-receipt/` (`humanmirrorX402ExecutionReceipt`) with the input/output pair. 0.010 USDC. Keep the receipt; `X-HumanMirror-Trace` / `X-HumanMirror-Provenance` headers on responses carry the digest and HMAC.

## Notes
- Bundle alternative: `POST /api/v1/agent/security-intelligence/` (`purchaseSecurityIntelligence`, 5.000 USDC) is the thematic bundle the granular routes upsell to (`x-humanmirror-canonical-bundle`).
- Cheaper unlimited path: the Enterprise Fleet pass (`purchaseEnterpriseFleet`, 297 USDC / 30 days) removes the per-call 402 on Sanitize Shield, Payload Normalizer and Consensus Oracle only — not on the three `/api/x402/` routes above.
- Same capabilities over MCP: none of these four are MCP tools; the closest MCP surface is `list_humanmirror_x402_services` on `https://humanmirror.fr/api/x402/mcp/`, which returns the same prices and example bodies (`mcp/humanmirror-fr-tool-crosswalk.yml`).
