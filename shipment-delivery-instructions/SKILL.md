---
name: shipment-delivery-instructions
display: "Shipment Delivery Instructions"
description: Use this skill to capture delivery instructions — a safe place, a neighbour, an access code, or a preferred time.
version: 1.0.0
---

# Shipment Delivery Instructions

Use this skill when a customer wants to tell the carrier how to deliver — leave it in a safe place, with a neighbour, or behind a gate. The procedure confirms the address, captures the instruction, and saves it.

## When to use

Invoke when the customer asks to: leave in a safe place, leave with a neighbour, not ring the bell, use a gate/access code, or set a preferred delivery window. To change the address itself, use the [shipment-redirect procedure].

## Procedure

1. Look up the shipment via the [customer.shipping.get tool].
2. Confirm the delivery address on file with the customer.
3. Capture the instruction — safe place, neighbour, access code, or preferred time.
4. Save it via the [customer.shipping.set_instructions tool].
5. Confirm back what will happen and text a copy via the [twilio.apis.messages_create tool].

## Edge cases

- If the shipment is already out for delivery, the instruction may not apply to today's delivery — say so.
- If the instruction means leaving a package unattended, note the carrier may still require a signature and won't cover loss.
- For gate or access codes, confirm the digits back.
- If the instruction can't be saved, escalate via the [escalate-to-supervisor procedure].

## Tone

Helpful and concrete. Read the instruction back exactly as it will be sent to the carrier.
