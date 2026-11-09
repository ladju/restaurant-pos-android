# 📱 Rasa Nusantara POS - Complete Android System Architecture & Guide

The **Rasa Nusantara Restaurant POS** Android project has been architected and tailored based on the full `/grill-me` alignment interview.

---

## 🎯 Architecture Decisions Summary

| Domain | Decision | Implementation Details |
|---|---|---|
| **Target Hardware** | **Tablet & POS Terminal Optimized** | Adaptive landscape layout for Cashier POS and Kitchen KDS; responsive portrait mode for Waitstaff handhelds. |
| **Multi-Device Sync** | **Local LAN / WiFi Synchronization** | Cashier tablet acts as the local LAN hub; Kitchen KDS and Waitstaff phones connect over restaurant WiFi with zero internet required. |
| **Thermal Printing** | **Direct Bluetooth & LAN ESC/POS** | Instant 1-tap print to 58mm/80mm thermal receipt printers with automatic cash drawer kick (`ESC p`) and paper cutter (`GS V`). |
| **QRIS Payment Engine** | **Hybrid QRIS System** | Offline dynamic national QRIS code generation with instant cashier test simulation + pluggable settings for production Midtrans/Xendit/DOKU gateways. |
| **Food Stock Depletion** | **Soft Portion Depletion with Override** | Tracks portions in real time; alerts staff when stock hits 0, but permits cashier/waitstaff override upon kitchen ingredient confirmation. |
| **Security & Access** | **Supervisor PIN Protection (`8888`)** | Everyday cashier operations are fast and PIN-free; Supervisor PIN is required for voids, custom discounts, and Shift Z-Report drawer audits. |
| **Data & Reports** | **Local SQLite + 1-Click CSV/WhatsApp** | Full transaction and shift history stored locally with direct CSV export and Android native sharing (WhatsApp, Email, Drive). |

---

## 📦 Project Artifacts & Files

- **Android Studio Project Directory**: [`/home/antigravity/android-pos/android/`](file:///home/antigravity/android-pos/android)
- **Downloadable Project ZIP**: [`android-pos-project.zip`](file:///home/antigravity/.gemini/jetski/brain/v1/default/jetski_remote_agents_3p/230538bc-a4da-4d00-a1f4-fed4aacde68b/android-pos-project.zip) *(897 KB, ready to build in Android Studio)*
- **Interactive Browser Preview**: [`restaurant_pos.html`](file:///home/antigravity/.gemini/jetski/brain/v1/default/jetski_remote_agents_3p/230538bc-a4da-4d00-a1f4-fed4aacde68b/restaurant_pos.html) *(Preview all 5 stations and the new Settings modal directly in the chat side panel)*
- **Application ID**: `com.rasanusantara.pos`
- **Application Name**: `Rasa Nusantara POS`
- **Minimum Android SDK**: API 24 (Android 7.0 Nougat+)
- **Target Android SDK**: API 36 (Android 15+)

---

## ⚙️ Built-In Hardware & System Settings (New)

A dedicated **⚙️ Settings** modal is now accessible in the top navigation header:

1. **ESC/POS Thermal Receipt Printer**:
   - Paper width selector: `80mm (Standard Desktop POS)` vs `58mm (Handheld Mobile POS)`.
   - Connection protocol: `Bluetooth ESC/POS`, `LAN / WiFi Raw IP (e.g. 192.168.1.200:9100)`, or `Android System Print Dialog`.
   - Toggles: Automatic paper cutter (`GS V 65 0`) and automatic cash drawer kick pulse (`ESC p 0 25 250`).
2. **Dynamic QRIS & Payment Gateway**:
   - Selector: `Dynamic National QRIS (Offline)` vs `Midtrans Gateway` vs `Xendit QRIS`.
   - Pluggable merchant credentials: Merchant Name, National NMID, and Server/API Keys.
3. **Manager Security & Supervisor PIN**:
   - Configurable Supervisor PIN (Default: `8888`) required for voids, stock audits, and shift closing.

---

## 🚀 How to Build and Run in Android Studio

1. **Download & Extract**: Download [android-pos-project.zip](file:///home/antigravity/.gemini/jetski/brain/v1/default/jetski_remote_agents_3p/230538bc-a4da-4d00-a1f4-fed4aacde68b/android-pos-project.zip) to your computer and extract it.
2. **Open in Android Studio**: Select `File > Open...` and pick the `android-pos/android/` folder.
3. **Run on Device**: Connect your Android phone, tablet, or POS terminal with USB debugging enabled, and click **Run (▶)** (or `Shift + F10`).
4. **Generate APK**: Go to **Build > Build Bundle(s) / APK(s) > Build APK(s)**. The output file will be at:
   ```
   app/build/outputs/apk/debug/app-debug.apk
   ```
