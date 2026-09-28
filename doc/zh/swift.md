# Windows 上开发 Swift iOS App

**简体中文** · [English](../en/swift.md)

Swift 的 iOS 工程在 Windows 上可以直接编译、安装到 iPhone 并断点调试，不需要 Mac。支持 SwiftUI、Swift Package Manager 和与 Objective-C 混编，工程设置、target 依赖和编译参数按 Xcode 的规则读取，不需要改造。Swift 项目分两类，[Xcode 工程](#xcode)和只有 Package.swift 的[纯 Swift Package](#package)，下面分开介绍。使用 CocoaPods 的工程见 [CocoaPods](cocoapods.md)。

<a id="xcode"></a>

## Xcode 工程

有 .xcodeproj 或 .xcworkspace 的工程，依赖可以用 Swift Package 管理，构建前自动解析。

### 1. 新建

已有工程在 VS Code 中「文件 → [打开文件夹](https://www.kxapp.com/zh/guides/projects.html#open)」打开工程目录，或者把工程目录拖进 VS Code 即可。没有现成工程的，用下面的方式新建。

*以下两种做法任选其一*

- **VS Code 插件**

  命令面板运行 **KXApp: 新建项目**，[模板](https://www.kxapp.com/zh/guides/templates.html)选「iOS 应用（SwiftUI）」或「iOS 应用（Swift · UIKit）」。

- **命令行**

  ```shell
  kxapp project create -t app_swiftui -n MyApp -o D:\projects
  ```

### 2. 体检

检查并修好编译需要的环境。

*以下两种做法任选其一*

- **VS Code 插件**

  [KXApp 视图](https://www.kxapp.com/zh/guides/ide-sidebar.html)标题栏「···」中运行「[体检并修复开发环境](https://www.kxapp.com/zh/guides/ide-setup.html#update)」。

- **命令行**

  ```shell
  kxapp doctor .\MyApp.xcodeproj
  ```

<a id="add-package"></a>

### 3. 添加 Swift Package 依赖

相当于 Xcode 的 Add Package Dependencies。远程包默认用最新版本，允许升级到下一个主版本之前，和 Xcode 一样，添加时需要联网。

*以下两种做法任选其一*

- **VS Code 插件**

  命令面板运行 **KXApp: 添加 Swift Package 依赖…**，或在 KXApp 视图中右键 target 选择它。按提示输入包的 Git 地址或选择本地包目录，再选要用的产品。

- **命令行**

  按包的位置执行其中一条。

  **远程包**

  ```shell
  kxapp project add-package -P .\MyApp.xcodeproj --url https://github.com/Alamofire/Alamofire.git --product Alamofire
  ```

  **本地包**

  ```shell
  kxapp project add-package -P .\MyApp.xcodeproj --path ..\MyKit
  ```

  指定版本、target 的写法见 [project add-package](https://www.kxapp.com/zh/guides/cli-kxapp.html#project-add-package)。

### 4. 编码

打开 .swift 文件就有补全、跳转定义和错误提示，SwiftUI 和系统框架的 API 也能补全。引用工程里其他 target 或 Swift Package 的模块时先构建一次。提示异常时见[代码提示与索引](https://www.kxapp.com/zh/guides/ide-intellisense.html)。

### 5. 调试

[USB 连接 iPhone](https://www.kxapp.com/zh/guides/device-setup.html)，在 KXApp 视图中选中设备，按 [F5](https://www.kxapp.com/zh/guides/ide-debug.html) 编译、安装并停在断点上。Swift 和 Objective-C 代码都能设断点。

### 6. 发布

用 [Release 配置构建](https://www.kxapp.com/zh/guides/build.html#debug-release)，工程目录下生成 build\MyApp.ipa。上传到 App Store Connect 见[发布与上架](https://www.kxapp.com/zh/guides/publish.html)。

*以下两种做法任选其一*

- **VS Code 插件**

  在 KXApp 视图的「构建配置」节点切到 Release，命令面板运行 **KXApp: 构建**。

- **命令行**

  按工程类型执行其中一条。

  **.xcodeproj 工程**

  ```shell
  kxapp build .\MyApp.xcodeproj -c Release
  ```

  **.xcworkspace 工作区**

  ```shell
  kxapp build .\MyApp.xcworkspace -c Release
  ```

<a id="package"></a>

## 纯 Swift Package

只有 Package.swift、没有 Xcode 工程的项目，在 VS Code 中打开 Package.swift 所在目录就能编写和编译检查。Swift Package 本身打包不成 App，在 Mac 上也一样，所以要装到 iPhone 或出 ipa 时分两种情况。

- **包本身是一个 App**，可执行 target 里是 SwiftUI 或 UIKit 的 App 入口。按下面的步骤转为 App 工程。
- **包只提供库**，它是给 App 用的。在 App 工程里按上面第 3 步[添加 Swift Package 依赖](#add-package)即可。

### 1. 编码与编译检查

打开 .swift 文件就有补全、跳转定义和错误提示，SwiftUI、UIKit 等 iOS 框架的 API 也能补全。编译检查在 Package.swift 所在目录执行。

```shell
kxapp build .
```

### 2. 转为 App 工程

转换后包目录下多出一个 MyApp 子目录，里面是 App 工程。App 的代码还是包里的那份，改包里的代码就是改 App。把这个子目录和包一起提交到版本库。

App 用到的同包 target 没有对应的 library 产品时，转换会在 Package.swift 的 products 里补一行 .library。**转换完成后检查并提交 Package.swift 的这处改动。**

*以下两种做法任选其一*

- **VS Code 插件**

  命令面板运行 **KXApp: 将 Swift Package 转为 App 工程**（或点 KXApp 视图里的提示行），按提示填写 App 名和 Bundle ID。完成后新工程自动设为启动项目。

- **命令行**

  在 Package.swift 所在目录执行。

  ```shell
  kxapp project spm2app . -n MyApp -b com.example.myapp
  ```

### 3. 调试与发布

在 KXApp 视图中把[启动项目](https://www.kxapp.com/zh/guides/ide-sidebar.html#startup)切到 MyApp，之后按上面 Xcode 工程的[调试和发布](#xcode)步骤操作，ipa 生成在 MyApp\build\MyApp.ipa。命令行构建时指定这个工程。

```shell
kxapp build .\MyApp\MyApp.xcodeproj -c Release
```

## 常见问题

| 现象 | 处理 |
|---|---|
| Debug 构建链接时报 undefined symbol: …vpfi | 开源 Swift 编译器的已知问题，出现在 `@State private var count = 0` 这类带初始值的属性上，而结构体的 init 写在另一个文件里。设置环境变量 `KXAPP_SWIFT_WHOLE_MODULE=all` 后重开 VS Code 再构建，Swift 目标改为整模块编译。详见[常见问题](https://www.kxapp.com/zh/guides/troubleshooting.html#vpfi) |
