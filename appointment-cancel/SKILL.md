---
name: appointment-cancel
display: "Appointment Cancel"
description: Use this skill to cancel an existing appointment, capture the reason, and apply the cancellation policy.
version: 1.0.0
---

# Appointment Cancel

Use this skill when a customer wants to cancel an existing appointment. The procedure confirms which appointment, offers a reschedule first, applies the cancellation policy, and notifies both sides.

## When to use

Invoke when the customer asks to: cancel, drop, or call off an appointment. Prefer offering a reschedule before cancelling — if they'd rather move it, hand to the [appointment-reschedule procedure].

## Procedure

1. Look up the customer's current appointment by phone number via the [customer.appointments.get tool].
2. If they have more than one, confirm which appointment they mean.
3. Offer to reschedule instead of cancelling.
4. If they still want to cancel, capture the reason from the standard list: no longer needed, found another provider, timing, cost, other.
5. Check the cancellation policy (notice window, fees). If a fee applies, disclose it and get explicit confirmation to proceed — and verify the caller first via the [verify-step-up procedure] if a fee or refund is involved.
6. Cancel the booking via the [customer.appointments.cancel tool].
7. Send a cancellation confirmation SMS via the [twilio.apis.messages_create tool].
8. Notify the assigned agent or technician via internal message.

## Edge cases

- Same-day cancellations may incur a fee or need manager approval — escalate via the [escalate-to-supervisor procedure].
- If no appointment is found, confirm the phone number or name on file before giving up.
- If the appointment is already cancelled, confirm that to the customer and stop.

## Tone

Warm and non-judgemental. Offer a reschedule before cancelling, but don't pressure a customer who has decided.
