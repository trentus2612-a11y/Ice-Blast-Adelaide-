# CLAUDE.md

Context for Claude Code working in this repo.

## What this is

Marketing site and planning docs for **Ice Blast Adelaide**, a dry ice cleaning business being started by three partners in Golden Grove, South Australia. Services: engine bays, 4x4 underbodies and chassis, parts cleaning. Workshop-based with mobile as an option.

The business has not launched yet. Nothing here is live.

## Repo layout

```
index.html              The website. Single file, no build step.
assets/logo.jpg         Brand logo
assets/results/         Before/after photos used by the comparison sliders
docs/                   Planning documents, not part of the site
```

`docs/` holds the pitch, startup plan, market test plan, business plan and equipment list. They are standalone HTML and Markdown, reference `../assets/logo.jpg`, and are not linked from the site.

## Stack

Deliberately plain. One HTML file with inline CSS and vanilla JS. No framework, no bundler, no dependencies, no build step. Open `index.html` in a browser and it works.

Only external request is Google Fonts (Chakra Petch and Inter).

Keep it this way unless there's a strong reason not to. The owners are not developers and need to be able to edit it.

## Brand

- Background near-black `#04070A`, panels `#0A1017`, raised `#0E151D`
- Ice blue `#1BA3F2`, bright `#7FD6FF`, deep `#0A6DAE`
- Steel text `#AEBCC7`, dim `#6C7A85`, white `#EFF6FB`
- Display type: Chakra Petch (square sans, tapered corners, matches the logo's angular cuts). Logo mark in the nav is italic to echo the wordmark.
- Body type: Inter
- Design direction: dashboard-style. Rounded panels, hairline borders, pill controls, one accent colour doing the work.

CSS custom properties are defined in `:root`. Use them rather than hardcoding colours.

## Australian English

Copy uses Australian spelling. Prices in AUD. Keep it that way.

The tone is direct and plain. No marketing fluff, no em dashes.

## The quote configurator

The main interactive feature, in `<section id="build">`.

An inline SVG side view of a dual-cab ute. Selectable areas are `<path class="zone">` elements with ids inside `<g id="zones">`. Everything else in the SVG is decorative and has `pointer-events:none` where it would block a zone.

Pricing lives in the `ITEMS` object in the configurator script:

```js
'z-engine': {label:'Engine bay', price:230, hrs:3, scale:true}
```

`scale:true` means the price is multiplied by both the condition multiplier and the vehicle type multiplier. Add-ons (`parts`, `coating`, `mobile`) are `scale:false` and stay flat.

Multipliers:
- Vehicle type: small car 0.85, sedan/SUV 1.0, 4x4/ute 1.15
- Condition: light 1.0, moderate 1.18, heavy 1.4

**These numbers are tuned to land on the published price list in the Prices section.** If you change a base price or a multiplier, check the result still sits inside the advertised ranges. A 4x4 full clean on moderate should come out around $2,400 against the listed $2,200 to $2,500.

## Before/after sliders

`<figure class="ba">` elements with `data-before` and `data-after` attributes holding image paths. The script builds the images, the drag handle and the labels. If either attribute is empty the slider does not initialise.

## Placeholders that must be replaced before launch

- Phone number `0400000000` — appears in the hero SMS link, the form fallback text, the contact panel, the mobile bar and the form success message
- Email `hello@iceblastadelaide.com.au` — contact panel and the `EMAIL` constant in the form script
- Workshop street address — currently only "Golden Grove, SA"

## Known issues to be honest about

**The before/after photos may be AI generated.** They came from a composite the owner supplied. They do not show work this business has done. They must be replaced with real job photos before the site goes public, otherwise the site misrepresents the business. This is not a cosmetic issue.

**The quote form has no backend.** It builds a `mailto:` link and opens the user's mail client. It works without hosting but it is fragile, and on some mobile setups nothing happens. A real form endpoint (Formspree, Netlify Forms, or similar) would be the first worthwhile upgrade.

**The opening offer says first ten bookings get 20% off.** Someone needs to actually track that.

## Things not to do

- Do not add a framework or build step
- Do not use em dashes in copy
- Do not replace Australian spelling
- Do not add the before/after photos of other operators' work
