# Changelog

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
