---
name: flight-seat-select
display: "Flight Seat Select"
description: Use this skill to choose or change a seat, disclosing any fee and collecting payment for paid seats.
version: 1.0.0
---

# Flight Seat Select

Use this skill when a traveller wants to choose or change a seat. The procedure reads the seat map, discloses any fee, and assigns the seat.

## When to use

Invoke when the traveller asks to pick a seat, change seats, or get extra legroom.

## Procedure

1. Look up the booking via the [customer.pnr.lookup tool].
2. Confirm which passenger and segment.
3. Read available seats via the [customer.flight.seatmap tool] and describe the options — window/aisle, extra legroom.
4. If the chosen seat carries a fee, disclose it; for a paid seat, verify the caller via the [verify-step-up procedure], then collect payment via the [take-phone-payment procedure] on voice or a payment link on messaging.
5. Assign the seat via the [customer.flight.assign_seat tool].
6. Confirm and text the seat assignment via the [twilio.apis.messages_create tool].

## Edge cases

- If the chosen seat is taken between reading the map and assigning, re-read and offer again.
- For exit-row seats, confirm the passenger meets the eligibility rules.
- On a basic-economy fare with no free selection, explain the restriction.
- If a paid seat's payment fails, leave the current seat unchanged and offer to retry or escalate via the [escalate-to-supervisor procedure].

## Tone

Friendly and concrete about any fee. Don't assign a paid seat before payment clears.
