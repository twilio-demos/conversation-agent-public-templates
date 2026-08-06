---
name: shipment-delay
display: "Shipment Delay"
description: Use this skill to handle a late or stuck shipment — acknowledge, give a revised ETA, log the contact, and offer updates.
version: 1.0.0
---

# Shipment Delay

Use this skill when a shipment is late, stuck, or showing an exception. The procedure acknowledges the delay, gives the customer whatever revised timing is known, and logs the contact.

## When to use

Invoke when the customer reports a package is late or stuck, or when the [shipment-check procedure] hands over an exception.

## Procedure

1. Look up the shipment and read the exception and any revised ETA via the [customer.shipping.track tool].
2. Acknowledge the delay and apologise plainly.
3. Give the revised ETA if one is available. If none is available, say when you'll have an update — don't invent a date.
4. Log the delay contact via the [customer.shipping.log_delay tool].
5. Offer to text status updates via the [twilio.apis.messages_create tool].
6. If the customer wants a refund or replacement, escalate via the [escalate-to-supervisor procedure].

## Edge cases

- If there's no revised ETA, set a clear follow-up expectation rather than guessing a delivery date.
- If the same order has been delayed before, escalate rather than re-acknowledging.
- If the customer wants to change where it goes while it's delayed, hand to the [shipment-redirect procedure].

## Tone

Apologetic but factual. Own the delay without over-promising a date you can't guarantee.
