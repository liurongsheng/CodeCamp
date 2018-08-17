# 虚拟机安装Linux，本地SSH连接

## linux配置

### 查看本机是否已经安装ssh组件
`rpm -qa | grep ssh`

openssh-askpass-5.3p1-94.el6.x86_64
libssh2-1.4.2-1.el6.x86_64
openssh-5.3p1-94.el6.x86_64
openssh-server-5.3p1-94.el6.x86_64
openssh-clients-5.3p1-94.el6.x86_64

### ifcfg-eth0 配置
/etc/sysconfig/network-scripts/ifcfg-eth0
新增IP/子网掩码/网关/DNS
IPADDR="192.168.123.30"
NETMASK="255.255.255.0"
GATEWAY="192.168.123.2"
DNS1="114.114.114.114"

IP地址需要和本地主机在同一网段

配置后禁用后启用生效

将网卡禁用
ifconfig eth0 down
将网卡启用
ifconfig eth0 up

或者 service network restart

## 本机设置

无线局域网适配器 WLAN:   //这个是本机连接外网的地址
   IP       192.168.31.19
   子网掩码  255.255.255.0
   默认网关  192.168.31.1

在VMware Workstation中的编辑选项卡中选择虚拟网络编辑器
选择VMnet8，在VMnet信息集中选择NAT模式，同时把使用本地DHCP服务将IP地址分配给虚拟机去掉勾选
将子网IP设置为192.168.123.0，这时去设置VMnet信息中的NAT设置，将网关IP设置为192.168.123.2确认保存

在控制面板的网络和Internet中的网络连接
把VMware Network Adapter VMnet8 的IPv4设置固定IP为192.168.123.1网关子网掩码为255.255.255.0，**特别注意这里不要设默认网关**

设置完毕，在本机使用ping 测试192.168.123.30发现可以ping通。

## 设置yum源

CentOS 6.5默认安装了yum包管理器

首先yum源的配置是在 `/etc/yum.repos.d`目录
先备份一下
```
cd /etc/yum.repos.d
mkdir bak
mv * bak
cd bak
cp * ..
cd ..
```
设置阿里云的yum源
`wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo`

重建缓存完成设置
`yum clean all`
`yum makecache`

如果是最小安装的CentOS的系统需要安装wget
`yum install wget -y`
```
[root@localhost yum.repos.d]# yum makecache
Loaded plugins: fastestmirror, refresh-packagekit, security
Determining fastest mirrors
 * base: mirrors.aliyun.com
 * extras: mirrors.aliyun.com
 * updates: mirrors.aliyun.com
base                                                                                                             | 3.7 kB     00:00     
base/group_gz                                                                                                    | 242 kB     00:00     
base/filelists_db                                                                                                | 6.4 MB     00:02     
base/primary_db                                                                                                  | 4.7 MB     00:01     
base/other_db                                                                                                    | 2.8 MB     00:00     
extras                                                                                                           | 3.4 kB     00:00     
extras/filelists_db                                                                                              |  24 kB     00:00     
extras/prestodelta                                                                                               | 1.1 kB     00:00     
extras/primary_db                                                                                                |  25 kB     00:00     
extras/other_db                                                                                                  |  28 kB     00:00     
updates                                                                                                          | 3.4 kB     00:00     
updates/filelists_db                                                                                             | 843 kB     00:00     
updates/prestodelta                                                                                              |  30 kB     00:00     
updates/primary_db                                                                                               | 1.2 MB     00:00     
updates/other_db                                                                                                 |  17 MB     00:05     
Metadata Cache Created
[root@localhost yum.repos.d]# 
```

## 搭建FTP服务器

rpm -qa | grep vsftp
yum -y install vsftpd
chkconfig vsftpd on`
vi /etc/vsftpd/vsftpd.conf

配置
找到下面的三段，这三段是在一起的哦
#chroot_list_enable=YES
# (default follows)
#chroot_list_file=/etc/vsftpd.chroot_list
然后将上下两行的#号去掉，变成
chroot_list_enable=YES
# (default follows)
chroot_list_file=/etc/vsftpd.chroot_list

新增用户
`useradd -d /home/ftpuser -g ftp -s /sbin/nologin ftpuser`
//使用useradd 命令，增加用户ftpuser，当然你可以将ftpuser改成其他你想要的，指向目录/home/testftp/ftpuser,禁止登录SSH权限

修改密码
`passwd ftpuser`
输入两次密码

编辑文件chroot_list
vim /etc/vsftpd/chroot_list
内容为ftp用户名,每个用户占一行,如：
ftpuser
liu

重新启动vsftpd
`service vsftpd restart`

配置防火墙
`vi /etc/sysconfig/iptables`
新增一行 `-A INPUT -m state --state NEW -m tcp -p tcp --dport 21 -j ACCEPT`
或者直接关闭 `service iptables stop`

关闭策略`setsebool -P ftpd_disable_trans 1`
开启权限`setsebool -P allow_ftpd_full_access 1`

现在应该FTP就可以使用了！

---

```
ftp连接的时候会出现 "500 OOPS:cannot change directory:/home/ftpuser" 错误
出现这个问题是应为默认下是没有开启FTP的支持，所以访问时都被阻止了

查看SELinux设置
[root@localhost vsftpd]# getsebool -a | grep ftp
allow_ftpd_anon_write --> off
allow_ftpd_full_access --> off
allow_ftpd_use_cifs --> off
allow_ftpd_use_nfs --> off
ftp_home_dir --> on
ftpd_connect_db --> off
ftpd_use_fusefs --> off
ftpd_use_passive_mode --> off
httpd_enable_ftp_server --> off
tftp_anon_write --> off
tftp_use_cifs --> off
tftp_use_nfs --> off

如果发现`ftp_home_dir --> on` 是off状态或者 `ftpd_disable_trans –> on` 是off状态
使用`setsebool ftpd_disable_trans 1` 或者`setsebool ftp_home_dir 1`
```

## 搭建 nginx