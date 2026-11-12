# Changelog

## Unreleased

- **Run and debug without Xcode**: with KXBuild installed (Windows, Linux, or a Mac without Xcode), Build & Run,
  Run Without Debugging and Attach to Running App work on a connected iPhone or iPad: breakpoints, stepping,
  variables and the app's output in the console. The first debug run for an iOS version copies the system
  libraries from the device, which takes a few minutes.

## 0.1.3

- **Without Xcode**: on Windows, Linux, or a Mac without Xcode, projects build, clean and run tests on a
  connected iPhone or iPad when KXBuild is installed; the device list and the project editor work too. Run,
  debug, simulators and code completion still need Xcode on macOS.

## 0.1.2

- **Large source trees**: opening a folder such as a WebKit checkout no longer stalls. Project discovery skips
  CMake and WebKit build output, treats the projects under an `.xcworkspace` as part of that workspace, and code
  completion builds in the background only after you pick the startup project when the folder holds more than five
  projects. SourceKit-LSP starts only for files that belong to an Xcode project or a Swift package.

## 0.1.1

- **Device debugging**: debugging on a device no longer hangs when another paired device is not supported by the
  installed Xcode; attaching gives up after 10 seconds when no attach starts.
- **Build errors**: signing and provisioning failures are shown as the build failure summary and in the Problems
  panel on `project.pbxproj`.
- **Run Without Debugging**: launch failures on the device (for example a locked device) are reported.
- **Projects under `/private/tmp`**: build errors, test failures and breakpoints land on the files you have open,
  and code intelligence gets compiler arguments.
- **Tests on a simulator**: test files no longer report "No such module 'Testing'" when a simulator is the run
  destination.
- **SourceKit-LSP**: the restart command is always in the Command Palette and starts the server when it is not
  running.
- **Asset catalog editor**: the App Store icon is written without an alpha channel; `actool` diagnostics are
  attached to the right set and listed once; renaming a set to an existing name is caught; changes made by other
  tools are picked up. Icon previews say when they need Xcode 26.
- **Localization editor**: varying a String Catalog entry by plural or device keeps the catalog valid; `.strings`
  files keep their spacing on save; `%arg` placeholders follow the keys from the last build.
- **Property list editor**: changing a value's type tells you when the old value is dropped (undo restores it).
- **Project settings editor**: only deployment targets the installed SDK supports are offered; renaming a build
  setting that is not set is rejected; edits to `project.pbxproj` files without reference comments stay minimal,
  and original line endings are kept.
- New extension icon.

## 0.1.0

First public release.

- **Build, run and debug**: pick project, scheme, configuration and run destination from the status bar or side
  bar; build with `xcodebuild`, install and launch on a simulator or a connected device, and debug with Xcode's
  `lldb-dap`. Run without debugging, attach to a running app. Build errors and warnings in the Problems panel.
  `Cmd+R`, `Cmd+B` and `Cmd+.` as in Xcode.
- **Code intelligence**: SourceKit-LSP with a built-in build server for Swift, Objective-C, C and C++, sharing
  Xcode's index in DerivedData.
- **Tests**: XCTest and Swift Testing in the Test Explorer.
- **Devices and simulators**: list devices, boot and shut down simulators from the side bar.
- **Property list editor**: Info.plist, `.entitlements`, `.xcprivacy` and other plists, XML or binary; `.strings`
  editor; provisioning profile viewer.
- **Asset catalog editor**: app icons (fill all sizes from one image), image, color, data and symbol sets,
  tvOS and visionOS icons, compile check with `actool`.
- **Icon Composer documents**: `.icon` editing with previews rendered by Xcode's `ictool`.
- **Localization editor**: String Catalogs (`.xcstrings`) and `.lproj` `.strings` / `.stringsdict`; adding a
  language registers it in the project.
- **Project settings editor**: General and Build Settings of `project.pbxproj`, with resolved values per level.
- English and Simplified Chinese user interface.
