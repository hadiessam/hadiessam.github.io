# Connecting hadiessam.com to the site

The site is **already live** at https://hadiessam.github.io

Follow these steps only after buying the domain.

---

## 1. Buy the domain

Cheapest at-cost registrar: **Cloudflare Registrar** — about **$8.57/year** for a `.com`
(no markup, no inflated renewal). Namecheap is a fine alternative at roughly $11–14.

Search for `hadiessam.com` and complete the purchase.

---

## 2. Point the DNS at GitHub Pages

In the registrar's DNS panel, create these records.

### Apex domain (`hadiessam.com`)

Four `A` records, all with host `@`:

| Type | Name | Value           |
|------|------|-----------------|
| A    | @    | 185.199.108.153 |
| A    | @    | 185.199.109.153 |
| A    | @    | 185.199.110.153 |
| A    | @    | 185.199.111.153 |

### Optional IPv6

Four `AAAA` records, host `@`:

| Type | Name | Value                |
|------|------|----------------------|
| AAAA | @    | 2606:50c0:8000::153  |
| AAAA | @    | 2606:50c0:8001::153  |
| AAAA | @    | 2606:50c0:8002::153  |
| AAAA | @    | 2606:50c0:8003::153  |

### www subdomain

| Type  | Name | Value                 |
|-------|------|-----------------------|
| CNAME | www  | hadiessam.github.io   |

> If Cloudflare manages the DNS, set these records to **DNS only** (grey cloud) while
> GitHub issues the certificate, then you can proxy them afterwards if you want.

---

## 3. Tell GitHub about the domain

```bash
cd "E:/Hadi work/Website"

# the file already exists locally but is gitignored until now
# (remove it from .gitignore first)
git add CNAME
git commit -m "Point the site at hadiessam.com"
git push
```

`CNAME` must contain exactly one line:

```
hadiessam.com
```

Then in the repository: **Settings → Pages → Custom domain** → enter `hadiessam.com`
→ **Save**.

---

## 4. Turn on HTTPS

Back on **Settings → Pages**, wait for the certificate to be issued (usually 5–30
minutes, sometimes up to 24 hours), then tick **Enforce HTTPS**.

---

## 5. Verify

```bash
curl -sI https://hadiessam.com | head -3
curl -sI https://www.hadiessam.com | head -3
```

Both should return `HTTP/2 200`.

---

## Notes

- `sitemap.xml` and `robots.txt` already reference `https://hadiessam.com/`, so no
  changes are needed there.
- The `<link rel="canonical">` tag and all Open Graph URLs also already point at
  `hadiessam.com`.
- Do not add the `CNAME` file before the DNS records exist, or the GitHub Pages URL
  will start redirecting to a domain that does not resolve yet.
