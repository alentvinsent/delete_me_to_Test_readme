# 🚀 Space iOS

[![Platform](https://img.shields.io/badge/platform-iOS-blue.svg)](https://developer.apple.com/ios/)
[![Swift](https://img.shields.io/badge/swift-5.0+-orange.svg)](https://swift.org/)
[![License](https://img.shields.io/badge/license-Space%20Storage-green.svg)](#license)

**Space** is a modern logistics and storage solution designed to simplify the way you store your belongings. By leveraging a seamless integration with UPS, Space allows users to order storage boxes, schedule pickups, and manage their stored items directly from their iPhone.

---

## 🛠 Tech Stack

- **Lanuage**: Swift
- **UI Frameworks**: UIKit, SwiftUI
- **Infrastructure**: AWS (SNS), Google Services
- **Third-party Integrations**: Stripe, Sentry, Segment
- **Tooling**: Fastlane, Bundler, Xcode

---

## 🚀 Getting Started (First-Time Setup)

This guide is designed for developers setting up the project on a **fresh Macbook**.

### 1. Install Xcode
1. Download **Xcode** from the Mac App Store.
2. Once installed, open Xcode and install the **Command Line Tools** if prompted.
3. Alternatively, run in Terminal:
   ```bash
   xcode-select --install
   ```

### 2. Install Homebrew & Dependencies
We use [Homebrew](https://brew.sh/) to manage system tools and **Ruby** to run Fastlane.

1. **Install Homebrew**:
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```
2. **Install Ruby & Bundler**:
   MacOS comes with Ruby, but we recommend using a version manager like `rbenv` to avoid permission issues:
   ```bash
   brew install rbenv
   rbenv init # Follow the instructions to add to your shell profile (.zshrc)
   brew install ruby-build
   rbenv install 3.2.2 # Install a modern Ruby
   rbenv global 3.2.2
   gem install bundler
   ```

### 3. Clone & Initialize Project
1. **Clone the repository**:
   ```bash
   git clone https://github.com/spacereimagined/space-ios.git
   cd space-ios
   ```
2. **Install project dependencies**:
   ```bash
   bundle install
   ```

### 4. Open & Build
1. Open **`Space.xcodeproj`** in Xcode.
2. **Wait for SPM**: Xcode will automatically begin resolving **Swift Package Manager** dependencies (visible in the top status bar). Wait for this to finish.
3. Select the **Space(Dev)** scheme and an **iPhone Simulator**.
4. Press **Cmd + R** to build and run.

---

## 📱 Build & Environments

1. Open **Space.xcodeproj** in Xcode.
2. Select the **Space(Dev)** scheme from the top toolbar for local development.
3. Choose a target **iPhone Simulator** or a physical device.
4. Press **Cmd + R** (or the Play button) to build and run the app.

### Environments

| Scheme | Purpose |
| :--- | :--- |
| **Space(Dev)** | Local development and debugging. |
| **Space(Beta)** | Shared builds for internal/external testing. |
| **Space(Prod)** | Official production release configuration. |

---

## 🚢 Deployment (Fastlane)

We use **[Fastlane](https://fastlane.tools/)** to automate our delivery process. It handles everything from code signing to uploading builds to TestFlight.

### 🚀 Common Deployment Lanes
To deploy a build, use the following commands:
```bash
# Deploy to Development
bundle exec fastlane dev

# Deploy to Beta
bundle exec fastlane beta

# Deploy to Production
bundle exec fastlane prod
```

### 📖 Internal Fastlane Documentation
For more detailed information on our automation setup, please refer to:
- **[Fastlane README](file:///Users/caw/Desktop/SPACE/space-ios/fastlane/README.md)**: Auto-generated list of available lanes.
- **[Developer Guide](file:///Users/caw/Desktop/SPACE/space-ios/fastlane/DEVELOPER_GUIDE.md)**: A deep dive into CI/CD, local runners, and troubleshooting Fastlane-specific errors.

---

## 📂 Project Structure

- `Space/`: Main application source code.
  - `Networking/`: API interaction and networking layer.
  - `Services/`: Business logic and modular services (Auth, Payments, Boxes).
  - `Scenes/`: View controllers and UI components.
  - `Constants.swift`: Global configuration and environment constants.
- `Space.xcodeproj`: Xcode project configuration.
- `fastlane/`: Deployment automation scripts.

---

## 🛠 Troubleshooting

If the app fails to build or run on your device, try these common solutions:

### 🔑 Code Signing & Certificates
- **Error**: "Development cannot be started..." or "Provisioning profile mismatch".
- **Fix**: We use **Fastlane Match**. Ensure you have access to the certificates repo in github and the `MATCH_PASSWORD`. If certs are broken, you can reset them with:
  ```bash
  bundle exec fastlane match nuke
  ```

### 📱 Running on Physical Device
- **Error**: "Untrusted Developer".
- **Fix**: On your iPhone, go to **Settings > General > VPN & Device Management**, find your developer certificate, and tap **Trust**.

### 💎 Dependency & Package Issues
- **Error**: Package resolution fails or hangs.
- **Fix**: 
  1. Open **File > Packages > Resolve Package Versions**.
  2. If it still fails, **Force Quit Xcode** and reopen it. This often triggers a fresh resolution that solves persistent issues.
  3. Prefix commands with `bundle exec` to ensure the project-specific Fastlane version is used.
  
### 🧹 Clean Build & Restart
- **Fix**: If Xcode is behaving unexpectedly (indexing forever, strange build errors):
  1. Clean the build folder (**Shift + Cmd + K**).
  2. Delete **Derived Data** (File > Workspace Settings > Derived Data > Delete or Xcode > Settings > Locations > Derived Data > Delete ).
  3. **Restart Xcode**: Sometimes a simple quit and reopen is the "magic fix" after cleaning.
  4. **Wait**: Always wait for Xcode to finish **Indexing** and **Processing Files** (check the top status bar) before attempting to build.

---

## 🛠 Git pushing rules with .xcodeproj file

### ⚠️ The Project File (`.xcodeproj`)
The `Space.xcodeproj` file is the heart of the project. It tracks every file, folder, and configuration.

**Crucial Best Practice**:
- When you create or add a new file (e.g., a `.swift` file), Xcode automatically updates the `.xcodeproj` file to include a reference to it.
- **You MUST push the `.xcodeproj` changes along with your new files.**
- **If you forget**: Other developers will pull your code but their Xcode won't "see" your new files (they will appear as missing references or not show up at all), causing the app to fail to compile.

---

## ⚖️ License

Copyright © 2024 **Space Storage, Inc.** All rights reserved.
