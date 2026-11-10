# Everfair website: notes for Claude Code

Single static file: `index.html`. Keep it self-contained: no external scripts, fonts, images or network requests. Deploys to Vercel on push to `main`.

## What the page is
A full-screen landscape built around the Everfair acacia logo. The tree is the logo path, placed centrally as part of the scene (not as a pasted logo). No wordmark, tagline or other visible text — Andrew asked for it to be dropped; there's only a visually-hidden `<h1>` for accessibility/SEO.

## Design direction (from Andrew)
- African savannah, not cartoonish. Simple: little detail, little colour.
- One smooth sky gradient. No clouds, background trees, grass blades or haze.
- Tree is central and fairly large, slightly smaller than full-bleed.
- Night with stars is the hero look; day and sunset exist too.

## How it works
- The sky follows the visitor's local time. Sunrise 6:00, sunset 18:36 (constants `SUNRISE`, `SUNSET`).
- `SKY` and `GRD` tables are keyframes by hour; `sample()` interpolates; `mute()` desaturates them. Edit the tables to change colours.
- `render(h)` sets CSS variables and positions the sun, moon, tree shadow and rim light.
- The tree's colours come from a vertical gradient (`#tg`): canopy on top, trunk below. It only animates once, on load (`reveal` fade-in) — no continuous sway or canopy wind shimmer; that read as "weird little movements" on some monitors.
- A soft `drop-shadow` rim light (`--rim`) outlines the tree from the sun/moon side. Keep this subtle — it's been toned down twice already (full moon should not light up the canopy).
- Stars are drawn on a canvas. Shooting stars appear only at night and are intentionally rare (`Math.random() < 0.0004` per frame, gated on `shooters.length === 0`) — don't raise this without being asked.
- `prefers-reduced-motion` turns off sway, star drift and twinkle.
- The ground is a single flat tone (`--fg`, from `GRD`); there's no separate "far ridge" band. Keep it that way — a second ground tone reads as banding.
- There's a `#preview` time-of-day slider (`.preview` div, hidden unless `location.hash === '#preview'`), for dev use only — it must never be visible or linked from the public page.

## Constraints
- Must work on phones: layout is computed from viewport size in `layout()`, and the scenery is rebuilt on resize.
- Keep the file small and fast. No frameworks.
- The logo is Everfair's brand mark: don't redraw or distort the tree path.
