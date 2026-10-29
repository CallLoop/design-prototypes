# design-prototypes

Design concepts and clickable prototypes for **Call Loop**, kept in one place so they're easy to share with the team via a link.

Each prototype is a single self-contained HTML file — no build step, no dependencies. Open it in a browser and click around.

## Prototypes

| Prototype | File | Design-system page | What it covers |
|---|---|---|---|
| Analytics | [CallLoop-Analytics-Prototype.html](CallLoop-Analytics-Prototype.html) | [02 · Analytics](design-system/prototypes/analytics.md) | Analytics / reporting screens, plus a Forecast tab (credits, volume and value) |
| Buy number | [CallLoop-BuyNumber-Prototype.html](CallLoop-BuyNumber-Prototype.html) | [03 · Buy number](design-system/prototypes/buy-number.md) | Flow for buying a phone number |
| ClickBank integration | [CallLoop-ClickBank-Prototype.html](CallLoop-ClickBank-Prototype.html) | [04 · ClickBank](design-system/prototypes/clickbank.md) | Connecting and using the ClickBank integration |
| Twilio integration | [CallLoop-Twilio-Prototype.html](CallLoop-Twilio-Prototype.html) | [05 · Twilio](design-system/prototypes/twilio.md) | Connecting Twilio and choosing numbers in one flow, plus buying Call Loop or Twilio numbers from one dialog (CWR-4577) |

## Design system

The design system is in [design-system/](design-system/README.md), synced from the Figma **00 Design System** file:

- **[01 · Foundations](design-system/01-foundations.md)** covers the design tokens, component specs and technical setup. [tokens.css](design-system/tokens.css) is the source of truth, and every prototype inlines its `:root` block.
- **One page per prototype** (02, 03, …) lists the screens, the components and tokens it uses, and where it deviates from the system.

## Viewing a prototype

- **Online:** the repo is published with GitHub Pages at **https://callloop.github.io/design-prototypes/**, a hub page with a card for every prototype. Each prototype also has a short link, for example [/analytics](https://callloop.github.io/design-prototypes/analytics), [/buy-number](https://callloop.github.io/design-prototypes/buy-number) and [/clickbank](https://callloop.github.io/design-prototypes/clickbank). Its full file name works too. Every push to `main` redeploys the site in about a minute. The repo and site are public, so anyone with a link can open them.
- **Locally:** clone the repo (or download the file) and open the `.html` file in your browser.

## Adding a new prototype

1. Export or save the prototype as a single `.html` file.
2. Name it `CallLoop-<Feature>-Prototype.html`.
3. Paste the `:root` block from [design-system/tokens.css](design-system/tokens.css) into it, unchanged.
4. Create its design-system page from [design-system/prototypes/_template.md](design-system/prototypes/_template.md), then add it to the [design-system index](design-system/README.md).
5. Add a row to the table above.
6. Add an entry to the `PROTOTYPES` list in [index.html](index.html) so it gets a card on the hub page.
7. Add its short link: copy [analytics/index.html](analytics/index.html) to `<slug>/index.html` and change the file name and title in it. The `slug` must match the one in the `PROTOTYPES` entry.
8. Commit and push to `main`.
