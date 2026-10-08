# Windows 上编译 Kotlin Multiplatform iOS App

**简体中文** · [English](../en/kotlin-multiplatform.md)

Kotlin Multiplatform 工程在 Windows 上可以编译 iOS App、安装到 iPhone 并调试。iosApp 工程和 Gradle 构建脚本都不用改，Compose Multiplatform 同样支持。Swift 和 Kotlin 代码都能设断点，从 Swift 可以单步进入 Kotlin。

## 步骤

### 1. 安装开发环境

按 Kotlin Multiplatform 官网的说明安装 Android Studio，并在插件市场装上 Kotlin Multiplatform 插件。

### 2. 新建

已有工程在 VS Code 中「文件 → [打开文件夹](https://www.kxapp.com/zh/guides/projects.html#open)」打开工程根目录，或者把工程目录拖进 VS Code 即可。没有现成工程的，用 Android Studio 或 JetBrains 的 Kotlin Multiplatform 向导新建，勾选 iOS 目标，再在 VS Code 中打开。

### 3. 体检

**第一次打开工程必须先做这一步。**它会检查 Kotlin Multiplatform 环境，并准备好 iOS 端的工程。第一次运行要下载几百 MB，时间较长。升级 Kotlin 版本后再运行一次。

*以下两种做法任选其一*

- **VS Code 插件**

  [KXApp 视图](https://www.kxapp.com/zh/guides/ide-sidebar.html)标题栏「···」中运行「[体检并修复开发环境](https://www.kxapp.com/zh/guides/ide-setup.html#update)」。

- **命令行**

  ```shell
  kxapp doctor D:\work\mykmpapp\iosApp\iosApp.xcodeproj
  ```

### 4. 编码

iosApp 里的 Swift 代码在 VS Code 中有[补全、跳转和错误提示](https://www.kxapp.com/zh/guides/ide-intellisense.html)。共享的 Kotlin 代码照常用 Android Studio 或 IntelliJ IDEA 编写。

### 5. 调试

[USB 连接 iPhone](https://www.kxapp.com/zh/guides/device-setup.html)，在 KXApp 视图中选中设备，按 [F5](https://www.kxapp.com/zh/guides/ide-debug.html)。Swift 和 Kotlin 代码都能设断点、单步、看变量，Kotlin 对象按类和字段展开。

### 6. 发布

用 [Release 配置构建](https://www.kxapp.com/zh/guides/build.html#debug-release)，iosApp 目录下生成 .ipa。上传到 App Store Connect 见[发布与上架](https://www.kxapp.com/zh/guides/publish.html)。

*以下两种做法任选其一*

- **VS Code 插件**

  在 KXApp 视图的「构建配置」节点切到 Release，命令面板运行 **KXApp: 构建**。

- **命令行**

  ```shell
  kxapp build .\iosApp\iosApp.xcodeproj -c Release
  ```
