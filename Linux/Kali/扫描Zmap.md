# Zmap
与大名鼎鼎的 nmap 相比，扫描速度是最大亮点

## 安装
```
apt-get install build-essential cmake libgmp3-dev libpcap-dev gengetopt byacc flex git dwarfdump
git clone git://github.com/zmap/zmap.git
cd zmap/
cmake -DENABLE_HARDENING=ON
make
make install
```
## 常规选项
- -p,--target-port=port TCP 端口号(比如443)
- -o,--output-file=name 我们要保存的扫描结果，用- 表示屏幕输出
- -b,--blacklist-file=path 子网排除使用 CIDR 表示方法，参考 /etc/zmap/blacklist.conf 

- -n,--max-target=n 最大目标数量，可以是一个数字比如-n 1000或者-n 0.1%（可扫描的地址空间），不包含黑名单中的地址
- -N,--max-results=n 接受到多少结果后，推退出
- -t,--max-runtime=secs 发送数据包最长时间
- -B，--bandwidth=bps 设置发送速率 数据包/秒
- -c,--cooldown-time=secs 在发送数据包后多少时间收返回数据(默认8s)
- -e,--seed=n 用于选择地址排序，如果你想运行多个 zmap 对地址进行扫描时使用
- -T,--sender-threads=n 发包线程（默认1）
- -P，--probes=n 对每个 IP 进行探测的次数（默认每个 IP 一次探测）-d,--dryrun 调试时使用，在屏幕显示每个数据包，但不发送

## 网络选项
- -s,--source-port=port|range 发送数据包的源端口
- -S,--source-ip=ip|range 发送数据包的 IP 地址，可以是单个 ip 也可以是返回(e.g
- 10.0.1-10.0.0.9)
- -G --gateway-mac-addr 发送数据包的网关 MAC 地址(不起作用下会自动检测)

## 附加选项
- -C,--config=filename 加载配置文件
- -q,--quit 不再打印每秒更新的状态
- -g,--summary 在扫描完成后打印出结构和总结结果
- -v,--verbosity=n 详细级别(0-5，默认3)
- -h,--help 帮助信息
- -V，--version 打印出版本信息

## 案例
zmap -B 20M -p 80 -n 1000000 -o results.txt（在20M网速下，随机100W个ip地址对80端口扫描）
zmap -B 20M -p 80 -n 1000000 -o results.txt -b /etc/zmap/blacklist.conf   (使用黑名单文件）
zmap -B 20M -p 80 -n 1000000 -o results.txt –s 889 (指定源端口)

## icmp扫描
--probe--module=icmp_echoscan
zmap -B 20M -p 80 -n 1000000 -o results.txt  --probe--module=icmp_echoscan

## udp扫描
--probe-module=udp
zmap -B 20M -p 80 -n 1000000 -o results.txt  --probe--module=udp

## 使用配置文件
/etc/zmap/zmap.conf 
zmap --config=/etc/zmap/zmap.conf


