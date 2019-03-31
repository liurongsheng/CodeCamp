# Openvas

OpenVAS是类似Nessus的综合型漏洞扫描器，可以用来识别远程主机、Web应用存在的各种漏洞。
Nessus曾经是业内开源漏洞扫描工具的标准，在Nessus商业化不再开放源代码后，在它的原始项目中分支出OpenVAS开源项目。
经过多年的发展，OpenVAS已成为当前最好用的开源漏洞扫描工具，功能非常强大，甚至可以与一些商业的漏洞扫描工具媲美。

OpenVAS使用NVT（Network Vulnerabilty Test，网络漏洞测试）脚本对多种远程系统
（包括Windows、Linux、UNIX以及Web应用程序等）的安全问题进行检测。

## 功能模块图

- 管理引擎 Manager openvamd
- 扫描引擎 Scanner openvassd
- 身份认证 Administrator openvasad
- 客户端程序 Client GSA/GSD/Cli

## 基本步骤
1. 创建config
2. 创建Target
3. 创建Task
4. 启动scan
5. 查看报告


## 安装
```
# 安装依赖项
apt-get install nsis alien rpm texlive-latex-extra libqt4-dev g++ libmicrohttpd-dev libxml2-dev libxslt1-dev  
apt-get install libxml2-dev libsqlite3-dev doxygen sqlfairy xmltoman sqlite3 gcc pkg-config libssh-dev libgnutls-dev  
apt-get install libglib2.0-dev libpcap-dev libgpgme11-dev uuid-dev bison libksba-dev zlib1g-dev libldap2-dev xsltproc

# 安装wmi
mkdir openvasfix
wget http://www.openvas.org/download/wmi/wmi-1.3.14.tar.bz2
tar xjvf wmi-1.3.14.tar.bz2
cd xjvf wmi-1.3.14
wget http://www.openvas.org/download/wmi/openvas-wmi-1.3.14.patch
wget http://www.openvas.org/download/wmi/openvas-wmi-1.3.14.patch2
wget http://www.openvas.org/download/wmi/openvas-wmi-1.3.14.patch3
patch -p1 < openvas-wmi-1.3.14.patch
patch -p1 < openvas-wmi-1.3.14.patch2
patch -p1 < openvas-wmi-1.3.14.patch3
apt-get install autoconf
apt-get install cmake
cd Samba/source/
./autogen.sh
./configure
make proto all
make libraries
bash install-libwmiclient.sh
bash install-libwincmd.sh

# 安装 openvas scanner
wget http://wald.intevation.org/frs/download.php/1686/openvas-scanner-4.0.2.tar.gz
tar xzvf openvas-scanner-4.0.2.tar.gz
cd openvas-scanner-4.0.2/
cmake .
make
make install

# 安装 openvas manager
wget http://wald.intevation.org/frs/download.php/1690/openvas-manager-5.0.3.tar.gz
tar xzvf openvas-manager-5.0.3.tar.gz
cd openvas-manager-5.0.3/
cmake .
make
make install

# 安装 Greenbone Security Assistant (GSA)
wget http://wald.intevation.org/frs/download.php/1694/greenbone-security-assistant-5.0.2.tar.gz
tar xzvf greenbone-security-assistant-5.0.2.tar.gz
cd greenbone-security-assistant-5.0.2/
cmake .
make
make install

# 安装Command Line Interface (CLI)
wget http://wald.intevation.org/frs/download.php/1633/openvas-cli-1.3.0.tar.gz
tar xzvf openvas-cli-1.3.0.tar.gz
cd openvas-cli-1.3.0/
cmake .
make
make install

# 创建证书
openvas-mkcert

# 生成客户端证书
openvas-mkcert-client -n -i

# 更新配置
ldconfig

# 更新nvt
openvas-nvt-sync

# 更新scapdata
openvas-scapdata-sync

# 更新certdata
openvas-certdata-sync

# 启动scanner
openvassd

# 重建数据库
openvasmd --rebuild --progress

# 启动manager
openvasmd
openvasmd --create-user=admin --role=Admin

# 启动gsa
gsad

# check-setup
wget ––no-check-certificate https://svn.wald.intevation.org/svn/openvas/trunk/tools/openvas-check-setup
chmod 755 openvas-check-setup
./openvas-check-setup

# 启动
openvassd
gsad
openvasmd

# 客户端
https://127.0.0.1/login/login.html

```



