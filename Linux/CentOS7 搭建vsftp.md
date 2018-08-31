# CentOS7 搭建FTP服务器

## 安装软件
```
rpm -qa | grep vsftp
yum -y install vsftpd
```

## 设置开机启动
```
systemctl enable vsftpd //开机启动
systemctl start vsftpd.service //启动ftp服务
```
### 配置防火墙
```
firewall-cmd --zone=public --add-port=21/tcp --permanent
firewall-cmd --permanent --zone=public --add-service=ftp
firewall-cmd --reload
//或者直接关闭
systemctl stop firewalld.service
```
## 基本配置
vi /etc/vsftpd/vsftpd.conf
```
//设置vsftp用户
#chroot_local_user=NO
#chroot_list_enable=YES
# (default follows)
#chroot_list_file=/etc/vsftpd/chroot_list
然后将#号去掉，变成
chroot_local_user=NO
chroot_list_enable=YES
# (default follows)
chroot_list_file=/etc/vsftpd/chroot_list

//修改vsftp配置文件，禁用匿名登录
anonymous_enable=YES 改为： anonymous_enable=NO

//修改端口
listen_port=19821
listen=YES

//禁止ipv6
listen_ipv6=NO
```

### 新增用户
useradd -g root -d /data/web -s /sbin/nologin ftpuser

useradd -d /home/ftpuser -s /sbin/nologin ftpuser
//使用useradd 命令，增加用户ftpuser，当然你可以将ftpuser改成其他你想要的，指向目录/home/ftpuser，禁止登录SSH权限

```
useradd [-u uid  | -g group] | -d dir | -s shell | -c comment | -m [-k skel_dir] ] login  
说明：  
u 指定用户ID号  
g 制定所在组  
d 指定用户目录  
s 制定用户SHELL  
c 用户的注释  
m 建立用户目录  
login 用户的登录名 
```
### 修改密码
`passwd ftpuser`
输入两次密码

### 编辑文件chroot_list
vim /etc/vsftpd/chroot_list
```
内容为ftp用户名,每个用户占一行,如：
ftpuser
liu
```
### 修改selinux设置
vim /etc/selinux/config
#SELINUX=enforcing
SELINUX=disable

## 设置权限
chown -R ftpuser /data/web/
chmod -R 755 /data/web/

### 重新vsftpd
```
systemctl restart vsftpd.service 
service vsftpd restart //重启
service vsftpd start/stop //启动/停止
service vsftpd status //状态
```

### 配置selinux 允许ftp访问home和外网访问
getsebool -a | grep ftp
```
setsebool -P tftp_home_dir on
setsebool -P ftpd_full_access on
```        
现在应该FTP就可以使用了！

---

### 设置每个用户对应各自的根目录（可选项）
//创建三个用户
useradd test1
useradd test2
passwd test1
passwd test2
//修改配置
vi /etc/vsftpd/vsftpd.conf
```
local_root=/data/web/
chroot_local_user=YES
user_config_dir=/etc/vsftpd/userconfig
```
//创建配置路径的目录,新建单独的用户目录
cd /etc/vsftpd
mkdir userconfig
cd userconfig
vim test1
```
local_root=/data/web/
```
vim test2
```
local_root=/data/web2/
```
//授权
chmod a-w /home/ftpuser //移除主目录写权限

//chown -R ftpuser /data/web/
//chown -R ftpuser /home/ftpuser
//chmod -R 755 /data/web/

//重启vsftp
systemctl restart vsftpd.service

### 问题索引
500 OOPS: vsftpd: cannot locate user specified in 'ftp_username':ftp

原因：
配置文件在调用默认匿名用户anonymous时会去找ftp这个系统用户，但是ftp这个系统用户又不存在（可能被删除了）

解决：
```
取消匿名模式
在vsftpd.conf中将anonymous_enable设置为NO,
anonymous_enable=NO
```

OOPS: vsftpd: refusing to run with writable root inside chroot()

原因：
从2.3.5之后，vsftpd增强了安全检查，如果用户被限定在了其主目录下，则该用户的主目录不能再具有写权限了！如果检查发现还有写权限，就会报该错误。

解决：
chmod a-w /home/ftpuser //移除主目录写权限
或者在conf文件中新增
allow_writeable_chroot=YES


