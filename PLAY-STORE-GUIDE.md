# SHADOW COPY 3D — Play Store Publishing Guide

Follow these steps in order. Steps 1–3 are one-time setup; steps 4–8 you
repeat for every update.

## Step 1 — Create your Play Console account (one time)

1. Go to https://play.google.com/console and sign in with a Google account.
2. Pay the one-time **$25** developer registration fee.
3. Complete identity verification (Play asks for it before you can publish).

## Step 2 — Create the app

1. Play Console → **Create app**.
2. App name: **Shadow Copy** (you can also use "Shadow Copy 3D" — see
   `STORE-LISTING.md`).
3. Default language: **English (United States)**.
4. App or game: **Game**.
5. Free or paid: **Free**.
6. Declarations: accept the developer program policies, and confirm:
   - It does **not** contain ads (unless you add them later).
   - It is **not** a COVID/contact-tracing app, etc. — answer honestly.
7. The app's **Dashboard** now shows a setup checklist. Work through it:

## Step 3 — Fill in the dashboard tasks

### Privacy policy (required before you can publish)
- Host `PRIVACY_POLICY.md` somewhere public with a stable URL. Easiest free
  options: a GitHub repository's raw file, GitHub Pages, or your own website.
- Play Console → **App content → Privacy policy** → paste the URL.
- Why it's required even though the game collects nothing: Play requires a
  policy URL for every app.

### App access
- "Does your app require sign-in?" → **No** (the game has no accounts).

### Ads
- "Does your app contain ads?" → **No**.

### Content rating
- **App content → Content rating** → Start questionnaire.
- Answer honestly (no realistic violence against humans, no sexual content,
  no gambling, no user chat). Expect a rating of **Everyone**.
- Apply the rating to all countries it offers.

### Target audience and content
- Target age group: **13+** is the safe choice (or "Everyone" if the rating
  questionnaire allows it — the game has mild sci-fi robot combat).
- Confirm the app is **not** primarily directed at children.

### News app, COVID, data safety, etc.
- News: **No**. Government: **No**.
- **Data safety** — use the ready answers in `STORE-LISTING.md`:
  "No data collected, no data shared." (The game stores progress only on the
  device and never contacts a server.)

### Store listing
- Play Console → **Grow → Store presence → Main store listing**.
- Paste the texts from `STORE-LISTING.md`:
  - App name, short description (max 80 chars), full description.
  - App icon: upload `play-store-icon-512.png` (512×512).
  - Feature graphic: **1024×500** — make one in any image editor
    (title + a screenshot of the game works well).
  - Phone screenshots: **at least 2** — capture them from the game running
    on your phone or an emulator (menu screen + gameplay).
  - Category: **Game → Puzzle** (or Action — pick Puzzle, since the core
    mechanic is puzzle-solving with the shadow clone).
  - Tags: puzzle, 3d, shadow, clone, sci-fi (Play suggests tags as you type).
  - Contact email: your support email (shown publicly on the listing).

### Countries
- **Release → Production → Countries / regions** — select the countries
  you want (or "all available").

## Step 4 — Build the signed release AAB

Follow `README-ANDROID.md` → "Build the signed release AAB for the Play Store".
You will get `android/app/release/app-release.aab`.

**Back up your upload keystore (.jks) and passwords in two places.** If you
lose it, you cannot update the app, ever.

## Step 5 — Upload to Internal testing first (recommended)

1. Play Console → **Release → Testing → Internal testing → Create new release**.
2. Upload `app-release.aab`.
3. Add yourself as a tester (your Gmail) and install it from the Play link
   on your phone. Play-test: menu, touch controls, sound, vibration,
   pause, save-after-restart, and the whole of Level 1.
4. Fix anything that breaks, rebuild, upload a new version
   (bump `versionCode` each time).

## Step 6 — Promote to Production

1. **Release → Production → Create new release**.
2. Either upload the same AAB again or **Promote release** from Internal
   testing.
3. Release notes: e.g. "First release — 3D action-puzzle adventure with the
   shadow-clone mechanic. 3 levels, sentinel drones, checkpoints."
4. Review and roll out. Play's review usually takes **a few hours to a few
   days**. Watch your email for the approval notice (or policy questions).

## Step 7 — After launch

- Watch **Android vitals** (crashes/ANRs) in the console for the first week.
- For every update: replace `www/index.html`, `npx cap sync android`,
  bump `versionCode` in `android/app/build.gradle`, rebuild the signed AAB,
  upload to Production with release notes.

## Common gotchas

- **"App bundle not signed"** — you uploaded a debug build. Use the wizard in
  `README-ANDROID.md` (Generate Signed App Bundle) and pick **release**.
- **"Version code already used"** — bump `versionCode` by 1 in
  `android/app/build.gradle` and rebuild.
- **"Missing privacy policy"** — paste the hosted policy URL under
  App content → Privacy policy.
- **"Target API level" warning** — this project targets API 36, which meets
  the current requirement. If Play raises it later, update `targetSdkVersion`
  in `android/variables.gradle` and rebuild.
- **64-bit requirement** — WebView-based apps are compliant; nothing to do.
- **"Designed for families"** — only opt in if you want the extra review;
  not required.
