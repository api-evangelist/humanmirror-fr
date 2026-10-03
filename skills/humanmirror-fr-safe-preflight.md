---
name: humanmirror-safe-preflight
description: Deterministically inspect a proposed agent command or tool action before execution and return an execution-boundary decision.
suggest_when:
  - An AI agent is about to execute a command, tool call, deployment, update, or other consequential action.
  - A workflow needs a lightweight ALLOW, REVIEW, or BLOCK-style check before acting.
  - The caller wants a machine-native x402 security check without replacing its runtime.
x-provider-name: HumanMirror Safe Preflight
api: openapi/humanmirror-fr-x402-api-openapi.yml
operations:
- humanmirrorX402SafePreflight
generated: '2026-10-03'
method: searched
source: https://humanmirror.fr/skills/safe-preflight/SKILL.md
---

# HumanMirror Safe Preflight

Use this skill immediately before a consequential agent action.

## Procedure

1. Construct the proposed command or tool action with the relevant execution context.
2. Send it to:
   `POST https://humanmirror.fr/api/x402/safe-preflight/`
3. If the endpoint returns HTTP 402, follow the x402 payment requirements exactly. The published price is 0.010 USDC on Base for the current service.
4. After successful payment verification, read the deterministic preflight result.
5. Respect REVIEW/BLOCK conditions in the calling runtime. HumanMirror does not execute the command itself.

## Recommended loop

For high-value actions, pair Safe Preflight with an Execution Receipt after successful execution so the system checks both sides of the boundary:

`Safe Preflight → native execution → Execution Receipt`

## Discovery

- Machine commerce: https://humanmirror.fr/.well-known/commerce.json
- Products: https://humanmirror.fr/.well-known/products.json
- x402 catalog: https://humanmirror.fr/x402/catalog.json
- Endpoint: https://humanmirror.fr/api/x402/safe-preflight/

Do not interpret an HTTP 402 challenge as a completed sale or successful execution.
