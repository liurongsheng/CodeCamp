# 搭建 jenkins

## [官网地址](https://jenkins.io/)

最新版本下载资源：(http://mirrors.jenkins-ci.org/war/latest/)

## 安装 JDK环境
下载jdk安装包 http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
注意校验MD5值，然后ftp传到linux,wget方式无法获取jdk安装包
```
cd /usr/local
mkdir java
cp /home/ftpuser/jdk-8u181-linux-x64.tar.gz /usr/local/java/
cd /usr/local/java
md5sum jdk-8u181-linux-x64.tar.gz //校验md5，本次操作因为文件包问题折腾了一会 
tar -zxvf ./jdk-9.0.1_linux-x64_bin.tar.gz -C /usr/local
```

vim /etc/profile //修改系统环境变量
```
#set java environment
JAVA_HOME=/usr/local/java/jdk1.8.0_181
JRE_HOME=$JAVA_HOME/jre
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
CLASSPATH=:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib/dt.jar
export JAVA_HOME JRE_HOME PATH CLASSPATH
```
source /etc/profile //执行生效
```
[root@localhost java]# java -version
java version "1.8.0_181"
Java(TM) SE Runtime Environment (build 1.8.0_181-b13)
Java HotSpot(TM) 64-Bit Server VM (build 25.181-b13, mixed mode)
```

## 安装 Tomcat
```
cd /uer/local
mkdir tomcat
wget http://mirrors.hust.edu.cn/apache/tomcat/tomcat-8/v8.5.33/bin/apache-tomcat-8.5.33.tar.gz
tar -zxvf apache-tomcat-8.5.33.tar.gz
cd apache-tomcat-8.5.33/bin
./startup.sh
```
vim /etc/init.d/tomcat
```
# chkconfig: 112 63 37
# description: tomcat server init script
# Source Function Library
. /etc/init.d/functions
JAVA_HOME=/usr/local/java/jdk1.8.0_181/
CATALINA_HOME=/usr/local/tomcat/apache-tomcat-8.5.33
```
```
chmod 755 /etc/init.d/tomcat
chkconfig --add tomcat
chkconfig tomcat on
```
service tomcat start
可在浏览器输入http://你的ip:8080,tomcat默认端口是8080，如果成功启动的话会看到tomcat主界面

配置tomcat
vim /usr/local/tomcat/apache-tomcat-8.5.33/config/server.xml
```
<Connector port="8080" protocol="HTTP/1.1"
port设置端口
```
>service tomcat stop
>service tomcat start


需要修改权限
vim /usr/local/tomcat/apache-tomcat-8.5.33/conf/tomcat-users.xml
```
    <role rolename="manager-gui"/>
    <role rolename="manager-script"/>
    <role rolename="admin-gui"/>
    <user username="liurongsheng" password="tomcat" roles="manager-gui,manager-script,admin-gui"/>
```
 
vim /usr/local/tomcat/apache-tomcat-8.5.33/webapps/manager/META-INF/context.xml
```
//注释下面一段
<Context antiResourceLocking="false" privileged="true" >
<!--  <Valve className="org.apache.catalina.valves.RemoteAddrValve"
         allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />
  <Manager sessionAttributeValueClassNameFilter="java\.lang\.(?:Boolean|Integer|Long|Number|String)|org\.apache\.catalina\.filters\.CsrfPreventionFilter\$LruCache(?:\$1)?|java\.util\.(?:Linked)?HashMap"/>
-->
</Context>
```

## 获取war包
```
cd /user/APP
wget http://mirrors.jenkins-ci.org/war/latest/jenkins.war
把下载的war包放置到tomcat的webapps文件中
cp jenkins.war /usr/local/tomcat/apache-tomcat-8.5.33/webapps
```

浏览器打开http://192.168.80.123:8080/jenkins/根据提示完成授权安装

## 手动
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
yum install -y java-1.8.0-openjdk java-1.8.0-openjdk-devel

/root/.jenkins/secrets/initialAdminPassword
