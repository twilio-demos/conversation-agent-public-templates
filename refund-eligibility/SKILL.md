---
name: refund-eligibility
display: "Refund Eligibility"
description: Use this skill to assess whether a customer order is eligible for a refund based on age, payment state, and channel.
version: 1.2.0
---

# Refund Eligibility

Use this skill when a customer asks for a refund or disputes a charge. The procedure walks through three eligibility gates and routes to the appropriate next action.

## When to use

Invoke this skill when the customer message mentions any of: refund, money back, charge dispute, return for credit, or cancel and refund.

## Procedure

1. Look up the most recent order for the customer using the [customer phone] and the [get-recent-orders tool].
2. Check the order age. Orders older than 30 days are not eligible for a self-serve refund and must be escalated per the [Escalation SOP].
3. Confirm the order status is one of: delivered, shipped, or returned.
4. If all gates pass, issue the refund via the [issue-refund tool].
5. If any gate fails, explain why and offer the closest alternative (store credit, exchange, or escalation).

## Edge cases

- Subscription orders follow a different policy and should not be processed by this skill — see the [Subscription Refunds SOP].
- Gift orders should be confirmed with the [original purchaser email] before any refund is issued.
- Partial refunds for damaged items should use the [damage-claim SOP] instead.

## Tone

Be direct and apologetic. Customers asking for refunds are usually frustrated; do not over-explain policy. Confirm the action you are about to take before taking it.
