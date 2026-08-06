---
name: flight-earlier-later
display: "Flight Earlier / Later"
description: Use this skill to find earlier or later flight options for a traveller and hand the chosen one to rebooking.
version: 1.0.0
---

# Flight Earlier / Later

Use this skill when a traveller wants to move to an earlier or later flight but hasn't picked one yet. The procedure searches alternatives and offers options; the actual change is done by the [flight-change procedure].

## When to use

Invoke when the traveller asks to get on an earlier or later flight, or wants to know what else is available on their route today.

## Procedure

1. Look up the booking via the [customer.pnr.lookup tool].
2. Ask whether they want earlier or later, and any time constraint (e.g. must land before 6pm).
3. Search alternatives via the [customer.flight.search_alternatives tool].
4. Offer up to three options with times and any fare difference.
5. When the traveller picks one, hand to the [flight-change procedure] to confirm the price and rebook.

## Edge cases

- If there are no alternatives in their window, widen the search or offer standby if the carrier supports it.
- If they qualify for a same-day change program, mention it.
- If every option costs more, say so before they choose.
- If nothing works and the traveller is stuck, escalate via the [escalate-to-supervisor procedure].

## Tone

Helpful and option-oriented. Give concrete choices with times and cost, not open-ended questions.
