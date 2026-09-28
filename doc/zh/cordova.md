# Windows 上打包 Cordova iOS App

**简体中文** · [English](../en/cordova.md)

Cordova 工程在 Windows 上可以打包 iOS 并真机调试，不需要 Mac。cordova platform add ios 生成的 platforms/ios 按普通 Xcode 工程编译，cordova 命令和插件照常使用。

## 步骤

### 1. 创建 Cordova 工程并添加 iOS 平台

已有工程直接在工程目录添加 iOS 平台，之后在 VS Code 中「文件 → [打开文件夹](https://www.kxapp.com/zh/guides/projects.html#open)」打开 platforms/ios 目录，或者把整个 Cordova 工程拖进 VS Code 即可。没有现成工程的，用下面的方式新建。用 npm 安装 Cordova，创建工程，再进入工程目录添加 iOS 平台，Xcode 工程生成在 platforms/ios 下。

```shell
npm install -g cordova
```

```shell
cordova create MyApp com.example.myapp MyApp
```

```shell
cd MyApp
```

```shell
cordova platform add ios
```

### 2. 体检

它会检查编译需要的环境，并准备好 iOS 端的工程。

*以下两种做法任选其一*

- **VS Code 插件**

  [KXApp 视图](https://www.kxapp.com/zh/guides/ide-sidebar.html)标题栏「···」中运行「[体检并修复开发环境](https://www.kxapp.com/zh/guides/ide-setup.html#update)」。

- **命令行**

  ```shell
  kxapp doctor .\platforms\ios\App.xcworkspace
  ```

工程默认用 Swift Package 管理依赖，不需要 CocoaPods。**添加的插件带 CocoaPods 依赖时，platforms/ios 下会出现 Podfile**，Windows 上 Cordova 不会自动安装，要在 platforms/ios 目录执行一次 pod install，之后每次增删这类插件都要重新执行，见 [CocoaPods](cocoapods.md)。

```shell
cd platforms\ios
pod install
```

### 3. 编码

网页代码照常在 www/ 下编写，改完执行 cordova prepare ios 同步到 iOS 工程。原生插件代码在 VS Code 中有[补全和跳转](https://www.kxapp.com/zh/guides/ide-intellisense.html)。

### 4. 调试

[USB 连接 iPhone](https://www.kxapp.com/zh/guides/device-setup.html)，在 KXApp 视图中选中设备，按 [F5](https://www.kxapp.com/zh/guides/ide-debug.html)。原生代码在 VS Code 中断点调试，网页部分用浏览器的远程调试工具，两边互不影响。

### 5. 发布

用 [Release 配置构建](https://www.kxapp.com/zh/guides/build.html#debug-release)，platforms/ios 下生成 .ipa。上传到 App Store Connect 见[发布与上架](https://www.kxapp.com/zh/guides/publish.html)。

*以下两种做法任选其一*

- **VS Code 插件**

  在 KXApp 视图的「构建配置」节点切到 Release，命令面板运行 **KXApp: 构建**。

- **命令行**

  ```shell
  kxapp build .\platforms\ios\App.xcworkspace -c Release
  ```
