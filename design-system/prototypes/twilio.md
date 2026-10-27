# 05 · Twilio integration

[← Design system index](../README.md) · [Foundations](../01-foundations.md) · Prototype: [CallLoop-Twilio-Prototype.html](../../CallLoop-Twilio-Prototype.html)

Clickable version of the Figma design "16 Integrations – Twilio Integration" (Jira [CWR-4577](https://callloop.atlassian.net/browse/CWR-4577)): connecting your own Twilio account, using its numbers in Call Loop, and disconnecting. On top of the design, it adds separate trial and paid-plan connect flows. Paid accounts see a warning that their Call Loop numbers will be released.

## Screens and states

| Screen / state | How to reach it | Notes |
|---|---|---|
| Integrations list | Default | Twilio card first; "Connect" or a connected pill (`callloop`) with a ⋯ menu |
| **Release warning (paid only)** | Plan switch → Paid, then Twilio → Connect | New, not in Figma. Says toll-free and local numbers will be released, what happens, two ways to keep them (port out via support, create a new account at `/new-organization`), and an acknowledgement checkbox that gates Continue |
| New organization (`/new-organization`) | Paid warning → "Create a new account" | Full-screen onboarding step "Tell us about your company": company name (required) + team size; Continue enabled once both are set. ✕ goes back. Continue creates a trial org and lands on Integrations, where Twilio connects with no warning |
| Connect Twilio | Trial: Connect. Paid: Continue on the warning | API Key + API Token (show/hide). Apply stays disabled until both are filled |
| Edit Twilio connection | ⋯ → Edit | Prefilled credentials |
| Disconnect Twilio | ⋯ → Disconnect | Phone numbers / Triggers / Broadcasts toggles; Disconnect enabled once all three are off |
| Numbers list | Sidebar → Numbers | External numbers get an "External" chip and a disconnect action |
| Buy number → Manage external number | Numbers → Buy number | Step 1: pick Twilio numbers, already added ones disabled, "Hide added numbers" switch. Empty state with a link to Integrations when Twilio isn't connected |
| Buy number → Payment | Continue | Selected list (collapsible), card, monthly total / unused time / charged today |
| Disconnect number | Trash/unlink icon on an External row | Affected features list + destructive acknowledgement |
| Toasts | After connect, disconnect, buy | Paid connect toast says how many numbers were released |

## Design-system components used

| Component | Variant(s) | Where |
|---|---|---|
| Sidebar | UI Kit/Sidebar, plan card (Free Trial / Pro Monthly) | Left rail |
| Button | Primary, Secondary, disabled | Cards, modals |
| Input | Default, password with eye | Connect / Edit |
| Alert | Info (`--notify2`), Warning (`--warn4` / `--warn3`) | Modals |
| Switch, Checkbox | — | Disconnect toggles, number picker, acknowledgements |
| Dropdown | Card ⋯ menu | Twilio card |
| Tabs | Master/Tabs | Buy number modal |

## Tokens used

Text `--black`, `--g1`, `--g2`; surfaces `--g4`, `--blue5`; borders `--g3`; accents `--blue1`, `--blue3`, `--purple1`/`--purple3` (External chip); states `--ok`, `--ok3`, `--warn1`–`--warn4`, `--err`, `--err3`, `--notify2`; effects `--shadow1`.

## Deviations from the design system

| Value | Where | Why / proposed action |
|---|---|---|
| `#F22F46` | Twilio logo | Brand colour, stays local |

## Open questions

- Paid warning: should Continue be blocked while the account has active broadcasts that are sending?
- Figma spells it "Twillio" in several places; the prototype uses "Twilio". Fix in Figma?
- The Figma frame "If account exists" (a dead end with "Got it") is replaced in the prototype by the paid-plan warning. Confirm with design.
