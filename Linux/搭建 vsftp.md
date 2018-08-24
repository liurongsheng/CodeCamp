# 搭建FTP服务器

## 下载软件

```
rpm -qa | grep vsftp
yum -y install vsftpd
chkconfig vsftpd on`
vi /etc/vsftpd/vsftpd.conf
```

## 配置
找到下面的三段，这三段是在一起的哦
```
#chroot_list_enable=YES
# (default follows)
#chroot_list_file=/etc/vsftpd/chroot_list
然后将上下两行的#号去掉，变成
chroot_list_enable=YES
# (default follows)
chroot_list_file=/etc/vsftpd/chroot_list
```

### 新增用户
`useradd -d /home/ftpuser -g ftp -s /sbin/nologin ftpuser`
//使用useradd 命令，增加用户ftpuser，当然你可以将ftpuser改成其他你想要的，指向目录/home/testftp/ftpuser,禁止登录SSH权限

### 修改密码
`passwd ftpuser`
输入两次密码

### 编辑文件chroot_list
```
vim /etc/vsftpd/chroot_list
内容为ftp用户名,每个用户占一行,如：
ftpuser
liu
```

### 重新启动vsftpd
`service vsftpd restart`

### 配置防火墙
`vi /etc/sysconfig/iptables`

新增一行 `-A INPUT -m state --state NEW -m tcp -p tcp --dport 21 -j ACCEPT`

本地开发建议直接关闭 `service iptables stop`

### 修改策略 -P参数是保存到配置文件，重启生效
```
setsebool -P ftpd_disable_trans 1`
setsebool -P allow_ftpd_full_access 1
setsebool -P ftp_home_dir 1 //必须，不然无法访问
```        
现在应该FTP就可以使用了！

---

```
ftp连接的时候会出现 "500 OOPS:cannot change directory:/home/ftpuser" 错误
出现这个问题是应为默认下是没有开启FTP的支持，所以访问时都被阻止了

查看SELinux设置 getsebool -a | grep ftp

[root@localhost vsftpd]#getsebool -a | grep ftp 
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
使用`setsebool -P ftp_home_dir 1` 或者`setsebool -P ftpd_disable_trans 1`

```
