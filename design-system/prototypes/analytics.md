# 02 · Analytics

[← Design system index](../README.md) · [Foundations](../01-foundations.md) · Prototype: [CallLoop-Analytics-Prototype.html](../../CallLoop-Analytics-Prototype.html)

This prototype explores analytics and reporting: a channel comparison across Messages and Credits, a Forecast tab that projects credits, messages, engagements and revenue, plus a detail view for each channel (SMS, Voice, Ringless) with filters, stats, charts and tables. The static mockups are in `Design/Analytics — *.png`.

## Screens and states

| Screen / state | How to reach it | Notes |
|---|---|---|
| Analytics → Messages | `#messages` (default) | Channel comparison: stats, stacked chart, tables |
| Analytics → Credits | `#credits` | Usage breakdown, "Credits used over time", credits by source |
| Analytics → Forecast (Beta) | `#forecast` | Value first: expected revenue, engagements, return on credits and messages (each with likely range and change vs the basis-period average); highlights (fastest-growing source, efficiency, biggest upcoming broadcast, last month's forecast accuracy); "How you're growing" monthly trend lines (12 months + 3 forecast) for revenue, engagements, messages and credits per engagement; expected value by source; scheduled broadcasts; campaigns & triggers and engagements by channel. Spend is in a lower "Credits & plan" section: credits and balance, weekly credits chart, plan-fit card (Pro tiers 500–50K a month, or ×12 billed annually, with a Monthly / Annually switch, current and best-fit tiers, Custom above 50K), credits by channel |
| Forecast: low balance | Next 90 days + "Scheduled + usual broadcasts" | Warning alert with an Upgrade plan button when the balance runs out before the period ends |
| Forecast: Compare plans modal | "Compare plans" on the plan card, or "Upgrade plan" in the low-balance banner | Monthly / Annually switch. For each Pro plan: price, cost per plan credit, cost per extra credit, credits to buy for the forecast, and estimated cost a month. Shows the current plan and bigger plans only, never lower ones. Marks Current and Best value (the cheapest upgrade, only if it beats today), with Save badges |
| Forecast: Upgrade plan (payment) modal | "Switch to …" on the plan card, or "Select" in Compare plans | Step 2 of 2. Billing radios (Monthly / Annually with a Save badge), saved card, Details panel (plan, credits, additional credit, total). "Upgrade" shows a toast and updates the plan card |
| Forecast: new account | Prototype switch, top right ("New account (9 days)") | Only scheduled broadcasts are forecast; info alert says when campaigns, triggers and other sending are added |
| SMS detail | `#sms` | Conversions funnel and "SMS delivered / MMS delivered / Failed" series |
| Voice detail | `#voice` | Transfers by source, call forwarding by number, "Live answer / Voicemail / Failed" series |
| Ringless detail | `#ringless` | Callbacks by source, ringless outcomes over time |
| Empty states | Prototype switch, top right | "No conversions / transfers / callbacks" variants, matching the `Design/*detail — no …` mockups |
| Filters open | Date, service, source and phone dropdowns | Date picker with presets and a draft range |

## Design-system components used

| Component | Variant(s) | Where |
|---|---|---|
| Sidebar | UI Kit/Sidebar: nav item, active state (`--aqua2` + `--blue1` icon), NEW badge, trial card | Left rail |
| Tabs | Master/Tabs: Normal / Hover / Active | Messages / Credits |
| Dropdown | Master/Dropdown rows (Simple, Checkbox), panel with `--shadow1` | Filter buttons, date picker |
| Input | Input/Left Icon (search inside dropdowns) | Filter search |
| Tooltip | Tooltip/Simple, dark | Chart hovers |
| Badge / counter | Count badge (`--blue1`) | Selected-filter count |
| Alert | Warning (`--warn4` / `--warn3`) and info (`--notify2`) banners | Forecast: low balance, new account |
| Pill | Confidence High (`--ok3`/`--ok2`), Medium (`--blue5`/`--blue2`), Low (`--warn4`/`--warn3`) | Forecast by source |
| Button | Primary (`--blue1`), secondary (`--blue5`) | Upgrade plan, Compare plans, empty-state actions |
| Highlight card | Bordered card, `--blue1` label | Forecast highlights |
| Trend card | Bordered card with inline SVG line: actual solid `--blue1`, forecast dashed, range band `--blue5` | How you're growing |
| Plan meter | Stacked bar: Plan credits `--blue1`, Credits to buy `--warn1`, each with an info tooltip | Credits & plan |
| Segmented control | Monthly / Annually, `--g4` track, white active segment with `--shadow2` | Plan card |
| Dialog | 20px radius, `--shadow1`, `rgba(20,22,26,.2)` overlay, close X, steps (`--blue1` numbered squares) | Compare plans, Upgrade plan. Same pattern as Buy number |
| Radio row, card select | Bordered 8px rows; `--ok3`/`--ok` Save badge; Visa mark | Upgrade plan |
| Tier chips | Outlined chips; current `--g1` outline, best fit `--blue5` fill + `--blue1` outline, too-small tiers `--g2` text | Plan card |

## Tokens used

- **Text:** `--black` and `--g1` (muted, the most used); `--text` for sidebar icon strokes.
- **Surfaces and borders:** `--g4` hover/background, `--g3` borders and dividers, `--g2` hover border.
- **Accents:** `--blue1` / `--blue2` / `--blue3` links, tabs and focus; `--blue5` / `--blue6` selection and input focus ring; `--aqua2` active nav; `--purple1` / `--purple3` NEW badge.
- **Effects:** `--shadow1` popovers.

## Deviations from the design system

| Value | Where | Why / proposed action |
|---|---|---|
| Chart series `#C4E5C6` (success), `#F6CD92` (warning), `#F5A3A3` (failure) | Stacked charts and legends | There's no data-viz palette in Figma. **Proposal:** add a chart palette to Figma, or switch to `--ok3` / `--warn1` / `--err3`-based tints |
| Font size 13px (table, legend, bar list, date picker), 15px (`.h3`, funnel values), 11px (trial card, NEW badge) | Several | Not on the type scale. Map to S1/P2 (14), H3 or P1 (16), and S4 (10) or S2 (12) |
| Radius 12px (cards, trial), 6px (options, NEW badge), 3px (progress, bars) | Several | Figma only uses 4 and 8 for components. 12px cards are common in the app, so consider a `--r-lg` token |
| `#757D8A`, `#1364F9`, `#14161A`, `#05944F`, `#BA7D04`, `#C6AFE2`, `#B7BFC8`, `#F86919` hard-coded | JS templates, SVG | Equal to tokens. Replace with `var(--…)` |
| Tooltip / prototype switch background `rgba(20,22,26,.9)` / `.92` | Tooltip, `.proto` | `--black` at 90% or 92%. Tooltip/Simple in Figma should confirm the exact value |
| Forecast bars: diagonal hatch `rgba(20,22,26,.13)`, range whiskers in `--g1`, dashed `--blue1` "today" divider | Forecast chart | No pattern for projected data in Figma. **Proposal:** add "forecast" and "range" variants to the chart spec |
| Confidence pill and alert banner | Forecast | Not in the Figma kit yet. Built from state tokens; confirm against a Figma Alert/Tag component |
| Logo gradient `#3F24E3 → #41BDED` | Sidebar logo SVG | Brand asset. Keep it local |

## Open questions

- Forecast: should the likely range be shown on every stat, or only in tooltips? Is "about 8 times out of 10" the right promise?
- Forecast: return on credits drops when the forecast includes Voice or Ringless sends (revenue isn't tracked for them). Show it per channel, or only for SMS?
- Forecast: with the current prices, buying extra credits is often cheaper than moving up a monthly plan (3.25¢ extra on 2.5K vs 3.58¢ per plan credit on 5K). The card and Compare plans only ever offer bigger plans (or the same plan billed annually), and recommend one only when it costs less than today. Should extra-credit prices be higher than the next plan's per-credit price?
- Forecast: the annual price list had "330K" for $7,560. The prototype uses 300K (25K × 12). Please confirm.
- Forecast: the reference payment modal shows 2.8¢ additional credit for Pro Annual 420K, but the price list gives 2.85¢ for the 35K plan. The prototype uses the price list.
- Forecast: should "usual broadcasts" be on by default for accounts that send broadcasts on a regular cadence?

- Should chart colours become official tokens?
- The 13px body size is used a lot for dense tables. Does the product actually use 13px, or should it be 14px (S1)?
