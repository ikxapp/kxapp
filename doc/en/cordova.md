# Build Cordova iOS apps on Windows

**English** · [简体中文](../zh/cordova.md)

Package a Cordova project for iOS on Windows and debug it on your iPhone. The platforms/ios project that cordova platform add ios creates builds like any Xcode project, and cordova commands and plugins work as usual.

## Steps

### 1. Create a Cordova project and add the iOS platform

For an existing project, add the iOS platform in the project folder. Then open platforms/ios in VS Code with File > [Open Folder…](https://www.kxapp.com/guides/projects.html#open), or drag the whole Cordova project into VS Code. Otherwise, create one. Install Cordova with npm, create the project, then add the iOS platform from inside the project folder. The Xcode project is generated under platforms/ios.

```shell
npm install -g cordova
```

```shell
cordova create MyApp com.example.myapp MyApp
```

```shell
cd MyApp
```

```shell
cordova platform add ios
```

### 2. Run doctor

Doctor checks your build environment and prepares the iOS project.

*Use either of these*

- **VS Code extension**

  In the title bar of the [KXApp view](https://www.kxapp.com/guides/ide-sidebar.html), open the ··· menu and run [Doctor (fix environment)](https://www.kxapp.com/guides/ide-setup.html#update).

- **Command line**

  ```shell
  kxapp doctor .\platforms\ios\App.xcworkspace
  ```

By default the project manages dependencies with Swift packages and doesn't need CocoaPods. **If a plugin you add has CocoaPods dependencies, a Podfile appears in platforms/ios.** Cordova doesn't install those pods on Windows, so run pod install once in platforms/ios, and again whenever you add or remove such a plugin. See [CocoaPods](cocoapods.md).

```shell
cd platforms\ios
pod install
```

### 3. Write code

Keep writing your web code under www/, and run cordova prepare ios after changes to sync it to the iOS project. Native plugin code gets [completion and go to definition](https://www.kxapp.com/guides/ide-intellisense.html) in VS Code.

### 4. Debug

[Connect your iPhone over USB](https://www.kxapp.com/guides/device-setup.html), select it in the KXApp view and press [F5](https://www.kxapp.com/guides/ide-debug.html). Debug native code with breakpoints in VS Code and the web content with your browser's remote debugging tools. The two work independently.

### 5. Release

[Build with the Release configuration](https://www.kxapp.com/guides/build.html#debug-release) to get an .ipa under platforms/ios. To upload it to App Store Connect, see [Release and App Store submission](https://www.kxapp.com/guides/publish.html).

*Use either of these*

- **VS Code extension**

  Switch the configuration to Release in the Build configuration node of the KXApp view, then run **KXApp: Build** from the Command Palette.

- **Command line**

  ```shell
  kxapp build .\platforms\ios\App.xcworkspace -c Release
  ```
