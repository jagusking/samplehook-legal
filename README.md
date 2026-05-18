# SampleHook Legal — publishing guide

This folder contains the Privacy Policy + Terms of Use that App Store Connect
requires URLs for. Two ways to publish; pick one.

## Option A — Separate repo, custom domain (Recommended)

Cleanest because it keeps the iOS source repo private if you ever want to,
and gives you a real `samplehook.app/privacy` URL.

1. Create a new public GitHub repo named `samplehook-legal`.
2. Copy `privacy.md`, `terms.md`, `index.md`, and `_config.yml` into the root
   of that repo.
3. In repo **Settings → Pages**:
   - Source: **Deploy from a branch**, branch: `main`, folder: `/ (root)`
   - Click **Save**
4. Wait ~1 minute. The site is live at
   `https://<your-github-username>.github.io/samplehook-legal/`
5. To get the friendly `samplehook.app/privacy` URL:
   - Buy `samplehook.app` (or use whichever domain you control)
   - DNS: add a CNAME record pointing `samplehook.app` → `<username>.github.io`
   - In Pages settings, set the custom domain to `samplehook.app`
   - Wait for the cert provision (~10 min)
6. Final URLs to paste into App Store Connect:
   - Privacy: `https://samplehook.app/privacy/`
   - Terms: `https://samplehook.app/terms/`

## Option B — Subfolder of the existing repo

Faster but couples publishing to the iOS source repo.

1. Push this `legal/` folder as-is to `main`.
2. In the existing VoxShot repo **Settings → Pages**:
   - Source: **Deploy from a branch**, branch: `main`, folder: `/legal`
   - Click **Save**
3. Wait. The site goes live at
   `https://<username>.github.io/VoxShot/privacy/`
4. Paste that URL into App Store Connect. (No custom domain unless you wire
   one up.)

## After publishing

- Verify both URLs load in a browser and on mobile Safari before pasting them
  into App Store Connect.
- Update App Store Connect → App → **App Information** → **Privacy Policy URL**
- Apple displays the Terms URL as **EULA**. If you don't set one, Apple uses
  their default EULA. To use your own:
  - App → **App Information** → **License Agreement** → **Set Custom EULA** →
    paste the Terms URL or upload the markdown content as a EULA.

## Updating the policies later

- Edit the `.md` files
- Bump the "Last updated" date at the top of each
- Commit + push — GitHub Pages auto-rebuilds in ~30s
- Mention the change in the next app release notes

## Contact emails referenced

The policies reference `support@samplehook.app` and `privacy@samplehook.app`. Set
these up before publishing — easiest path is to enable email forwarding from
your domain registrar (Cloudflare Email Routing is free) and point both to a
single inbox you check.
