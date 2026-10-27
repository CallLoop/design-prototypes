# Call Loop design system

The local copy of the Call Loop design system, synced read-only from Figma, plus one page for each prototype that uses it.

| # | Page | What's in it |
|---|---|---|
| 01 | [Foundations](01-foundations.md) | Design tokens (colour, type, effects, radii), component specs, and how tokens reach the prototypes |
| 02 | [Analytics](prototypes/analytics.md) | Analytics / reporting prototype |
| 03 | [Buy number](prototypes/buy-number.md) | Buy-a-phone-number flow |
| 04 | [ClickBank integration](prototypes/clickbank.md) | Integrations page and the ClickBank connect flow |
| 05 | [Twilio integration](prototypes/twilio.md) | Connect your own Twilio account, external numbers, trial vs paid connect flow |

Files:

- [tokens.css](tokens.css) holds the canonical tokens. Every prototype inlines its `:root` block.
- [prototypes/_template.md](prototypes/_template.md) is the starting point for a new prototype page.

## Adding a page for a new prototype

Every new `CallLoop-<Feature>-Prototype.html` gets its own page here.

1. Copy `prototypes/_template.md` to `prototypes/<feature>.md`, using kebab-case such as `buy-number.md`.
2. Fill in every section. Under **Deviations**, list each value the prototype uses that isn't a token, along with why.
3. Add a row to the table above, numbered next in sequence. Prototype pages keep the order they were added in.
4. Make sure the prototype's `:root` block is an exact copy of the one in `tokens.css` (see [Foundations → How tokens reach a prototype](01-foundations.md#how-tokens-reach-a-prototype)).
