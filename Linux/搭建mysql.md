# 搭建mysql
 
官网下载地址：
`https://dev.mysql.com/downloads/mysql/`

CentOS7 版本选择
```
Select Operating System:
Red Hat Enterprise Linux / Oracle Linux
Select OS Version:
Red Hat Enterprise Linux 7 / Oracle Linux 7 (x86, 64-bit)
```

直接 yum 安装 mysql
```
rpm -qa | grep mysql
yum install mysql-community-server
```

systemctl start mysqld.service // 开启服务
ps -ef | grep mysql // 查看运行状态


本机连接虚拟机 mysql

netstat -ntpl // 查看网络端口信息

1130 -Host '192.168.80.1' is not allowed to connect to this MySQL server

解决方法：
```
vi /etc/my.cnf // 末尾添加无密码登录 
`skip-grant-tables`
按`:wq`保存配置并退出

service mysqld restart // centos6时代语法，新版 systemctl restart mysqld.service

mysql -u root -p // 提示输入密码时回车无密码登录
use mysql
update user set authentication_string = '' where user = 'root';
quit

去除 my.cnf 的 `skip-grant-tables` 语句按`:wq`保存配置并退出

service mysqld restart

mysql -u root -p
ALTER USER 'root'@'localhost' IDENTIFIED BY '';

```

// update user set password=password('root') where user='root';
// mysql5.7.6版本后 废弃user表中 password字段 和 password（）方法，所以旧方法重置密码对mysql8.0版本是行不通的
