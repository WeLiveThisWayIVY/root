# courier-app

Debug build of the courier app for Android.

## Download

**[courier-app v0.1 — debug APK](courier-app-v0.1-debug.apk)**

The file sits in this folder, next to this README.

## Install

1. Open the download link above on the Android phone.
2. Download the file.
3. Open it; Android asks to allow install from this source — allow it.
4. Install, then open the app.

## What it does

First build. Nothing wired to the courier service yet.

## Build

Requires JDK 17 and the Android SDK. From this folder:

```
gradlew assembleDebug
```

The APK comes out in `app/build/outputs/apk/debug/`.
