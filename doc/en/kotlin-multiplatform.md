# Build Kotlin Multiplatform iOS apps on Windows

**English** · [简体中文](../zh/kotlin-multiplatform.md)

Build the iOS app of a Kotlin Multiplatform project on Windows, install it on your iPhone and debug it. The iosApp project and your Gradle build scripts need no changes, and Compose Multiplatform works too. Set breakpoints in both Swift and Kotlin, and step from Swift into Kotlin.

## Steps

### 1. Set up your environment

Install Android Studio as described in the Kotlin Multiplatform docs, then install the Kotlin Multiplatform plugin from its plugin marketplace.

### 2. Create a project

To use an existing project, open its root folder in VS Code with File > [Open Folder…](https://www.kxapp.com/guides/projects.html#open), or drag the folder into VS Code. Otherwise, create one with the Kotlin Multiplatform wizard in Android Studio or on the JetBrains website, select the iOS target, and open it in VS Code.

### 3. Run doctor

**Do this first whenever you open a project for the first time.** Doctor checks your Kotlin Multiplatform setup and prepares the iOS project. The first run downloads a few hundred MB and takes a while. Run it again after you upgrade Kotlin.

*Use either of these*

- **VS Code extension**

  In the title bar of the [KXApp view](https://www.kxapp.com/guides/ide-sidebar.html), open the ··· menu and run [Doctor (fix environment)](https://www.kxapp.com/guides/ide-setup.html#update).

- **Command line**

  ```shell
  kxapp doctor D:\work\mykmpapp\iosApp\iosApp.xcodeproj
  ```

### 4. Write code

The Swift code in iosApp gets [completion, go to definition and error checking](https://www.kxapp.com/guides/ide-intellisense.html) in VS Code. Keep writing the shared Kotlin code in Android Studio or IntelliJ IDEA.

### 5. Debug

[Connect your iPhone over USB](https://www.kxapp.com/guides/device-setup.html), select it in the KXApp view and press [F5](https://www.kxapp.com/guides/ide-debug.html). In both Swift and Kotlin you can set breakpoints, step through code and inspect variables. Kotlin objects expand by class and field.

### 6. Release

[Build with the Release configuration](https://www.kxapp.com/guides/build.html#debug-release) to get an .ipa in the iosApp folder. To upload it to App Store Connect, see [Release and App Store submission](https://www.kxapp.com/guides/publish.html).

*Use either of these*

- **VS Code extension**

  Switch the configuration to Release in the Build configuration node of the KXApp view, then run **KXApp: Build** from the Command Palette.

- **Command line**

  ```shell
  kxapp build .\iosApp\iosApp.xcodeproj -c Release
  ```
