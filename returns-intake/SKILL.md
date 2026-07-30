---
name: returns-intake
display: "Returns Intake"
description: Use this skill to capture return reason, item condition, and routing for inbound product returns.
version: 0.4.1
---

# Returns Intake

Use this skill when a customer wants to return a physical item. The procedure collects the data needed to generate a return label and route the item to the right reverse-logistics lane.

## When to use

Invoke when the customer mentions: return, send back, exchange, doesn't fit, or wrong item. Do not use for refunds without a physical return — use refund-eligibility for those.

## Procedure

1. Confirm the order and item being returned.
2. Ask for the return reason from the standard list: damaged, defective, wrong item, doesn't fit, changed mind.
3. Ask the condition of the item: unopened, opened-unused, used, damaged.
4. Decide the lane:
   - Damaged or defective → quality lane (no restocking fee).
   - Unopened → restock lane.
   - Opened-unused or used → inspection lane.
5. Generate a return label using the create-return-label tool.
6. Send the label to the customer's email on file.

## Tone

Be efficient. Customers returning items want this to be fast — do not editorialize on why they are returning.
