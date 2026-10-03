---
name: HumanMirror Purchase Firewall
description: Bind an autonomous purchase or payment intent before execution, then reconcile the observed result afterward.
suggest_when:
  - An AI agent is about to make or authorize a purchase, payment, checkout, or transaction.
  - A system needs evidence that the transaction actually executed matches the buyer-approved intent.
  - A workflow needs authorization-to-execution drift detection without replacing the payment provider.
---

# HumanMirror Purchase Firewall

Use this skill around consequential autonomous purchases.

## Before execution

1. Gather the exact action the agent intends to execute: merchant/provider, amount, asset/currency, network, cart or quote state, target and any relevant policy context.
2. Call the HumanMirror bind endpoint:
   `POST https://humanmirror.fr/api/value/bind/`
3. Preserve the returned bind identifier with the workflow state.
4. Do not treat the bind as settlement, custody, signing authority, KYC, or payment authorization.

## Execute normally

Let the existing checkout, wallet, PSP, merchant, 0x quote flow, UCP flow, or other native execution path run normally.

HumanMirror does not sign, custody funds, broadcast transactions, or replace the payment rail.

## After execution

1. Gather the observed result: transaction hash, merchant response, amount, destination, order state or equivalent evidence.
2. Call:
   `POST https://humanmirror.fr/api/value/close/`
3. Inspect the resulting MATCH / DRIFT evidence.
4. Escalate DRIFT to the caller or policy layer instead of silently treating the action as authorized.

## Discovery

- Purchase Firewall: https://humanmirror.fr/.well-known/purchase-firewall.json
- Machine commerce: https://humanmirror.fr/.well-known/commerce.json
- 0x firm Quote adapter: https://humanmirror.fr/api/value/0x-bind/
- UCP adapter: https://humanmirror.fr/api/value/ucp-bind/

Use HumanMirror as execution evidence around the native payment stack, not as a financial guarantee.
