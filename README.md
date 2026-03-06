# How to create Capacitor apps (iOS and Android) from web app codebase

If you want to do it manually, follow the [guide_to_create_capacitor_app_manually.md](guide_to_create_capacitor_app_manually.md).

If you want a one-click solution, use `create_capacitor_apps.sh`.

# What is the use of the script called `create_capacitor_apps.sh`

This script creates Capacitor apps for iOS and Android.
It builds native iOS and Android apps from the Space Web App codebase using the Capacitor framework.

Normally, you would need to run multiple commands to set up the Space Web App, which can be difficult for beginners.
This script automates the entire process of setting up the project and installing the required dependencies for building mobile apps.

---

## Quick Start

### Prerequisites

Before running the script, make sure you have:

- **Node.js** (v16 or higher)
- **npm** (comes with Node.js)
- **Xcode** (for iOS)
- **Android Studio** (for Android)

### Running the Script

1. Open Terminal in the project folder
2. Give the script permission to run (only needed once):
   ```bash
   chmod +x create_capacitor_apps.sh
   ```
3. Start the build process:
   ```bash
   ./create_capacitor_apps.sh
   ```
4. Follow the on-screen prompts

---

## What this script does (step-by-step)

### Step 1: Environment Setup

The script checks for a `.env` file:
- If missing, it copies `.env.example` to `.env` (make sure you have updated your `.env` file)
- If `APP_URL` or `STATIC_URL` in `.env` have absolute URLs (like `http://localhost`), it warns you because these cause white screens on real devices

> **Note:** Localhost URLs will work in simulators because the web app runs on the same machine. However, for real devices, you need to change the URL to the actual server (like `https://app.spacereimagined.io/`) so the app can access the official Space website. 

### Step 2: Dependency Installation

Runs `npm install` to download all required packages into the `node_modules` folder.

### Step 3: Production Build

Runs `npm run production` to create an optimized build in the `dist/` folder.

### Step 4: Capacitor Initialization

If Capacitor isn't initialized yet, it sets up the project with:
- App name: "Space App"
- App ID: `io.spacereimagined.app`
- Web directory: `dist`

### Step 5: Platform Setup

Checks and adds iOS and Android platforms:
- Creates `ios/` folder with Xcode project
- Creates `android/` folder with Android Studio project

### Step 6: Sync

Copies your web build to both native projects and updates plugins.

### Step 7: Launch

Prompts you to choose:
- `1` - Launch on iOS
- `2` - Launch on Android
- `3` - Launch on both
- `4` - Skip (manual launch later)

---

## Common Errors & Solutions

### Error: White Screen on Real Device

**Cause:** Absolute URLs in `.env` file (like `http://localhost:8080`)

**Solution:**
1. Open `.env` file
2. Clear or remove absolute URLs from `APP_URL` and `STATIC_URL`
3. Re-run the script

```env
# Bad (causes white screen)
APP_URL=http://localhost:8080
STATIC_URL=http://localhost:8080

# Good
APP_URL=
STATIC_URL=
```

---

### Error: "iOS directory exists but missing Podfile"

**Cause:** The `ios/` folder is corrupted or incomplete

**Solution:**
- When prompted, press `y` to remove and re-add the iOS platform

---

### Error: "Android directory exists but missing build.gradle"

**Cause:** The `android/` folder is corrupted or incomplete

**Solution:**
- When prompted, press `y` to remove and re-add the Android platform

---

### Error: "No devices found" when launching

**Cause:** No simulator or physical device connected

**Solution:**
- **iOS:** Open Xcode → Window → Devices and Simulators → Create a simulator
- **Android:** Open Android Studio → Tools → Device Manager → Create device

---

### Error: "Signing & Capabilities" issues (iOS)

**Cause:** Xcode needs your Apple ID for app signing

**Solution:**
1. Open `ios/App/App.xcworkspace` in Xcode
2. Select the project in the left sidebar
3. Go to "Signing & Capabilities" tab
4. Choose your Team (requires Apple ID)

---

### Error: "SDK location not found" (Android)

**Cause:** Android SDK path not configured

**Solution:**
1. Open Android Studio
2. Go to Preferences → Appearance & Behavior → System Settings → Android SDK
3. Note the "Android SDK Location" path
4. Create/update `local.properties` in the `android/` folder:
   ```properties
   sdk.dir=/Users/YOUR_USERNAME/Library/Android/sdk
   ```

---

### Error: "npm install" fails

**Cause:** Network issues or outdated npm

**Solution:**
```bash
# Update npm
npm install -g npm@latest

# Clear npm cache
npm cache clean --force

# Try again
npm install
```

---

### Error: "Capacitor not found"

**Cause:** Capacitor not installed globally

**Solution:**
```bash
npm install -g @capacitor/core @capacitor/cli
```

---

## Frequently Asked Questions (FAQs)

### Q: Do I need a Mac for iOS development?

**A:** Yes, Xcode and iOS simulators only run on macOS. Android development works on Windows, Mac, and Linux.

---

### Q: Can I run this on a physical device?

**A:** Yes! Connect your device via USB before running the script:
- **iOS:** Trust the computer on your device when prompted
- **Android:** Enable USB Debugging in Developer Options

---

### Q: How do I update the app after making code changes?

**A:**
1. Make your code changes
2. Re-run the script (it will rebuild and resync)
3. Or manually run:
   ```bash
   npm run production
   npx cap sync
   ```

---

### Q: Where are my native project files?

**A:**
- **iOS:** `ios/App/App.xcworkspace` (open this in Xcode)
- **Android:** `android/` folder (open in Android Studio)

---

### Q: How do I change the app icon?

**A:**
1. Replace icons in `static/assets/images/`
2. Re-run the script to sync changes
3. For iOS: Use Xcode's Asset Catalog
4. For Android: Update `android/app/src/main/res/` folders

---

### Q: How do I change the app name or bundle ID?

**A:** Edit `capacitor.config.json`:
```json
{
  "appId": "com.yourcompany.yourapp",
  "appName": "Your App Name",
  "webDir": "dist"
}
```
Then run `npx cap update`

---

### Q: The script keeps asking me to install dependencies. Is this normal?

**A:** Yes, the script runs `npm install` every time to ensure all dependencies are up to date. This is safe to run multiple times.

---

### Q: Can I skip certain steps?

**A:** The script is designed to run fully automated. If you need more control, you can run commands manually:

```bash
# Individual commands
npm install                    # Install dependencies
npm run production             # Build for production
npx cap add ios               # Add iOS platform
npx cap add android           # Add Android platform
npx cap sync                  # Sync assets
npx cap run ios               # Run on iOS
npx cap run android           # Run on Android
```

---

## Manual Launch Options

If you chose "Skip" in the script, here's how to launch manually:

### iOS

```bash
# Option 1: CLI
npx cap run ios

# Option 2: Xcode
open ios/App/App.xcworkspace
# Then press Cmd+R to run
```

### Android

```bash
# Option 1: CLI
npx cap run android

# Option 2: Android Studio
# Open the 'android/' folder in Android Studio
# Then press the Run button (green play icon)
```

---

## Troubleshooting Checklist

If something goes wrong, check these:

- [ ] Node.js installed (`node -v` should show v16+)
- [ ] npm installed (`npm -v`)
- [ ] Xcode installed (macOS only)
- [ ] Android Studio installed
- [ ] At least one simulator or device available
- [ ] `.env` file exists and has proper URLs for real devices
- [ ] Internet connection for downloading dependencies

