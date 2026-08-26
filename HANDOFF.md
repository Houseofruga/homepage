# House of Ruga — homepage handoff

State as of 2026-08-26. Working tree clean, everything pushed to `main`.

## What this repo is

The **houseofruga.com** studio homepage. Plain **static HTML — no framework, no build step**.
This repo is **studio-homepage-only**: product landing pages do NOT live here. Each product's
landing + app live on their own subdomain repo (e.g. TrailWatch is at
`trailwatch.houseofruga.com`, in a separate repo).

## Files

- `index.html` — the entire homepage (inline `<style>` + a little vanilla JS at the bottom).
- `vercel.json` — redirects. `/trailwatch` and `/trailwatch/` 301 → `https://trailwatch.houseofruga.com`
  (the landing used to live here and was moved out; this keeps old links alive).
- `houseofruga-logo.svg` — the colorful House of Ruga mark. Used in the header AND footer.
- `trailwatch/logo.svg` — TrailWatch logo (lime scribble + wordmark). Used by the product card.
- `House of Ruga color index.zip` — a Claude Design export (design source, NOT a site asset).
  Untracked on purpose — keep it out of commits.

Assets use **root-absolute paths** (`/houseofruga-logo.svg`, `/trailwatch/logo.svg`), so preview
must be served from the repo root, not opened as `file://`:

```bash
python3 -m http.server 8000
```

## Deploy

Solo static site — **push straight to `main`, don't branch/PR.**
Flow: `commit → push to main → Vercel auto-deploys`.
Site is fronted by **Cloudflare** — after a deploy, purge the Cloudflare cache (or hard-refresh)
or you'll see the old version. (Cloudflare fronts Vercel because Jio blocks Vercel's IPs directly.)

## Design / identity

Rebuilt from a Claude Design `.dc.html` that the user hand-designs, ported to plain HTML/CSS/JS.

- **Palette:** cream bg `#FFF8E5`, ink `#291A1A`, dark product band `#1A1010`,
  TrailWatch accent lime `#9FF50A`.
- **Type:** Clash Display 600/700 (Fontshare) for the big uppercase thesis/headings,
  Satoshi 400/500/700 (Fontshare) for body, JetBrains Mono 400/500 (Google) for labels/eyebrows.
- **Sections, top → bottom:** header logo → mono eyebrow → bold thesis
  ("Tools we built for ourselves. Now yours.") → dark **PRODUCTS** band with product cards →
  "Say hi." contact → footer ("HOUSE OF RUGA — EST. 2026").
- **Motion:** thesis word-by-word rise on load + IntersectionObserver scroll-reveal (`data-reveal`).
  Both gated on `prefers-reduced-motion`. Mobile breakpoint is `max-width:760px`.
- **Contact:** email is `houseofrugaofficial@gmail.com` (real business email). X is the only public
  social. The GitHub org link is intentionally hidden — keep it hidden on public pages.

## To add a new product

1. Add its logo here: `<product>/logo.svg`.
2. Add a product card to the PRODUCTS band in `index.html`, linking straight OUT to
   `https://<product>.houseofruga.com` (`target="_blank" rel="noopener noreferrer"`).
3. Build the product's landing on its own subdomain repo — NOT here.
4. If a product path is ever retired to its subdomain, add a redirect pair in `vercel.json`
   (mirror the `/trailwatch` entries).

## Right now

Homepage is done and live. Nothing is mid-edit. Next work is likely a new product card or a
homepage copy tweak.
