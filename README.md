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

## 🚀 Getting Started

### Prerequisites

- **macOS** with the latest version of **Xcode** installed.
- **Ruby** (v2.7+) for managing development dependencies via Bundler.
- **Optional**: [Homebrew](https://brew.sh/) for managing system packages.

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/spacereimagined/space-ios.git
   cd space-ios
   ```

2. **Install Ruby dependencies**:
   ```bash
   bundle install
   ```

3. **Open the project**:
   - Locate and open **`Space.xcodeproj`** in Xcode.

---

## 📱 Running the App

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

## ⚖️ License

Copyright © 2024 **Space Storage, Inc.** All rights reserved.
