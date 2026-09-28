# Windows 上构建 Flutter iOS App 并真机调试

**简体中文** · [English](../en/flutter.md)

Flutter 工程在 Windows 上可以构建 iOS 端并真机调试，不需要 Mac。原生断点和 Dart 断点同时可用，热重载照常。iOS 端的构建和运行用快蝎代替 flutter build ios 和 flutter run，其他 flutter 命令照常使用。

## 步骤

### 1. 安装 Flutter 与 VS Code 扩展

按 Flutter 官网的说明安装 Flutter SDK，把 flutter 命令加入 PATH，新开一个终端能看到版本号即可。VS Code 扩展市场安装 Flutter 扩展，Dart 扩展会一起装上。

```shell
flutter --version
```

### 2. 新建

已有工程在 VS Code 中「文件 → [打开文件夹](https://www.kxapp.com/zh/guides/projects.html#open)」打开 Flutter 工程根目录，或者把工程目录拖进 VS Code 即可。没有现成工程的，用 flutter create 或下面的方式新建。

*以下两种做法任选其一*

- **VS Code 插件**

  命令面板运行 **KXApp: 新建项目**，[模板](https://www.kxapp.com/zh/guides/templates.html)选「Flutter 应用」。

- **命令行**

  ```shell
  kxapp project create -t flutter_app -n myflutterapp -o D:\work
  ```

### 3. 体检

**第一次打开工程必须先做这一步。**它会检查 Flutter 环境，并准备好 iOS 端的工程。

*以下两种做法任选其一*

- **VS Code 插件**

  [KXApp 视图](https://www.kxapp.com/zh/guides/ide-sidebar.html)标题栏「···」中运行「[体检并修复开发环境](https://www.kxapp.com/zh/guides/ide-setup.html#update)」。

- **命令行**

  ```shell
  kxapp doctor D:\work\myflutterapp
  ```

工程里有需要 CocoaPods 的插件时，体检之后再在 ios 目录安装依赖，见 [CocoaPods](cocoapods.md)。没有这类插件的跳过。

```shell
cd ios
pod install
```

### 4. 编码

Dart 代码的[补全、跳转和错误提示](https://www.kxapp.com/zh/guides/ide-intellisense.html#who)由 Flutter 扩展提供，ios/ 下的 Swift、Objective-C 代码由快蝎提供。

### 5. 调试

[USB 连接 iPhone](https://www.kxapp.com/zh/guides/device-setup.html)，在 KXApp 视图中选中设备，按 [F5](https://www.kxapp.com/zh/guides/ide-debug.html)。先命中原生断点，App 启动后自动接上 Dart 调试，Dart 断点和热重载都能用。

### 6. 发布

用 [Release 配置构建](https://www.kxapp.com/zh/guides/build.html#debug-release)，ios 目录下生成 build\Runner.ipa。上传到 App Store Connect 见[发布与上架](https://www.kxapp.com/zh/guides/publish.html)。

*以下两种做法任选其一*

- **VS Code 插件**

  在 KXApp 视图的「构建配置」节点切到 Release，命令面板运行 **KXApp: 构建**。

- **命令行**

  ```shell
  kxapp build .\ios\Runner.xcworkspace -c Release
  ```
