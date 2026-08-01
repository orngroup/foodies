# Foodies — installable PWA demo

**Love Food. Love Life.** A dating app that matches people on shared cuisine, suggests a venue that works for both, and books the table.

This is a self-contained **clickable demo** — no backend, no real accounts. All images (your headshots + venue art + app icon) are bundled, so it works fully offline once loaded.

## What's new in this version
- Uses your **real headshots** for profiles
- A proper **Foodies app icon** (script "F" + heart, brand red, maskable for Android/iOS)
- **Installable**: an "Install Foodies" prompt on Android/Chrome, and Add-to-Home-Screen guidance on iPhone
- **Notifications**: asks permission at a natural moment, then sends real alerts on new matches, messages and bookings (also re-triggerable from Profile → Notifications)
- Works offline via a service worker

## The full journey
Onboarding (social/email → details → cuisine → dietary/faith prefs → verified photo) → **swipe matching** with shared-cuisine highlighting, super-like & rewind → "It's a Match" that suggests a venue for **both** → chat with icebreakers, typing indicators & in-chat venue sharing → venue detail → **book a table** → confirmation with the offer applied → profile, safety prompts, Free vs **Gold Foodie** plans.

## Files
```
index.html                  the app
sw.js                       service worker (offline + notifications)
manifest.webmanifest        install metadata
icon-192/512.png            app icons (any)
icon-192/512-maskable.png   app icons (maskable)
apple-touch-icon.png        iOS home-screen icon
favicon.png                 browser tab icon
img/                        headshots (p*.jpg) + venue art (v*.jpg)
```

## Host on GitHub Pages
1. Create a repo (e.g. `foodies-demo`).
2. Upload **everything in this folder, keeping the `img/` folder** to the repo root.
3. Settings → **Pages** → Deploy from a branch → `main` / root → Save.
4. Live at `https://<username>.github.io/foodies-demo/` in ~1 minute.

### Installing on your phone
- Open the Pages URL in the phone browser.
- **Android/Chrome:** tap **Install** on the banner (or menu → Install app). It asks for notifications after you enter the app.
- **iPhone/Safari:** tap **Share → Add to Home Screen**. Open it from the icon; it runs full-screen.

> Notifications and install require **HTTPS** — which GitHub Pages provides automatically. They won't work from a file opened directly off disk.

## Run locally
```
python3 -m http.server 8000
```
then visit http://localhost:8000 (note: install/notifications need the hosted HTTPS URL).

## Next steps
- Build the **venue portal** (offers, incoming bookings, pay-per-booking fee) and **admin backend**.
- Wire real auth (Google/Apple/email), a database, and image storage behind this front end.
- Gold price shown as £14.99/mo (original deck said £90) — adjust in `index.html`.
