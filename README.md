# conversation-agent-public-templates

Community-contributable starter procedures for Twilio Conversation Agent. Fork these into your
workspace as starting points, then bind the abstract `customer.*` tool labels to your own systems.
PRs welcome.

New here? Read **[TEMPLATE-GUIDE.md](TEMPLATE-GUIDE.md)** — it covers the `SKILL.md` schema, the
`twilio.*` vs `customer.*` label rule, and how procedures reference each other.

## Templates

### Core
| Template | What it does |
|---|---|
| [verify-step-up](verify-step-up/) | Twilio Verify OTP gate — a reusable step-up any sensitive action can require |
| [escalate-to-supervisor](escalate-to-supervisor/) | Reassure, recall prior context, hand to a human only if still needed |

### Appointment
| Template | What it does |
|---|---|
| [appointment-book](appointment-book/) | Book a new appointment — find a slot, confirm, notify |
| [appointment-reschedule](appointment-reschedule/) | Move an existing appointment to a new slot |
| [appointment-cancel](appointment-cancel/) | Cancel an appointment, capture reason, apply policy |

### Shipment
| Template | What it does |
|---|---|
| [shipment-check](shipment-check/) | Look up status and ETA |
| [shipment-confirm](shipment-confirm/) | Confirm a delivery was received |
| [shipment-delay](shipment-delay/) | Handle a late/stuck shipment |
| [shipment-redirect](shipment-redirect/) | Change the destination (verified) |
| [shipment-delivery-instructions](shipment-delivery-instructions/) | Capture safe-place / neighbour / access instructions |

### Flight
| Template | What it does |
|---|---|
| [flight-check](flight-check/) | Flight status — times, gate, delays |
| [flight-change](flight-change/) | Rebook to a chosen flight, collect fare difference |
| [flight-earlier-later](flight-earlier-later/) | Find earlier/later options, hand to `flight-change` |
| [flight-seat-select](flight-seat-select/) | Choose or change a seat (paid seats collect payment) |
| [flight-status-points](flight-status-points/) | Loyalty tier and points balance |

### Payments
| Template | What it does |
|---|---|
| [take-phone-payment](take-phone-payment/) | Agent-assisted card capture on a live voice call (voice only) |

### Commerce
| Template | What it does |
|---|---|
| [refund-eligibility](refund-eligibility/) | Assess refund eligibility and route to next action |
| [returns-intake](returns-intake/) | Capture return reason, condition, and reverse-logistics lane |

## Contributing

1. Read [TEMPLATE-GUIDE.md](TEMPLATE-GUIDE.md).
2. Add a directory named for your slug, containing one `SKILL.md`.
3. Use `twilio.*` labels for Twilio platform tools (real twilio-mcp names) and `customer.*` for
   systems the forker binds.
4. Name a failure path (usually `[escalate-to-supervisor procedure]`) and gate sensitive actions
   behind `[verify-step-up procedure]`.
5. Open a PR.