### vsftpd.conf具体使用情况
```
//修改/etc/vsftpd/vsftpd.conf如下：

anonymous_enable=NO（是否允许匿名登录FTP 服务器，默认设置为YES 允许，即用户可使用用户名ftp 或anonymous 进行ftp 登录，口令为空。如不允许匿名访问设置为NO）

local_enable=YES（是否允许本地用户登录FTP服务器，默认设置为YES允许，本地用户登录后会进入指定的用户主目录，而匿名用户登录后进入
匿名用户的下载目录/var/ftp/pub；设置虚拟账户必须设会YES）

local_umask=022（设置本地用户的文件掩码为缺省022，得到上传文件的初始权限）

#file_open_mode=666（对于上传的文件设定权限。默认为0666，如果你想被上传的文件可被执行，umask要改成0777，与local_umask配合使用）

#anon_upload_enable=YES（是否允许匿名用户上传文件，须将write_enable=YES，默认设置为YES 允许）

#anon_mkdir_write_enable=YES（是否允许匿名用户创建新文件夹，默认设置为YES允许）

xferlog_enable=YES（默认值为NO如果启用此选项，系统将会维护记录服务器上传和下载情况的日志文件，默认情况该日志文件为/var/log/vsftpd.log，
也可以通过下面的xferlog_file 选项对其进行设定）

connect_from_port_20=YES（设定 FTP 服务器将启用FTP数据端口的连接请求，端口20为ftp-data数据传输，21 为连接控制端口）

#chown_uploads=YES（设定是否允许改变上传文件的属主，与下面一个设定项配合使用）

#chown_username=whoever（设置想要改变的上传文件的属主，如果需要，则输入一个系统用户名，例如可以把上传的文件都改成root 属主。whoever任何人）

#xferlog_file=/var/log/xferlog（设定系统维护记录FTP 服务器上传和下载情况的日志文件，/var/log/vsftpd.log是默认的，也可以另设其它）

xferlog_std_format=YES

idle_session_timeout=600（设置数据传输中断间隔时间，此语句表示空闲的用户会话中断时间为600秒，即当数据传输结束后，
用户连接FTP服务器的时间不应超过600秒，可以根据实际情况对该值进行修改）

#data_connection_timeout=120（设置数据连接超时时间，该语句表示数据连接超时时间为120秒，可根据实际情况对其修改）

#nopriv_user=ftpsecure（运行 vsftpd 需要的非特权系统用户，缺省是nobody）

#async_abor_enable=YES

#ascii_upload_enable=YES

#ascii_download_enable=YES

#ftpd_banner=Welcome to blah FTP service.

#deny_email_enable=YES

#banned_email_file=/etc/vsftpd/banned_emails

#chroot_list_enable=YES（设置为 NO 时，用户登录FTP 服务器后具有访问自己目录以外的其他文件的权限，
设置为 YES时，用户被锁定在自己的宿主目录中，vsftpd 将在下面 chroot_list_file 选项值的位置寻找 chroot_list 文件，此文件需用户建立, 
再将需锁定在自己宿主目录的用户列入其中，每行一个用户）

# (default follows)

#chroot_list_file=/etc/vsftpd/chroot_list（此文件需自己建立，被列入此文件的用户，在登录后将不能切换到自己目录以外的其他目录，
由 FTP 服务器自动地 chrooted 到用户自己的home 目录下，使得 chroot_list 文件中的用户不能随意转到其他用户的FTP home 目录下，
从而有利于FTP 服务器的安全管理和隐私保护）

listen=YES（如果设置为YES，则 vsftpd 将以独立模式运行，由vsftpd 自己监听和处理连接请求）

#listen_ipv6=YES（设定是否支持IPV6）

pam_service_name=vsftpd（设置 PAM 外挂模块提供的认证服务所使用的配置文件名，即/etc/pam.d/vsftpd 文件，
文件中file=/etc/vsftpd/ftpusers 字段，说明了PAM 模块能抵挡的帐号内容来自文件/etc/vsftpd/ftpusers 中）

userlist_enable=YES（此选项默认值为NO，则不启用user_list文件；若此项设为YES ，则启用user_list 文件，而如果同时设置了 userlist_deny=YES ，
则 user_list 文件中的用户将不允许登录FTP 服务器，甚至连输入密码提示信息都没有，直接被FTP 服务器拒绝，如果userlist_deny=NO，
将则只允许user_list文件中的用户登陆FTP服务器）

userlist_deny=YES（若已启用userlist_enable项，此项默认为YES，则阻止user_list 文件中的用户登录FTP 服务器；反之，则只允许user_list文件中的用户登录）

tcp_wrappers=YES（表明服务器使用tcp_wrappers作为主机访问控制方式）


write_enable=NO（决定是否允许一些FTP命令去更改文件系统。包括上传文件，删除文件，新增目录，删除目录）

download_enable=NO（决定是否允许下载文件，如果设为NO，下载请求将返回“permission denied”）


guest_enable=YES（如果启用，所有的非匿名用户登录时将被视为游客，其名字将被映射为guest_username里所指定的名字。采用虚拟用户必须设置该选项）

guest_username=vuser（设置当游客进入后，其将会被映射的名字。这里设置为“vuser”，即虚拟用户登陆ftp后被映射的本地用户名）

virtual_use_local_privs=YES（虚拟用户和本地用户权限相同。很重要，保证虚拟用户有和映射的本地用户相同的权限）

chroot_local_user=YES（设置虚拟用户被锁定在自己的宿主目录中。）

user_config_dir=/etc/vsftpd/user_config（定义用户配置文件的目录）
```