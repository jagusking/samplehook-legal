# SampleHook Legal — publishing via Vercel

Static HTML pages (Privacy + Terms) for the SampleHook iOS app, deployed on
Vercel and served at `https://samplehook.app/`. Same pattern Crate Dive uses
(`SampleScout/landing/`).

## Files

- `index.html` — landing page linking to both legal pages
- `privacy.html` — Privacy Policy
- `terms.html` — Terms of Use
- `vercel.json` — `cleanUrls: true` + rewrites so `/privacy` and `/terms` map to the `.html` files

## One-time deploy

1. Push the `samplehook-legal` repo to GitHub.
2. https://vercel.com/new → **Import Git Repository** → pick `jagusking/samplehook-legal`
3. Framework Preset: **Other** (it's plain HTML)
4. Root Directory: leave blank (or `./`)
5. Click **Deploy**. ~30 seconds to a `*.vercel.app` preview URL.

## Custom domain

1. Vercel project → **Settings → Domains** → **Add**
2. Enter `samplehook.app` → Vercel will detect the apex and offer two DNS options
3. Recommended: **A record** to `76.76.21.21` (Vercel's apex IP). Add in Cloudflare:
   - Type **A**, Name `@`, IPv4 `76.76.21.21`, Proxy status **DNS only** (gray cloud)
4. Optionally also add `www.samplehook.app`:
   - Type **CNAME**, Name `www`, Target `cname.vercel-dns.com`, **DNS only**
5. Vercel auto-provisions SSL within 60 seconds. Done.

## Updating later

- Edit the HTML files locally
- `git push origin main` from this repo
- Vercel auto-deploys in ~20 seconds

## Switching from GitHub Pages

If GitHub Pages was previously wired to the same domain:

1. GitHub repo → **Settings → Pages → Custom domain → Remove**
2. In Cloudflare DNS, delete the four `185.199.10X.153` A records that pointed to GitHub Pages
3. Then add the Vercel A record above
