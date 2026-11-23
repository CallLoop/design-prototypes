# 09 · New pricing

[← Design system index](../README.md) · [Foundations](../01-foundations.md) · Prototype: [CallLoop-NewPricing-Prototype.html](../../CallLoop-NewPricing-Prototype.html) · Canvas page: [09 · New pricing](https://claude.ai/artifact/62ESFez9wPT6KSf9QTKxyB#page-new-pricing)

The 2026 pricing rollout (CWR-4775): the "keep your current pricing" announcement modal shown from Dec 1, the Upgrade plan modal on the new plan lines, and the Buy credits pack allowances per plan (CWR-4788). Tabs in the prototype: `#announce`, `#upgrade`, `#buy-credits`, `#packs`.

Unlike the other prototypes, this one is built on the **Broadcast Design System** (Lydia's Figma "Broadcast Design System": Figtree, `main` #2B5CFF), not on [tokens.css](../tokens.css). Its tokens, `bundle.css` and the `window.Broadcast` component bundle are inlined in the file; React 18 loads from cdnjs.

## Screens and states

| Screen / state | How to reach it | Notes |
|---|---|---|
| Announcement: offer | `#announce`, "Preview as old plan" select | Countdown to Dec 31, 11:59 PM PT; today's annual price vs the price after Dec 31. Plans whose price doesn't go up show no modal. Pattern from the removed migration offer (CWR-3454) |
| Announcement: retiring plans | Pick a 250 plan, or the 420K/yr stop in Compare | 250: moves to 500 after Dec 31. 35K: kept 12 months, next renewal plan Annual 600,000 |
| Announcement: Compare annual plans | Compare annual plans | Upgrade-style slider with only today's annual plans at the customer's tier or higher (500 and up), Custom card, Back |
| Announcement: Payment | Keep my current pricing, or Continue in Compare | Upgrade plan's payment step: Annually with "Save $X vs new price", card, Auto-recharge, Details with Locked until (today + 1 year) |
| Announcement: done, banner | Switch to Annual…; Remind me later or × | Banner stays until the customer chooses |
| Upgrade plan | `#upgrade` | 12 slider stops 500–100K, monthly/annual, Pay As You Go ($49/yr + 9¢), Custom card. Old-price customers get a "Keep my pricing" alert and no Current tag |
| Buy credits | `#buy-credits`, "Preview as plan" select | Packs up to the plan's max with prices; bigger packs up to 10,000 show "Upgrade plan" (10,000 = Custom only) |
| Credit packs per plan | `#packs` | Today vs new prices with unchanged boundary rows vs proposed max pack |

## Design-system components used

Broadcast DS: Modal (`l` 800, `m` 528, `s` 280 with `steps`), Slider, Select, Alert, Banner, Tag, Button, Radio, Toggle, Checkbox, Tabs, DropdownMenu, DataTable, SidebarItem, Icon.

## Deviations from the design system

| Value | Where | Why / proposed action |
|---|---|---|
| Countdown tiles (20/600 `main` numerals on white, in a `grey-4` panel) | Announcement | New pattern; becomes a component if reused |
| Credits field trigger + DropdownMenu | Buy credits | The DS Select has no right-hand price per option |
| Visa mark as text | Payment, Buy credits | The DS card logos are uploads, not in the bundle |

## Open questions

- Pack allowances (CWR-4788): billing picks `billing_credit_price_boundary` by plan price; with the new prices and today's rows the 500 plan gets 1,000, 7.5K gets 5,000 and 75K/100K annual find no row. Proposed: even graduation (500/1K → 500, 2.5K/5K → 1,000, 7.5K/10K → 2,500, 15K–25K → 5,000, 50K–100K → 7,500), rows by monthly price (annual ÷ 12), max upgrade 10,000 on every row, 10,000 buyable on Custom only.
- Custom card copy: "More than 100,000 credits / mo" now that 100K is a standard plan.
