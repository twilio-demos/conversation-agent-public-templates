---
name: flight-status-points
display: "Flight Status & Points"
description: Use this skill to read a traveller's loyalty tier and points/miles balance and progress to the next tier.
version: 1.0.0
---

# Flight Status & Points

Use this skill when a traveller asks about their frequent-flyer status or points balance. The procedure reads their loyalty record and explains their standing.

## When to use

Invoke when the traveller asks about: their tier or status, miles/points balance, or how close they are to the next tier.

## Procedure

1. Identify the member — ask for the frequent-flyer number, or look it up via the [customer.loyalty.get_status tool].
2. Read the tier, points/miles balance, and progress to the next tier from the [customer.loyalty.get_status tool].
3. Tell the traveller their status and balance in plain language.
4. Offer to text a summary via the [twilio.apis.messages_create tool].

## Edge cases

- If the account isn't found, confirm the number or the traveller's name.
- If recent activity hasn't posted yet, note that some miles may still be pending.
- If the traveller wants to redeem points or book an award, that's a different flow — escalate via the [escalate-to-supervisor procedure].

## Tone

Friendly. This is good news for most travellers — deliver the balance and any next-tier progress clearly.
