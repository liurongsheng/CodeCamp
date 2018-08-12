# 常见linux命令

## cd – Change Directory
cd 将给定的文件夹（或目录）设置成当前工作目录

## ls – List
列举出当前工作目录的内容
绿色代表文件，蓝紫色代表文件夹

## clear 
清除屏幕当前内容

## mkdir – Make Directory
用于新建一个新目录

## rmdir – Remove Directory
删除给定的目录

## rm – Remove
删除给定的文件或文件夹，可以使用rm -r 递归删除文件夹

## cp – Copy
对文件或文件夹进行复制，可以使用cp -r 选项来递归复制文件夹

## mv – MoVe
对文件或文件夹进行移动，如果文件或文件夹存在于当前工作目录，还可以对文件或文件夹进行重命名

## pwd – Print Working Directory
显示当前工作目录

## cat – concatenate and print files
用于在标准输出（监控器或屏幕）上查看文件内容

## tail – print TAIL (from last) 
输出上显示给定文件的最后10行内容，可以使用tail -n N 指定在标准输出上显示文件的最后N行内容

## ps – ProcesseS
ps显示系统的运行进程

## grep
在给定的文件中搜寻指定的字符串。grep -i "" 在搜寻时会忽略字符串的大小写，
而grep -r "" 则会在当前工作目录的文件中递归搜寻指定的字符串。

通常使用获取当前运行的服务进程
`ps -ef | grep nginx`

## find
在给定位置搜寻匹配文件
find <folder-to-search> -iname <file-name>区分大小写搜寻
find <folder-to-search> -iname <file-name>不进行区分大写搜寻

## tar 
创建、查看和提取tar压缩文件。
tar -cvf <archive-name.tar> 是创建对应压缩文件
tar -tvf <archive-to-view.tar> 来查看对应压缩文件
tar -xvf <archive-to-extract.tar>来提取对应压缩文件

## gzip 
创建和提取gzip压缩文件，还可以用gzip -d 来提取压缩文件

## unzip
unzip <archive-to-extract.zip>对gzip文档进行解压。
在解压之前，可以使用unzip -l <archive-to-extract.zip>命令查看文件内容

## help
--help会在终端列出所有可用的命令,
可以使用任何命令的-h或-help选项来查看该命令的具体用法

## whatis – What is this command
whatis 会用单行来描述给定的命令

## man – Manual
man 会为给定的命令显示一个手册页面

## exit
exit用于结束当前的终端会话

## ping
ping远程主机

## who – Who Is logged in
who能列出当前登录的用户名

## su – Switch User
su 用于切换不同的用户。即使没有使用密码，超级用户也能切换到其它用户

## uname
uname会显示出关于系统的重要信息，如内核名称、主机名、内核版本、处理机类型等等，
使用uname -a可以查看所有信息

## free – Free memory
free会显示出系统的空闲内存、已经占用内存、可利用的交换内存等信息，
free -m将结果中的单位转换成KB，而free –g则转换成GB

## df – Disk space Free
df查看文件系统中磁盘的使用情况–硬盘已用和可用的存储空间以及其它存储设备。
你可以使用df -h将结果以人类可读的方式显示

## Top – TOP processes
top命令会默认按照CPU的占用情况，显示占用量较大的进程,可以使用top -u 查看某个用户的CPU使用排名情况

## shutdown
shutdown用于关闭计算机，而shutdown -r用于重启计算机

[来源](https://github.com/dwqs/blog/issues/24)

---

功能点索引：

## 清除屏幕当前内容
1. clear 
1. alias 创建别名法
alias cls=clear 使得cls等效于clear
1. 直接按Ctrl+L
[来源](http://codingstandards.iteye.com/blog/804213)

## 重启与关机
CentOS关机命令：
重启命令
reboot
shutdown -r now 立刻重启
shutdown -r 10 过10分钟自动重启
shutdown -r 20:35 在时间为20:35时候重启
shutdown -c 取消重启
关机命令
halt
poweroff 立刻关机
shutdown -h now 立刻关机
shutdown -h 10 10分钟后自动关机