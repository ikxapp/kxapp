# Windows 上使用 Unity 开发编译发布 iOS 游戏

**简体中文** · [English](../en/unity.md)

Unity 导出的 iOS 工程在 Windows 上可以编译、安装到 iPhone 并调试原生层。Unity 中照常导出，导出目录按普通 Xcode 工程使用，不需要安装 Unity 插件，也不用改 Unity 项目设置。

## 步骤

### 1. 开发 Unity 项目并导出 Xcode 工程

在 Unity 中照常开发项目。装好 iOS Build Support 模块后，Build Settings 切换到 iOS，Build 到一个目录，然后在 VS Code 中「文件 → [打开文件夹](https://www.kxapp.com/zh/guides/projects.html#open)」打开这个目录。

### 2. 体检

检查并修好编译需要的环境。用了 Firebase、Google Mobile Ads 等带 iOS 依赖的插件时，导出目录里会有 Podfile，之后在导出目录执行 pod install，见 [CocoaPods](cocoapods.md)。

*以下两种做法任选其一*

- **VS Code 插件**

  [KXApp 视图](https://www.kxapp.com/zh/guides/ide-sidebar.html)标题栏「···」中运行「[体检并修复开发环境](https://www.kxapp.com/zh/guides/ide-setup.html#update)」。

- **命令行**

  ```shell
  kxapp doctor .\Unity-iPhone.xcodeproj
  ```

### 3. 编码

C# 脚本照常在 Unity 中编写，改完重新导出。导出目录里的 Objective-C 插件代码在 VS Code 中有[补全和跳转](https://www.kxapp.com/zh/guides/ide-intellisense.html)。

### 4. 调试

[USB 连接 iPhone](https://www.kxapp.com/zh/guides/device-setup.html)，在 KXApp 视图中选中设备，按 [F5](https://www.kxapp.com/zh/guides/ide-debug.html)。原生代码在 VS Code 中断点调试，C# 脚本用 Unity 自己的调试器，两边互不影响。

### 5. 发布

用 [Release 配置构建](https://www.kxapp.com/zh/guides/build.html#debug-release)，导出目录下生成 .ipa。上传到 App Store Connect 见[发布与上架](https://www.kxapp.com/zh/guides/publish.html)。

*以下两种做法任选其一*

- **VS Code 插件**

  在 KXApp 视图的「构建配置」节点切到 Release，命令面板运行 **KXApp: 构建**。

- **命令行**

  target 固定为 Unity-iPhone，按导出目录的情况执行其中一条。

  **没有 Podfile**

  ```shell
  kxapp build .\Unity-iPhone.xcodeproj -c Release -t Unity-iPhone
  ```

  **有 Podfile，已执行 pod install**

  ```shell
  kxapp build .\Unity-iPhone.xcworkspace -c Release -t Unity-iPhone
  ```
