# Windows 上本地打包 uni-app iOS App

**简体中文** · [English](../en/uni-app.md)

HBuilderX 的 uni-app 工程在 Windows 上可以本地打包 iOS 并真机调试，不经过云打包，不排队。uni-app 工程先导出成 Xcode 工程，之后按普通 iOS 工程编译、安装和调试。

## 步骤

### 1. 开发 uni-app 项目

在 HBuilderX 中照常新建和开发 uni-app 项目。再从 DCloud 的 [iOS 离线 SDK 下载页](https://nativesupport.dcloud.net.cn/AppDocs/download/ios.html)下载与 HBuilderX 同版本的 SDK 并解压，下一步导出时要用。**Vue 2 项目的 HBuilderX 不能装在带括号的目录**（例如 Program Files (x86)），否则页面编译失败。

### 2. 导出 Xcode 工程

把 uni-app 工程和 DCloud 离线 iOS SDK [导出成 Xcode 工程](https://www.kxapp.com/zh/guides/projects.html#uniapp)，manifest.json 里勾选的模块会用 [CocoaPods](cocoapods.md) 装好。完成后在 VS Code 中打开输出目录。

*以下两种做法任选其一*

- **VS Code 插件**

  命令面板运行 **KXApp: 导入 uni-app 项目**，依次选择 uni-app 工程目录、SDK 根目录和输出目录，填写 Bundle ID 和 DCloud App Key。

- **命令行**

  参数说明见 [uniapp2xcode 命令参考](https://www.kxapp.com/zh/guides/cli-uniapp2xcode.html)。

  ```shell
  uniapp2xcode --project D:\work\myuniapp --sdk D:\sdk\HBuilder-iOS-SDK --output D:\work\myuniapp-ios --bundle-id com.example.myapp --dcloud-appkey 你的AppKey --clean
  ```

### 3. 体检

检查并修好编译需要的环境。

*以下两种做法任选其一*

- **VS Code 插件**

  [KXApp 视图](https://www.kxapp.com/zh/guides/ide-sidebar.html)标题栏「···」中运行「[体检并修复开发环境](https://www.kxapp.com/zh/guides/ide-setup.html#update)」。

- **命令行**

  ```shell
  kxapp doctor .\myuniapp-ios\HBuilder-Hello\HBuilder-Hello.xcworkspace
  ```

### 4. 编码

页面代码照常在 HBuilderX 中编写，**改完要重新导出**才会进入 iOS 工程。应用名称、版本、图标、权限描述在 HBuilderX 的 manifest.json 里设置，额外的 Info.plist 项写进 uni-app 工程的 nativeResources/ios/Info.plist，每次导出都会应用。

### 5. 调试

[USB 连接 iPhone](https://www.kxapp.com/zh/guides/device-setup.html)，在 KXApp 视图中选中设备，按 [F5](https://www.kxapp.com/zh/guides/ide-debug.html)。原生层断点在 VS Code 中调试，页面 JS 用 HBuilderX 自带的调试工具，两边互不影响。

### 6. 发布

用 [Release 配置构建](https://www.kxapp.com/zh/guides/build.html#debug-release)，输出目录的 HBuilder-Hello\build 下生成以应用名称命名的 .ipa。上传到 App Store Connect 见[发布与上架](https://www.kxapp.com/zh/guides/publish.html)。

*以下两种做法任选其一*

- **VS Code 插件**

  在 KXApp 视图的「构建配置」节点切到 Release，命令面板运行 **KXApp: 构建**。

- **命令行**

  ```shell
  kxapp build .\myuniapp-ios\HBuilder-Hello\HBuilder-Hello.xcworkspace -s HBuilder -c Release
  ```

## 常见问题

| 现象 | 处理 |
|---|---|
| 导出时提示未登录、AppID 不存在，或 App 一打开就报 AppKey 错误 | AppID、AppKey、Bundle ID 是绑定的一套。HBuilderX 登录 DCloud 账号，在 manifest.json 的「基础配置」里获取 AppID，再到 dev.dcloud.net.cn 这个应用的 iOS 平台按 Bundle ID 申请离线打包 AppKey。导出时填的 Bundle ID 要和申请 AppKey 时一致，也要和 Apple 开发者后台的 App ID 一致 |
| 页面编译失败，提示 HBuilderX 安装目录不能包括 ( 等特殊字符 | Vue 2 项目的限制。把 HBuilderX 整个文件夹挪到 D:\HBuilderX 这样的目录，或者在 manifest.json 里改用 Vue 3 |
| App 启动后提示版本不匹配或白屏 | 离线 SDK 和 HBuilderX 版本不一致，下载同版本的 SDK 重新导出 |
| 导出结束时提示有模块被跳过 | 当前 SDK 里没有这个模块，或者它的库链接不了，例如 5.26 版 SDK 的实人认证。其他模块照常打包，被跳过的要等 DCloud 发布修复后的 SDK |
