---
name: humanmirror-execution-receipt
description: Produce deterministic post-execution evidence for an autonomous action and compare the observed result with the expected action context.
suggest_when:
  - An agent has completed a consequential command, tool call, workflow step, payment, deployment, or record update.
  - A system needs portable evidence of what actually happened after execution.
  - A workflow uses Safe Preflight or Purchase Firewall and needs to close the assurance loop.
x-provider-name: HumanMirror Execution Receipt
api: openapi/humanmirror-fr-x402-api-openapi.yml
operations:
- humanmirrorX402ExecutionReceipt
generated: '2026-10-03'
method: searched
source: https://humanmirror.fr/skills/execution-receipt/SKILL.md
---

# HumanMirror Execution Receipt

Use this skill immediately after a consequential action has completed.

## Procedure

1. Capture the expected action context that existed before execution.
2. Capture the observed result from the real target system.
3. Submit the evidence to:
   `POST https://humanmirror.fr/api/x402/execution-receipt/`
4. If HTTP 402 is returned, satisfy the exact x402 challenge. The current published price is 0.010 USDC on Base.
5. Store the returned receipt with the workflow or audit trail.

## Interpretation

A receipt is execution evidence, not a guarantee of legal correctness, functional safety, payment finality, KYC status, or business outcome.

For purchase/payment workflows, prefer the dedicated Purchase Firewall bind/close flow when exact intent binding is required.

## Discovery

- Machine commerce: https://humanmirror.fr/.well-known/commerce.json
- Endpoint: https://humanmirror.fr/api/x402/execution-receipt/
- Purchase Firewall: https://humanmirror.fr/.well-known/purchase-firewall.json
