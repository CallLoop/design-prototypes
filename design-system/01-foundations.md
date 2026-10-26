# 01 · Foundations

[← Design system index](README.md)

This page covers the design tokens, component specs and technical setup that every prototype shares. To see how a single prototype uses them, open its page from the [index](README.md).

## Technical setup

### Source of truth

| | |
|---|---|
| **Figma** | [00 Design System](https://www.figma.com/design/BOVX8Hmx1HfwwBeDwOcZQL/00-Design-System?node-id=1799-396), page "⚙️ System" |
| **Last synced** | 2026-10-19. The sync was read-only and Figma was not modified. |
| **Local tokens** | [tokens.css](tokens.css) |

The Figma file uses classic **styles** (paint, text and effect), not Variables. The local token names are short aliases of those style names. The [Colour](#colour) table maps one to the other.

### How tokens reach a prototype

Prototypes are single self-contained HTML files with no build step, so they can't `@import` the shared CSS. Instead, every `CallLoop-*-Prototype.html` inlines an **identical copy** of the `:root { … }` block from `tokens.css`, with a sync comment at the top. Only that block is shared. The typography classes in `tokens.css` are a reference, and prototypes don't load them.

### Updating tokens

1. Edit `tokens.css` first. If the change came from Figma, update the sync date above.
2. Paste the new `:root` block over the existing one in **every** prototype.
3. Never rename or remove a variable that a prototype uses. Add a new one instead, then migrate the prototypes.
4. If a prototype needs a value that isn't a token, write it down in that prototype's **Deviations** section instead of adding it to `:root`.

### Conventions

- **Font:** Inter, through `var(--font)`. The base text colour is `--black`.
- **Radii:** use `--r-xs` (4px) for X-Small controls and `--r` (8px) for everything else. Figma has no other radius tokens.
- **Focus ring:** `outline: 2px solid var(--blue1); outline-offset: 1px`.
- **Input focus:** `box-shadow: inset 0 0 0 1px var(--blue1), 0 0 0 3px var(--blue6)`.

## Colour

The CSS variable names keep the short names the prototypes already use. Figma style names are in the first column.

| Figma style | CSS var | Value |
|---|---|---|
| Primary/color-blue-1 | `--blue1` | `#1364F9` |
| Primary/color-blue-1-disabled | `--blue1-dis` | `#1364F9` @ 40% |
| Primary/color-blue-2 | `--blue2` | `#1854EA` |
| Primary/color-blue-3 | `--blue3` | `#1885EA` |
| Primary/color-blue-3-disabled | `--blue3-dis` | `#1885EA` @ 40% |
| Primary/color-blue-4 | `--blue4` | `#1362AC` |
| Primary/color-blue-5 | `--blue5` | `#E7EFFE` |
| Primary/color-blue-6 | `--blue6` | `#D0E0FE` |
| Primary/color-black | `--black` | `#14161A` |
| Primary/color-white | `--white` | `#FFFFFF` |
| Primary/color-grey-1 | `--g1` | `#757D8A` |
| Primary/color-grey-2 | `--g2` | `#B7BFC8` |
| Primary/color-grey-2-disabled | `--g2-dis` | `#B7BFC8` @ 45% |
| Primary/color-grey-2-light | `--g2-light` | `#B7BFC8` @ 30% |
| Primary/color-grey-3 | `--g3` | `#E0E6EE` |
| Primary/color-grey-4 | `--g4` | `#F3F5F8` |
| Secondary/color-purple-1 / 2 / 3 | `--purple1` / `2` / `3` | `#7A16F5` / `#C6AFE2` / `#F0E4FF` |
| Secondary/color-aqua-1 / 2 | `--aqua1` / `2` | `#A4C5DB` / `#E4F4FF` |
| Secondary/color-orange-1 / 2 / 3 | `--orange1` / `2` / `3` | `#F86919` / `#D6BAAA` / `#FFEEE4` |
| States/color-success-1 / 2 / 3 | `--ok` / `--ok2` / `--ok3` | `#05944F` / `#026233` / `#E7F6ED` |
| States/color-notify-1 / 2 | `--notify1` / `2` | `#2E9AE4` / `#E6F7FF` |
| States/color-warning-1 … 4 | `--warn1` … `4` | `#FFC043` / `#BA7D04` / `#855A04` / `#FFF8E9` |
| States/color-error-1 / 2 / 3 | `--err` / `--err2` / `--err3` | `#E11900` / `#A11200` / `#FFF1F0` |
| *(no Figma style)* | `--text` | `#2C2D2E`. This is legacy and only used for sidebar icon strokes. Prefer `--black`. |

**Gradients:** `--grad1` runs top to bottom from `#F3F5F8` to `#EEF5FF`. `--grad2` fades from `#F3F5F8` to `#F3F5F8` @ 80% toward the left edge. `--grad3` is effectively flat `#E7EFFE`.

## Effects

| Figma | CSS var | Use |
|---|---|---|
| Shadow/1 | `--shadow1` | Dropdowns and popovers |
| Shadow/2 | `--shadow2` | Subtle card lift |
| Shadow/3 | `--shadow3` | Modals and large overlays |

## Typography

All text uses Inter. Headings have −2% letter-spacing.

| Style | Size / line height | Weights |
|---|---|---|
| H1 | 40 / 48 | Semi Bold |
| H2 | 28 / 32 | Regular, Semi Bold |
| H3 | 20 / 24 | Regular, Semi Bold |
| Blockquote | 20 / 28 | Italic |
| P0 | 16 / 24 | Italic, Regular, Semi Bold, Bold |
| P1 | 16 / 20 | Regular, Medium, Semi Bold |
| P2 | 14 / 20 | Regular, Medium, Semi Bold |
| S1 | 14 / 16 | Regular, Medium, Semi Bold |
| S2 | 12 / 16 | Regular, Medium, Semi Bold |
| S3 | 12 / 18 | Regular, Medium |
| S4 | 10 / 12 | Medium |

## Components (key specs)

**Buttons** use a radius of 8, except X-Small and icon buttons, which use 4. Labels are 14 Semi Bold, and the icon gap is 8.

| Size | Height | Padding |
|---|---|---|
| X-Small | 24 | 4 / 8, 14 Regular label |
| Small | 32 | 8 / 12 |
| Medium | 40 | 12 / 16 (12 on the icon side). Icon-only buttons are 40×40. |
| Large | 44 | 14 / 36 |

| Type | Normal | Hover | Disabled |
|---|---|---|---|
| Primary | `--blue1` bg, white text | `--blue2` | `--blue1-dis` bg, white text |
| Secondary (blue) | `--blue5` bg, `--blue1` text | `--blue6` bg, `--blue2` text | `--blue5` bg, `--blue1-dis` text |
| Secondary (Large) / Tertiary | `--g2-light` or `--g4` bg, `--black` text | `--g3` | `--g4` bg, `--g2` text |
| Quaternary (destructive) | `--err3` bg, `--err` text | `--err` bg, white text | — |
| Google | white, 1px `--g2` border, `--g1` text | `--notify2` bg, `--notify1` border | — |

**Inputs** are 40 high with a radius of 8, a white background and 14 Regular text. The placeholder colour is `--g2`, and the label is 12 Medium `--g1` with an 8px gap.

| State | Border |
|---|---|
| Normal | 1px `--g3` |
| Hover | 3px `--blue6` @ 40% |
| Active / typing | 3px `--blue6` |
| Positive | 3px `--ok3` |
| Negative | `--err3` background and a 3px `--err3` border |
| Disabled | `--g1` text |

The input variants are Default, Left Icon, Right Icon, Left + Right Icon, List, Card Simple and Card Stripe. Card Stripe is 416 wide.

**Control:** checkbox and radio rows follow the input spec (40 high, radius 8; checked rows get a 3px `--blue6` border). The checkbox itself comes in 16 and 20, the radio is 16, and the toggle is 32×24.

**Dropdown:** the panel is 200 wide, white, with radius 8 and `--shadow1`, and padding of 12/8/8/8 when it has a title. The title is 12 Medium `--g1`. Rows are 32 high (48 with a checkbox and icon), with 14 Regular text and a `--g4` hover. Action rows use 14 Semi Bold `--blue1` text.

**Tabs:** 26 high, with 14 text. Normal is `--g1` Regular, hover is `--black`, and active is `--blue1` Medium.

**Tooltip:** white 14 Regular text on a dark background, in Top, Bottom, Left and Right variants. The warning tooltip uses `--black` text.

**Status:** 14 Regular text with a 16px icon and an 8–10 gap.

| Colour | Statuses |
|---|---|
| `--ok` | Active, Finished, Verified, Approved, Success |
| `--notify1` | Scheduled, In Review |
| `--blue1` | Sending |
| `--purple1` | Collecting results |
| `--orange1` | Paused, Limited |
| `--warn2` | Archived, Unverified |
| `--err` | Failed, Invalid, Rejected, Void, Missed |
| `--g1` | Draft, Disabled, Inactive, Unassigned, Unsubscribed, Processing, Refunded |

**Textarea:** 536 wide, with 14 Regular text and a `--g2` placeholder. A 12 Regular `--blue1` counter sits beside it.
