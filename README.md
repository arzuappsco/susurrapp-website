# Susurr — Marketing Website

The static marketing site for **Susurr**, a private, on-device reading companion for iOS.
Built with plain HTML + CSS and a few lines of vanilla JavaScript. No build step, no dependencies.

**Live site:** https://susurrapp.com

---

## Files

```
.
├── index.html              # Home
├── features.html           # Features
├── support.html            # Support + FAQ
├── privacy.html            # Privacy policy (placeholder — paste your copy)
├── terms.html              # Terms of service (placeholder — paste your copy)
├── 404.html                # Custom not-found page
├── styles.css              # Shared stylesheet (design system)
├── CNAME                   # Custom domain for GitHub Pages (susurrapp.com)
├── robots.txt              # Crawler rules + sitemap reference
├── sitemap.xml             # SEO sitemap
├── favicon.ico             # Multi-res favicon (16/32/48/64)
├── apple-touch-icon.png    # iOS home-screen icon (180×180)
└── assets/
    ├── favicon.svg                 # Vector favicon (modern browsers)
    ├── apple-touch-icon-152.png    # Older iPad icon
    ├── og-image.png / .svg         # Social share image (1200×630)
    ├── hero-shot.svg               # Hero device mockup (placeholder)
    └── shot-*.svg                  # Feature screenshots (placeholders)
```

---

## Deploy to GitHub Pages

### 1. Create the repository
For a custom domain, the repo name doesn't matter (any name works). Push these files to the
**root** of the default branch (e.g. `main`).

```bash
git init
git add .
git commit -m "Susurr marketing site"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

### 2. Enable Pages
In the repo: **Settings → Pages**
- **Source:** Deploy from a branch
- **Branch:** `main` / `/ (root)`
- Save.

GitHub builds the site in ~1 minute. It will first appear at
`https://<your-username>.github.io/<repo-name>/`.

### 3. Point the custom domain
The included **`CNAME`** file already sets the domain to `susurrapp.com`. At your DNS provider,
add these records for **`susurrapp.com`**:

**Apex domain (susurrapp.com)** — add all four `A` records:
```
A    @    185.199.108.153
A    @    185.199.109.153
A    @    185.199.110.153
A    @    185.199.111.153
```

**www subdomain (recommended)** — add a `CNAME` record:
```
CNAME    www    <your-username>.github.io.
```

Then in **Settings → Pages → Custom domain**, confirm `susurrapp.com` is set, and once DNS
verifies, tick **Enforce HTTPS**. (DNS can take up to 24h to propagate; HTTPS provisioning a bit
longer after that.)

> Note: all canonical URLs, the sitemap, the Open Graph image URL, and the 404 page are already
> set for `https://susurrapp.com` at the domain root. If you ever deploy under a project path
> instead (e.g. `username.github.io/susurr/`), you'd need to update those root-relative paths.

---

## Before launch — checklist

- [ ] Replace the placeholder screenshots in `assets/` (`hero-shot.svg`, `shot-*.svg`) with real captures. Keep the filenames and you won't need to touch the HTML.
- [ ] Swap the custom **App Store** button for Apple's official badge from the [App Store Marketing Resources](https://developer.apple.com/app-store/marketing/guidelines/), and point its `href` to your real App Store URL (currently `index.html#download` / `#`).
- [ ] Paste your real **privacy policy** into `privacy.html` and **terms of service** into `terms.html` (look for the `START` / `END` markers), and fill in the "Last updated" dates.
- [ ] Confirm the contact email — currently `hello@susurrapp.com`.
- [ ] Optionally regenerate `og-image.png` if you change the tagline.

---

## Local preview

No tooling required — open `index.html` in a browser. To test the 404 page and the
root-relative paths exactly as they'll behave in production, serve the folder over HTTP:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

---

## Editing notes

- The nav bar and footer are duplicated in each HTML file (there's no templating). If you change
  a nav or footer link, update it across all pages.
- Colors, fonts, and spacing live as CSS variables at the top of `styles.css` (`:root`).
- Fonts are **Fraunces** (headings) and **Hanken Grotesk** (body), loaded from Google Fonts.
- The site respects `prefers-reduced-motion` and includes focus styles and a skip link for accessibility.
