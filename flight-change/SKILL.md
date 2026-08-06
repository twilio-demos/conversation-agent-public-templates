---
name: flight-change
display: "Flight Change"
description: Use this skill to rebook a traveller onto a specific chosen flight, disclosing fees and collecting any fare difference.
version: 1.0.0
---

# Flight Change

Use this skill when a traveller wants to change to a specific flight they've already chosen. The procedure discloses the cost, verifies the caller, rebooks, and collects any fare difference.

## When to use

Invoke when the traveller has a target flight in mind. To browse earlier or later options first, use the [flight-earlier-later procedure], which hands back here once they've chosen.

## Procedure

1. Look up the booking via the [customer.pnr.lookup tool].
2. Confirm which segment they're changing and the target flight.
3. Check the fare difference and any change fee; disclose the total to the traveller.
4. Verify the caller via the [verify-step-up procedure] before rebooking or taking payment.
5. Get explicit confirmation to proceed at the quoted price.
6. Rebook via the [customer.flight.rebook tool].
7. If a fare difference is owed, collect it via the [take-phone-payment procedure] on a voice call, or send a payment link on messaging.
8. Send the updated itinerary via the [twilio.apis.messages_create tool].

## Edge cases

- If the requested fare class is unavailable, offer the nearest available and re-quote.
- If the fare is non-changeable, or the booking is an award/miles ticket, explain the rules and escalate via the [escalate-to-supervisor procedure].
- If payment fails, do not rebook — leave the original flight intact and offer to retry or escalate.

## Tone

Clear about cost before acting. Quote the total, get a yes, then change — never rebook before the traveller has agreed to the price.
