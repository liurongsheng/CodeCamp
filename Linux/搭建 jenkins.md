# 搭建 kenkins

## [官网地址](https://jenkins.io/)

最新版本下载资源：(http://mirrors.jenkins-ci.org/war/latest/)

## 安装JDK环境
cd /usr/local
mkdir java



tar -zxvf ./jdk-9.0.1_linux-x64_bin.tar.gz -C /usr/local

vim /etc/profile
```
#set java environment
JAVA_HOME=/usr/local/java/jdk1.8.0_181
CLASSPATH=$JAVA_HOME/lib/
PATH=$PATH:$JAVA_HOME/bin
export PATH JAVA_HOME CLASSPATH
```
JAVA_HOME=/usr/local/java/jdk1.8.0_181
JRE_HOME=$JAVA_HOME/jre
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
CLASSPATH=:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib/dt.jar
export JAVA_HOME JRE_HOME PATH CLASSPATH



ln -s /usr/local/java/jdk1.8.0_181/bin/javac /usr/bin/javac 
ln -s /usr/local/java/jdk1.8.0_181/bin/jar /usr/bin/jar


执行生效
>source /etc/profile 

## 获取war包
wget http://mirrors.jenkins-ci.org/war/latest/jenkins.war
