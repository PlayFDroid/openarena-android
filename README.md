# OpenArena for Android

[![Build, Test & Release OpenArena APK](https://github.com/PlayFDroid/openarena-android/actions/workflows/build-release.yml/badge.svg)](https://github.com/PlayFDroid/openarena-android/actions/workflows/build-release.yml)
[![License: GPL v2](https://img.shields.io/badge/License-GPL_v2-blue.svg)](COPYING)

A modernized Android port of **[OpenArena](http://www.openarena.ws/)**, the classic open-source standalone multiplayer first-person shooter based on the *ioquake3* / *Quake III Arena* engine.

Maintained by **[PlayFDroid](https://github.com/PlayFDroid)** for modern Android devices, packaging, and the F-Droid ecosystem.

---

## Features & Modernizations

- **16 KB Page-Size Aligned**:
  Fully compliant with Android 15, Android 16, and modern 16 KB page-size Linux kernels (`-Wl,-z,max-page-size=16384` and `zipalign -P 16 4`).
- **Touchscreen Controls with Autoshoot**:
  Features ray-traced crosshair target scanning. When an enemy enters the crosshair, the weapon automatically fires, dramatically improving playability on mobile screens without requiring complicated claw grips.
- **First-Person View by Default**:
  Starts directly in the authentic Quake 3 / OpenArena first-person shooter perspective (`cg_thirdPerson 0`).
- **Tap-to-Respawn & Emergency Fire Button**:
  - Tap anywhere on the screen when eliminated to immediately respawn.
  - An unobtrusive manual fire button is placed on the right edge below jump for manual firing, rocket jumping, and pre-firing corners.
- **Hardware Mouse & Gamepad Support**:
  Full mouse pointer capture (`requestPointerCapture`) and physical gamepad support via SDL. Gyroscope aiming is also available and configurable.
- **Modern Android NDK Toolchain**:
  Built with recent Android Clang (NDK r27/r28+) and Gradle 9, replacing obsolete GCC dependencies and old Ant scripts.
- **Integrated Asset Downloader**:
  Automatically downloads official game data packs (`data-0.8.8.zip`) on first launch into app-specific storage.

---

## Building from Source

### Prerequisites

- **JDK 17**
- **Android SDK** with build-tools (35.0.0+)
- **Android NDK** (r27 or r28+)

### Build Commands

```bash
# Clone the repository
git clone https://github.com/PlayFDroid/openarena-android.git
cd openarena-android

# Configure build settings
./changeAppSettings.sh -a

# Build native libraries and release APK
./build.sh release
```

The signed release APK will be generated in the root directory:
```text
OpenArena-0.8.8.44.apk
```

To install directly to a connected device over ADB:
```bash
adb install -r OpenArena-0.8.8.44.apk
```

---

## Project Structure

- `project/jni/application/src/engine/`: OpenArena GLES client and server engine sources (ioquake3-based).
- `project/jni/application/src/vm/`: Quake Virtual Machine bytecode sources (`qagame`, `cgame`, `ui`).
- `project/jni/application/src/AndroidData/`: Android-specific assets, scripts, and `pak7-android.pk3`.
- `project/jni/sdl-1.2/`: SDL 1.2 Android port with on-screen virtual controls and OpenGL ES rendering.
- `project/app/`: Gradle Android application wrapper.

---

## License

- **OpenArena Engine & VM**: Licensed under the [GNU General Public License v2 (GPLv2)](COPYING).
- **libsdl-android framework**: Licensed under the [GNU Lesser General Public License (LGPL)](COPYING).
- **Game assets**: Content assets belong to the OpenArena project and are downloaded from official release mirrors.
