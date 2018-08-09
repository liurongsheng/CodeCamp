# react-native运行问题集锦

## 用react-native-cli 初始化项目，运行后提示 Unable to resolve module `AccessibilityInfo`
 
由于新版react-native-cli中的react和react native 版本不匹配 可以选用react-native-cli@1.2.0

```
"dependencies": {
    "react": "^16.4.1",
    "react-native": "^0.55.4"
},
"devDependencies": {
    "babel-preset-react-native": "^4.0.0",
}, 
```
```
npm update
npm cache clean --force
cd android && gradlew clean && cd .. && react-native run-android
```


## 使用"android": "node node_modules/react-native/local-cli/cli.js run-android"
运行时进度条读取到一半，node弹框自动消失，这个时候无论如何项目都不会成功跑起，最后会红屏显示
```
unable to load script from assets 'index.android.bundle'.
Make sure your bundle ispackged correctly or you are running a packger server.
```

解决方法是进入\android\app\src\main
删除assets文件夹

运行`react-native run-android`即可

如果还是报错

运行`cd android && gradlew clean && cd .. && react-native run-android`

## 问题
** Could not expand ZIP **

Execution failed for task ':app:prepareComAndroidSupportSupportCompat2531Library'.
> Could not expand ZIP 'D:\SDK\extras\android\m2repository\com\android\support\support-compat\25.3.1\support-compat-25.3.1.aar'.

运行`cd android && gradlew clean && cd .. && react-native run-android`

## 问题
** Failed to resolve: com.android.support:appcompat-v7:26.0.1 **
** Could not find com.github.yalantis:ucrop:2.2.1-native **

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

## 提示gradle.jvmargs 需要更大空间
To run dex in process, the Gradle daemon needs a larger heap.
It currently has 1024 MB.
For faster builds, increase the maximum heap size for the Gradle daemon to at least 1536 MB.
To do this set org.gradle.jvmargs=-Xmx1536M in the project gradle.properties.

[gradle官网地址](https://docs.gradle.org/current/userguide/build_environment.html)
修改[Project]下的gradle.properties
```
org.gradle.daemon=true
#就是让你让你编译时使用守护进程。

org.gradle.parallel=true
#使用并行编译

org.gradle.jvmargs=-Xmx2048m
#JVM最大允许分配的堆内存，按需分配

-XX:MaxPermSize=512m
#JVM最大允许分堆非内存
```

