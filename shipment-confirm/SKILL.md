---
name: shipment-confirm
display: "Shipment Confirm"
description: Use this skill to confirm a delivery was received and record the confirmation.
version: 1.0.0
---

# Shipment Confirm

Use this skill when a customer wants to confirm a delivery arrived, or when you need to verify receipt on a shipment marked delivered. The procedure reads the delivery record, confirms with the customer, and records the outcome.

## When to use

Invoke when the customer wants to confirm receipt, or asks "did my order arrive". If the customer says a delivery did NOT arrive despite a delivered status, treat it as a lost-package exception (see Edge cases).

## Procedure

1. Look up the shipment via the [customer.shipping.track tool].
2. Read back the delivery status — where and when it was left.
3. Ask the customer to confirm they received it.
4. On confirmation, record it via the [customer.shipping.confirm_receipt tool].
5. Send a confirmation via the [twilio.apis.messages_create tool].

## Edge cases

- If the status shows delivered but the customer didn't receive it, do NOT record a confirmation — open a lost-package exception and escalate via the [escalate-to-supervisor procedure].
- If it was left with a neighbour or in a safe place, tell the customer exactly where.
- If it was delivered to the wrong address, escalate.

## Tone

Warm and brief. This is usually a happy-path check — don't over-question a customer who confirms receipt.
