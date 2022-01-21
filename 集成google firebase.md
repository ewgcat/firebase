[firebase](https://firebase.google.com/)

### 安卓原生集成
#### 1.注册应用

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1fab0bbf27384152a0f3f07c411bb41a~tplv-k3u1fbpfcp-watermark.image?)
#### 2.下载配置文件

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/08ad9f79386a4586b56a278119679952~tplv-k3u1fbpfcp-watermark.image?)

#### 3.添加 Firebase SDK
项目级 build.gradle（`<项目>/build.gradle`）：

```
buildscript {
  repositories {
    // Check that you have the following line (if not, add it):
    google()  // Google's Maven repository
  }
  dependencies {
    ...
    // Add this line
    classpath 'com.google.gms:google-services:4.3.10'
  }
}

allprojects {
  ...
  repositories {
    // Check that you have the following line (if not, add it):
    google()  // Google's Maven repository
    ...
  }
}
```
应用级 build.gradle（`<项目>/<应用模块>/build.gradle`）：

```
apply plugin: 'com.android.application'

// Add this line
apply plugin: 'com.google.gms.google-services'

dependencies {
  // Import the Firebase BoM
  implementation platform('com.google.firebase:firebase-bom:29.0.4')
  // Add the dependency for the Firebase SDK for Google Analytics
  // When using the BoM, don't specify versions in Firebase dependencies
  implementation 'com.google.firebase:firebase-analytics-ktx'

  // Add the dependencies for any other desired Firebase products
  // https://firebase.google.com/docs/android/setup#available-libraries
}
```

### IOS原生集成
#### 1.注册应用
![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d5c30c0e1eb041f88d2ff564f99d9b9e~tplv-k3u1fbpfcp-watermark.image?)
#### 2.下载配置文件
![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/64bf6dd627874eb4ba690a0c55838c1a~tplv-k3u1fbpfcp-watermark.image?)
#### 3.添加 Firebase SDK
![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e9d2d4e9306b41ae84e7888ce625ea24~tplv-k3u1fbpfcp-watermark.image?)
#### 4.添加初始化代码
要在您的应用启动时连接 Firebase，请将下面的初始化代码添加到您的主 **`AppDelegate`** 类。

```
@import UIKit;
@import Firebase;

@implementation AppDelegate
- (BOOL)application:(UIApplication *)application
    didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [FIRApp configure]
  return YES;
}
```
