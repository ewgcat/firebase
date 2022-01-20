## 背景

监控开发及线上代码报错信息
### 一、flutter集成

使用Firebase控制台添加项目
https://firebase.google.com

yaml

```
firebase_core: 1.10.0

firebase_crashlytics: 2.3.0

firebase_analytics: 8.3.4
```
在项目入口初始化

```
void main() {

runZonedGuarded(() async {

WidgetsFlutterBinding.*ensureInitialized*();

FirebaseApp firebaseApp = await Firebase.*initializeApp*();

var appId = firebaseApp.options.appId;

logger("Firebase_appId: $appId");

FlutterError.*onError* = FirebaseCrashlytics.*instance*.recordFlutterError;

_runApp();

}, (error, stack) {

FirebaseCrashlytics.*instance*.recordError(error, stack);

logger(error);

logger(stack);

});

}
```
### 二、安卓原生集成
#### 1.注册应用
![image.png](https://upload-images.jianshu.io/upload_images/8069591-38819ed9612909e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 2.下载配置文件
![image.png](https://upload-images.jianshu.io/upload_images/8069591-7b216f4018c6704c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

为不同编译环境设置不同的配置文件，如下图所示，根据项目都buildTypes存放不同的配置文件（需要执行flutter clean命令，不然会有缓存）
![image.png](https://upload-images.jianshu.io/upload_images/8069591-304ebee9f33d0f14.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 3.设置sdk

-   项目根目录下build.gradle配置如下：

![image.png](https://upload-images.jianshu.io/upload_images/8069591-eb5f976a25ab9872.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

-   app目录下build.gradle配置如下：

![image.png](https://upload-images.jianshu.io/upload_images/8069591-1215e1f59dd18eb5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/8069591-4874134d24bc1e3e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 三、iOS原生集成
#### 1.注册应用
![image](https://upload-images.jianshu.io/upload_images/8069591-e0942d85eeb073d3.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 2.下载配置文件
![image.png](https://upload-images.jianshu.io/upload_images/8069591-406f0ee2344bc7e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 3.入口调用
![image](https://upload-images.jianshu.io/upload_images/8069591-f902327eb52273e7.image?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
为不同编译环境设置不同的配置文件，如下图所示,生成不同id的配置文件

![image.png](https://upload-images.jianshu.io/upload_images/8069591-d193ba19d2b6d067.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/8069591-bf9fa96387b591f2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

脚本如下

```
# Name of the resource we're selectively copying                        
  GOOGLESERVICE_INFO_PLIST=GoogleService-Info.plist                     
                        
  # Get references to dev and prod versions of the GoogleService-Info.plist                     
  # NOTE: These should only live on the file system and should NOT be part of the target (since we'll be adding them to the target manually)                      
  GOOGLESERVICE_INFO_DEV=${PROJECT_DIR}/${TARGET_NAME}/Firebase/Dev/${GOOGLESERVICE_INFO_PLIST}                     
  GOOGLESERVICE_INFO_PROD=${PROJECT_DIR}/${TARGET_NAME}/Firebase/Prod/${GOOGLESERVICE_INFO_PLIST}                     
                        
  # Make sure the dev version of GoogleService-Info.plist exists                      
  echo "Looking for ${GOOGLESERVICE_INFO_PLIST} in ${GOOGLESERVICE_INFO_DEV}"                     
  if [ ! -f $GOOGLESERVICE_INFO_DEV ]                     
  then                      
  echo "No Development GoogleService-Info.plist found. Please ensure it's in the proper directory."                     
  exit1                     
  fi                      
                        
  # Make sure the prod version of GoogleService-Info.plist exists                     
  echo "Looking for ${GOOGLESERVICE_INFO_PLIST} in ${GOOGLESERVICE_INFO_PROD}"                      
  if [ ! -f $GOOGLESERVICE_INFO_PROD ]                      
  then                      
  echo "No Production GoogleService-Info.plist found. Please ensure it's in the proper directory."                      
  exit1                     
  fi                      
                        
  # Get a reference to the destination location for the GoogleService-Info.plist                      
  PLIST_DESTINATION=${BUILT_PRODUCTS_DIR}/${PRODUCT_NAME}.app                     
  echo "Will copy ${GOOGLESERVICE_INFO_PLIST} to final destination: ${PLIST_DESTINATION}"                     
                        
  # Copy over the prod GoogleService-Info.plist for Release builds                      
  if [ "${CONFIGURATION}" == "Release" ]                      
  then                      
  echo "Using ${GOOGLESERVICE_INFO_PROD}"                     
  cp "${GOOGLESERVICE_INFO_PROD}" "${PLIST_DESTINATION}"                      
  else                      
  echo "Using ${GOOGLESERVICE_INFO_DEV}"                      
  cp "${GOOGLESERVICE_INFO_DEV}" "${PLIST_DESTINATION}"                     
  fi                      
```
验证不同编译条件下,是否正常加载配置文件,显示包内容,查看配置文件

![image.png](https://upload-images.jianshu.io/upload_images/8069591-98a3411fb339eb3d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
