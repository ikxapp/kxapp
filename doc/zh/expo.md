# Windows 上本地构建 Expo iOS App

**简体中文** · [English](../en/expo.md)

Expo 工程在 Windows 上可以本地构建 iOS 端并真机调试，不需要 Mac，也不经过 EAS Build。没有 ios/ 目录的工程，体检时会自动生成。JS 部分照常运行 Metro，原生代码可以断点调试。

## 步骤

### 1. 安装 Expo 开发环境

按 Expo 官网的说明安装 Node.js，新开一个终端能看到版本号即可。

```shell
node --version
```

### 2. 新建

已有工程在 VS Code 中「文件 → [打开文件夹](https://www.kxapp.com/zh/guides/projects.html#open)」打开工程根目录，或者把工程目录拖进 VS Code 即可。没有现成工程的，用下面的方式新建。

*以下两种做法任选其一*

- **VS Code 插件**

  命令面板运行 **KXApp: 新建项目**，[模板](https://www.kxapp.com/zh/guides/templates.html)选「Expo 应用」。

- **命令行**

  父目录用短路径，依赖目录很深。

  ```shell
  kxapp project create -t expo_app -n expohello -o D:\work
  ```

### 3. 体检

**第一次打开工程必须先做这一步。**它会检查 Expo 环境，并生成、准备好 iOS 端的工程。

*以下两种做法任选其一*

- **VS Code 插件**

  [KXApp 视图](https://www.kxapp.com/zh/guides/ide-sidebar.html)标题栏「···」中运行「[体检并修复开发环境](https://www.kxapp.com/zh/guides/ide-setup.html#update)」。

- **命令行**

  ```shell
  kxapp doctor D:\work\expohello
  ```

体检之后在 ios 目录安装原生依赖，见 [CocoaPods](cocoapods.md)。

```shell
cd ios
pod install
```

### 4. 编码

JS 和 TypeScript 照常在 VS Code 中编写，保存后 Metro 自动刷新。ios/ 下的原生代码由快蝎提供[补全和跳转](https://www.kxapp.com/zh/guides/ide-intellisense.html)。

### 5. 调试

另开一个终端在工程目录运行 npx expo start，然后选中设备按 [F5](https://www.kxapp.com/zh/guides/ide-debug.html)。原生断点在 VS Code 中调试，JS 断点用 Metro / Hermes 自己的调试器，两边互不影响。

### 6. 发布

用 [Release 配置构建](https://www.kxapp.com/zh/guides/build.html#debug-release)，JS 会打包进 App，ios 目录下生成 .ipa。上传到 App Store Connect 见[发布与上架](https://www.kxapp.com/zh/guides/publish.html)。

*以下两种做法任选其一*

- **VS Code 插件**

  在 KXApp 视图的「构建配置」节点切到 Release，命令面板运行 **KXApp: 构建**。

- **命令行**

  ```shell
  kxapp build .\ios\expohello.xcworkspace -c Release
  ```
