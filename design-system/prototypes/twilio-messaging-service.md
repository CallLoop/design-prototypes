# 08 · Twilio Messaging Service

[← Design system index](../README.md) · [Foundations](../01-foundations.md) · Prototype: [CallLoop-TwilioMessagingService-Prototype.html](../../CallLoop-TwilioMessagingService-Prototype.html)

Adds a required **Messaging Service** selector to the Buy number modal when the provider is Twilio (Jira [CWR-4778](https://callloop.atlassian.net/browse/CWR-4778), design [CWR-4779](https://callloop.atlassian.net/browse/CWR-4779)). Since CWR-4728 the backend needs `messagingServiceSid` to buy or reserve a number in the customer's Twilio account. The list comes from `getCustomerTwilioMessagingServices`. The UI says **Broadcast** (`BRAND_NAME`).

The dark bar at the bottom switches the Twilio account between several services, one, none and a load error, and the number between paid and the first free one.

## Screens and states

| Screen / state | How to reach it | Notes |
|---|---|---|
| Choose provider | Opens first | Twilio selected and connected, as in the live modal |
| Choose number · Local | Continue | Current structure kept: 10DLC alert, Country, area code + digit filter, 4 numbers in one column (160px list), Refresh. Messaging Service field below the list |
| Choose number · Toll-Free | Toll-Free tab | Toll-free alert, digit filter, 12 numbers in a 3 × 4 grid, Messaging Service field below |
| Choose number · In your account | First tab | No selector: those numbers keep their current Twilio service, shown in the list |
| Messaging Service · open | Click the field | Name + SID per option, search when more than 5, Refresh in the footer |
| Messaging Service · empty | Default | Nothing is pre-selected, even with one service. Continue / Confirm disabled until a number and a service are chosen |
| Messaging Service · loading | Switching scenario | Disabled field with spinner |
| Messaging Service · none | "No services" | Warning alert with Refresh only, no external links. Primary button disabled |
| Messaging Service · load error | "Load error" | Inline error with "Try again" |
| Payment | Continue (paid) | Messaging Service row with a Change link back to Choose number |
| Done | Buy number, or Confirm (first free number) | "{number} is ready to use. It's in the {service} Messaging Service in your Twilio account." |

## Design-system components used

| Component | Variant(s) | Where |
|---|---|---|
| Button | Primary / Secondary Medium, ghost link | Actions, Refresh, Change |
| Alert | Notify, Warning | 10DLC / toll-free alerts, no-services state |
| Tabs | Default | In your account / Local / Toll-Free |
| Radio | Small | Available numbers |
| Select | Two-line value (name + SID) | Messaging Service |

## Tokens used

Text `--black`, `--g1`; surfaces `#fff`, `--g4`, `--blue5`; borders `--g3`, `--g2`; accents `--blue1`, `--blue3`, `--blue6`; states `--notify2`, `--warn4`, `--warn1`, `--warn3`, `--err`; effects `--shadow1`.

## Deviations from the design system

| Value | Where | Why / proposed action |
|---|---|---|
| Monospace 11px SID line | Select value and options | No mono text style in the DS. Keep local or add a caption-mono style |
| 13px number text | Toll-Free grid | Lets three numbers fit per row at the 494px dialog width. Check against the live grid |

## Open questions

- On purchase the backend sets `UseInboundWebhookOnNumber=true` on the chosen service, which affects other numbers already in it. Product decision pending (noted in CWR-4778).
