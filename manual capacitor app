# Guide to Create Capacitor App Manually

A step-by-step beginner-friendly guide to manually create iOS and Android apps from your web app codebase using Capacitor.

---

## What is Capacitor?

Capacitor is a tool that converts your web app into a native mobile app. It creates a wrapper around your web code so it can run on iOS and Android devices.

---

## Prerequisites

Before starting, make sure you have these installed:

| Tool | Required For | How to Check |
|------|--------------|--------------|
| **Node.js** (v16+) | All platforms | Run `node -v` |
| **npm** | All platforms | Run `npm -v` |
| **Xcode** | iOS only (macOS) | Download from Mac App Store |
| **Android Studio** | Android only | Download from developer.android.com |
| **CocoaPods** | iOS only | Run `sudo gem install cocoapods` |

---

## Step-by-Step Guide

### Step 1: Set Up Your Environment File

Your `.env` file controls how your app connects to servers.

1. Check if `.env` file exists in your project root
2. If not, copy the example file:
   ```bash
   cp .env.example .env
   ```
3. Open `.env` and update the values

**Important:** For real devices, use actual URLs (like `https://app.spacereimagined.io/`). For simulators, empty values or localhost may work.

---

### Step 2: Install Dependencies

Install all the packages your project needs:

```bash
npm install
```

This creates a `node_modules/` folder with all dependencies.

**Tip:** If this fails, try:
```bash
npm cache clean --force
npm install
```

---

### Step 3: Build Your Web App

Create a production build of your web app:

```bash
npm run production
```

This creates a `dist/` folder with optimized files. Capacitor will use these files for the mobile app.

---

### Step 4: Install Capacitor

Add Capacitor to your project:

```bash
npm install @capacitor/core @capacitor/cli
```

---

### Step 5: Initialize Capacitor

Set up Capacitor in your project:

```bash
npx cap init "Space App" "io.spacereimagined.app" --web-dir dist
```

This creates a `capacitor.config.json` file with your app settings.

**What each parameter means:**
- `"Space App"` - The name displayed on the device
- `"io.spacereimagined.app"` - Unique app identifier (reverse domain format)
- `--web-dir dist` - Tells Capacitor where your built web files are

---

### Step 6: Add iOS Platform (macOS only)

Add iOS support to your project:

```bash
npx cap add ios
```

This creates an `ios/` folder with an Xcode project.

---

### Step 7: Add Android Platform

Add Android support to your project:

```bash
npx cap add android
```

This creates an `android/` folder with an Android Studio project.

---

### Step 8: Sync Your App

Copy your web build to the native projects:

```bash
npx cap sync
```

This command:
- Copies files from `dist/` to iOS and Android projects
- Updates native plugins
- Ensures everything is in sync

**Run this command every time you:**
- Make changes to your web code
- Add or update plugins
- Change configuration

---

### Step 9: Open and Run in IDE

#### For iOS (macOS):

**Option A: Using Terminal**
```bash
npx cap run ios
```

**Option B: Using Xcode**
```bash
open ios/App/App.xcworkspace
```
Then press `Cmd + R` in Xcode to run.

#### For Android:

**Option A: Using Terminal**
```bash
npx cap run android
```

**Option B: Using Android Studio**
1. Open Android Studio
2. Select "Open an existing project"
3. Choose the `android/` folder
4. Press the green Run button

---

## Common Commands Reference

| Command | What It Does |
|---------|--------------|
| `npm install` | Install dependencies |
| `npm run production` | Build web app |
| `npx cap init` | Initialize Capacitor |
| `npx cap add ios` | Add iOS platform |
| `npx cap add android` | Add Android platform |
| `npx cap sync` | Copy web build to native projects |
| `npx cap run ios` | Run on iOS simulator/device |
| `npx cap run android` | Run on Android emulator/device |
| `npx cap open ios` | Open in Xcode |
| `npx cap open android` | Open in Android Studio |
| `npx cap update` | Update native projects after config changes |

---

## Workflow Summary

```
1. npm install           → Install dependencies
2. npm run production    → Build web app
3. npx cap sync          → Copy build to native projects
4. npx cap run ios/android → Run on device
```

**After making code changes, repeat steps 2-4.**

---

## Troubleshooting

### Problem: White screen on real device

**Cause:** Your `.env` has localhost URLs that the device cannot access.

**Solution:** 
- Update `APP_URL` and `STATIC_URL` in `.env` to your production server URL
- Rebuild and resync

---

### Problem: "No devices found"

**Cause:** No simulator running or device connected.

**Solution:**
- **iOS:** Open Xcode → Window → Devices and Simulators → Start a simulator
- **Android:** Open Android Studio → Tools → Device Manager → Start an emulator

---

### Problem: iOS build fails with signing error

**Cause:** Apple requires a developer certificate to run apps.

**Solution:**
1. Open `ios/App/App.xcworkspace` in Xcode
2. Select your project in the left sidebar
3. Go to "Signing & Capabilities" tab
4. Sign in with your Apple ID
5. Select your Team

---

### Problem: Android SDK not found

**Cause:** Android Studio installed but SDK path not set.

**Solution:**
1. Open Android Studio
2. Go to Preferences → Appearance & Behavior → System Settings → Android SDK
3. Copy the "Android SDK Location" path
4. Create file `android/local.properties` with:
   ```properties
   sdk.dir=/Users/YOUR_USERNAME/Library/Android/sdk
   ```

---

### Problem: CocoaPods error (iOS)

**Cause:** CocoaPods not installed or outdated.

**Solution:**
```bash
# Install CocoaPods
sudo gem install cocoapods

# Update pods in iOS folder
cd ios/App
pod install
cd ../..
```

---

### Problem: Changes not showing in app

**Cause:** Forgot to rebuild and resync.

**Solution:**
```bash
npm run production
npx cap sync
```

---

## Tips for Beginners

1. **Always sync after changes** - Run `npx cap sync` after any web code changes

2. **Use Xcode/Android Studio for debugging** - They have better error messages than the terminal

3. **Keep Capacitor updated** - Run `npm update @capacitor/core @capacitor/cli` periodically

4. **Test on real devices early** - Simulators don't catch all issues

5. **Check the docs** - [Capacitor Documentation](https://capacitorjs.com/docs) has detailed guides

---

## Quick Reference Card

```bash
# First time setup
npm install
npm run production
npx cap init "Space App" "io.spacereimagined.app" --web-dir dist
npx cap add ios
npx cap add android
npx cap sync

# After code changes
npm run production
npx cap sync
npx cap run ios        # or android

# Open in IDE
npx cap open ios       # opens Xcode
npx cap open android   # opens Android Studio
```

---

*This guide covers the manual process. For automated setup, use `create_capacitor_apps.sh`.*
