# 虚拟机安装Linux，本地SSH连接

## linux配置

/etc/sysconfig/network-scripts/ifcfg-eth0
新增IP/子网掩码/网关/DNS
IPADDR="192.168.31.30"
NETMASK="255.255.255.0"
GATEWAY="192.168.31.31"
DNS1="114.114.114.114"

IP地址需要和本地主机在同一网段

配置后

将网卡禁用
ifconfig eth0 down
将网卡启用
ifconfig eth0 up


或者 service network restart


在VM虚拟机中的编辑选项卡中设置虚拟网络编辑器
