# 在Windows 上用 Godot 开发编译iOS应用和游戏

**简体中文** · [English](../en/godot.md)

Godot 导出的 iOS 工程在 Windows 上可以编译、安装到 iPhone 并调试原生层，不需要 Mac。Godot 中照常导出，导出目录按普通 Xcode 工程使用，不用改 Godot 项目设置。

## 步骤

### 1. 开发 Godot 项目并导出 Xcode 工程

在 Godot 中照常开发项目。「编辑器 → 管理导出模板」下载好导出模板，「项目 → 导出」添加 iOS 预设，填上 App Store Team ID 和 Bundle Identifier，导出到 Godot 项目以外的一个空目录，文件名如 MyGame.ipa。Windows 上 Godot 只生成 Xcode 工程 MyGame.xcodeproj，不生成 ipa。然后在 VS Code 中「文件 → [打开文件夹](https://www.kxapp.com/zh/guides/projects.html#open)」打开这个目录。

### 2. 体检

检查并修好编译需要的环境。

*以下两种做法任选其一*

- **VS Code 插件**

  [KXApp 视图](https://www.kxapp.com/zh/guides/ide-sidebar.html)标题栏「···」中运行「[体检并修复开发环境](https://www.kxapp.com/zh/guides/ide-setup.html#update)」。

- **命令行**

  ```shell
  kxapp doctor .\MyGame.xcodeproj
  ```

### 3. 编码

GDScript 和场景照常在 Godot 中编辑，改完重新导出到同一个目录。导出目录里的原生代码在 VS Code 中有[补全和跳转](https://www.kxapp.com/zh/guides/ide-intellisense.html)。

### 4. 调试

[USB 连接 iPhone](https://www.kxapp.com/zh/guides/device-setup.html)，在 KXApp 视图中选中设备，按 [F5](https://www.kxapp.com/zh/guides/ide-debug.html)。原生代码在 VS Code 中断点调试，GDScript 用 Godot 自己的调试器，两边互不影响。

### 5. 发布

用 [Release 配置构建](https://www.kxapp.com/zh/guides/build.html#debug-release)，导出目录下生成 .ipa。上传到 App Store Connect 见[发布与上架](https://www.kxapp.com/zh/guides/publish.html)。

*以下两种做法任选其一*

- **VS Code 插件**

  在 KXApp 视图的「构建配置」节点切到 Release，命令面板运行 **KXApp: 构建**。

- **命令行**

  ```shell
  kxapp build .\MyGame.xcodeproj -c Release
  ```
