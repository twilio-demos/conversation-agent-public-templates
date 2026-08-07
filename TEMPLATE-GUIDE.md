# Authoring Guide — Procedure Templates

How to write a template others can fork. One `SKILL.md` per directory.

## File shape

The directory name is the slug. Inside it, a single `SKILL.md` = frontmatter + markdown body.

```
---
name: appointment-book          # kebab slug, unique in this repo, no `twilio.` prefix
display: "Appointment Book"      # human label shown in the app
description: <one line>          # the LLM reads this to decide when to swap this playbook in
version: 1.0.0
---
```

On fork, the runtime rewrites `name` → `<org.id>.<slug>`. The `twilio.` prefix is reserved for
Twilio-published templates — don't use it here.

## Body sections

- `# Title`
- one-paragraph intro — what the procedure does
- `## When to use` — trigger phrases / conditions; point at sibling procedures for adjacent intents
- `## Procedure` — numbered steps
- `## Edge cases` — optional but expected
- `## Tone` — optional

## Tool references — the label rule

Reference tools as prose in square brackets. Two namespaces:

| Prefix | Who provides it | Bind on fork? | Examples |
|---|---|---|---|
| `twilio.*` | Twilio platform (via twilio-mcp) | No — Twilio-side | `[twilio.apis.verify_send tool]`, `[twilio.apis.messages_create tool]`, `[twilio.apis.lookups_fetch tool]`, `[twilio.apis.agent_pay_start tool]` |
| `customer.*` | The customer's own systems (MCP tunnel) | Yes — after fork | `[customer.appointments.book tool]`, `[customer.shipping.track tool]` |

Label form: `[<namespace>.<service>.<verb> tool]`. The Twilio platform side is always the fixed
3-segment **`twilio.apis.<tool>`** — `twilio` (author attestation) + `apis` (the MCP server name) +
the real twilio-mcp tool name (see the twilio-mcp README's Tools table). Don't drop the `apis`
segment, and don't invent `twilio.<tool>` — the runtime won't resolve it.

Templates stay abstract — do **not** write `{{ tool: }}` tokens or a `references[]` array. Those
are produced inside the app after fork, when the customer binds each label to a live connector via
the comment/Review flow.

## Referencing other procedures

`[<slug> procedure]` — e.g. `[verify-step-up procedure]`, `[escalate-to-supervisor procedure]`. At
runtime this becomes a swap chip: the agent can load that playbook mid-call without telling the
caller. Use it for:

- a shared gate every sensitive action needs → `[verify-step-up procedure]`
- the failure path → `[escalate-to-supervisor procedure]`
- handing to a sibling verb → `flight-earlier-later` → `[flight-change procedure]`

A swap target is loaded mid-conversation, so **don't write greetings or self-introductions** in
its body — the agent is already talking to the caller.

## Conventions

- Sensitive actions (payments, refunds, account/address changes) require `[verify-step-up procedure]` first.
- Every procedure names a failure path — usually `[escalate-to-supervisor procedure]`.
- Confirm with the caller before any irreversible write (booking, cancel, charge).
- Match the voice of the existing templates: concise, direct, no filler.

## Channel notes

Most procedures run on voice and messaging. Agent-assisted payment (`take-phone-payment`) is
**voice only** — the `agent_pay_*` tools need a live call SID.
