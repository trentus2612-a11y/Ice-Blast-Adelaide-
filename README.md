# Ice Blast Adelaide

Website and planning documents for Ice Blast Adelaide, a dry ice cleaning business in Golden Grove, South Australia.

## Running it

There is no build step. Open `index.html` in a browser.

To serve it locally (needed if you want the fonts and paths to behave exactly as they will live):

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000

## What's here

| Path | What it is |
|---|---|
| `index.html` | The website |
| `assets/logo.jpg` | Logo |
| `assets/results/` | Before and after photos for the comparison sliders |
| `docs/pitch.html` | Business pitch, for the partners |
| `docs/startup-plan.html` | How to start without a large outlay |
| `docs/saturday-plan.html` | The hire-a-machine-on-Saturdays loop |
| `docs/market-test.html` | Advertise, book a Saturday, hire the machine |
| `docs/business-plan.md` | Original rough business plan |
| `docs/equipment-list.md` | Full equipment list with specs and supplier questions |
| `CLAUDE.md` | Project context for Claude Code |

## The images are not in the repo yet

Every HTML and Markdown file is in. The photos are not, so the logo and the
before/after sliders show as broken until they land.

Drop them into `assets/` using the exact filenames in `assets/README.md` and
everything picks them up with no code changes.

## Before this goes live

- [ ] Replace the phone number. Search for `0400000000`
- [ ] Replace the email. Search for `hello@iceblastadelaide.com.au`
- [ ] Add the workshop street address
- [ ] **Replace the before and after photos with real jobs.** The current ones are placeholders and do not show work this business has done
- [ ] Put a real form backend behind the quote form, or accept that it relies on `mailto:`
- [ ] Check the configurator prices still match the published price list

## Site sections

1. Hero with logo and trust tiles
2. Results, drag-to-compare before and after sliders
3. Build a quote, interactive vehicle configurator
4. How it works
5. Prices, plus the opening offer
6. Quote form and contact details
7. FAQ

## Stack

Plain HTML, CSS and vanilla JavaScript in one file. No dependencies, no framework, no build. Google Fonts is the only external request.

This is deliberate. The owners need to be able to edit it.
