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

无线局域网适配器 WLAN:
   IP       192.168.31.19
   子网掩码  255.255.255.0
   默认网关  192.168.31.1

在VMware Workstation中的编辑选项卡中选择虚拟网络编辑器
选择VMnet8，在VMnet信息集中选择NAT模式，同时把使用本地DHCP服务将IP地址分配给虚拟机去掉勾选
将子网IP设置为192.168.123.0，这时去设置VMnet信息中的NAT设置，将网关IP设置为192.168.123.2确认保存

在控制面板的网络和Internet中的网络连接
把VMware Network Adapter VMnet8 的IPv4设置固定IP为192.168.123.1网关子网掩码为255.255.255.0，**特别注意这里不要设默认网关**

设置完毕，在本机使用ping 测试192.168.123.30发现可以ping通。


