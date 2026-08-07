---
name: appointment-reschedule
display: "Appointment Reschedule"
description: Use this skill to move an existing appointment to a new time slot.
version: 1.0.0
---

# Appointment Reschedule

Use this skill when a customer wants to move an existing appointment. The procedure validates the new slot, updates the booking system, and notifies both parties.

## When to use

Invoke when the customer asks to: reschedule, move, change time, push back, or bring forward an appointment. For cancellations, use the [appointment-cancel procedure].

## Procedure

1. Look up the customer's current appointment by phone number via the [customer.appointments.get tool].
2. Ask the customer for their preferred new time. Offer 3 nearby slots if they are flexible.
3. Validate the slot using the [customer.appointments.list_slots tool].
4. Update the booking via the [customer.appointments.reschedule tool].
5. Send a confirmation SMS to the customer with the new date and time via the [twilio.apis.messages_create tool].
6. Notify the assigned agent or technician via internal message.

## Edge cases

- If the new slot is more than 30 days out, confirm the customer still wants the appointment at all.
- Same-day reschedules require manager approval — escalate.
- If the customer is more than 15 minutes late to confirm, the offered slot may be taken; re-validate.
