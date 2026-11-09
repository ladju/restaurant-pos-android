# Rasa Nusantara POS - Android Application Project

This is a complete, native Android project for the **Rasa Nusantara Restaurant POS** (Cashier POS, Waitstaff Mobile Ordering, Kitchen Display System / KDS, Portion-Based Food Stock Tracking, Dynamic QRIS Digital Payments, and Shift Z-Report Sales Recap).

---

## 📱 Project Specifications

- **Package Name (Application ID)**: `com.rasanusantara.pos`
- **Application Name**: `Rasa Nusantara POS`
- **Architecture**: Native Android Project powered by Capacitor & Android Gradle Plugin (AGP)
- **Minimum Android SDK**: API 24 (Android 7.0 Nougat+) — Compatible with over 98% of active Android devices worldwide
- **Target Android SDK**: API 36 (Android 15+)
- **Network Dependency**: **100% Offline-First**. Bundled with local Tailwind CSS, local SVG QRIS generator, and persistent browser storage.

---

## 🚀 How to Build and Run in Android Studio

### Prerequisites
- [Android Studio](https://developer.android.com/studio) (Koala, Ladybug, Iguana, or later)
- JDK 17 or later (bundled with Android Studio)
- An Android device (phone, tablet, or POS terminal) with **USB Debugging** enabled, OR an Android Virtual Device (AVD Emulator).

---

### Step 1: Open the Project
1. Launch **Android Studio**.
2. Click **Open** (or `File > Open...`).
3. Select the `android/` folder inside this directory:
   ```
   android-pos/android/
   ```
4. Android Studio will automatically recognize the Gradle build files and sync the dependencies.

---

### Step 2: Run on an Android Phone / Tablet / POS
1. Connect your Android device via USB (or start an Android Emulator).
2. Ensure your device appears in the top device dropdown in Android Studio.
3. Click the green **Run (▶)** button (or press `Shift + F10`).
4. The app will compile, install, and launch automatically with:
   - Fullscreen kiosk-ready interface
   - Screen kept awake continuously for cashier and kitchen counters (`FLAG_KEEP_SCREEN_ON`)
   - Haptic vibration feedback on item adds and payment settlements

---

### Step 3: Generate the Standalone APK File (`.apk`)
To install the app on any Android device without Android Studio:
1. In Android Studio, go to the top menu: **Build > Build Bundle(s) / APK(s) > Build APK(s)**.
2. When the build finishes, a notification will appear: `"APK(s) generated successfully"`.
3. Click **locate** to reveal `app-debug.apk`:
   ```
   app/build/outputs/apk/debug/app-debug.apk
   ```
4. Copy this `.apk` to any Android tablet or phone via USB, Google Drive, or WhatsApp, and tap to install!

---

### Alternative: Build APK from the Command Line
If you have Android SDK installed on your computer:
```bash
cd android/
./gradlew assembleDebug
```
The output APK will be generated at:
```
app/build/outputs/apk/debug/app-debug.apk
```

---

## 🛠️ Included Android Optimizations

| Feature | Implementation | Description |
|---|---|---|
| **Always-On Screen** | `FLAG_KEEP_SCREEN_ON` in `MainActivity.java` | Prevents cashier and kitchen KDS tablets from sleeping during restaurant hours. |
| **Tactile Haptic Feedback** | `android.permission.VIBRATE` | Vibrates the device when buttons are tapped or payments settle. |
| **Offline Tailwind & Assets** | Bundled in `app/src/main/assets/public/` | Works 100% offline without needing active WiFi. |
| **Thermal Printing** | Android WebKit Print Adapter | Click "Print Receipt" to output 80mm thermal receipts directly to Bluetooth/USB/Network ESC/POS printers. |
| **Android Back Button** | Hardware back-button listener | Back button gracefully closes popups/modals before exiting. |
| **Hardware Acceleration** | Enabled in `AndroidManifest.xml` | Smooth 60fps scrolling across 100+ menu items. |

---

## 📂 Directory Layout

```
android-pos/
├── android/                   # Native Android Studio Project
│   ├── app/
│   │   ├── src/main/
│   │   │   ├── AndroidManifest.xml   # Permissions (Vibrate, WakeLock, Internet)
│   │   │   ├── java/com/rasanusantara/pos/
│   │   │   │   └── MainActivity.java # Keep-screen-on & native bridge
│   │   │   ├── res/                  # App icons & launcher themes
│   │   │   └── assets/public/        # Bundled POS web application & assets
│   │   └── build.gradle
│   ├── build.gradle
│   ├── gradlew
│   └── settings.gradle
├── www/                       # Web source assets
│   ├── index.html
│   └── tailwind.min.js
├── capacitor.config.json      # App ID & Android configuration
└── package.json
```
