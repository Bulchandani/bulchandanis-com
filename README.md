# bulchandanis.com — family hub

Static landing page at the apex of `bulchandanis.com`. Single `index.html`, no build step. Lists each family member with a card linking to their subdomain (or a "Coming soon" placeholder until their site exists).

## Structure

```
bulchandanis-hub/
├── index.html       Single-page hub
├── CNAME            bulchandanis.com (for GitHub Pages fallback)
├── README.md        This file
├── .gitignore
└── assets/
    └── tarun.jpg    Tarun's headshot
    (rhea.jpg + reyna.jpg to be added when available)
```

## Adding a new family member's site

1. They build and deploy their site at `<name>.bulchandanis.com` (their own repo, their own Cloudflare Pages project)
2. Drop their photo in `assets/<name>.jpg`
3. Edit `index.html`:
   - Replace the placeholder member card's `<div class="member-photo">` initial with `<img src="assets/<name>.jpg" alt="...">`
   - Update the `member-bio` paragraph
   - Change the CTA from `<span class="member-cta--soon">Coming soon</span>` to `<a class="member-cta member-cta--live" href="https://<name>.bulchandanis.com">Visit site →</a>`
4. Push. Cloudflare Pages auto-deploys.

## Deployment

Hosted on Cloudflare Pages, custom domain `bulchandanis.com` (and optionally `www.bulchandanis.com` redirected to apex).

```bash
git init
git add .
git commit -m "Initial family hub"
gh repo create Bulchandani/bulchandanis-com --public --source=. --remote=origin --push
```

Then in Cloudflare:
1. Workers & Pages → Create application → Pages → Connect to Git → pick the repo
2. Build settings: Framework preset `None`, build command empty, output directory `/`
3. Save and Deploy → get the `*.workers.dev` (or `*.pages.dev`) URL
4. Settings → Domains → Add Custom Domain → `bulchandanis.com`
5. (Optional) Add another custom domain `www.bulchandanis.com` for the www variant
6. Cloudflare auto-creates routing records and provisions SSL

## Design notes

- Same typography as `tarun.bulchandanis.com` (Space Grotesk + DM Sans) for family-of-sites cohesion.
- Each member gets a distinct gradient: Tarun (teal–purple, current brand), Rhea (coral–pink), Reyna (blue–cyan).
- Single-column on mobile (< 880px), 3-column on desktop.
- WCAG 2.1 AA: focus-visible rings, semantic HTML, prefers-reduced-motion respected, real text in headings (not images).
