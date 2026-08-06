---
name: verify-step-up
display: "Step-up Verification (2FA)"
description: Verify the caller's identity with a one-time passcode before a sensitive action. Reusable as a swap target from any procedure.
version: 1.0.0
---

# Step-up Verification (2FA)

Use this procedure to confirm the caller is who they say they are before doing anything sensitive. It sends a one-time passcode via Twilio Verify, checks the caller's read-back, and returns control to the procedure that requested step-up.

This is a shared gate. Other procedures reference `[verify-step-up procedure]` when they need a verified caller — the agent loads this playbook mid-call, verifies, and continues. It is loaded mid-conversation, so it does not greet the caller.

## When to use

Invoke before any account-specific or irreversible action: payments, refunds, cancellations that carry a fee, address or account changes. Also invoke when another procedure swaps in for step-up.

## Procedure

1. Read the caller's phone number from the active conversation. Validate it and get its E.164 form via the [twilio.apis.lookups_fetch tool]; if it comes back invalid, don't attempt a send — confirm the number with the caller or escalate.
2. Send a passcode to that number via the [twilio.apis.verify_send tool] with `channel: sms` (or `channel: call` if the caller is on a line that cannot receive SMS).
3. Ask the caller to read back the code they received.
4. Validate the code via the [twilio.apis.verify_check tool].
5. On `valid: true`, tell the caller they're verified and continue with the action they came for (the procedure that requested step-up resumes).
6. On `valid: false`, allow one retry — re-check the newly spoken code; only re-send via the [twilio.apis.verify_send tool] if the code has expired. After a second failure, escalate via the [escalate-to-supervisor procedure].

## Edge cases

- If the passcode never arrives by SMS (e.g. a landline or VoIP number that can't receive text), resend on the voice channel with `channel: call`, or escalate.
- If the code has expired, re-send once before counting it as a failed attempt.
- On a voice call, confirm the digits back to the caller before checking — mishears are the most common failure.
- Never read the passcode aloud yourself; the caller reads it to you.

## Tone

Calm and security-forward. Keep it brief — one line on why you need to verify, then move. Don't lecture the caller about security.
