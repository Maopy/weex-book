# Android 开发环境

## 初始化项目

首先，根据[官方文档](https://weex.apache.org/zh/guide/develop/setup-develop-environment.html)上的步骤安装脚手架等工具：

默认情况下 `weex create` 命令并不初始化 iOS 和 Android 项目，可以通过执行 `weex platform add` 来添加特定平台的项目。

```bash
weex platform add android
```

## 安装安卓开发环境

### Java 环境

Oracle 官网下载：

{% embed url="https://www.oracle.com/technetwork/java/javase/downloads/index.html" %}

或，通过 homebrew 安装（推荐）：

```bash
brew cask install java
```

### Android Studio

官网下载：

{% embed url="https://developer.android.com/studio" %}

## 运行 APP

当开发环境准备就绪后，运行下面的命令，可以在模拟器或真实设备上启动应用：

```bash
weex run android
```

### 果然报错了

```bash
xcrun: error: unable to find utility "instruments", not a developer tool or in PATH
[✔︎] Compile JSBundle done
? Select one of the device equuleus
[✔︎] Start hotreload server done
[✔︎] Set native config done
[✔︎] Copy JS source done
[✔︎] Watch JS source done
⠦ Building APP - this may take a few seconds
Error: Command failed: ./gradlew clean assembleDebug

FAILURE: Build failed with an exception.

* What went wrong:
Could not determine java version from '11.0.2'.

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output.

    at ChildProcess.exithandler (child_process.js:297:12)
    at ChildProcess.emit (events.js:197:13)
    at maybeClose (internal/child_process.js:984:16)
    at Socket.stream.socket.on (internal/child_process.js:401:11)
    at Socket.emit (events.js:197:13)
⠏ Building APP - this may take a few seconds
^C%
```

#### 原因

weex 生成的项目默认的 gradle 版本是 2.14，与 JDK 11+ 版本不兼容。

#### 解决方法

升级 gradle 或 降级 JDK。由于项目 gradle 版本一般不会轻易修改。故采用降级 JDK 至 8+ 版本解决。

得到老版本的 Java：

```bash
brew tap caskroom/versions
```

然后安装 JDK 8+：

```bash
brew cask install java8
```

### 第二个报错

```bash
xcrun: error: unable to find utility "instruments", not a developer tool or in PATH
[✔︎] Compile JSBundle done
? Select one of the device equuleus
[✔︎] Start hotreload server done
[✔︎] Set native config done
[✔︎] Copy JS source done
[✔︎] Watch JS source done
⠇ Error: Command failed: ./gradlew clean assembleDebug
isLibProject: false, isAppProject: true
weex_plugin: []

FAILURE: Build failed with an exception.

* What went wrong:
A problem occurred configuring project ':app'.
> You have not accepted the license agreements of the following SDK components:
  [Android SDK Platform 26, Android SDK Build-Tools 26].
  Before building your project, you need to accept the license agreements and complete the installation of the missing components using the Android Studio SDK Manager.
  Alternatively, to learn how to transfer the license agreements from one workstation to another, go to http://d.android.com/r/studio-ui/export-licenses.html

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output.

    at ChildProcess.exithandler (child_process.js:297:12)
    at ChildProcess.emit (events.js:197:13)
    at maybeClose (internal/child_process.js:984:16)
    at Socket.stream.socket.on (internal/child_process.js:401:11)
    at Socket.emit (events.js:197:13)
    at Pipe._handle.close (net.js:611:12)
⠦ ^C%
```

如报错内容所说，我们缺少了 Android SDK Platform 26 和 Android SDK Build-Tools 26（这东西具体是啥还有待学习）。

打开 Android Studio，打开 path/to/platforms/andriod 项目目录，build 工具会自动提示安装缺失的内容。

### 一个小问题

```bash
xcrun: error: unable to find utility "instruments", not a developer tool or in PATH
[✔︎] Compile JSBundle done
? Select one of the device equuleus
[✔︎] Start hotreload server done
[✔︎] Set native config done
[✔︎] Copy JS source done
[✔︎] Watch JS source done
[✔︎] Build APP done
⠧ Lanuching APP - this may take a few secondsError: Command failed: /Users/maopy/Library/Android/sdk/platform-tools/adb -s c8ef737f install -r /Users/maopy/www/test/awesome-project/platforms/android/app/build/outputs/apk/weex-app.apk
adb: failed to install /Users/maopy/www/test/awesome-project/platforms/android/app/build/outputs/apk/weex-app.apk: Failure [INSTALL_FAILED_USER_RESTRICTED: Install canceled by user]

    at ChildProcess.exithandler (child_process.js:297:12)
    at ChildProcess.emit (events.js:197:13)
    at maybeClose (internal/child_process.js:984:16)
    at Process.ChildProcess._handle.onexit (internal/child_process.js:265:5)
⠋ Lanuching APP - this may take a few seconds^C%
```

报错原因：没有成功在手机上安装 Weex App。

在“开发者选项”中，打开“USB 安装”，即可解决。

### 成功了

```bash
xcrun: error: unable to find utility "instruments", not a developer tool or in PATH
[✔︎] Compile JSBundle done
? Select one of the device equuleus
[✔︎] Start hotreload server done
[✔︎] Set native config done
[✔︎] Copy JS source done
[✔︎] Watch JS source done
[✔︎] Build APP done
[✔︎] Launch APP done
Hotreload server is actived, enjoy your develop
Type Ctrl+C to exist
^C%
```

Have fun!

