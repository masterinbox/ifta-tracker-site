# IFTA Tracker marketing site

Static site — no build step, no dependencies. Pages: `/` (landing),
`/terms/`, `/privacy/`, `/support/`. The app's paywall and Settings link to
`haultax.app/terms` and `haultax.app/privacy`, so keep those paths stable.

## Deploy to GitHub Pages

From this `website/` folder:

```bash
cd website
git init -b main
git add -A
git commit -m "IFTA Tracker marketing site"
gh repo create ifta-tracker-site --public --source . --push
gh api repos/{owner}/ifta-tracker-site/pages -X POST -f build_type=legacy -f "source[branch]=main" -f "source[path]=/"
```

The site goes live at `https://<your-username>.github.io/ifta-tracker-site/`
within a minute or two. (Relative paths throughout, so it works at any base
URL.)

## Custom domain (haultax.app)

1. Buy `haultax.app` at any registrar.
2. In the GitHub repo → Settings → Pages → Custom domain → `haultax.app`
   (this creates the CNAME file), and check **Enforce HTTPS** once the cert
   issues.
3. At the registrar, add DNS records:
   - `A` records for the apex: `185.199.108.153`, `185.199.109.153`,
     `185.199.110.153`, `185.199.111.153`
   - `CNAME` for `www` → `<your-username>.github.io`
4. Then update App Store Connect (or ask Claude to do it via API):
   support URL `https://haultax.app/support/`, marketing URL
   `https://haultax.app/`, privacy policy URL `https://haultax.app/privacy/`.

## Local preview

```bash
python3 -m http.server 8901 --directory website
```

## Launch-day edits

- `index.html`: swap the "Coming to the App Store" button for the real
  App Store badge/link, and change the CTA copy back to "Start free — 7 days".
- Promotional/seasonal copy: the `#get` section and hero sub-line.
