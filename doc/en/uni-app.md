# Build uni-app iOS apps locally on Windows

**English** · [简体中文](../zh/uni-app.md)

Package the iOS app of an HBuilderX uni-app project locally on Windows and debug it on your iPhone. There's no cloud packaging, no queue and no Mac. You export the uni-app project as an Xcode project first, then build, install and debug it like any other iOS project.

## Steps

### 1. Develop the uni-app project

Create and develop your uni-app project in HBuilderX as usual. Then download the SDK matching your HBuilderX version from DCloud's [iOS offline SDK download page](https://nativesupport.dcloud.net.cn/AppDocs/download/ios.html) and unzip it. You'll need it for the export in the next step. **For Vue 2 projects, HBuilderX can't be installed in a folder whose path contains parentheses** (such as Program Files (x86)), or page compilation fails.

### 2. Export an Xcode project

Combine the uni-app project and the DCloud iOS offline SDK and [export them as an Xcode project](https://www.kxapp.com/guides/projects.html#uniapp). The modules checked in manifest.json are installed with [CocoaPods](cocoapods.md). When it's done, open the output folder in VS Code.

*Use either of these*

- **VS Code extension**

  Run **KXApp: Import uni-app Project** from the Command Palette. Select the uni-app project folder, the SDK root folder and the output folder, then enter the bundle ID and DCloud App Key.

- **Command line**

  For the options, see the [uniapp2xcode command reference](https://www.kxapp.com/guides/cli-uniapp2xcode.html).

  ```shell
  uniapp2xcode --project D:\work\myuniapp --sdk D:\sdk\HBuilder-iOS-SDK --output D:\work\myuniapp-ios --bundle-id com.example.myapp --dcloud-appkey YOUR_APPKEY --clean
  ```

### 3. Run doctor

Doctor checks your build environment and fixes anything missing.

*Use either of these*

- **VS Code extension**

  In the title bar of the [KXApp view](https://www.kxapp.com/guides/ide-sidebar.html), open the ··· menu and run [Doctor (fix environment)](https://www.kxapp.com/guides/ide-setup.html#update).

- **Command line**

  ```shell
  kxapp doctor .\myuniapp-ios\HBuilder-Hello\HBuilder-Hello.xcworkspace
  ```

### 4. Write code

Keep writing pages in HBuilderX. **Export again after each change** to bring it into the iOS project. Set the app name, version, icons and permission descriptions in manifest.json in HBuilderX. Put any extra Info.plist keys in nativeResources/ios/Info.plist in the uni-app project. Both are applied on every export.

### 5. Debug

[Connect your iPhone over USB](https://www.kxapp.com/guides/device-setup.html), select it in the KXApp view and press [F5](https://www.kxapp.com/guides/ide-debug.html). Debug the native layer with breakpoints in VS Code and page JS with the debugging tools built into HBuilderX. The two work independently.

### 6. Release

[Build with the Release configuration](https://www.kxapp.com/guides/build.html#debug-release) to get an .ipa named after your app under HBuilder-Hello\build in the output folder. To upload it to App Store Connect, see [Release and App Store submission](https://www.kxapp.com/guides/publish.html).

*Use either of these*

- **VS Code extension**

  Switch the configuration to Release in the Build configuration node of the KXApp view, then run **KXApp: Build** from the Command Palette.

- **Command line**

  ```shell
  kxapp build .\myuniapp-ios\HBuilder-Hello\HBuilder-Hello.xcworkspace -s HBuilder -c Release
  ```

## FAQ

| Symptom | Fix |
|---|---|
| Export says you're not signed in or the AppID doesn't exist, or the app shows an AppKey error as soon as it opens | The AppID, AppKey and bundle ID are one bound set. Sign in to your DCloud account in HBuilderX and get the AppID under "基础配置" (basic settings) in manifest.json. Then at dev.dcloud.net.cn, apply for the offline packaging AppKey on this app's iOS platform with your bundle ID. The bundle ID you export with must match the one used for the AppKey and the App ID in your Apple Developer account. |
| Page compilation fails with "HBuilderX 安装目录不能包括 ( 等特殊字符" (install folder can't contain "(") | A limit for Vue 2 projects. Move the whole HBuilderX folder to a path like D:\HBuilderX, or switch the project to Vue 3 in manifest.json. |
| Version mismatch or blank white screen after launch | The offline SDK and HBuilderX versions differ. Download the SDK matching your HBuilderX and export again. |
| Export reports skipped modules at the end | The current SDK doesn't include the module, or its libraries can't be linked, for example face verification in the 5.26 SDK. The other modules are packaged as usual. Skipped modules have to wait for DCloud to release a fixed SDK. |
