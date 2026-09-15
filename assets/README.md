# Assets

The image files are not in the repo yet. Drop them in here with exactly these
names and the site picks them up with no code changes.

| File | Used by | Size it is drawn at |
|---|---|---|
| `assets/logo.jpg` | Hero on `index.html`, and `docs/market-test.html` | Square, shown up to 470px wide |
| `assets/results/engine-before.jpg` | First before/after slider | 644 x 330 |
| `assets/results/engine-after.jpg` | First before/after slider | 644 x 330 |
| `assets/results/under-before.jpg` | Second before/after slider | 644 x 385 |
| `assets/results/under-after.jpg` | Second before/after slider | 644 x 385 |

Both halves of a slider must be the same size and shot from the same angle, or
the drag handle will not line up.

If you name a file something else, change the `data-before` and `data-after`
attributes on the matching `<figure class="ba">` in `index.html`.

**These must be photos of work this business has actually done before the site
goes public.** See the note in `CLAUDE.md`.
