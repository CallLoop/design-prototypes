# 03 · Buy number

[← Design system index](../README.md) · [Foundations](../01-foundations.md) · Prototype: [CallLoop-BuyNumber-Prototype.html](../../CallLoop-BuyNumber-Prototype.html)

This prototype covers the two-step flow for buying a phone number. Step 1, "Choose number", has three tabs: Local, Toll-Free and External. Step 2, "Payment", shows the selected numbers, the card and the charge summary. Every step and tab is 494px wide (`--dlg-w`). The height follows each tab's content (about 780px for Local and External, 595px for Toll-Free) and is capped at the window height, where the content area scrolls. On Payment, the selected-numbers list scrolls after 360px, so the card and totals stay visible. Local shows 4 numbers and Toll-Free shows 12, and Refresh pages through by that amount.

## Screens and states

| Screen / state | How to reach it | Notes |
|---|---|---|
| Step 1 · Local tab | Default | A2P 10DLC alert (US only), Country select, a stacked City / Area code + "Filter by digits" finder, and a 1-column radio list of 4 numbers with the location right-aligned |
| Step 1 · Toll-Free tab | Tab | Toll-free verification alert, "Filter by digits", and a 3-column radio grid of 12 numbers |
| Step 1 · External tab | Tab | Search, "Hide added numbers" toggle, and a sortable multi-select table (Phone number, Purchased) |
| City / Area code mode | Toggle on the right of the finder | Changes the placeholder and how the first field filters |
| No matches | Filter that matches nothing | Empty message, and Continue is disabled |
| Refresh | Refresh button | Shows the next page of numbers and selects the first one |
| Step 2 · Payment | Continue | Collapsible "Selected numbers: N" table, Card select with "Primary" badge, and a totals box (monthly total, unused-time credit, total charged today with a tooltip) |
| Number bought | Buy number | Toast, then back to step 1. External numbers get the "Added" state; local and toll-free numbers drop out of the list |

## Design-system components used

| Component | Variant(s) | Where |
|---|---|---|
| Tabs | Master/Tabs | Local / Toll-Free / External |
| Alert | Info (`--notify2`), with a title and an optional body and "Learn more" link | 10DLC, toll-free verification, External hint |
| Select | Leading icon (flag, card brand), chevron, optional badge | Country, Card |
| Input | Input/Left Icon, stacked in one bordered group | City / Area code, Filter by digits, External search |
| Radio | Native, `accent-color: --blue1` | Local and toll-free number grids |
| Toggle | Master/Toggle (32×24) | Hide added numbers |
| Button | Primary, Primary disabled (`--blue1-dis`), Secondary (`--g2-light`) | Continue / Buy number, Refresh / Back |
| Tooltip / toast | Dark surface | "Added" tag, "Total charged today" help, feedback |

## Tokens used

- **Text:** `--black`, `--g1`, `--g2` (placeholders).
- **Surfaces and borders:** `--g4`, `--g3`, `--g2`.
- **Accents:** `--blue1` / `--blue2` / `--blue3` / `--blue4`, `--blue6` focus, `--blue1-dis`, `--g2-light`; `--notify2` info background.
- **Effects:** `--shadow1`.

## Deviations from the design system

| Value | Where | Why / proposed action |
|---|---|---|
| Overlay `rgba(20,22,26,.2)`; toast `rgba(20,22,26,.9)` / `.92` | Panel backdrop, toast, tooltips | No overlay token in Figma. Consider a `--scrim` token |
| Font size 13px | Kicker and list footer | Not on the scale. Use S2 (12) or S1 (14) |
| Radius 12px, 20px, 10px, 6px, 2px | Panel, alert, totals box, pills, toggle | Toggle and pill radii are inherent to their shape. Consider `--r-lg` for 12px panels |
| Flag and card-brand artwork | Country and Card selects | Brand colours, not tokens. Swap for the icon set's flags and card logos |

## Open questions

- Does the "External" tab need its own empty state?
- The payment summary repeats "Monthly total" (the "10 × $5" line and the subtotal line). Should the second one be "Subtotal"?
- Should the 10DLC alert only appear for US numbers? The prototype hides it for Canada.
- Local and toll-free tabs allow one number at a time (radio), but the payment step lists many. Should those tabs allow multi-select too?
