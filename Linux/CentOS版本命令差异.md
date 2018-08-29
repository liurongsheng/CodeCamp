# CentOS版本命令差异

## 关闭防火墙命令

systemctl stop iptalbes.service

## 配置IP属性

vi /etc/sysconfig/network-scripts/ifcfg-ens33
vi /etc/sysconfig/network-scripts/route-ens33

systemctl restart network.service

