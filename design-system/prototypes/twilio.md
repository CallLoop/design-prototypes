# 05 · Twilio integration

[← Design system index](../README.md) · [Foundations](../01-foundations.md) · Prototype: [CallLoop-Twilio-Prototype.html](../../CallLoop-Twilio-Prototype.html)

Clickable rework of the Figma design "16 Integrations – Twilio Integration" (Jira [CWR-4577](https://callloop.atlassian.net/browse/CWR-4577)). It differs from the first version in three ways:

1. **One flow.** Connecting Twilio leads straight into choosing numbers. Integrations → Connect opens the **Connect Twilio** modal (unchanged from the Figma design). Apply connects the account and opens the [03 · Buy number](buy-number.md) dialog on Twilio → "In your account". In the Buy number dialog, a not-yet-connected Twilio shows a **Connect** button that opens the same modal on top of the dialog. Once connected, the Twilio card becomes a normal source card and is selected.
2. **No plan difference.** Trial and paid accounts connect the same way. There is no release warning and no "create a new account" detour. Call Loop numbers keep working next to Twilio numbers.
3. **Two sources, one UI.** The Buy number dialog has a source picker (Call Loop or Twilio). Both sources share the Local and Toll-Free tabs and the number finder. Twilio adds an "In your account" tab for numbers the customer already has there.

Use the prototype's **Twilio: Not connected / Connected** switch (top right) to start from either state.

## How the source is made clear

The source has one visual language everywhere it appears. The **Call Loop** mark is the brand-blue "C", and the **Twilio** mark is the Twilio logo with the account name.

| Place | What it shows |
|---|---|
| Source picker (step 1, top) | The Twilio card carries the same **New** badge after its name. Two stacked full-width radio cards with the mark, the name and a second line saying where the number lives and who bills it. Call Loop: "$5.00/month per number, billed by Call Loop". Twilio: "Numbers in your Twilio account. Call Loop charges a $5.00/month fee". This line is the same on every tab and never shows a Twilio price. Selection uses the DS blue for both, so the marks carry identity and the blue carries state |
| Destination strip (Payment only) | The source mark and "Bought from **Call Loop**" / "Bought in your **Twilio** account **callloop**" / "Uses numbers in your **Twilio** account", with the monthly price and who bills it. On the Choose step the source cards carry this line instead, so the dialog fits without scrolling |
| Payment | The same strip at the top, a Source column in the selected-numbers table, then the costs split into **Charged by Call Loop** (card, fee, proration) and **Charged by Twilio** (number rental billed to the Twilio account). Existing Twilio numbers show only the Call Loop part |
| Primary button | "Buy number" (Call Loop), "Buy in Twilio" (new Twilio number), "Add N numbers" (existing Twilio numbers) |
| Toast | "1 number bought from Call Loop" / "1 number bought in Twilio (callloop)" / "2 Twilio numbers added to Call Loop" |
| Numbers page | Kept exactly as the live page (incl. CWR-4595). The only change is the integration's logo (16px) after the type, e.g. "Local" + Twilio logo. Hovering or focusing it shows "From your Twilio account callloop"; screen readers hear "Twilio number". When more integrations arrive, each shows its own logo, so the column names the exact provider instead of a generic word. New rows are highlighted after a purchase |

## Screens and states

| Screen / state | How to reach it | Notes |
|---|---|---|
| Integrations list | Default | Twilio card first, with a **New** badge in the top-right corner, styled like the live app's (same as Native: `--purple3` / `--purple1`). When connected it sits left of the ⋯ menu. Not connected: Connect. Connected: a `callloop` pill, "N numbers in Call Loop", and a ⋯ menu (Add Twilio numbers, Edit credentials, Docs, Disconnect) |
| Connect Twilio modal | Integrations → Connect, or the Connect button on the Twilio card in Buy number | The Figma credentials modal: Twilio logo, "Connect Twilio", info alert, API Key and API Token (show/hide), Apply (disabled until both are filled) / Cancel. From Buy number it opens on top of the dialog and returns to it with Twilio connected and selected. From Integrations, Apply opens Buy number on Twilio → "In your account" (kicker "Twilio integration"). The Buy number dialog always has 2 steps |
| Buy number · Twilio not connected | Numbers → Buy number before connecting | The Twilio row has no radio: logo, "Twilio", "Connect your account to use or buy numbers in it" and a **Connect** button. Call Loop stays selected |
| Choose number · Call Loop | Buy number (default source) | Same as 03 · Buy number: Local / Toll-Free tabs, 10DLC and toll-free alerts, Country, City / Area code, digit filter, radio list |
| Choose number · Twilio · In your account | Default Twilio tab after connecting | No alert (the Twilio card says the numbers stay in Twilio). Multi-select table (Phone number, Type, Bought in Twilio). Numbers already in Call Loop are dimmed with an "In Call Loop" tag. Search, "Hide added", Sync |
| Choose number · Twilio · Local / Toll-Free | Tabs | Same finder and list as Call Loop, with a different inventory. The alerts tell the customer to register 10DLC or verify toll-free in their Twilio account |
| Payment | Continue | Destination strip, selected numbers with Source, then a Call Loop charge block and, for new Twilio numbers, a Twilio charge block |
| Done | Buy / Add | Closes the dialog and lands on Numbers (filter All) with the new rows highlighted. A number bought in Twilio also shows up under "In your account" |
| Edit Twilio connection | ⋯ → Edit credentials | Prefilled credentials |
| Disconnect Twilio | ⋯ → Disconnect | Toggles for Twilio phone numbers, Triggers and Broadcasts. Disconnect turns on once all three are off. It removes only Twilio numbers, and the copy says Call Loop numbers aren't affected |
| Disconnect number | Not reachable in this version | Designed ("Stays in your Twilio account", affected-features list, acknowledgement), but the live Numbers page has no row actions. It needs an entry point (see open questions) |

### Removed in this rework

- The paid-plan release warning ("Before you connect Twilio") and its acknowledgement
- The `/new-organization` screen that was reached from that warning
- The Trial / Paid prototype switch
- The connect step inside the Buy number dialog (tried and dropped; connecting uses its own modal again)
- The "External" purple chip on Numbers, replaced by the Twilio logo after the type

## Design-system components used

| Component | Variant(s) | Where |
|---|---|---|
| Sidebar | UI Kit/Sidebar | Left rail |
| Button | Primary, Primary disabled, Secondary | Cards, dialogs |
| Input | Default, password with eye; stacked finder | Connect step, Local / Toll-Free |
| Select | Leading icon (flag, card brand), badge | Country, Card |
| Alert | Info (`--notify2`) with title and body | Every step |
| Tabs | Master/Tabs, with a count pill | Dialog number type, Numbers source filter |
| Radio card | **New:** source picker card (mark, title, sub, radio dot) | Buy number step 1 |
| Destination strip | **New:** `--g4` row with source mark, title and billing line | Top of Payment |
| Source chip | **New:** `srcchip.cl` / `srcchip.tw` | Payment table only |
| New badge | As in the live app: `--purple3` background, `--purple1` text, 12px, radius 6px | Twilio integration card (top right), Twilio source card |
| Switch, Checkbox | — | Hide added, number picker, disconnect toggles, acknowledgement |
| Dropdown | Card ⋯ menu | Twilio card |

## Tokens used

Text `--black`, `--g1`, `--g2`; surfaces `--g4`, `--blue5`; borders `--g3`, `--g2`; accents `--blue1`–`--blue4`, `--blue6`, `--blue1-dis`; states `--ok`, `--ok2`, `--ok3`, `--warn2`, `--err`, `--err3`, `--notify2`; effects `--shadow1`. The Buy number dialog uses `--dlg-w` (494px).

## Deviations from the design system

| Value | Where | Why / proposed action |
|---|---|---|
| Dialog top padding 24px (03 · Buy number uses 32px), kicker gap 16px, overlay inset 24px, source card padding 8px 12px; 10DLC and toll-free alert bodies shortened to one sentence | Buy number dialog | So every step fits a 900px-tall window without scrolling. Apply the same to 03 · Buy number if accepted |
| `#F22F46` | Twilio mark | Brand colour, stays local |
| Overlay `rgba(20,22,26,.2)`; toast `rgba(20,22,26,.92)` | Backdrop, toast | Same as 03 · Buy number. Consider a `--scrim` token |
| Font size 13px | Dialog kicker, destination strip | Not on the scale. Use S2 (12) or S1 (14) |
| Source picker card, destination strip, source chip | Buy number dialog | New patterns. If accepted, add them to Foundations and to Figma "00 Design System" |

## Open questions

- **Pricing for Twilio numbers.** The prototype charges a $5/month Call Loop fee per Twilio number (the Figma payment step for external numbers). Twilio's rental ($1.15 local / $2.15 toll-free) is shown for illustration. Confirm the fee and whether Call Loop should show Twilio's price at all, since it can change.
- **10DLC / toll-free verification for Twilio-bought numbers.** Does Call Loop register them, or does the customer do it in Twilio? The prototype's alert says "in your Twilio account".
- **Default source.** Buy number opens on Call Loop. Should it open on Twilio once Twilio is connected?
- **Mixed cart.** One purchase is one source. Should the customer be able to buy Call Loop and Twilio numbers in one checkout?
- **Disconnecting one Twilio number.** The live Numbers page has no row actions. Where should "Disconnect number" live: the number's edit page, or a row ⋯ menu?
- **Disconnect copy.** Confirm that disconnecting Twilio leaves Call Loop numbers, and the triggers and broadcasts that use them, untouched.
- Figma spells it "Twillio" in several places; the prototype uses "Twilio". Fix in Figma?
