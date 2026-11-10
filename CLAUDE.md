# Everfair website: notes for Claude Code

Single static file: `index.html`. Keep it self-contained: no external scripts, fonts, images or network requests. Deploys to Vercel on push to `main`.

## What the page is
A full-screen landscape built around the Everfair acacia logo. The tree is the logo path, placed centrally as part of the scene (not as a pasted logo). The "Everfair" wordmark sits on the ground below it. No other text. Do not add a tagline.

## Design direction (from Andrew)
- African savannah, not cartoonish. Simple: little detail, little colour.
- One smooth sky gradient. No clouds, background trees, grass blades or haze.
- Tree is central and fairly large, slightly smaller than full-bleed.
- Night with stars is the hero look; day and sunset exist too.

## How it works
- The sky follows the visitor's local time. Sunrise 6:00, sunset 18:36 (constants `SUNRISE`, `SUNSET`).
- `SKY` and `GRD` tables are keyframes by hour; `sample()` interpolates; `mute()` desaturates them. Edit the tables to change colours.
- `render(h)` sets CSS variables and positions the sun, moon, tree shadow and rim light.
- The tree's colours come from a vertical gradient (`#tg`): canopy on top, trunk below.
- The canopy moves via the `#wind` SVG filter plus a slight sway animation.
- Stars are drawn on a canvas. Shooting stars appear only at night.
- `prefers-reduced-motion` turns off sway, wind, star drift and twinkle.
- The ground is a single flat tone (`--fg`, from `GRD`); there's no separate "far ridge" band. Keep it that way — a second ground tone reads as banding. No time-of-day slider in the shipped page; it's not public-facing.

## Constraints
- Must work on phones: layout is computed from viewport size in `layout()`, and the scenery is rebuilt on resize.
- Keep the file small and fast. No frameworks.
- The logo is Everfair's brand mark: don't redraw or distort the tree path.
