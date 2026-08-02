# Find Foodies — Setup & Launch Guide

Everything you need to take this from demo to live, in plain English. Work top to bottom.

---

## What's in this package

```
findfoodies/
├── index.html          → marketing website (homepage)
├── app/                → the PWA dating app (what users use)
│   └── firebase-config.js   ← your keys go here
├── portal/             → restaurant partner login + dashboard
├── admin/              → your admin console
├── firebase.json       → Firebase Hosting config
└── SETUP-GUIDE.md      → this file
```

Live URL structure once hosted:
- `findfoodies.com/`         → website
- `findfoodies.com/app/`     → the app (users log in here — linked from the top of the site)
- `findfoodies.com/portal/`  → restaurants (linked at the bottom of the site under "Partners")
- `findfoodies.com/admin/`   → you

**Right now everything runs in DEMO MODE** — real-looking, sample data, nothing saved. The steps below switch it to live.

---

## Part 1 — Put it live on Firebase Hosting (about 20 minutes)

You need: a Google account, and Node.js installed on your computer (nodejs.org).

1. **Create a Firebase project**
   - Go to https://console.firebase.google.com → *Add project* → name it `findfoodies` → follow prompts.

2. **Install the Firebase tools** (in a terminal / command prompt):
   ```
   npm install -g firebase-tools
   firebase login
   ```

3. **Point this folder at your project.** Unzip this package, open a terminal *inside* the `findfoodies` folder, then:
   ```
   firebase use --add
   ```
   Pick your `findfoodies` project when asked.

4. **Deploy:**
   ```
   firebase deploy --only hosting
   ```
   Firebase prints a live URL like `https://findfoodies.web.app`. Open it — your site, app, portal and admin are all live (still in demo mode).

5. **Use your own domain** (optional, when ready): Firebase console → *Hosting* → *Add custom domain* → `findfoodies.com`, follow the DNS steps at your registrar (123-reg/GoDaddy).

**You now have a live PWA people can visit and install.** For a pitch or early testers, you could stop here.

---

## Part 2 — Make sign-in real (Firebase Authentication)

1. Firebase console → *Build → Authentication → Get started*.
2. Enable **Google** and **Email/Password** (add **Apple** later — needs an Apple Developer account).
3. Firebase console → *Project settings → General → Your apps* → click the web icon `</>` → register an app → copy the `firebaseConfig` object it shows you.
4. Open `app/firebase-config.js` and paste those values over the placeholders at the top.
5. In the same file, set `const DEMO_MODE = true;` to `false` once a developer has wired the auth calls (the `FF.signInWithGoogle` function has commented-out live code showing exactly what goes there).

> The commented "LIVE:" lines in `firebase-config.js` show the real Firebase code for each function. A developer fills these in — it's a well-trodden path, a few days of work.

---

## Part 3 — Make data real (Firestore database)

1. Firebase console → *Build → Firestore Database → Create database* → Start in **production mode** → pick a location (europe-west for UK).
2. Create these collections (a developer wires the app to read/write them):
   - `users/{uid}` — profile, cuisines, taste profile, photos
   - `likes` — who liked whom
   - `matches` — mutual likes
   - `messages/{matchId}` — chat messages
   - `bookings` — table bookings
   - `venues` — restaurants (until you use Google Places)
   - `recommendations` — member-suggested restaurants
   - `reports` — safety reports
3. **Security rules matter most here.** Set rules so users can only read/write their own data and can't see others' private info. Get this reviewed — it's where data leaks happen. Firebase has templates; a developer should tailor them.

---

## Part 4 — Real restaurant data (Google Places) — optional, do when ready

1. Go to https://console.cloud.google.com → same Google account → your Firebase project is already there.
2. *APIs & Services → Enable APIs → enable **Places API**.*
3. *Credentials → Create credentials → API key.* Restrict the key to Places API and your domain.
4. Paste the key into `app/firebase-config.js` (`GOOGLE_PLACES_KEY`) and set `USE_PLACES = true`.
5. A developer maps Places results into the app's venue format (the `FF.getVenues` function shows where). **Note:** Places charges per request after a free monthly credit — fine at small scale, watch it as you grow.

> **OpenTable / TheFork:** these are *partner programmes you apply to* (opentable.com/restaurant-solutions/api-partners), not instant keys. Approval favours established apps. Launch with Places + your own booking flow first; apply to OpenTable later once you have users to show them.

---

## Part 5 — Launch on Google Play (do this first — friendlier than Apple)

Your app is a PWA, so you wrap it for the Play Store with a **TWA (Trusted Web Activity)** — no rewrite needed.

1. Pay the **one-time $25** Google Play developer fee: https://play.google.com/console
2. Use **PWABuilder** (free): https://www.pwabuilder.com → enter your live app URL (`findfoodies.com/app/`) → it generates a signed Android package.
3. Upload that package in the Play Console, fill in listing (icon, screenshots, description, privacy policy URL), and submit.
4. Dating apps need a privacy policy and content rating — fill these honestly. Review usually takes a few days.

## Part 6 — Apple App Store (next)

1. **Apple Developer account: £79/year** (developer.apple.com).
2. Wrap the PWA (PWABuilder also outputs iOS, or use Capacitor).
3. Apple's review is stricter — have real T&Cs, a working sign-in, account deletion, and safety features (you have these). Expect a couple of review rounds.

---

## Sensible launch order (recommended)

1. ✅ Deploy to Firebase Hosting (demo) — **you can do this today.**
2. Wire Firebase Auth + Firestore (developer, ~1–2 weeks).
3. Test with real friends as founding members.
4. Add Google Places for real venues.
5. Sign a handful of local restaurants (use the portal + your phone demo to pitch them).
6. Launch on Google Play.
7. Add Apple, ID verification (Stripe Identity/Yoti), and OpenTable once you have traction.

---

## Honest notes

- **Demo vs live:** everything looks real but stores nothing until Parts 2–3 are done. Don't take real users until auth + database + security rules are live and reviewed.
- **You'll want a developer** for Parts 2–4 and the security rules. This package is the exact spec — hand it over and it saves them (and you) weeks.
- **Costs to expect:** Firebase (free tier generous, then pay-as-you-grow), Google Places (per-request), Play $25 one-time, Apple £79/yr, ID checks ~£1–1.50 each (later), a developer's time.
- **Compliance:** dating + user data = GDPR duties, T&Cs, moderation, and a real privacy policy. Sort these before public launch.

Questions or want any part expanded into step-by-step with screenshots? Keep this file — it's your roadmap.
