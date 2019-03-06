# Android 开发环境

## 初始化项目

默认情况下 `weex create` 命令并不初始化 iOS 和 Android 项目，你可以通过执行 `weex platform add` 来添加特定平台的项目。

```bash
weex platform add android
```

## 安装安卓开发环境

### Java 环境

Oracle 官网下载：

{% embed url="https://www.oracle.com/technetwork/java/javase/downloads/index.html" %}

或

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

