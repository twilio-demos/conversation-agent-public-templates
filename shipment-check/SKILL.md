---
name: shipment-check
display: "Shipment Check"
description: Use this skill to look up a shipment's status and expected delivery date and read it back to the customer.
version: 1.0.0
---

# Shipment Check

Use this skill when a customer wants to know where their order is. The procedure looks up the shipment, reads the current status and ETA, and offers to text a tracking link.

## When to use

Invoke when the customer asks: where's my order, track my package, delivery status, or when will it arrive. To confirm a delivery happened, use the [shipment-confirm procedure]; to handle a late package, use the [shipment-delay procedure]; to change the destination, use the [shipment-redirect procedure].

## Procedure

1. Identify the shipment — ask for the order or tracking number, or look it up by phone via the [customer.shipping.track tool].
2. Read the current status and expected delivery date from the [customer.shipping.track tool].
3. Tell the customer the status and ETA in plain language.
4. Offer to text the tracking link via the [twilio.apis.messages_create tool].
5. If the shipment shows an exception or is past its ETA, hand to the [shipment-delay procedure].

## Edge cases

- If the customer has more than one active shipment, confirm which one they mean.
- If no tracking is found, confirm the order number; if it still can't be located, escalate via the [escalate-to-supervisor procedure].
- If the status is delivered but the customer says they didn't receive it, hand to the [shipment-confirm procedure].

## Tone

Quick and reassuring. Lead with the answer — status and date — before any detail.
