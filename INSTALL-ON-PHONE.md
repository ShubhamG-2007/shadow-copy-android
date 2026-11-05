# Install Shadow Copy on your phone — no Play Store needed

You picked: just install it on your own phone for testing.
You need an APK file. The ZIP is source code, it cannot be installed directly.

Pick ONE path below. Path A is easiest — no Android Studio to install.

---

## Path A — Cloud build (recommended, no Android Studio)

Time: about 10 minutes + 5–8 minutes build time. Free. Works from any computer or even from your phone's browser to set up.

1. Go to https://github.com and create a free account if you don't have one.
2. Click **+ → New repository**. Name it `shadow-copy-android`. Keep it Public. Click **Create repository**.
3. On the new empty repo page, click **uploading an existing file**.
4. Unzip `shadow-copy-3d-android.zip` on your computer/phone, select ALL files inside the `shadow-copy-3d-android` folder (including the hidden `.github` folder — if you can't see it, upload it separately), drag them into GitHub, and click **Commit changes**.
   - Make sure `www/index.html`, `android/`, `package.json` and `.github/workflows/build-apk.yml` are all in the repo root.
5. Click the **Actions** tab at the top. Click **Build debug APK** on the left, then **Run workflow → Run workflow**.
6. Wait for the green tick (about 5–8 minutes). Click the finished run.
7. Scroll down to **Artifacts**, download **Shadow-Copy-debug-apk**. It downloads as a ZIP — unzip it to get `app-debug.apk`.
8. Send `app-debug.apk` to your phone (WhatsApp to yourself, Google Drive, email, or USB cable).
9. On your phone, tap the APK file → **Install**. If it asks, allow **Install unknown apps** for that app (Files / Chrome / WhatsApp), then tap Install again.
10. Open **Shadow Copy** from your app drawer and play. Test touch controls, sound, and closing/reopening — your progress should save.

To update the game later: replace `www/index.html` in the repo, re-run the workflow, download the new APK.

---

## Path B — Android Studio on your computer

Use this if you already have a computer and prefer to build locally.

1. Install **Node.js 18+** from https://nodejs.org and **Android Studio** (latest) from https://developer.android.com/studio. During Android Studio setup, install the Android SDK.
2. Unzip `shadow-copy-3d-android.zip` on your computer.
3. Open a terminal in the unzipped folder and run:
   ```
   npm install
   npx cap sync android
   ```
4. In Android Studio: **File → Open…** and select the `android` folder inside the unzipped project. Wait for Gradle sync to finish (first run downloads files — needs internet).
5. **Build → Build App Bundle(s) / APK(s) → Build APK(s)**. When it finishes, click **locate**.
6. The file is `android/app/build/outputs/apk/debug/app-debug.apk`. Copy it to your phone and tap it to install (allow "Install unknown apps" when asked).

Tip: you can also plug the phone in with USB, turn on **Developer options → USB debugging**, pick your phone in Android Studio, and press **Run ▶** — it installs and launches the game directly.

---

## If install is blocked

- "Install blocked / unknown sources" → Settings → Apps → tap the app you opened the APK from (Files, Chrome, or WhatsApp) → **Install unknown apps → Allow**.
- "App not installed" → uninstall any older Shadow Copy test version first, then install again. Make sure you have at least 100 MB free.
- The APK is a debug build, so Play Protect may warn you. Tap **Install anyway** — this is your own game, built from your own code.

This APK is for testing only. It cannot be uploaded to the Play Store — the Play Store needs a signed AAB instead (see PLAY-STORE-GUIDE.md).
