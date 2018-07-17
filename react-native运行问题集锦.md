# react-native运行问题集锦

使用"android": "node node_modules/react-native/local-cli/cli.js run-android",运行时
进度条读取到一半，node弹框自动消失，这个时候无论如何项目都不会成功跑起，最后会红屏显示
```
unable to load script from assets 'index.android.bundle'.
Make sure your bundle ispackged correctly or you are running a packger server.
```

解决方法是进入\android\app\src\main
删除assets文件夹

运行`react-native run-android`即可

如果还是报错

运行`cd android && gradlew clean && cd .. && react-native run-android`

## Could not expand ZIP

Execution failed for task ':app:prepareComAndroidSupportSupportCompat2531Library'.
> Could not expand ZIP 'D:\SDK\extras\android\m2repository\com\android\support\support-compat\25.3.1\support-compat-25.3.1.aar'.

运行`cd android && gradlew clean && cd .. && react-native run-android`

## Failed to resolve: com.android.support:appcompat-v7:26.0.1

修改android project的gradle，添加maven { url 'https://maven.google.com' }

D:\gitHub\jianguanrn\android\build.gradle
```
allprojects {
    repositories {
        mavenLocal()
        jcenter {
            url 'http://jcenter.bintray.com'
        }
        maven { url 'https://jitpack.io' }
        maven { url 'https://maven.google.com' }
        maven {
            // All of React Native (JS, Obj-C sources, Android binaries) is installed from npm
            url "$rootDir/../node_modules/react-native/android"
        }
    }
}
```
同时在android sdk中的SDK Tools 中 Android Support Repository更新到最新版本

最后运行`react-native run-android`

## 

