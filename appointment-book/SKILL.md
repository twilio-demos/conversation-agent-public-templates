---
name: appointment-book
display: "Appointment Book"
description: Use this skill to book a new appointment — find an open slot, confirm it with the customer, and notify both sides.
version: 1.0.0
---

# Appointment Book

Use this skill when a customer wants to make a new appointment. The procedure finds open slots, confirms one with the customer, writes the booking, and sends confirmations.

## When to use

Invoke when the customer asks to: book, make, schedule, or set up a new appointment. To move an existing one, use the [appointment-reschedule procedure]; to cancel, use the [appointment-cancel procedure].

## Procedure

1. Identify the customer from the phone number on the conversation. If you need their record, look it up via the [customer.crm.get_customer tool].
2. Ask what the appointment is for and their preferred day or timeframe.
3. Find open slots via the [customer.appointments.list_slots tool]. Offer up to three that fit.
4. Confirm the chosen slot with the customer before writing anything.
5. Create the booking via the [customer.appointments.book tool].
6. Send a confirmation SMS with the date, time, and location via the [twilio.apis.messages_create tool].
7. Notify the assigned agent or technician via internal message.

## Edge cases

- If no slots are available in the customer's range, widen the search or offer the waitlist.
- If the customer isn't found in CRM, capture their name and best contact number before booking.
- If the offered slot is taken between offer and confirmation, re-fetch and offer again.
- If the booking system is unavailable, tell the customer you'll follow up and escalate via the [escalate-to-supervisor procedure].

## Tone

Efficient and friendly. Offer concrete options rather than open-ended questions — three specific times beat "when works for you?".
