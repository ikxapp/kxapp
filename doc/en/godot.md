# Build Godot iOS projects on Windows

**English** · [简体中文](../zh/godot.md)

The iOS project Godot exports can be built on Windows, installed on your iPhone and debugged at the native layer. Export from Godot as usual and use the export folder like any Xcode project. Your Godot project settings stay as they are.

## Steps

### 1. Develop in Godot and export an Xcode project

Develop your project in Godot as usual. Download the export templates from Editor > Manage Export Templates, add an iOS preset in Project > Export, fill in App Store Team ID and Bundle Identifier, and export to an empty folder outside the Godot project with a file name such as MyGame.ipa. On Windows, Godot writes the Xcode project MyGame.xcodeproj instead of an .ipa. Then open that folder in VS Code with File > [Open Folder…](https://www.kxapp.com/guides/projects.html#open).

### 2. Run doctor

Doctor checks your build environment and fixes anything missing.

*Use either of these*

- **VS Code extension**

  In the title bar of the [KXApp view](https://www.kxapp.com/guides/ide-sidebar.html), open the ··· menu and run [Doctor (fix environment)](https://www.kxapp.com/guides/ide-setup.html#update).

- **Command line**

  ```shell
  kxapp doctor .\MyGame.xcodeproj
  ```

### 3. Write code

Edit GDScript and scenes in Godot as usual, then export again to the same folder. Native code in the export folder gets [completion and go-to-definition](https://www.kxapp.com/guides/ide-intellisense.html) in VS Code.

### 4. Debug

[Connect your iPhone over USB](https://www.kxapp.com/guides/device-setup.html), select it in the KXApp view and press [F5](https://www.kxapp.com/guides/ide-debug.html). Native code gets breakpoints in VS Code, and GDScript uses Godot's own debugger. The two don't get in each other's way.

### 5. Release

[Build with the Release configuration](https://www.kxapp.com/guides/build.html#debug-release) to get an .ipa in the export folder. To upload it to App Store Connect, see [Publish to the App Store](https://www.kxapp.com/guides/publish.html).

*Use either of these*

- **VS Code extension**

  Switch the configuration to Release in the Build configuration node of the KXApp view, then run **KXApp: Build** from the Command Palette.

- **Command line**

  ```shell
  kxapp build .\MyGame.xcodeproj -c Release
  ```
