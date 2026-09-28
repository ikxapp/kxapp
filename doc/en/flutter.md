# Build and debug Flutter iOS apps on Windows

**English** · [简体中文](../zh/flutter.md)

Build the iOS side of a Flutter project on Windows and debug it on your iPhone, no Mac needed. Native and Dart breakpoints both work, and so does hot reload. Use KXApp in place of flutter build ios and flutter run for iOS. Every other flutter command works as usual.

## Steps

### 1. Install Flutter and the VS Code extension

Install the Flutter SDK as described on the Flutter website and add the flutter command to PATH. Open a new terminal and check that this prints a version. Then install the Flutter extension from the VS Code Marketplace, which installs the Dart extension too.

```shell
flutter --version
```

### 2. Create a project

To use an existing project, open the Flutter project's root folder in VS Code with File > [Open Folder…](https://www.kxapp.com/guides/projects.html#open), or drag the folder into VS Code. Otherwise, create one with flutter create or one of the options below.

*Use either of these*

- **VS Code extension**

  Run **KXApp: New Project** from the Command Palette and pick the "Flutter App" [template](https://www.kxapp.com/guides/templates.html).

- **Command line**

  ```shell
  kxapp project create -t flutter_app -n myflutterapp -o D:\work
  ```

### 3. Run doctor

**Do this first whenever you open a project for the first time.** Doctor checks your Flutter setup and prepares the iOS project.

*Use either of these*

- **VS Code extension**

  In the title bar of the [KXApp view](https://www.kxapp.com/guides/ide-sidebar.html), open the ··· menu and run [Doctor (fix environment)](https://www.kxapp.com/guides/ide-setup.html#update).

- **Command line**

  ```shell
  kxapp doctor D:\work\myflutterapp
  ```

If the project uses plugins that need CocoaPods, install their dependencies in the ios folder after doctor. See [CocoaPods](cocoapods.md). Otherwise, skip this.

```shell
cd ios
pod install
```

### 4. Write code

The Flutter extension provides [completion, go to definition and error checking](https://www.kxapp.com/guides/ide-intellisense.html#who) for Dart. KXApp provides them for the Swift and Objective-C code under ios/.

### 5. Debug

[Connect your iPhone over USB](https://www.kxapp.com/guides/device-setup.html), select it in the KXApp view and press [F5](https://www.kxapp.com/guides/ide-debug.html). Native breakpoints hit first. Once the app starts, the Dart debugger attaches automatically, so Dart breakpoints and hot reload both work.

### 6. Release

[Build with the Release configuration](https://www.kxapp.com/guides/build.html#debug-release) to get build\Runner.ipa in the ios folder. To upload it to App Store Connect, see [Release and App Store submission](https://www.kxapp.com/guides/publish.html).

*Use either of these*

- **VS Code extension**

  Switch the configuration to Release in the Build configuration node of the KXApp view, then run **KXApp: Build** from the Command Palette.

- **Command line**

  ```shell
  kxapp build .\ios\Runner.xcworkspace -c Release
  ```
