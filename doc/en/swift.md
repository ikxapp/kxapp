# Develop Swift iOS apps on Windows

**English** · [简体中文](../zh/swift.md)

Build Swift iOS projects on Windows, install them on your iPhone and debug with breakpoints. SwiftUI, Swift Package Manager and mixed Swift and Objective-C are all supported. KXApp reads build settings, target dependencies and compiler flags by Xcode's rules, so your project works as is. Swift projects come in two kinds, [Xcode projects](#xcode) and [standalone Swift packages](#package) with only a Package.swift. Each is covered below. For projects that use CocoaPods, see [CocoaPods](cocoapods.md).

<a id="xcode"></a>

## Xcode projects

A project with an .xcodeproj or .xcworkspace. Dependencies can be Swift packages, which are resolved automatically before each build.

### 1. Create a project

To use an existing project, open its folder in VS Code with File > [Open Folder…](https://www.kxapp.com/guides/projects.html#open), or drag the folder into VS Code. Otherwise, create one.

*Use either of these*

- **VS Code extension**

  Run **KXApp: New Project** from the Command Palette and pick the "iOS App (SwiftUI)" or "iOS App (Swift, UIKit)" [template](https://www.kxapp.com/guides/templates.html).

- **Command line**

  ```shell
  kxapp project create -t app_swiftui -n MyApp -o D:\projects
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

<a id="add-package"></a>

### 3. Add a Swift package dependency

This is the equivalent of Add Package Dependencies in Xcode. As in Xcode, a remote package defaults to its latest version and allows updates up to the next major version, and adding one needs a network connection.

*Use either of these*

- **VS Code extension**

  Run **KXApp: Add Swift Package Dependency…** from the Command Palette, or right-click a target in the KXApp view and choose it there. Enter the package's Git URL or pick a local package folder, then choose the products you need.

- **Command line**

  Run the command for where the package lives.

  **Remote package**

  ```shell
  kxapp project add-package -P .\MyApp.xcodeproj --url https://github.com/Alamofire/Alamofire.git --product Alamofire
  ```

  **Local package**

  ```shell
  kxapp project add-package -P .\MyApp.xcodeproj --path ..\MyKit
  ```

  To set a version or target, see [project add-package](https://www.kxapp.com/guides/cli-kxapp.html#project-add-package).

### 4. Write code

Open a .swift file and you get completion, go to definition and error checking, including for SwiftUI and system framework APIs. Build once before you import modules from other targets or Swift packages in the project. If completion misbehaves, see [Code completion and indexing](https://www.kxapp.com/guides/ide-intellisense.html).

### 5. Debug

[Connect your iPhone over USB](https://www.kxapp.com/guides/device-setup.html), select it in the KXApp view and press [F5](https://www.kxapp.com/guides/ide-debug.html). KXApp builds, installs and stops at your breakpoints. Breakpoints work in both Swift and Objective-C code.

### 6. Release

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

<a id="package"></a>

## Standalone Swift packages

For a project with only a Package.swift and no Xcode project, open the folder containing Package.swift in VS Code to write and compile-check code. A Swift package can't be packaged as an app on its own, and that's true on a Mac too. To install it on an iPhone or produce an .ipa, find your case below.

- **The package is an app.** Its executable target holds a SwiftUI or UIKit app entry point. Follow the steps below to convert it to an app project.
- **The package only provides libraries** for apps to use. In the app project, [add it as a Swift package dependency](#add-package) as in step 3 above.

### 1. Write code and compile-check

Open a .swift file and you get completion, go to definition and error checking, including for SwiftUI, UIKit and other iOS framework APIs. To compile-check, run this in the folder containing Package.swift.

```shell
kxapp build .
```

### 2. Convert to an app project

Converting adds a MyApp subfolder to the package folder with the app project inside. The app still uses the package's code, so when you edit the package, you edit the app. Commit this subfolder to version control along with the package.

If the app uses a target from the same package that has no matching library product, the conversion adds a .library entry to products in Package.swift. **After converting, review and commit that change to Package.swift.**

*Use either of these*

- **VS Code extension**

  Run **KXApp: Convert Swift Package to App Project** from the Command Palette (or click the package's row in the KXApp view), then enter the app name and bundle ID. The new project becomes the startup project.

- **Command line**

  Run this in the folder containing Package.swift.

  ```shell
  kxapp project spm2app . -n MyApp -b com.example.myapp
  ```

### 3. Debug and release

In the KXApp view, switch the [startup project](https://www.kxapp.com/guides/ide-sidebar.html#startup) to MyApp. From there, follow the [debug and release steps](#xcode) for Xcode projects above. The .ipa is written to MyApp\build\MyApp.ipa. On the command line, build this project.

```shell
kxapp build .\MyApp\MyApp.xcodeproj -c Release
```

## Troubleshooting

| Symptom | Fix |
|---|---|
| A Debug build fails to link with undefined symbol: …vpfi | A known issue in the open-source Swift compiler. It happens with a property that has an initial value, such as `@State private var count = 0`, when the struct's init is in another file. Set the environment variable `KXAPP_SWIFT_WHOLE_MODULE=all`, reopen VS Code and build again. Swift targets are then built as a whole module. See [Troubleshooting](https://www.kxapp.com/guides/troubleshooting.html#vpfi). |
