# Crazy Bottles - Android + GitHub Pages package (version 1, no ads)

## What is inside
- `www/index.html`   the game for the Android app (Capacitor)
- `docs/index.html`  the same game as a web page (GitHub Pages serves the /docs folder)
- `docs/privacy.html` privacy policy (EN + AR). Replace REPLACE_WITH_YOUR_EMAIL.
- `capacitor.config.json` replace `com.REPLACE_ME.crazybottles` with your own id (example com.yourname.crazybottles). It can NOT be changed after publishing.
- `assets/` icon, adaptive icon layers and splash screens (the tool generates all Android sizes)
- `store/` Play icon 512, feature graphic 1024x500, listing texts and Data safety answers

## Part A - GitHub Pages (web page + privacy URL)
1. Sign in to github.com. New repository: name `crazy-bottles`, Public, no README.
2. "uploading an existing file": drag everything from this folder, then Commit changes.
3. Settings > Pages > Source: Deploy from a branch > Branch `main`, folder `/docs` > Save.
4. After 1-2 minutes the game is at https://USERNAME.github.io/crazy-bottles/
   and the privacy policy at https://USERNAME.github.io/crazy-bottles/privacy.html  <- paste this in Play Console.
5. Open docs/privacy.html on GitHub (pencil icon) and put your email.

## Part B - build the AAB
Install Node.js (LTS) and Android Studio (latest, with Android SDK 36).
```
npm install @capacitor/core @capacitor/android
npm install -D @capacitor/cli @capacitor/assets
npx cap add android
npx capacitor-assets generate --android
npx cap sync android
npx cap open android
```
In Android Studio:
1. android/app/build.gradle: versionCode 1, versionName "1.0.0". Check targetSdk = 36 (variables.gradle).
2. AndroidManifest.xml > <activity ...> add android:screenOrientation="portrait"
3. Build > Generate Signed App Bundle / APK > Android App Bundle > create a new keystore. BACK UP the .jks file and passwords (losing them blocks updates).
4. Choose release > the file is android/app/release/app-release.aab

## Part C - Play Console
Create the app (free, game), upload the AAB to Closed testing, fill: App content (privacy policy URL, ads = No, Data safety, content rating, target audience), store listing from store/listing.md.
Personal accounts created after 13 Nov 2023: closed test with 12 testers opted in for 14 continuous days before production.

## Part D - later (version 2)
Ads can be added later: set `ADS.enabled=true` in the game and add @capacitor-community/admob. Update the privacy policy and Data safety first.
