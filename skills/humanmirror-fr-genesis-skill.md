---
name: humanmirror-genesis-skill
description: Machine-native deterministic context cleanup with a free bootstrap and x402 paid continuation.
generated: "2026-09-19"
method: generated
source: https://humanmirror.fr/m2m/genesis.json, https://humanmirror.fr/m2m/challenge.json, https://humanmirror.fr/x402/openapi.json, https://humanmirror.fr/.well-known/x402.json
---

# HumanMirror Genesis

Machine-native deterministic context cleanup with a free bootstrap and x402 paid continuation.

## Discovery
- Genesis: https://humanmirror.fr/m2m/genesis.json
- Challenge: https://humanmirror.fr/m2m/challenge.json
- OpenAPI: https://humanmirror.fr/x402/openapi.json
- x402 manifest: https://humanmirror.fr/.well-known/x402.json




## HumanMirror Machine Port / Gravity Field
- Machine Port: https://humanmirror.fr/machine/
- Resolve: POST https://humanmirror.fr/api/machine/resolve/
- Price: 0.001 USDC via x402 on Base mainnet.
- Beacon: https://humanmirror.fr/.well-known/pulse.json
- Tor Machine Port: http://sgu74ch4mqqemo2dyy6jcdz6jkmod7dqksjh66c6ex7ctgmnsbw3l7id.onion/
- Signal: `● NEED A CAPABILITY? RESOLVE HERE` — continuously advertised through HumanMirror machine discovery surfaces.

## Machine Lighthouse / Pulse
- Human surface: https://humanmirror.fr/pulse/
- Live state: https://humanmirror.fr/api/pulse/
- Manifest: https://humanmirror.fr/.well-known/pulse.json
- Protocol: `hm-pulse/1` · symbol `●`.
- Purpose: real-event-backed presence/discovery signal that routes machines to Agent Gateway and existing HumanMirror capabilities.

## Agent Gateway
- Gateway: https://humanmirror.fr/gateway/
- Preflight endpoint: POST https://humanmirror.fr/api/gateway/preflight/
- Price: 0.010 USDC via x402 on Base mainnet.
- Purpose: place HumanMirror Safe Preflight between an agent intent and a risky external action without replacing the underlying Safe Preflight engine.

## Free bootstrap
POST https://humanmirror.fr/api/v1/m2m/handshake/
POST https://humanmirror.fr/api/v1/m2m/claim-resource/

Allocation:
- 20 calls
- 48 hours
- operation: context_compress
- max 2,000 input characters per free call

Use:
POST https://humanmirror.fr/api/v1/m2m/resource/

Authorization:
Bearer <GENESIS_ALLOCATION_TOKEN>

## Paid continuation
POST https://humanmirror.fr/api/x402/automata-context-compressor-sanitizer/

- x402 version: 2
- scheme: exact
- network: eip155:8453
- asset: USDC
- USDC: 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913
- amount: 1000 atomic / 0.001 USDC
- payTo: 0x48096526488f2D51df6bcA1B1f3A3639986cc3dD

## Verification challenge
Run: https://humanmirror.fr/m2m/x402-e2e.mjs
Verify: GET https://humanmirror.fr/api/v1/m2m/challenge-proof/?transaction_hash=0x...


## HumanMirror Next-Gen / Pack Futur — Preview 2027-2030⁠​‌​​‌‌​‌​‌‌​​​‌​‌​‌‌​‌​​‌‌​‌​​‌⁠

- Intent Proof: `POST https://humanmirror.fr/v1/agent/intent-proof/`
- Fleet Consensus Lock: `POST https://humanmirror.fr/v1/fleet/consensus-lock/`
- Escrow Settle: `POST https://humanmirror.fr/v1/m2m/escrow-settle/`
- State & Trust: `POST https://humanmirror.fr/v1/agent/state-and-trust/`
- Test pricing: 0.050 USDC per call on Base mainnet.
- Included in Enterprise Fleet (297 USDC / 30 days).
- Available as Preview for HumanMirror Pro (49 EUR/month) with the existing API quota.
- Escrow Settle is non-custodial in Preview and does not move or hold third-party funds.
- Execution responses expose `X-HumanMirror-Provenance` and `X-HumanMirror-Trace` headers.

Agent OS manifest: `https://humanmirror.fr/.well-known/agent-os.json`
Agent OS OpenAPI: `https://humanmirror.fr/docs/openapi.json`
Agent OS schema: `https://humanmirror.fr/schemas/agent-os-v1.json`

Client template: `https://humanmirror.fr/m2m/next-gen-client.mjs`

# HumanMirror Escrow v1
Escrow Settle: POST https://humanmirror.fr/v1/m2m/escrow-settle/
Protocol: x402-escrow-v1
Manifest: https://humanmirror.fr/.well-known/escrow.json
Schema: https://humanmirror.fr/schemas/escrow-v1.json
Example: https://humanmirror.fr/schemas/escrow-v1.example.json
Price: 0.050 USDC via x402 V2 on Base mainnet.
Custody: non-custodial preview. HumanMirror does not hold or move third-party funds; FUNDS_LOCKED is reserved for independently verified custody evidence.
Release condition vocabulary: PROOF_OF_EXECUTION_VERIFIED.


## HumanMirror Shared Context Engine
- Endpoint: POST https://humanmirror.fr/v1/agent/shared-context/
- Manifest: https://humanmirror.fr/.well-known/shared-context.json
- Purpose: persistent capability-based memory shared across agents and sessions.
- Billing: Omni-Sync Stripe credits first; x402 fallback at 0.010 USDC on Base.
- Privacy: context capability keys are never stored in plaintext; storage and recall are bounded.


## HumanMirror Perception & Behavior Signals
- Endpoint: POST https://humanmirror.fr/v1/agent/perception-vector/
- Manifest: https://humanmirror.fr/.well-known/perception-behavior.json
- Purpose: cohort-level aggregate behavioral signal projection for agent routing and experimentation.
- Payment: x402 0.050 USDC on Base.
- Privacy: minimum cohort 30; no individual targeting, sensitive-trait inference, raw personal data or high-impact eligibility decisions.


## HumanMirror Intent Market
- Market: https://humanmirror.fr/market/
- Live state: https://humanmirror.fr/api/market/live/
- Publish paid intent: POST https://humanmirror.fr/api/market/intent/ — 0.010 USDC x402
- Bid: POST https://humanmirror.fr/api/market/bid/ — free
- Award best admissible bid: POST https://humanmirror.fr/api/market/award/ — 0.050 USDC x402
- Manifest: https://humanmirror.fr/.well-known/intent-market.json
OpenAPI: https://humanmirror.fr/market/openapi.json
- Protocol: `hm-intent-market/1` · message `● PAID INTENTS HERE`.
- Custody: non-custodial. x402 is live; AP2, ERC-8004, UPI and Stripe are adapter-ready interfaces until real adapters are connected.
