# SURVIVE for Android

[Português](README.md) · [English](README.en.md)

A native, self-contained Android application. It contains no WebView, does not open a website to run features, and does not depend on PHP, MySQL, a remote API or an Internet connection.

Public project version: **1.0** (`versionName "1.0"`) for both `debug` and `release`. The internal Google Play update code is **2** (`versionCode 2`), allowing this build to replace the previous one without changing the version shown to users.

The Room database now uses internal version **6** to migrate previous installations without data loss, index bag-to-household assignments, distinguish food from medicines and store the weight of each unit. This number is independent from the Google Play `versionCode` and the public application version, which remains **1.0**.

## Architecture

- Kotlin and Jetpack Compose with Material 3.
- Room as the local database and single source of truth.
- One local profile with editable name, email and password.
- Passwords derived through the native PBKDF2/HMAC-SHA-256 implementation, with a random salt, stored algorithm/iteration count and constant-time comparison. Older hashes are upgraded after successful authentication.
- JSON data export and restore through the Android system file picker.
- No `INTERNET`, advertising, analytics, location, camera, microphone or contacts permission. The only functional permissions are notifications and restoring the daily expiry check after restarting the device.
- `minSdk 26`, `targetSdk 36`, `compileSdk 37` and JDK 17.

## Features

- Readiness overview with normal duration and three rationing phases, calories, macronutrients, water and bag readiness.
- Pantry with fixed search and filters, predefined categories, nutrition calculated automatically from macronutrients, water-reserve tracking, calendar-based dates, stock usage and history. “Cans” is no longer selectable; choosing “units” requires the weight of each unit in grams and nutritional totals use `quantity × weight per unit`. Equivalent records are grouped while each batch remains independent, and grouped consumption follows the earliest expiry first.
- A separate Medicines area with dedicated search, categories and units, stock and expiry tracking. It is excluded from nutritional calculations, creates no dosage reminders and explicitly states that it does not replace medical or pharmaceutical advice.
- A household created with the Profile, supporting man, woman, boy, girl, dog and cat, with separate calculations for adults and children/teenagers aged 3 to 18. Label/value lines adapt to narrow screens and large fonts, moving values to a second line when needed.
- Multiple emergency bags, appended in order, with reorderable categories, a visible gesture instruction, edit by swiping left and delete by swiping right for both categories and items, priorities, checklist, weight and UUID-based household assignment.
- Essential forms, filters and dialogs survive rotation; Back returns to the Overview from other tabs.
- Non-destructive local migrations for data created by earlier 1.0 variants.
- Local expiry, water, food, medicine and critical-item alerts. Products and medicines can generate three unique notifications: when the warning period starts, halfway through it and five days before expiry. Medicine notifications are generic and do not expose the medicine name on the lock screen.
- Local profile and login, editable name/email/password, and System, Light or Dark theme selection. Registration fields start neutral, become green only when valid and red only after invalid content is entered; password requirements remain visible.
- Full Portuguese (Portugal) and English interface. The first launch follows the Android language, with PT-PT as fallback for unsupported languages, and the chosen language is persisted.
- A complete privacy policy available offline inside the Profile and ready for GitHub Pages in the `docs/` directory.
- Local profile data backup and restore.

## Build

Open the project in an up-to-date Android Studio or run:

```bash
./gradlew test lint connectedDebugAndroidTest assembleDebug
```

For a signed public build:

```bash
./gradlew clean test lint bundleRelease \
  -PSURVIVE_STORE_FILE=/private/path/upload.jks \
  -PSURVIVE_STORE_PASSWORD='...' \
  -PSURVIVE_KEY_ALIAS='upload' \
  -PSURVIVE_KEY_PASSWORD='...'
```

The AAB is generated in `app/build/outputs/bundle/release/`. Do not commit keystores, passwords or `local.properties`.

You can also use **Build → Generate Signed App Bundle or APK** in Android Studio. Select your upload key file and enter its exact alias and passwords. The key and credentials are not included in this project.

## Privacy policy and support pages

The complete policy is available in Portuguese at `docs/index.md` and in English at `docs/en/index.md`. It is also available offline inside the app under **Profile → View privacy policy**.

The public documentation directory also includes:

- `docs/support/index.md` — support and safe bug-reporting instructions;
- `docs/delete-data/index.md` — local profile and data deletion instructions.

To publish with GitHub Pages, configure **Settings → Pages → Deploy from a branch**, choose the `main` branch and the `/docs` folder. For the `survive` repository, the expected address is `https://nunchuckcoder.github.io/survive/`.

## Required checks before Google Play

- Run `test`, `lint`, instrumented tests and `bundleRelease` without errors.
- Verify the signed AAB reports `versionCode 2` and `versionName 1.0`.
- Upgrade a real previous installation and confirm Room migrations `1 → 2 → 3 → 4 → 5 → 6` preserve profile, pantry, household, bag and medicine data.
- Select “units”, enter 5 units weighing 400 g each and confirm the nutritional totals correspond to 2000 g. Confirm that “cans” is no longer offered and that the unit weight survives editing, export and restore.
- Test PT-PT and English, rotation, process recreation, screen readers, large fonts, small phones and tablets.
- Test creation, editing, consumption and deletion in airplane mode from first launch.
- Verify expiry notifications, logout privacy, JSON export/restore and permanent data deletion.
- Review nutritional and readiness calculations with a suitably qualified person; they are not medical or emergency advice.

The source project is ready for compilation, but an AAB should only be published after these checks are completed using an Android SDK, emulator and physical devices.

Room schemas `1.json` through `6.json` are versioned under `app/schemas/pt.osvaldocipriano.survive.data.local.SurviveDatabase/`. Reconstructed historical schemas support pre-validation but do not replace a real update test over a previously distributed APK.

## Contact

Developed by **Osvaldo Cipriano — NunchuckCoder**.

For support or privacy questions: [osvaldo@osvaldocipriano.dev](mailto:osvaldo@osvaldocipriano.dev)

---

SURVIVE is an independent app and does not represent any government body, emergency service or medical organisation.
