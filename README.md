# Owner Info

A simple Android app (HTML/JS running inside a WebView) that ties ownership
info to a rental vehicle.

## What it does

**First launch — onboarding (5 fields, entered by the manager):**
1. Agency
2. First Name
3. Last Name
4. 8-digit PIN ID (digits only, exactly 8)
5. Vehicle Serial ID (bottom field)

Agency, First Name, Last Name, and the Serial ID are stored/displayed in ALL
CAPS automatically. Saved data is stored on-device (WebView local storage)
so it survives app restarts.

**After onboarding — display screen:**
- Agency
- Number (the PIN ID)
- Name (Last, First)
- **Must sync in N days** — starts at 14 on the day onboarding is completed,
  counts down in real time by calendar day (14 → 1), then restarts at 14.
  This is driven by the actual date, not a running timer, so it's correct
  even if the app has been closed for a while.
- Serial # (footer)

A small "Edit owner info" link lets a manager correct any of the 5 fields
later without resetting the sync countdown (the original onboarding date is
preserved unless you clear app data).

## App icon

A vector icon: white background, blue circle, lowercase white "i" —
`app/src/main/res/drawable/ic_launcher_foreground.xml`.

## Project structure

```
OwnerInfo/
├── app/
│   ├── build.gradle.kts
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── java/com/mdmac/ownerinfo/MainActivity.kt   (WebView host)
│       ├── assets/index.html                          (the whole app UI/logic)
│       └── res/...                                    (icon, theme, strings)
├── build.gradle.kts
├── settings.gradle.kts
├── gradle.properties
├── gradlew / gradlew.bat / gradle/wrapper/...
└── .github/workflows/build.yml                        (builds the APK on GitHub)
```

This project was test-built locally (`gradlew assembleDebug`) before
delivery and compiles clean.

---

## Uploading this to your GitHub repo from your phone (no Termux, no git CLI)

Your repo: https://github.com/mdmac1983/Owner_Info.git

1. **Extract the zip** on your phone first (Files app → tap the zip →
   Extract, or any zip app). You should end up with a folder called
   `OwnerInfo` containing everything above.

2. Open **github.com/mdmac1983/Owner_Info** in your phone's browser. In
   Chrome, tap the **⋮ menu → Desktop site**. This makes GitHub's uploader
   let you pick a whole folder at once instead of one file at a time.

3. Tap **Add file → Upload files**.

4. Tap **choose your files**, and in the picker look for an option to
   **select a folder** (not just individual files) — choose the `app`
   folder first. This uploads the whole `app/` folder (and everything
   inside it) in one go, keeping the folder structure intact.

5. Scroll down and tap **Commit changes**.

6. Repeat steps 3–5 for the `gradle` folder and the `.github` folder.

7. Do one more **Add file → Upload files** pass for the remaining loose
   files in the root of the extracted folder: `build.gradle.kts`,
   `settings.gradle.kts`, `gradle.properties`, `gradlew`, `gradlew.bat`,
   `.gitignore`, `README.md`. Select them all together, then **Commit
   changes**.

   > If your phone's picker won't let you select a whole folder, upload
   > file-by-file instead — when GitHub's upload box asks for a file name,
   > type the full relative path (e.g. `app/src/main/AndroidManifest.xml`)
   > and it will recreate that folder automatically.

## Getting the built APK

Once everything is pushed, GitHub Actions builds the APK automatically:

1. On GitHub (site or app), open the **Actions** tab of the repo.
2. You'll see a **Build APK** run start on its own after your last commit.
   If it doesn't, tap **Build APK → Run workflow**.
3. Wait for the green checkmark (a couple of minutes).
4. Open that run, scroll to **Artifacts**, and download
   **owner-info-debug-apk**. Unzip it on your phone to get `app-debug.apk`.
5. Tap the APK to install it (you may need to allow "install unknown apps"
   for your browser/files app the first time).
