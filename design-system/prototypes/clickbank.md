# 04 · ClickBank integration

[← Design system index](../README.md) · [Foundations](../01-foundations.md) · Prototype: [CallLoop-ClickBank-Prototype.html](../../CallLoop-ClickBank-Prototype.html)

This prototype covers the Integrations page and the ClickBank integration: connecting, editing and disconnecting accounts, and the field mappings shared by all connected accounts.

## Screens and states

| Screen / state | How to reach it | Notes |
|---|---|---|
| Integrations list | Default | Connected native integrations plus "Explore" cards |
| ClickBank: empty | Prototype switch, top right ("fresh") | "Connect ClickBank account" empty state |
| ClickBank: Accounts | ClickBank card | Account list with row menu (edit / disconnect), "Connect another account" |
| ClickBank: Mappings | Section on the detail page | External field → Call Loop field; a tooltip explains that mappings apply to all accounts |
| ClickBank: Settings | Tab | Includes a webhook value with copy-to-clipboard |
| Connect / Edit modal | Connect button, or Edit in the row menu | Form with validation errors |
| Disconnect modal | Disconnect in the row menu | Destructive confirmation |
| Toast | After save, disconnect or copy | Dark toast |

## Design-system components used

| Component | Variant(s) | Where |
|---|---|---|
| Sidebar | UI Kit/Sidebar, with plan card | Left rail |
| Button | Primary, Secondary, Tertiary, Quaternary (destructive, `--err` / `--err3`) | Page actions, modals |
| Input | Input/Default with Normal, Active-Typing and Negative states | Connect form |
| Dropdown | Dropdown panel + Master/Dropdown rows | Row menu, mapping selects |
| Tabs | Master/Tabs | Detail tabs |
| Tooltip | Tooltip/Simple | Mappings help |
| Status | Status colours (`--ok2` / `--ok3`) | Connected state |
| Modal | Not in the Figma System page | Connect / Disconnect |

## Tokens used

- **Text:** `--black`, `--g1`, `--text` (icons).
- **Surfaces and borders:** `--g4`, `--g3`, `--g2`.
- **Accents:** `--blue1` through `--blue6`, `--aqua2` active nav, `--purple1` / `--purple3` NEW badge, `--notify2`.
- **States:** `--ok2` / `--ok3` success; `--err` / `--err2` / `--err3` errors and destructive actions.
- **Effects:** `--shadow1` (menus, modals, toast).

## Deviations from the design system

| Value | Where | Why / proposed action |
|---|---|---|
| Integration logo colours: `#356AE6`, `#2B8A3E`, `#C2410C`, `#4D7C2F`, `#1D5FD1`, `#B0179F`, `#1E7E34` | Integration card initials | Third-party brand colours. Keep them local, or use real logos |
| `.h2` 17/24 | Section headings | Not on the scale. Use H3 (20/24) or P1 Semi Bold (16/20) |
| Font size 13px, 15px, 11px | Alerts, tooltips, crumbs, card names, plan card | Map to S1/P2 (14), P1 (16), and S4/S2 |
| Radius 12px, 16px, 20px, 22px, 32px, 6px, 3px | Cards, logos, modals, pills | Figma uses 4/8 only. 12px cards and 16px logo tiles need a decision |
| `rgba(19,100,249,.4)`, `rgba(183,191,200,.3)` | Disabled buttons | Replace with `--blue1-dis` and `--g2-light` |
| `#14161A`, `#757D8A`, `#B7BFC8`, `#05944F`, `#026233`, `#1364F9` hard-coded | JS templates, prototype switch | Replace with `var(--…)` |
| Modal (`rgba(20,22,26,.2)` scrim, `--shadow1`) | Connect / Disconnect | Figma has `--shadow3` meant for overlays. Consider using it, and add a Modal spec to Figma |

## Open questions

- Should Modal become a documented component? The `Design/Modal — account exists warning` mockup uses one too.
- Should the modal use Shadow/3 instead of Shadow/1?
