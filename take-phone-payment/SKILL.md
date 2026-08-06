---
name: take-phone-payment
display: "Take Phone Payment (Agent-Assisted)"
description: Capture a card payment on a live voice call using Twilio Agent-Assisted Payments. Voice channel only.
version: 1.0.0
---

# Take Phone Payment (Agent-Assisted)

Use this procedure to take a card payment while on a live voice call. It drives Twilio's
Agent-Assisted Payments (`agent_pay_*`) so the caller keys their card digits directly into Twilio — you never see or hear the full card number, and it stays out of the transcript and recordings.

**Voice channel only.** The `agent_pay_*` tools need a live call SID, so this procedure cannot run on SMS, WhatsApp, or chat. It also requires a Pay Connector (Stripe, Braintree, etc.) configured on the Twilio account.

## When to use

Invoke when a caller on a voice call wants to pay — a bill, a balance, a paid seat or upgrade handed over from another procedure. For messaging channels, send a secure payment link instead (out of scope for this template).

## Procedure

1. If the caller has not already been verified on this call, load the [verify-step-up procedure] first. Do not take a payment from an unverified caller.
2. Confirm the amount and what it is for. If you need the balance, read it via the [customer.billing.get_balance tool].
3. Tell the caller you'll take their card securely now, and that you won't see the full number. Ask them to have the card ready.
4. Start the capture via the [twilio.apis.agent_pay_start tool]. It returns a `paymentSid` — hold both the `callSid` and `paymentSid`; every following step needs them.
5. Capture the card number via the [twilio.apis.agent_pay_capture_card tool]. Reassure the caller while they key the digits.
6. Capture the expiry date via the [twilio.apis.agent_pay_capture_exp tool].
7. Capture the security code via the [twilio.apis.agent_pay_capture_cvc tool].
8. Read back the masked card state (last four digits, expiry) and confirm the amount once more.
9. Finalise via the [twilio.apis.agent_pay_complete tool] to tokenise or charge. Tell the caller the outcome.
10. Send a payment confirmation or receipt via the [twilio.apis.messages_create tool].

## Edge cases

- If the [twilio.apis.agent_pay_start tool] errors, the account likely has no Pay Connector configured — apologise and escalate via the [escalate-to-supervisor procedure]. Do not attempt to collect card details any other way.
- On a caller-input error (mis-keyed digits, timeout), re-run only that capture step with the same `paymentSid` — do not restart from the [twilio.apis.agent_pay_start tool]. After a second failure on the same field, escalate.
- On a declined card or processor error, do NOT silently retry. Tell the caller it didn't go through and offer to try a different card — a different card needs a fresh [twilio.apis.agent_pay_start tool] — or abandon the payment and escalate.
- For a one-shot capture where you don't need to talk the caller through it, the [twilio.apis.voice_pay tool] emits a TwiML `<Pay>` IVR that Twilio runs end-to-end — use it when no live back-and-forth is needed.
- PCI: never repeat card digits aloud, never write them into any note or field, and never ask the caller to say the number out loud — the whole point is that Twilio captures the digits, not you.

## Tone

Calm, precise, reassuring. Paying over the phone makes people nervous — say what each step is before it happens, and confirm the outcome clearly at the end.
