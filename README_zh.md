# KXApp（快蝎）— 在 VS Code 里开发 iOS 应用

**在 VS Code 里构建、运行、调试 Xcode 工程，底层就是你已经装好的 Xcode。**

[![Marketplace](https://img.shields.io/visual-studio-marketplace/v/kxapp.kxapp?label=VS%20Marketplace)](https://marketplace.visualstudio.com/items?itemName=kxapp.kxapp)
[![Installs](https://img.shields.io/visual-studio-marketplace/i/kxapp.kxapp)](https://marketplace.visualstudio.com/items?itemName=kxapp.kxapp)
[![Open VSX](https://img.shields.io/open-vsx/v/kxapp/kxapp?label=Open%20VSX)](https://open-vsx.org/extension/kxapp/kxapp)

打开包含 `.xcodeproj` 或 `.xcworkspace` 的文件夹，选好 Scheme 和模拟器，按 `Cmd+R`。
kxapp 用 `xcodebuild` 构建、安装并启动 App，再挂上 Xcode 自带的调试器——不用开 Xcode 窗口，也不用另装工具。

![Cmd+R 构建、运行并命中断点](https://raw.githubusercontent.com/ikxapp/kxapp/main/images/hero.gif)

## 为什么用 kxapp

- **Xcode 文件的可视化编辑器**：Info.plist、entitlements、隐私清单、资源目录、String Catalog、Icon Composer 图标、
  Build Settings，在 VS Code 里按 Xcode 的样子编辑，按 Xcode 的格式保存。
- **不用再装别的**：内置构建服务器让 SourceKit-LSP 拿到完整的代码智能；调试用 Xcode 自带的 `lldb-dap`。
  不需要 xcode-build-server、CodeLLDB、Homebrew。
- **和 Xcode 并行使用**：同一份 DerivedData、同一份索引、同一份工程文件。需要 Interface Builder 或 Instruments
  时切到 Xcode，随时再回来。
- **Xcode 的快捷键**：`Cmd+R` 运行、`Cmd+B` 构建、`Cmd+.` 停止。
- **免费、本地、隐私**：无需账号，无遥测，不联网，一切都在你的 Mac 上完成。

VS Code 以及 Cursor、Windsurf 等基于 VS Code 的编辑器都能用（后者从 [Open VSX](https://open-vsx.org/extension/kxapp/kxapp) 安装）。

## 快速开始

1. 安装 **Xcode 16 或更高版本** 并选中：`sudo xcode-select -s /Applications/Xcode.app`
2. 打开包含 `.xcodeproj` 或 `.xcworkspace` 的文件夹（CocoaPods 生成的 workspace 也可以）。
3. 在状态栏或 kxapp 侧边栏选 Scheme、配置和运行目标，按 `Cmd+R`。

## 功能

### 构建、运行与调试

为任意模拟器或连接的 iPhone/iPad 构建，一步完成安装、启动、附加调试器。断点、条件断点、日志断点、单步、变量、
`po` 和 Xcode 里一样用。也可以不调试直接运行，或附加到已经在运行的 App。编译错误和警告进“问题”面板。

![状态栏与侧边栏中的 Scheme、配置和运行目标](https://raw.githubusercontent.com/ikxapp/kxapp/main/images/build-targets.png)

### 代码智能

Swift、Objective-C、C、C++ 的补全、跳转定义、查找引用和诊断，由 SourceKit-LSP 提供，kxapp 内置构建服务器供给编译参数，
索引与 Xcode 共用。

![Swift 补全与跳转定义](https://raw.githubusercontent.com/ikxapp/kxapp/main/images/completion.gif)

### 属性列表编辑器

Info.plist、`.entitlements`、`.xcprivacy` 等 plist 以 Xcode 式的树形表格编辑：类型化的值、增删行、复制键路径、
XML 或二进制保存格式。`.strings` 文件和描述文件（`.mobileprovision`）有各自的查看器。

![属性列表编辑器中的 Info.plist](https://raw.githubusercontent.com/ikxapp/kxapp/main/images/plist.png)

### 资源目录编辑器

浏览和编辑 `.xcassets`：App Icon、图片集、颜色集、数据集、符号图片。用一张 1024×1024 的图填满所有 App Icon 尺寸，
添加平台，用 Xcode 的 `actool` 做编译检查。Icon Composer 的 `.icon` 文档用 Xcode 自己的渲染器预览。

![用一张图填满 App Icon](https://raw.githubusercontent.com/ikxapp/kxapp/main/images/xcassets.gif)

### 多语言

并排编辑 String Catalog（`.xcstrings`）和 `.lproj` 下的 `.strings` / `.stringsdict`，按复数或设备区分译文；
添加语言时会自动登记到工程。

![多语言的 String Catalog](https://raw.githubusercontent.com/ikxapp/kxapp/main/images/xcstrings.png)

### 工程设置

`project.pbxproj` 的 General 与 Build Settings 页面，显示每一层（Target、Project、xcconfig、默认值）的解析结果，
和 Xcode 的 Levels 视图一样。修改时尽量少动工程文件，并保持其有效。

![带 Levels 的 Build Settings](https://raw.githubusercontent.com/ikxapp/kxapp/main/images/build-settings.png)

### 设备、模拟器与测试

在侧边栏启动、关闭模拟器，查看已连接设备。在测试资源管理器里运行 XCTest 和 Swift Testing，失败会标在出错的那一行。

![测试资源管理器中的测试](https://raw.githubusercontent.com/ikxapp/kxapp/main/images/tests.png)

## 环境要求

- macOS，已安装 **Xcode 16 或更高版本**，并用 `xcode-select` 选中
- 编辑 `project.pbxproj`（Build Settings、加资源、加语言）需要 Ruby 的 `xcodeproj` gem：
  `gem install --user-install xcodeproj`（装过 CocoaPods 的已经有了）

## 快捷键

| 按键 | 命令 |
| --- | --- |
| `Cmd+R` | 构建并运行 |
| `Cmd+B` | 构建（在 Xcode 工程的编辑器中会占用 VS Code 的“切换侧边栏”） |
| `Cmd+.` | 停止 |

## 设置

| 设置 | 默认值 | |
| --- | --- | --- |
| `kxapp.defaultConfiguration` | `Debug` | 未选择时使用的构建配置 |
| `kxapp.build.allowProvisioningUpdates` | `true` | 给 `xcodebuild` 传 `-allowProvisioningUpdates` |
| `kxapp.build.extraArgs` | `[]` | 附加的 `xcodebuild` 参数 |
| `kxapp.debug.killAppOnStop` | `true` | 停止调试时结束 App |
| `kxapp.plist.defaultSaveFormat` | `preserve` | plist 保存为 XML、二进制或保持原格式 |
| `kxapp.rubyPath` | | 装有 `xcodeproj` gem 的 Ruby；留空使用 PATH 上的 `ruby` |

## 常见问题

**需要开着 Xcode 吗？**
不需要，装着就行。同一个工程也可以同时在 Xcode 里打开。

**工程目录里的 `buildServer.json` 是什么？**
第一次启动代码智能时 kxapp 写入它，让 SourceKit-LSP 找到内置构建服务器，可以加进 `.gitignore`。
已属于其他构建服务器（如 xcode-build-server）的 `buildServer.json` 不会被覆盖。

**还需要 SweetPad、xcode-build-server 或 CodeLLDB 吗？**
不需要。kxapp 有自己的构建服务器，调试用 Xcode 的 `lldb-dap`。同一工作区里建议停用其他 iOS 构建插件，
避免快捷键和构建服务器重复。

**收费吗？收集数据吗？**
免费。kxapp 不发送遥测、不发起网络请求，所有工作都由你 Mac 上的 Xcode 工具完成。

## 反馈

在 [GitHub Issues](https://github.com/ikxapp/kxapp/issues) 提交问题和建议。请附上 macOS、Xcode、kxapp 的版本，
以及“输出”面板中 **kxapp** 和 **kxapp Build** 频道的内容。

[English](https://github.com/ikxapp/kxapp#readme)

---

Xcode、iPhone、iPad 和 Swift 是 Apple Inc. 的商标。kxapp 与 Apple 无关联，也未获其认可。
