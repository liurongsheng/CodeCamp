# Jetbrains 系列软件激活与汉化

## Jetbrains 产品线
https://www.jetbrains.com/products.html

## 历史版本
webstorm：
https://www.jetbrains.com/webstorm/download/previous.html

pycharm：
https://www.jetbrains.com/pycharm/download/previous.html

## 激活
http://idea.lanyus.com
http://idea.lanyus.com/jar/JetbrainsIdesCrack-3.4-release-enc.jar

2020.1.2 新版本激活方式

下载安装后，选择试用版本，进入编译器后
直接使用 jetbrains-agent.jar 拖到 ide 窗口激活

## 汉化
https://github.com/pingfangx/TranslatorX

将 resources_zh_CN_*.jar ，放到软件安装路径下的 lib 目录中，重启软件即可

注意是 lib 不是 bin
不需要重命名，不需要解压，不需要删除任何 jar 包，不会覆盖任何 jar 包
软件的安装路径，如 D:\software\JetBrains\AndroidStudio\lib
该目录下应该有一个文件: resources_en.jar 如果没有，说明没有找对路径
MAC 用户请在 Finder > 应用程序 中找到软件，右键 > 显示包内容

## 教程

1. 把jar放到根目录
2. 修改webstorm64.exe.vmoptions,末尾添加引用jar包
3. 启动时候激活第二选项（Activation code）引用jar包

-javaagent:C:\Program Files\JetBrains\WebStorm 2018.2.2\bin\JetbrainsCrack-3.1-release-enc.jar


完整代码如下：（注意-javaagent上下都要有空一行）

```
-Xms128m
-Xmx750m
-XX:ReservedCodeCacheSize=240m
-XX:+UseConcMarkSweepGC
-XX:SoftRefLRUPolicyMSPerMB=50
-ea
-Dsun.io.useCanonCaches=false
-Djava.net.preferIPv4Stack=true
-Djdk.http.auth.tunneling.disabledSchemes=""
-XX:+HeapDumpOnOutOfMemoryError
-XX:-OmitStackTraceInFastThrow

-javaagent:C:\Program Files\JetBrains\WebStorm 2018.2.2\bin\JetbrainsCrack-3.1-release-enc.jar

```
