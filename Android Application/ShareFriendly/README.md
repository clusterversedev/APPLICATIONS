# ShareFriendly

**Ultra-Fast Android-to-Android File Sharing**

ShareFriendly is a premium, offline-first Android application for blazing-fast file sharing between Android devices. No internet required, no accounts, no cloud servers — just pure peer-to-peer speed.

![ShareFriendly](app/src/main/res/drawable/ic_launcher_foreground.xml)

## ✨ Features

### 🚀 Transfer
- **Ultra-fast transfers** up to 80+ MB/s via Wi-Fi Direct
- **Completely offline** — no internet connection needed
- **All file types** — photos, videos, music, documents, APKs, archives, and more
- **Multi-file transfers** with queue management
- **Pause/Resume/Cancel** with automatic reconnection
- **Real-time speed tracking** with smoothed EMA calculations
- **Large file support** — stream files without loading into memory
- **Foreground service** — transfers continue in background

### 🔒 Security
- **Optional PIN protection** (4 or 6 digit, PBKDF2-hashed)
- **Accept/Reject incoming transfers** — never auto-accept from unknown devices
- **Trusted devices** management
- **QR code connection** — scan to connect instantly
- **No data collection** — files stay on your devices

### 🎨 UI & Design
- **12 premium themes**: System, Light, Dark, AMOLED, Cyber, Neon, Aurora, Midnight, Ocean, Space, Minimal, Glass
- **8 animated wallpapers**: Neon Particles, Aurora Waves, Digital Grid, Space Particles, Cyber Energy, Data Streams, Abstract Liquid, Network Nodes
- **Material 3** design with dynamic color support
- **Glassmorphism** card effects
- **Smooth 60fps animations** — radar discovery, data flow, confetti completion
- **One-hand usability** with large touch targets

### 🎮 Mini-Games
- **Catch the Data** — collect falling data packets, avoid corrupt ones
- **Data Runner** — endless runner through firewalls, collect data orbs
- Games run without affecting transfer performance
- Live transfer stats overlay while playing

### 📋 Other
- **Transfer history** with speed, duration, and device info
- **Auto-organize** received files into categorized folders
- **Duplicate file handling** — replace, keep both, or skip
- **Storage space checks** before receiving
- **Animated onboarding** for first-time users
- **Comprehensive settings** for every aspect of the app
- **Accessibility** — screen reader support, dynamic font scaling

## 🏗️ Architecture

```
com.sharefriendly.app/
├── ShareFriendlyApp.kt           # Application class
├── MainActivity.kt                # Single activity, Compose entry
├── di/                            # Manual dependency injection
├── data/
│   ├── local/                     # Room database (history, trusted devices)
│   ├── preferences/               # DataStore preferences
│   └── repository/                # Repository pattern
├── domain/model/                  # Domain models
├── transfer/                      # Transfer engine
│   ├── NearbyConnectionsManager   # Google Nearby Connections API
│   ├── TransferEngine             # Orchestrator
│   ├── TransferService            # Foreground service
│   ├── SpeedTracker               # EMA-based speed calculation
│   └── TransferProtocol           # Wire protocol (kotlinx.serialization)
├── ui/
│   ├── theme/                     # 12 themes, typography, shapes
│   ├── components/                # Reusable composables
│   ├── wallpapers/                # 8 animated wallpapers
│   ├── navigation/                # Navigation graph
│   └── screens/                   # All app screens
│       ├── home/
│       ├── onboarding/
│       ├── discovery/
│       ├── filepicker/
│       ├── transfer/
│       ├── history/
│       ├── settings/
│       ├── theme/
│       ├── qr/
│       └── minigame/
└── util/                          # File, format, security utilities
```

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| Language | Kotlin 2.1.0 |
| UI | Jetpack Compose + Material 3 |
| Architecture | MVVM + Clean Architecture |
| State Management | StateFlow / Flow / Coroutines |
| Transfer | Google Nearby Connections API (P2P_POINT_TO_POINT) |
| Database | Room |
| Preferences | DataStore |
| Image Loading | Coil |
| QR Generation | ZXing |
| QR Scanning | CameraX + ML Kit |
| Serialization | kotlinx.serialization |
| Build | Gradle 8.11.1 + AGP 8.7.3 |

## 📱 Requirements

- **Min SDK**: 26 (Android 8.0 Oreo)
- **Target SDK**: 35 (Android 15)
- **Google Play Services**: Required for Nearby Connections API
- **Permissions**: Location, Nearby Devices, Bluetooth, Storage, Camera, Notifications

## 🚀 Getting Started

### Prerequisites
- Android Studio Meerkat or newer
- JDK 17+
- Two physical Android devices (for testing transfers)

### Build & Run

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd ShareFriendly
   ```

2. **Open in Android Studio**
   - Open Android Studio
   - File → Open → Select the `ShareFriendly` directory
   - Wait for Gradle sync to complete

3. **Build Debug APK**
   ```bash
   ./gradlew assembleDebug
   ```
   The APK will be at `app/build/outputs/apk/debug/app-debug.apk`

4. **Build Release APK**
   ```bash
   ./gradlew assembleRelease
   ```

5. **Install on device**
   ```bash
   ./gradlew installDebug
   ```

### Testing File Transfer

1. Install the app on **two** physical Android devices
2. On **Device A**: Tap **RECEIVE** → The device will start advertising
3. On **Device B**: Tap **SEND** → Select files → The device will discover Device A
4. Tap on the discovered device to connect
5. Accept the connection on Device A
6. Transfer begins!

Alternatively, use **QR Code** connection:
1. On the receiver: Open QR Display screen
2. On the sender: Scan the QR code with the QR Scanner

## 📁 Project Structure

```
ShareFriendly/
├── app/
│   ├── build.gradle.kts
│   ├── proguard-rules.pro
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── java/com/sharefriendly/app/   (71 Kotlin files)
│       └── res/
│           ├── drawable/
│           ├── mipmap-anydpi-v26/
│           └── values/
├── build.gradle.kts
├── settings.gradle.kts
├── gradle.properties
├── gradle/
│   ├── libs.versions.toml
│   └── wrapper/
└── README.md
```

## 🎨 Theme Showcase

| Theme | Colors |
|-------|--------|
| Cyber | Electric Blue + Neon Green |
| Neon | Hot Pink + Electric Purple |
| Aurora | Teal + Violet |
| Midnight | Deep Indigo + Royal Blue |
| Ocean | Cyan + Aquamarine |
| Space | Purple + Nebula Pink |
| Minimal | Warm Gray + Sage |
| Glass | Frosted Blue + Translucent |

## 📄 License

This project is for personal/educational use. No third-party branding or watermarks are included.

## 🤝 Credits

Built with ❤️ using:
- [Jetpack Compose](https://developer.android.com/jetpack/compose)
- [Material 3](https://m3.material.io/)
- [Google Nearby Connections API](https://developers.google.com/nearby/connections/overview)
- [ZXing](https://github.com/zxing/zxing)
- [CameraX](https://developer.android.com/training/camerax)
- [ML Kit](https://developers.google.com/ml-kit)
- [Coil](https://coil-kt.github.io/coil/)
