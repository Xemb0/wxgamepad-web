# WxGamepad — Marketing Site

Standalone landing site for **WxGamepad**, intended for the subdomain
**`wxgamepad.imautotech.in`**. Mirrors the `watchparty-web` setup (static, Netlify),
but marketing-only — WxGamepad has no web build, so there is no `/app/` web app.

## Stack
- Plain static HTML + [Tailwind CDN](https://cdn.tailwindcss.com) — **no build step**.
- Screenshot gallery is data-driven from the shared **`product-assets`** Supabase
  project (`js/supabase-config.js` + `js/gallery.js`, slug `wx-gamepad`) — the same
  project the imautotech site uses.

## Files
```
index.html             Landing page (hero, features, how-it-works, downloads, gallery)
privacy-policy.html    Privacy Policy  → use as the App Store / Play Store privacy URL
terms-of-service.html  Terms of Service (incl. auto-renewable subscription terms)
contact.html           Contact page
js/supabase-config.js  Shared product-assets Supabase client (anon key)
js/gallery.js          loadGallery('wx-gamepad') — screenshots + lightbox
netlify.toml           Static publish config
```

## Local preview
```bash
cd wxgamepad-web
python3 -m http.server 8080   # then open http://localhost:8080
```
(Use a server rather than opening the file directly, so the Supabase gallery fetch works.)

## Deploy (Netlify) + subdomain
1. Create a new Netlify site from this folder/repo. Publish directory = `.` (set in `netlify.toml`).
2. In Netlify → Domain settings, add the custom domain **`wxgamepad.imautotech.in`**.
3. At the `imautotech.in` DNS provider, add a **CNAME** record:
   `wxgamepad` → `<your-site>.netlify.app` (Netlify shows the exact target).
4. Once DNS propagates, point the apps/stores at the new URLs:
   - App Store Connect / Play Console **Privacy Policy URL** → `https://wxgamepad.imautotech.in/privacy-policy.html`
   - The iOS paywall currently uses `imautotech.in/privacy-policy`; update to the new URL for consistency.

## ⚠️ Placeholders to fill before going live (search the code for `TODO`)
- **Play Store link** — confirm `com.autotech.wxgamepad` listing is live (used in hero + download section).
- **App Store link** — currently "coming soon"; replace the `#` in `index.html` once the iOS app is approved.
- **Desktop server downloads** — currently point at
  `github.com/Xemb0/Autotech_WxGamepad/releases/latest`. Confirm the repo/releases are
  **public**, or swap for direct asset URLs (Drive / Supabase). The desktop CI publishes
  binaries to a GitHub Release.
- **Hero / OG image** — `index.html` references `product-assets/wx-gamepad/hero.png`. Confirm it exists or swap.
- **Support email** — `support@imautotech.in` (used on contact / privacy / terms pages).
- **Screenshots** — managed in the shared Supabase (`products`/`product_screenshots`, slug `wx-gamepad`).
