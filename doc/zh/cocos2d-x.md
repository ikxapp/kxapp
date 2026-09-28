# Windows 上编译 cocos2d-x 游戏的 iOS 版

**简体中文** · [English](../en/cocos2d-x.md)

cocos2d-x 游戏在 Windows 上可以编译 iOS 版、安装到 iPhone 并断点调试 C++ 代码，不需要 Mac。3.x 和 4.x 都支持，引擎源码作为子工程一起编译，不用改引擎，也不用改工程设置。

## 步骤

### 1. 安装 cocos2d-x 并新建工程

已有工程在 VS Code 中「文件 → [打开文件夹](https://www.kxapp.com/zh/guides/projects.html#open)」打开工程根目录，或者把工程目录拖进 VS Code 即可。没有现成工程的，用下面的方式新建。按 cocos2d-x 官网的说明下载引擎和依赖，运行引擎目录里的 setup.py 配好 cocos 命令，然后新建工程，再在 VS Code 中打开。

```shell
cocos new MyGame -l cpp -p com.example.mygame -d .
```

### 2. 体检

**第一次打开工程必须先做这一步。**它会检查 cocos2d-x 环境，并准备好 iOS 端的工程。4.x 的 Xcode 工程也在这一步生成，放在 build-xcode 目录。

*以下两种做法任选其一*

- **VS Code 插件**

  [KXApp 视图](https://www.kxapp.com/zh/guides/ide-sidebar.html)标题栏「···」中运行「[体检并修复开发环境](https://www.kxapp.com/zh/guides/ide-setup.html#update)」。

- **命令行**

  ```shell
  kxapp doctor D:\work\MyGame
  ```

### 3. 编码

在工程根目录下写 C++ 代码，有[补全、跳转和错误提示](https://www.kxapp.com/zh/guides/ide-intellisense.html)。Lua、JS 脚本装上 VS Code 对应的插件即可。

### 4. 调试

[USB 连接 iPhone](https://www.kxapp.com/zh/guides/device-setup.html)，在 KXApp 视图中选中设备，按 [F5](https://www.kxapp.com/zh/guides/ide-debug.html)。C++ 代码在 VS Code 中断点调试，Lua、JS 脚本用引擎自带的调试方式，两边互不影响。

### 5. 发布

用 [Release 配置构建](https://www.kxapp.com/zh/guides/build.html#debug-release)，生成 .ipa。上传到 App Store Connect 见[发布与上架](https://www.kxapp.com/zh/guides/publish.html)。

*以下两种做法任选其一*

- **VS Code 插件**

  在 KXApp 视图的「构建配置」节点切到 Release，命令面板运行 **KXApp: 构建**。

- **命令行**

  按引擎版本执行其中一条。

  **3.x 工程**

  ```shell
  kxapp build .\proj.ios_mac\MyGame.xcodeproj -c Release -t MyGame-mobile
  ```

  **4.x 工程**

  ```shell
  kxapp build .\build-xcode\MyGame.xcodeproj -c Release -t MyGame
  ```
