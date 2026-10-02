# hadiessam.com

Personal site for **Hadi Essam**, Performance Marketing Specialist.

Static site: one HTML file plus assets. No build step, no dependencies, no
server-side code.

## Contents

```
index.html                     the whole site (inline CSS + a little JS)
robots.txt                     crawler rules
sitemap.xml                    single-URL sitemap
assets/
  logo/                        logo marks + favicons
  proof/                       Meta Ads Manager screenshots (case-study evidence)
  creative/                    ad creatives
  reel/                        video stills
  docs/
    Hadi_Essam_CV.pdf          one-page CV
    Hadi_Essam_Portfolio.pdf   full 10-page portfolio
```

## Local preview

Open `index.html` directly in a browser, or serve it:

```bash
python -m http.server 8000
# then visit http://localhost:8000
```

## Deploying

The site is plain static files, so any static host works.

### GitHub Pages

```bash
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin git@github.com:<user>/<repo>.git
git push -u origin main
```

Then in the repository: **Settings → Pages → Source: main / (root)**.

### Cloudflare Pages

Connect the repository, or upload the folder directly:

```bash
npx wrangler pages deploy . --project-name hadiessam
```

Either way, point the `hadiessam.com` DNS at the host once it is live.

## Notes

- The proof screenshots are the source of truth for every figure on the page.
- `index.html` also carries a print stylesheet, so Ctrl+P reproduces the
  portfolio PDF layout.
