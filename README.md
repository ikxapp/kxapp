<div align="center">



# kxapp

**English** · [简体中文](README_zh.md)

**A cross-platform iOS IDE — iOS development, now on every platform**

Develop, debug on device, and ship iOS apps from Windows, Linux, or macOS.<br/>
Fully compatible with Xcode projects and the xcodebuild command. No Mac and no Xcode required.

<br/>

![Windows](https://img.shields.io/badge/Windows_10_/_11-0078D4?style=for-the-badge&logo=data:image/svg%2bxml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA4OCA4OCI+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgMTIuNCAzNS43IDcuNXYzNC41SDB6TTQwIDYuOSA4Ny4zIDB2NDEuOEg0MHpNMCA0NS43aDM1Ljd2MzQuNkwwIDc1LjN6TTQwIDQ1LjdoNDcuM1Y4OEw0MCA4MS4zeiIvPjwvc3ZnPgo=)
![Linux](https://img.shields.io/badge/Linux_/_WSL-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![macOS](https://img.shields.io/badge/macOS-000000?style=for-the-badge&logo=apple&logoColor=white)
![VS Code](https://img.shields.io/badge/VS_Code-007ACC?style=for-the-badge)

</div>

> [!IMPORTANT]
> 🚀 **kxapp is launching soon!**
> Hit ⭐ **Star** or 👀 **Watch** in the top-right corner and **Follow** the author to get release news and updates first.
> Found a problem or have a feature request? Open an [Issue](../../issues) .

<br/>

![A breakpoint hit in a Swift app running on an iPhone, in VS Code on Windows](images/debug.png)

<p align="center"><sub>VS Code on Windows, stopped at a breakpoint on a USB-connected iPhone</sub></p>

## ✨ Highlights

| | |
|---|---|
| 🖥️ **No Mac needed** | Build natively on your own machine. Not a VM, Hackintosh, or cloud Mac, so you get full native performance |
| 🧩 **No Xcode needed** | Ships with a complete toolchain. Install with one command and start coding |
| 📂 **No project changes** | Open existing Xcode projects as they are. They are handled the same way Xcode handles them |
| 💡 **IntelliSense** | Completion, go-to-definition, hover, and diagnostics as soon as a project opens, no build required |
| 🐞 **F5 on-device debugging** | Plug in your iPhone and press F5. Breakpoints, variables, call stacks, and device logs are all in VS Code, with Dart debugging for Flutter too |
| 📦 **One command to .ipa** | Release builds produce an .ipa ready for the App Store |
| 🔧 **xcodebuild compatible** | Existing build scripts and CI pipelines run unchanged |
| 🤖 **AI friendly** | Commands support `--json` output, and AI assistants like Copilot and Claude Code work as usual |

## 🖥️ Supported Platforms

| OS | Version | Develop | Device Debugging | Build & Release |
|:---:|:---:|:---:|:---:|:---:|
| <img src="images/windows.svg" width="18" /> **Windows** | Windows 10 / 11 | ✅ | ✅ | ✅ |
| <img src="https://cdn.simpleicons.org/linux/000000" width="18" /> **Linux** | Major distros / WSL | ✅ | ✅ | ✅ |
| <img src="https://cdn.simpleicons.org/apple/000000" width="18" /> **macOS** | macOS | ✅ | ✅ | ✅ |

## 🧱 Supported Tech Stacks

| Tech Stack | Coding | IntelliSense | Device Debugging | Build .ipa | App Store Release |
|---|:---:|:---:|:---:|:---:|:---:|
| <img src="https://cdn.simpleicons.org/swift/F05138" width="18" /> **[Swift / SwiftUI / UIKit](doc/en/swift.md)** | ✅ | ✅ | ✅ | ✅ | ✅ |
| <img src="https://cdn.simpleicons.org/apple/438EFF" width="18" /> **[Objective-C](doc/en/objective-c.md)** | ✅ | ✅ | ✅ | ✅ | ✅ |
| <img src="https://cdn.simpleicons.org/cplusplus/00599C" width="18" /> **C / C++** | ✅ | ✅ | ✅ | ✅ | ✅ |
| <img src="https://cdn.simpleicons.org/swift/F05138" width="18" /> **[Swift Package](doc/en/swift.md#package)** | ✅ | ✅ | ✅ | ✅ | ✅ |
| <img src="https://cdn.simpleicons.org/cocoapods/EE3322" width="18" /> **[CocoaPods](doc/en/cocoapods.md)** | ✅ | ✅ | ✅ | ✅ | ✅ |
| <img src="https://cdn.simpleicons.org/flutter/02569B" width="18" /> **[Flutter](doc/en/flutter.md)** | ✅ | ✅ | ✅ | ✅ | ✅ |
| <img src="https://cdn.simpleicons.org/react/61DAFB" width="18" /> **[React Native](doc/en/react-native.md)** | ✅ | ✅ | ✅ | ✅ | ✅ |
| <img src="https://cdn.simpleicons.org/expo/000020" width="18" /> **[Expo](doc/en/expo.md)** | ✅ | ✅ | ✅ | ✅ | ✅ |
| 🟢 **[uni-app (HBuilderX)](doc/en/uni-app.md)** | ✅ | ✅ | ✅ | ✅ | ✅ |
| <img src="https://cdn.simpleicons.org/kotlin/7F52FF" width="18" /> **[Kotlin Multiplatform / Compose](doc/en/kotlin-multiplatform.md)** | ✅ | ✅ | ✅ | ✅ | ✅ |
| <img src="https://cdn.simpleicons.org/unity/000000" width="18" /> **[Unity](doc/en/unity.md)** | ✅ | ✅ | ✅ | ✅ | ✅ |
| <img src="https://cdn.simpleicons.org/godotengine/478CBF" width="18" /> **[Godot](doc/en/godot.md)** | ✅ | ✅ | ✅ | ✅ | ✅ |
| <img src="https://cdn.simpleicons.org/cocos/55C2E1" width="18" /> **[cocos2d-x](doc/en/cocos2d-x.md)** | ✅ | ✅ | ✅ | ✅ | ✅ |
| <img src="https://cdn.simpleicons.org/apachecordova/35434F" width="18" /> **[Cordova](doc/en/cordova.md)** | ✅ | ✅ | ✅ | ✅ | ✅ |

Click a stack name for its step-by-step guide.

## 🛠️ Do Your Xcode Work in VS Code

Project settings, Info.plist, asset catalogs, and app icons all have visual editors. What you save is the original file, which Xcode opens as usual.

| Project Settings |
|:---:|
| ![Project settings editor](images/project-settings-general.png) |

Start new projects from templates such as SwiftUI, UIKit, Objective-C, Flutter, React Native, and Expo.

![Template list in the New Project wizard](images/new-project.png)

## ⌨️ Command-Line Quick Start

Examples use Windows paths. On Linux / macOS, replace backslashes with forward slashes.

### 1️⃣ Check the environment

After installing, run this in a new terminal. You are ready when every check passes.

```shell
kxapp doctor
```

### 2️⃣ Create a project

Specify the template, project name, bundle ID, and parent directory. The project is created at `D:\projects\MyApp`. Skip this step for an existing project.

```shell
kxapp project create -t app_swiftui -n MyApp -b com.example.myapp -o D:\projects
```

`kxapp project templates` lists all templates.

### 3️⃣ Set up signing

Put your .p12 certificate and .mobileprovision profile in the `keychain` folder at the project root.

### 4️⃣ Build and install on your iPhone

Connect the iPhone, tap Trust This Computer, and turn on Developer Mode. Add `--install` to build, sign, and install in one step.

```shell
kxapp build D:\projects\MyApp\MyApp.xcodeproj --install
```

### 5️⃣ Build a release .ipa

Switch to an Apple Distribution certificate and an App Store provisioning profile, then build with the Release configuration.

```shell
kxapp build D:\projects\MyApp\MyApp.xcodeproj -c Release
```

Upload the generated `build\MyApp.ipa` to App Store Connect with Transporter or Appuploader. TestFlight and App Review work as usual.

### 🔁 Scripts and CI

Specify the workspace and scheme, and add `--json` for machine-readable progress and results.

```shell
kxapp build ios/MyApp.xcworkspace -s MyApp -c Release --json
```

```json
{"type":"progress","phase":"CompileSwiftSources","current":12,"total":42}
{"type":"result","command":"build","data":{"success":true,"duration":"1m12s","ipa":["ios/build/MyApp.ipa"]}}
```

## ❓ FAQ

**Is kxapp a virtual machine, a Hackintosh, or a cloud Mac?**

None of these. kxapp is a complete, standalone toolchain that runs directly on your system with full native performance.

**What do I need for on-device debugging?**

An iPhone and a USB cable. On the iPhone, trust the computer and turn on Developer Mode (Settings → Privacy & Security → Developer Mode), then press F5.

**Can the builds be published to the App Store?**

Yes. The .ipa kxapp produces matches what Xcode produces, and TestFlight and App Review work as usual.

## 📣 Follow & Feedback

<div align="center">

⭐ **Star** this repo　·　👀 **Watch** for release notifications　·　➕ **Follow** the author for updates

🐛 Found a problem or have a suggestion? [Open an Issue](../../issues/new)

📧 Email [ikxapp@gmail.com](mailto:ikxapp@gmail.com)　

</div>
