# Windows 上开发 Objective-C iOS App

**简体中文** · [English](../en/objective-c.md)

Objective-C 的 iOS 工程在 Windows 上可以直接编译、安装到 iPhone 并断点调试。.xcodeproj 和 .xcworkspace 不需要改造。工程设置、target 依赖和编译参数都按 Xcode 的规则读取，直接编译出可以安装到手机的 App。支持 Objective-C 与 Swift 混编，使用 CocoaPods 的工程见 [CocoaPods](cocoapods.md)。

## 步骤

### 1. 新建

已有工程在 VS Code 中「文件 → [打开文件夹](https://www.kxapp.com/zh/guides/projects.html#open)」打开工程目录，或者把工程目录拖进 VS Code 即可。没有现成工程的，用下面的方式新建。

*以下两种做法任选其一*

- **VS Code 插件**

  命令面板运行 **KXApp: 新建项目**，[模板](https://www.kxapp.com/zh/guides/templates.html)选「iOS 应用（Objective-C · UIKit）」，混编工程选「Objective-C + Swift 混编」。

- **命令行**

  ```shell
  kxapp project create -t app_objc -n MyApp -o D:\projects
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

### 3. 编码

打开 .m、.h 文件就有补全、跳转定义和错误提示，系统框架的 API 也能补全。提示异常时见[代码提示与索引](https://www.kxapp.com/zh/guides/ide-intellisense.html)。

### 4. 调试

[USB 连接 iPhone](https://www.kxapp.com/zh/guides/device-setup.html)，在 KXApp 视图中选中设备，按 [F5](https://www.kxapp.com/zh/guides/ide-debug.html) 编译、安装并停在断点上。Objective-C 和 Swift 代码都能设断点。

### 5. 发布

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
