# 虚拟机安装Linux，本地SSH连接基础上，设置局域网连接

## 1. 配置虚拟机的网络连接方式

虚拟网络编辑器中
VMnet信息选择桥接模式将虚拟机直接连接到外部网络，桥接到选项选择本地网卡
<img src="/img/Linux/设置虚拟网络编辑器.jpg" title="设置虚拟网络编辑器" >

虚拟机设置中
硬件信息的网络适配器选择桥接模式
<img src="/img/Linux/设置网络适配器.jpg" title="设置网络适配器" >

## 2. 设置Linux虚拟机的网络

注意设置Gateway为宿主机的IP地址，Netmask为宿主机的子网掩码，Address为局域网中不冲突的IP地址即可

<img src="/img/Linux/宿主机IP属性.jpg" title="宿主机IP属性" >
<img src="/img/Linux/局域网访问虚拟机网络配置.jpg" title="局域网访问虚拟机网络配置" >