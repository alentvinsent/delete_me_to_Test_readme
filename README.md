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

## 🚢 Deployment

We use **Fastlane** to automate our deployment process to TestFlight.

To deploy a build to the development environment:
```bash
bundle exec fastlane dev
```

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

### 💎 Dependency Issues
- **Error**: Fastlane command not found or version mismatch.
- **Fix**: Always prefix commands with `bundle exec`. If issues persist, try:
  ```bash
  bundle install
  bundle update fastlane
  ```

### 🧹 Clean Build
- **Fix**: If Xcode is behaving unexpectedly, try cleaning the build folder (**Shift + Cmd + K**) or deleting the **Derived Data** folder.

---

## ⚖️ License

Copyright © 2024 **Space Storage, Inc.** All rights reserved.
