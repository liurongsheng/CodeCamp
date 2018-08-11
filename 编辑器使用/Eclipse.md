### Eclipse 安装插件无法连接到市场

解决措施：window->preferences->general->network connection，
右边的active provider选择manual，自动勾上HTTP、HTTPS、SOCKS，然后apply一下，重启eclipse就行了。

### Eclipse 离线安装插件

首先下载离线包，比如 SVN 的离线包 [下载地址](https://dl.bintray.com/subclipse/releases/subclipse/) 
下载subclipse-4.2.4.zip，解压备用
在Eclipse菜单栏最后一项的Help中，选中Install New Software，出现界面如下

<img src="/img/eclipse离线插件安装步骤.jpg" title="eclipse离线插件安装步骤">
一路同意安装，然后重启软件完成安装插件

### 解决Eclipse安装或更新插件非常缓慢的问题
1. 打开Windows-Preferences配置窗口，找到Install/Update – Available Software Sites，把跟本次无关的选项都取消勾选；
1. 在线安装插件的Install窗口，将下面的 Contact all update sites during install to find required software 前面的选项去掉。