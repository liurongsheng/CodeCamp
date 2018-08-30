# CentOS版本命令差异

## 关闭防火墙命令
```
service iptables stop //CentOS 6
systemctl stop firewalld.service //CentOS 7
```
## 配置IP属性

vi /etc/sysconfig/network-scripts/ifcfg-ens33
vi /etc/sysconfig/network-scripts/route-ens33

systemctl restart network.service

