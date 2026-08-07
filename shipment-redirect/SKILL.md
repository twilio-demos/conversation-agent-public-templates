---
name: shipment-redirect
display: "Shipment Redirect"
description: Use this skill to change a shipment's destination — a new address, a hold, or a pickup point.
version: 1.0.0
---

# Shipment Redirect

Use this skill when a customer wants to change where a shipment is delivered. Because redirecting a package is an address change, verify the caller before writing the new destination.

## When to use

Invoke when the customer asks to: change the delivery address, redirect, hold at a depot, or send to a pickup point.

## Procedure

1. Look up the shipment via the [customer.shipping.get tool].
2. Check it's still redirectable — not already out for delivery and not past the carrier's cutoff.
3. Verify the caller via the [verify-step-up procedure] before changing the destination.
4. Collect the new address or pickup location.
5. Confirm the new destination back to the customer before writing.
6. Submit the redirect via the [customer.shipping.redirect tool].
7. Send confirmation of the new destination via the [twilio.apis.messages_create tool].

## Edge cases

- If the shipment is past the carrier's cutoff or already out for delivery, it can't be redirected — explain, offer the next-best option (hold, reschedule), or escalate via the [escalate-to-supervisor procedure].
- If the new address fails validation, re-collect it.
- If the redirect carries a fee, disclose it and get explicit confirmation before submitting.

## Tone

Efficient, and careful with the address — read the new destination back clearly, since it's easy to mishear.
