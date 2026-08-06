---
name: flight-check
display: "Flight Check"
description: Use this skill to look up a flight's status — times, gate, and delays — and read it back to the traveller.
version: 1.0.0
---

# Flight Check

Use this skill when a traveller wants to know the status of a flight on their booking. The procedure looks up the booking, reads the current status, and offers to text the gate and times.

## When to use

Invoke when the traveller asks: is my flight on time, what gate, departure or arrival time, or is it delayed. To change the flight, use the [flight-change procedure]; to choose a seat, use the [flight-seat-select procedure].

## Procedure

1. Identify the booking — ask for the record locator (PNR), or look it up via the [customer.pnr.lookup tool].
2. Read the flight's current status via the [customer.flight.status tool] — departure and arrival times, gate, and any delay.
3. Tell the traveller the status in plain language.
4. Offer to text the gate and times via the [twilio.apis.messages_create tool].
5. If the flight is delayed or cancelled and they want to rebook, hand to the [flight-earlier-later procedure].

## Edge cases

- If the PNR isn't found, confirm the locator or the traveller's name; if it still can't be located, escalate via the [escalate-to-supervisor procedure].
- If the booking has multiple segments, give the status of each.
- If a schedule change has already been applied, point it out.

## Tone

Quick and factual. Lead with the answer.
