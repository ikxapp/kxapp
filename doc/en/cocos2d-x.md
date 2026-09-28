# Build cocos2d-x games for iOS on Windows

**English** · [简体中文](../zh/cocos2d-x.md)

Build the iOS version of a cocos2d-x game on Windows, install it on your iPhone and debug the C++ code with breakpoints, no Mac needed. Both 3.x and 4.x are supported. The engine source builds along with your game as a subproject, with no changes to the engine or the project settings.

## Steps

### 1. Install cocos2d-x and create a project

To use an existing project, open its root folder in VS Code with File > [Open Folder…](https://www.kxapp.com/guides/projects.html#open), or drag the folder into VS Code. Otherwise, create one. Download the engine and its dependencies as described on the cocos2d-x website, and run setup.py in the engine folder to set up the cocos command. Then create the project and open it in VS Code.

```shell
cocos new MyGame -l cpp -p com.example.mygame -d .
```

### 2. Run doctor

**Do this first whenever you open a project for the first time.** Doctor checks your cocos2d-x setup and prepares the iOS project. For 4.x, this step also generates the Xcode project in the build-xcode folder.

*Use either of these*

- **VS Code extension**

  In the title bar of the [KXApp view](https://www.kxapp.com/guides/ide-sidebar.html), open the ··· menu and run [Doctor (fix environment)](https://www.kxapp.com/guides/ide-setup.html#update).

- **Command line**

  ```shell
  kxapp doctor D:\work\MyGame
  ```

### 3. Write code

With the project root open, C++ code gets [completion, go to definition and error checking](https://www.kxapp.com/guides/ide-intellisense.html). For Lua and JS scripts, install the matching VS Code extensions.

### 4. Debug

[Connect your iPhone over USB](https://www.kxapp.com/guides/device-setup.html), select it in the KXApp view and press [F5](https://www.kxapp.com/guides/ide-debug.html). Debug C++ with breakpoints in VS Code, and Lua or JS scripts with the engine's own debugging tools. The two work independently.

### 5. Release

[Build with the Release configuration](https://www.kxapp.com/guides/build.html#debug-release) to get an .ipa. To upload it to App Store Connect, see [Release and App Store submission](https://www.kxapp.com/guides/publish.html).

*Use either of these*

- **VS Code extension**

  Switch the configuration to Release in the Build configuration node of the KXApp view, then run **KXApp: Build** from the Command Palette.

- **Command line**

  Run the command for your engine version.

  **3.x project**

  ```shell
  kxapp build .\proj.ios_mac\MyGame.xcodeproj -c Release -t MyGame-mobile
  ```

  **4.x project**

  ```shell
  kxapp build .\build-xcode\MyGame.xcodeproj -c Release -t MyGame
  ```
