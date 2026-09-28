# Develop Objective-C iOS apps on Windows

**English** · [简体中文](../zh/objective-c.md)

Build Objective-C iOS projects on Windows, install them on your iPhone and debug with breakpoints, no Mac needed. Your .xcodeproj and .xcworkspace work as is. KXApp reads build settings, target dependencies and compiler flags by Xcode's rules and builds an app you can install on your phone. Mixed Objective-C and Swift is supported. For projects that use CocoaPods, see [CocoaPods](cocoapods.md).

## Steps

### 1. Create a project

To use an existing project, open its folder in VS Code with File > [Open Folder…](https://www.kxapp.com/guides/projects.html#open), or drag the folder into VS Code. Otherwise, create one.

*Use either of these*

- **VS Code extension**

  Run **KXApp: New Project** from the Command Palette and pick the "iOS App (Objective-C, UIKit)" [template](https://www.kxapp.com/guides/templates.html), or "iOS App (Objective-C + Swift)" for a mixed project.

- **Command line**

  ```shell
  kxapp project create -t app_objc -n MyApp -o D:\projects
  ```

### 2. Run doctor

Doctor checks your build environment and fixes anything missing.

*Use either of these*

- **VS Code extension**

  In the title bar of the [KXApp view](https://www.kxapp.com/guides/ide-sidebar.html), open the ··· menu and run [Doctor (fix environment)](https://www.kxapp.com/guides/ide-setup.html#update).

- **Command line**

  ```shell
  kxapp doctor .\MyApp.xcodeproj
  ```

### 3. Write code

Open a .m or .h file and you get completion, go to definition and error checking, including for system framework APIs. If completion misbehaves, see [Code completion and indexing](https://www.kxapp.com/guides/ide-intellisense.html).

### 4. Debug

[Connect your iPhone over USB](https://www.kxapp.com/guides/device-setup.html), select it in the KXApp view and press [F5](https://www.kxapp.com/guides/ide-debug.html). KXApp builds, installs and stops at your breakpoints. Breakpoints work in both Objective-C and Swift code.

### 5. Release

[Build with the Release configuration](https://www.kxapp.com/guides/build.html#debug-release) to get build\MyApp.ipa in the project folder. To upload it to App Store Connect, see [Release and App Store submission](https://www.kxapp.com/guides/publish.html).

*Use either of these*

- **VS Code extension**

  Switch the configuration to Release in the Build configuration node of the KXApp view, then run **KXApp: Build** from the Command Palette.

- **Command line**

  Run the command for your project type.

  **.xcodeproj project**

  ```shell
  kxapp build .\MyApp.xcodeproj -c Release
  ```

  **.xcworkspace workspace**

  ```shell
  kxapp build .\MyApp.xcworkspace -c Release
  ```
