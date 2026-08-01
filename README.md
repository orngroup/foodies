# Find Foodies — full PWA demo

**Love Food. Love Life.** A dating & meet-up app that matches people on shared cuisine, then helps them find a venue and book a table.

Self-contained **clickable demo** (demo mode — sample data, no live backend). All images and data are bundled, so it runs fully offline once loaded. Destined for **findfoodies.com**.

## Complete feature set
- **Sign-up** — Google (realistic account-picker), Apple, Instagram, Facebook, or email
- **Onboarding** — details → cuisine picker → dietary & faith prefs (halal, kosher, vegan…) → verified photo
- **Swipe matching** — drag cards or buttons; green tags = cuisines you *both* love; super-like & rewind
- **"It's a Match"** — instantly suggests a venue that works for *both*
- **Chat** — icebreakers, typing indicators, in-chat venue sharing
- **Video date** — private in-app call before meeting (number stays hidden)
- **Safety centre** — share-my-plan, safe-arrival check-in, meet-in-public, block & report
- **Venues** — 24 sample London restaurants with postcode/area search, distance radius, dietary & offer filters, list + map view
- **Meet-ups** — group dining tables to join, not just 1-on-1
- **Book a table** → confirmation with the venue's offer applied
- **Profile**, Free vs **Gold Foodie** (£14.99/mo), Help & contact (hello@findfoodies.com)
- **Installable PWA** — real "heart + fork" app icon, offline support, notifications for matches/messages/bookings

## Files
```
index.html                app
venues.js                 London venue dataset (areas, postcodes, coordinates)
sw.js                     service worker (offline + notifications)
manifest.webmanifest      install metadata (Find Foodies)
icon-*.png                app icons — heart with a fork (incl. maskable)
apple-touch-icon.png      iOS home-screen icon
favicon.png               tab icon
img/                      headshots (p*.jpg) + venue art (rv*.jpg)
```

## Host on GitHub Pages
1. Create a repo (e.g. `findfoodies`).
2. Upload **everything, keeping the `img/` folder**, to the repo root.
3. Settings → **Pages** → Deploy from a branch → `main` / root → Save.
4. Live at `https://<username>.github.io/findfoodies/` in ~1 minute.

Later, point **findfoodies.com** at it (GitHub Pages supports custom domains under Settings → Pages).

### On your phone
- **Android/Chrome:** tap **Install** on the banner. It asks for notifications after you enter the app.
- **iPhone/Safari:** **Share → Add to Home Screen**, open from the icon.
- Install & notifications need **HTTPS** — GitHub Pages provides it automatically.

## What's real vs demo
- **Real:** London areas, postcodes, coordinates, distance maths, search, all UI flows, installability, notifications.
- **Demo:** the restaurants & people are sample data; **Google/Apple/social sign-in is a realistic mock** — genuine OAuth needs a backend + Google Cloud project + client ID. Live restaurant data and street maps also come with the backend build.

## Next steps (the real build)
1. **Backend** — real auth (Google/Apple/email OAuth), database (profiles, matches, messages, bookings), image storage.
2. **Venue portal** — restaurants log in to post offers, see bookings, pay the per-booking fee.
3. **Admin backend** — manage users, venues, revenue.
4. **Live data** — real restaurants (e.g. Google Places API) and maps.
5. Trademark check on "Find Foodies" (UK IPO, classes 9, 43, 45) before launch.
