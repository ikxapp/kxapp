# Windows 上开发使用 CocoaPods 的 iOS App

**简体中文** · [English](../en/cocoapods.md)

使用 CocoaPods 的 iOS 工程在 Windows 上照常用 pod 命令管理依赖，编译、安装到 iPhone 和断点调试都不需要 Mac。CocoaPods 随快蝎一起安装，终端里直接就能运行 pod。Podfile 和工程文件都不需要改造，Swift、Objective-C 工程都一样。

## 步骤

### 1. 体检

检查 CocoaPods 环境，没装的会装好。

*以下两种做法任选其一*

- **VS Code 插件**

  [KXApp 视图](https://www.kxapp.com/zh/guides/ide-sidebar.html)标题栏「···」中运行「[体检并修复开发环境](https://www.kxapp.com/zh/guides/ide-setup.html#update)」。

- **命令行**

  ```shell
  kxapp doctor
  ```

完成后新开一个终端，能看到版本号就可以了。

```shell
pod --version
```

### 2. 新建

新工程可以直接用带 Podfile 的模板，创建后自动执行 pod install，然后跳到第 4 步。

*以下两种做法任选其一*

- **VS Code 插件**

  命令面板运行 **KXApp: 新建项目**，[模板](https://www.kxapp.com/zh/guides/templates.html)选「iOS 应用（Swift · CocoaPods）」。

- **命令行**

  ```shell
  kxapp project create -t app_swift_cocoapods -n MyApp -o D:\projects
  ```

已有工程还没有 Podfile 的，在 .xcodeproj 所在目录生成一个。已经有 Podfile 的直接进入下一步。

```shell
pod init
```

### 3. 添加依赖

在 Podfile 里给 target 写上要用的库，版本写法见文末附录。

```shell
platform :ios, '15.0'
use_frameworks!

target 'MyApp' do
  pod 'Alamofire', '~> 5.9'
  pod 'SDWebImage'
end
```

然后在 Podfile 所在目录安装。它会下载依赖，生成 Pods 目录、Podfile.lock 和 **MyApp.xcworkspace**。

```shell
pod install
```

**从这以后编译和调试都用 .xcworkspace**，用 .xcodeproj 会找不到 Pods 里的库。每次修改 Podfile 后都要重新运行 pod install。Podfile.lock 要提交到版本库，团队里每个人装到的版本才一致。

### 4. 编码

VS Code 中「文件 → [打开文件夹](https://www.kxapp.com/zh/guides/projects.html#open)」打开 Podfile 所在目录，KXApp 视图里的[启动项目](https://www.kxapp.com/zh/guides/ide-sidebar.html#startup)选 .xcworkspace。源文件有补全、跳转定义和错误提示，Pods 里的库构建一次后也能补全和跳转。提示异常时见[代码提示与索引](https://www.kxapp.com/zh/guides/ide-intellisense.html)。

### 5. 调试

[USB 连接 iPhone](https://www.kxapp.com/zh/guides/device-setup.html)，在 KXApp 视图中选中设备，按 [F5](https://www.kxapp.com/zh/guides/ide-debug.html) 编译、安装并停在断点上。自己的代码和 Pods 里带源码的库都能设断点。

### 6. 发布

用 [Release 配置构建](https://www.kxapp.com/zh/guides/build.html#debug-release)，工程目录下生成 build\MyApp.ipa。上传到 App Store Connect 见[发布与上架](https://www.kxapp.com/zh/guides/publish.html)。

*以下两种做法任选其一*

- **VS Code 插件**

  在 KXApp 视图的「构建配置」节点切到 Release，命令面板运行 **KXApp: 构建**。

- **命令行**

  构建 pod install 生成的工作区。

  ```shell
  kxapp build .\MyApp.xcworkspace -c Release
  ```

## 更新依赖

pod install 只按 Podfile.lock 里记下的版本安装，不会升级已有的库。要升级时先看哪些库有新版本，再更新全部或指定的库。

```shell
pod outdated
```

```shell
pod update Alamofire
```

不带库名的 pod update 会在 Podfile 允许的范围内升级全部库。刚发布的新版本找不到时，加 --repo-update 先更新本地索引。

## 常见问题

| 现象 | 处理 |
|---|---|
| 编译报找不到 Pods 里的头文件或模块 | 构建的是 .xcodeproj，改成 .xcworkspace。刚改过 Podfile 的先运行 pod install |
| 提示 The sandbox is not in sync with the Podfile.lock | 拉取代码后 Podfile.lock 变了，运行 pod install |
| pod install 下载很慢或失败 | 在 Podfile 第一行指定国内镜像源，例如 `source 'https://mirrors.tuna.tsinghua.edu.cn/git/CocoaPods/Specs.git'` |
| 依赖装乱了想从头来 | 删掉 Pods 目录后重新 pod install，还不行再运行 pod cache clean --all 清缓存 |
| 提示找不到 pod 命令 | 先运行体检，完成后新开一个终端 |

## 附录 常用 pod 命令与版本写法

| 命令 | 作用 |
|---|---|
| `pod init` | 为当前目录的工程生成 Podfile |
| `pod install` | 按 Podfile 和 Podfile.lock 安装依赖，生成 .xcworkspace |
| `pod update [库名]` | 升级全部或指定的库，并更新 Podfile.lock |
| `pod outdated` | 列出有新版本的库 |
| `pod repo update` | 更新本地的库索引 |
| `pod search 关键字` | 搜索可用的库 |
| `pod cache clean --all` | 清空下载缓存 |
| `pod deintegrate` | 从工程中移除 CocoaPods |

| Podfile 写法 | 含义 |
|---|---|
| `pod 'Alamofire'` | 最新版本 |
| `pod 'Alamofire', '5.9.1'` | 固定这一个版本 |
| `pod 'Alamofire', '~> 5.9'` | 5.9 及以上、6.0 以下 |
| `pod 'Alamofire', '>= 5.0'` | 5.0 及以上 |
| `pod 'MyKit', :path => '../MyKit'` | 本地目录中的库 |
| `pod 'MyKit', :git => 'https://…/MyKit.git', :tag => '1.0.0'` | Git 仓库中的某个版本 |
