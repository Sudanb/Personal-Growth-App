# Personal Growth — Local PWA

A quantified-self tracker you host yourself and install as a real Android app.
Data stays in your browser's localStorage, never leaves the device.

## Files

- `index.html` — the app (single file, no build step)
- `manifest.webmanifest` — PWA manifest (name, icons, standalone display)
- `sw.js` — service worker (offline caching)
- `icon.svg` — app icon
- `icon-maskable.svg` — adaptive icon for Android's launcher mask

## Deploy — GitHub Pages (recommended, ~2 min)

Easiest path. Free. HTTPS. Works forever.

1. Create a new **public** repo on GitHub, e.g. `personal-growth`.
2. Upload all 5 files (plus this README if you want) to the repo root.
   - Web UI works: *Add file → Upload files → drag them in → Commit*.
3. In the repo: **Settings → Pages**.
4. Under *Source*, pick `Deploy from a branch`, branch `main`, folder `/ (root)`. Save.
5. Wait ~1 min. GitHub shows the URL — something like
   `https://<your-username>.github.io/personal-growth/`
6. Open that URL on your Poco in Chrome.
7. Chrome menu (⋮) → **Install app** (or "Add to Home Screen").
8. Launch from the home-screen icon. Standalone window, no browser chrome.

### Updating later

Edit `index.html` in GitHub (pencil icon → commit), wait ~30s, reopen the app.
The service worker caches aggressively — if a change doesn't appear:
- Pull down to refresh, OR
- Settings → Apps → Personal Growth → clear cache, OR
- Bump the `CACHE` version string in `sw.js` (e.g. `'personal-growth-v0.4'` → `'personal-growth-v0.5'`).

## Alternative — Netlify Drop

If you don't want a GitHub account:

1. Go to [app.netlify.com/drop](https://app.netlify.com/drop).
2. Drag the folder containing these files onto the page.
3. Netlify gives you a URL. Install as PWA from that URL same as above.

## What you get vs. the hosted artifact

- **Home-screen icon** that looks like an app
- **Standalone window** (no Chrome address bar)
- **Full offline** — works on airplanes, dead zones, flaky wifi
- **You own the URL** — artifact URL can be deprecated; GitHub Pages won't be
- **No dependency on claude.ai** to run the app
- Data stays only in the browser's localStorage on your phone

## What this still doesn't do (same as artifact)

- **No OS push notifications** — the purge warning is still an in-app banner
  only. True scheduled notifications need either background sync (unreliable)
  or a native wrapper (Capacitor, TWA). A monthly reminder on the 1st via your
  phone's clock app works just as well.
- **No cross-device sync** — data lives in one browser's localStorage on one
  device. If you clear Chrome data or switch phones, use **Export** first and
  paste the JSON back yourself.
- **No automatic backup** — manually export and save the JSON at the end of
  each month, that is literally what the Export tab is for.

## Going further — native APK

If you later want a real APK with proper push notifications:

1. Keep the PWA hosted on GitHub Pages
2. Use [Bubblewrap](https://github.com/GoogleChromeLabs/bubblewrap) to wrap the
   PWA URL as a TWA (Trusted Web Activity)
3. `bubblewrap init --manifest=https://<your-url>/manifest.webmanifest`
4. `bubblewrap build` → signed APK → sideload to the Poco

That's a separate hour's work. The hosted PWA is enough for daily use.
