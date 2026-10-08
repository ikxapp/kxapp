# Build and debug React Native iOS apps on Windows

**English** · [简体中文](../zh/react-native.md)

Build the iOS side of a React Native project on Windows and debug it on your iPhone. Run Metro for the JS as usual, and set breakpoints in native code. Build scripts in your project that call xcodebuild work without changes. See [xcodebuild and xcrun compatibility](https://www.kxapp.com/guides/cli-compat.html).

## Steps

### 1. Set up React Native

Install Node.js as described on the React Native website. Open a new terminal and check that this prints a version.

```shell
node --version
```

### 2. Create a project

To use an existing project, open its root folder in VS Code with File > [Open Folder…](https://www.kxapp.com/guides/projects.html#open), or drag the folder into VS Code. Otherwise, create one.

*Use either of these*

- **VS Code extension**

  Run **KXApp: New Project** from the Command Palette and pick the "React Native App" [template](https://www.kxapp.com/guides/templates.html).

- **Command line**

  Keep the parent path short, because the dependency folders nest deeply.

  ```shell
  kxapp project create -t react_native_app -n rnhello -o D:\work
  ```

### 3. Run doctor

**Do this first whenever you open a project for the first time.** Doctor checks your React Native setup and prepares the iOS project.

*Use either of these*

- **VS Code extension**

  In the title bar of the [KXApp view](https://www.kxapp.com/guides/ide-sidebar.html), open the ··· menu and run [Doctor (fix environment)](https://www.kxapp.com/guides/ide-setup.html#update).

- **Command line**

  ```shell
  kxapp doctor D:\work\rnhello
  ```

After doctor, install the native dependencies in the ios folder. See [CocoaPods](cocoapods.md).

```shell
cd ios
pod install
```

### 4. Write code

Write JS and TypeScript in VS Code as usual, and Metro reloads when you save. KXApp provides [completion and go to definition](https://www.kxapp.com/guides/ide-intellisense.html) for the native code under ios/.

### 5. Debug

In a second terminal, run npx react-native start in the project folder. Then select your device and press [F5](https://www.kxapp.com/guides/ide-debug.html). Debug native breakpoints in VS Code and JS breakpoints in the Metro / Hermes debugger. The two work independently.

### 6. Release

[Build with the Release configuration](https://www.kxapp.com/guides/build.html#debug-release). The JS is bundled into the app, and the .ipa is written to the ios folder. To upload it to App Store Connect, see [Release and App Store submission](https://www.kxapp.com/guides/publish.html).

*Use either of these*

- **VS Code extension**

  Switch the configuration to Release in the Build configuration node of the KXApp view, then run **KXApp: Build** from the Command Palette.

- **Command line**

  ```shell
  kxapp build .\ios\rnhello.xcworkspace -c Release
  ```
