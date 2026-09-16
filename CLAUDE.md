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
- Buttons and selectable cards are tactile. They sit on a solid coloured edge drawn with `box-shadow:0 4px 0`, and on `:active` they translate down by the same amount and lose the shadow, so they physically press. Keep that on anything tappable.

CSS custom properties are defined in `:root`. Use them rather than hardcoding colours.

## Australian English

Copy uses Australian spelling. Prices in AUD. Keep it that way.

The tone is direct and plain. No marketing fluff, no em dashes.

## The quote builder

The main interactive feature, in `<section id="build">`. It is a five step flow,
not a single screen. Steps are `<div class="qstep">` elements inside `.qb-body`,
shown one at a time by the `on` class. `goTo(i)` drives the progress bar, the
step counter, the Back and Next buttons and the running total.

Steps: vehicle, areas, condition, extras, quote and contact details. The contact
form is the last step, so the whole thing finishes in one place.

In step two the areas can be picked two ways, by tapping a `<path class="zone">`
on the inline SVG ute or by tapping the matching card in `#q-areas`. They stay in
sync through `syncAreas()`, keyed on the same id.

**Zones must not overlap.** They are painted in DOM order, so the last one wins a
shared pixel. Order is body, under, arch, engine. The wheel arch outer radius is
86, deliberately small enough that the arch band does not reach the centre of the
engine bay zone. Widening it again will make the engine bay untappable on a phone.

### Pricing

Pricing lives in the `ITEMS` object:

```js
'z-engine': {label:'Engine bay', price:250, hrs:3, cond:true, veh:false}
```

`cond` means the condition multiplier applies, `veh` means the vehicle size
multiplier applies. Add-ons (`parts`, `coating`, `mobile`) are flat.

Multipliers:
- Vehicle size: small car 0.85, sedan or SUV 1.0, 4x4 or ute 1.15
- Condition: light 1.0, moderate 1.18, heavy 1.4

**Engine bay does not scale with vehicle size.** That is deliberate. The published
price list has one engine bay row with no vehicle distinction, so holding it flat
makes the builder land on exactly $250, $295 and $350 for light, moderate and
heavy, matching the advertised $250 to $350 at every vehicle size.

**These numbers are tuned to the published price list in the Prices section.** The
calibration point is a 4x4 full clean on moderate, which comes out at $2,398
against the listed $2,200 to $2,500. Change a base price or a multiplier and
check that still holds.

Known and accepted: because the total is linear in the condition multiplier, a
full clean on light sits under the bottom of the published range and on heavy
sits over the top. Only the moderate column is calibrated. The published ranges
cannot all be hit by one multiplicative model, so this is a pricing decision for
the owners rather than a bug.

### The opening offer

`var OFFER=0.20;` in the builder script applies the advertised 20% off to every
quote and shows it as its own line. When the first ten bookings are gone, set it
to `0` and the line disappears on its own. Nothing else needs changing.

### Sending

There is still no backend. `submit()` validates, builds a plain text summary and
opens a `mailto:` link. Because that silently fails on some mobile setups, the
same text is also written into a read only textarea with a copy button, a text
message link and a call link. That panel appears every time, not only on failure,
so there is always a way through.

## Before/after sliders

`<figure class="ba">` elements with `data-before` and `data-after` attributes holding image paths. The script builds the images, the drag handle and the labels. If either attribute is empty the slider does not initialise.

## Placeholders that must be replaced before launch

- Phone number `0400000000` — appears in the hero SMS link, the form fallback text, the contact panel, the mobile bar and the form success message
- Email `hello@iceblastadelaide.com.au` — contact panel and the `EMAIL` constant in the form script
- Workshop street address — currently only "Golden Grove, SA"

## Known issues to be honest about

**The before/after photos may be AI generated.** They came from a composite the owner supplied. They do not show work this business has done. They must be replaced with real job photos before the site goes public, otherwise the site misrepresents the business. This is not a cosmetic issue.

**The quote form has no backend.** It builds a `mailto:` link and opens the user's mail client. It works without hosting but it is fragile, and on some mobile setups nothing happens. The copy and text fallback covers that, but a real form endpoint (Formspree, Netlify Forms, or similar) is still the first worthwhile upgrade.

**The opening offer says first ten bookings get 20% off.** Someone needs to actually track that. The builder applies it to every quote, so set `OFFER` to `0` once the ten are gone.

## Things not to do

- Do not add a framework or build step
- Do not use em dashes in copy
- Do not replace Australian spelling
- Do not add the before/after photos of other operators' work
- Do not let the fixed `.mobilebar` cover the builder's Back and Next buttons. An IntersectionObserver hides it while the builder is on screen
