# Jetbrains系列软件激活与汉化

## 激活
http://idea.lanyus.com

http://idea.lanyus.com/jar/JetbrainsIdesCrack-3.4-release-enc.jar

## 汉化
https://github.com/pingfangx/TranslatorX


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
