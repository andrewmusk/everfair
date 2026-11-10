# Everfair website

Static, single-page site for everfair.com. No build step, no dependencies.

- `index.html` is the whole site (HTML, CSS and JS inline, no external requests).
- `assets/everfair-logo-white.svg` is the original logo from Google Drive. The tree path is inlined in `index.html`; the file here is the source of truth.
- `vercel.json` sets basic security headers.

## Preview locally

    python3 -m http.server 8000

Open http://localhost:8000. Add `#preview` to the URL (http://localhost:8000/#preview) to show a time-of-day slider.

## Deploy

Pushing to `main` deploys to production on Vercel. Pull requests and other branches get preview URLs.

Vercel settings: Framework Preset "Other", no build command, no output directory.

## DNS

everfair.com is registered at GoDaddy and DNS stays there. Apex A record and a www CNAME point to Vercel (use the values shown on the domain card in Vercel's project settings). Do not change nameservers or the MX/TXT records, which carry email.
