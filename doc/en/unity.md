# Build Unity iOS projects on Windows

**English** · [简体中文](../zh/unity.md)

Build the iOS project that Unity exports on Windows, install it on your iPhone and debug the native layer, no Mac needed. Export from Unity as usual and treat the export folder as a regular Xcode project. You don't need a Unity plugin or any change to your Unity project settings.

## Steps

### 1. Develop in Unity and export an Xcode project

Develop your project in Unity as usual. With the iOS Build Support module installed, switch the platform to iOS in Build Settings and build to a folder. Then open that folder in VS Code with File > [Open Folder…](https://www.kxapp.com/guides/projects.html#open).

### 2. Run doctor

Doctor checks your build environment and fixes anything missing. If you use plugins with iOS dependencies, such as Firebase or Google Mobile Ads, the export folder contains a Podfile. In that case, run pod install in the export folder afterwards. See [CocoaPods](cocoapods.md).

*Use either of these*

- **VS Code extension**

  In the title bar of the [KXApp view](https://www.kxapp.com/guides/ide-sidebar.html), open the ··· menu and run [Doctor (fix environment)](https://www.kxapp.com/guides/ide-setup.html#update).

- **Command line**

  ```shell
  kxapp doctor .\Unity-iPhone.xcodeproj
  ```

### 3. Write code

Keep writing C# scripts in Unity and export again after changes. The Objective-C plugin code in the export folder gets [completion and go to definition](https://www.kxapp.com/guides/ide-intellisense.html) in VS Code.

### 4. Debug

[Connect your iPhone over USB](https://www.kxapp.com/guides/device-setup.html), select it in the KXApp view and press [F5](https://www.kxapp.com/guides/ide-debug.html). Debug native code with breakpoints in VS Code and C# scripts with Unity's own debugger. The two work independently.

### 5. Release

[Build with the Release configuration](https://www.kxapp.com/guides/build.html#debug-release) to get an .ipa in the export folder. To upload it to App Store Connect, see [Release and App Store submission](https://www.kxapp.com/guides/publish.html).

*Use either of these*

- **VS Code extension**

  Switch the configuration to Release in the Build configuration node of the KXApp view, then run **KXApp: Build** from the Command Palette.

- **Command line**

  The target is always Unity-iPhone. Run the command for your export folder.

  **No Podfile**

  ```shell
  kxapp build .\Unity-iPhone.xcodeproj -c Release -t Unity-iPhone
  ```

  **Podfile, after pod install**

  ```shell
  kxapp build .\Unity-iPhone.xcworkspace -c Release -t Unity-iPhone
  ```
