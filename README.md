# Vertex Mobile

Corporate landing site for **Vertex Mobile** — an independent Android studio
that builds lightweight, privacy-first mobile utilities. The site is a pure
static build served directly from GitHub Pages at
[vertexmobile.tech](https://vertexmobile.tech).

## Stack

No build step. Plain **HTML5 + CSS3 + vanilla JavaScript**, chosen for:

- Zero-config deployment to GitHub Pages
- Instant Time-to-Interactive (no framework hydration)
- No supply-chain surface and no runtime dependencies
- Trivial to audit for Google Play reviewers and SSP / AdTech partners

## Project structure

```
.
├── index.html                  # Landing page (hero, portfolio, features, CTA)
├── privacy-policy.html         # Play Store-compliant privacy policy
├── Terms_and_Conditions.html   # Terms of service
├── app-ads.txt                 # MUST remain at the root for AdMob verification
├── robots.txt
├── sitemap.xml
├── CNAME                       # Custom domain for GitHub Pages
└── assets/
    ├── css/styles.css          # Shared dark-theme stylesheet
    ├── js/main.js              # Mobile nav + micro-interactions
    └── img/                    # Brand mark, favicon
```

### `app-ads.txt`

`app-ads.txt` is served exactly at `https://vertexmobile.tech/app-ads.txt`
(no nested folder) — this is required by Google AdMob / IAB for
authorized-seller verification. Do **not** move it under `assets/`.

## Local development

No tooling is required. Serve the folder with any static server, e.g.

```bash
# Python 3
python3 -m http.server 8080

# or Node (if installed)
npx serve .
```

Then visit http://localhost:8080.

## Deploying to GitHub Pages

This repo deploys directly from the default branch — no Actions, no build.

1. Push to the `main` branch on GitHub.
2. In the repository settings, open **Settings → Pages**.
3. Set **Source = Deploy from a branch**, **Branch = `main`**, **Folder = `/` (root)**.
4. Under **Custom domain**, enter `vertexmobile.tech`. The `CNAME` file in
   this repo is already set accordingly.
5. Configure DNS for `vertexmobile.tech`:
   - An `A` record to each of GitHub Pages' four IPs, **or**
   - A `CNAME` record pointing to `<your-gh-username>.github.io`.
6. Enable **Enforce HTTPS** once the certificate has been issued.

Verify after deploy:

- `https://vertexmobile.tech/` — landing page renders
- `https://vertexmobile.tech/privacy-policy.html` — privacy page renders
- `https://vertexmobile.tech/app-ads.txt` — returns the publisher manifest
  as plain text (MIME `text/plain`)

## Editing the brand mark

The logo is an inline SVG (a gradient-stroked `V` with a signature dot on
the upper-right vertex). The master copy lives at
`assets/img/logo-mark.svg`; the header and footer inline a copy of the
same geometry to avoid an extra HTTP request.

## License

Code is MIT-licensed (see `LICENSE`). The "Vertex Mobile" name and the
associated brand mark are trademarks of Vertex Mobile and are **not**
covered by the code license.
