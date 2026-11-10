# Everfair website

Static one-page site (`index.html` + `assets/everfair.png`), deployed to everfair.com via Vercel. No build step — it's plain HTML/CSS.

## Editing

Edit `index.html` directly. Open it in a browser to preview (just open the file, no server needed). Commit and push to `main` to deploy.

## Deploying

The repo is connected to Vercel with GitHub integration:

- Every push to `main` deploys to **everfair.com**.
- Every pull request or branch gets its own preview URL.

DNS for everfair.com stays at GoDaddy (A record for `@`, CNAME for `www`, pointed at Vercel). GoDaddy's nameservers, MX, and TXT records are untouched, so email keeps working.

To change the domain or check deploy status, see the project in the [Vercel dashboard](https://vercel.com/dashboard).
