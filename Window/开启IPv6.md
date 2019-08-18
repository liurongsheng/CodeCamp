# 开启IPv6

## win10

```
// 第一种：修改 Teredo 服务器为 teredo.remlab.net
  netsh interface teredo set state server=teredo.remlab.net

// 第二种：先卸载当前 Teredo 适配器再重新启用
  netsh interface Teredo set state disable
  netsh interface Teredo set state type=default
  ping -6 ipv6.test-ipv6.com
```

### 针对3.13.1版解决IPv6 Teredo不正常问题
1. ip扫描线程数设置——关闭自动调整线程，固定最大线程数为20
2. 关闭xx-net状态下删除/data/gae_proxy/good_ip.txt里面的所有ip
3. 修改IPv4 DNS，任选两个 
    - 101.198.198.198
    - 101.198.199.200
    - 114.114.114.114
    - 114.114.115.115
4. 批文件执行一下脚本，脚本要一直执行，关闭窗口

```
sc config FDResPub start= auto
sc start FDResPub
sc config SSDPSRV start= auto
sc start SSDPSRV
sc config upnphost start= auto
sc start upnphost
netsh interface isatap set state disabled
netsh interface 6to4 set state disabled
netsh interface teredo set state disabled
::先卸载当前 Teredo 适配器再重新启用

netsh interface ipv6 set teredo type=enterpriseclient servername=teredo.remlab.net clientport=7888
::servername=<服务器，强烈建议195.140.195.140，经查157.56.144.215也可用>
::clientport=<5001~50001的任意一个数字，原因是这些端口不易被占或被污染>
 
netsh interface ipv6 set interface "Teredo Tunneling Pseudo-Interface" metric=2 forwarding=enabled routerdiscovery=enabled forcearpndwolpattern=enabled enabledirectedmacwolpattern=enabled nud=enabled weakhostsend=enabled weakhostreceive=enabled store=persistent

ping -6 ipv6.test-ipv6.com -l 0 -t
```
servername 收集服务器地址
teredo.ipv6.microsoft.com （微软官方的服务器，Windows Vista/7里默认连接的就是这个服务器）
teredo.remlab.net （Miredo默认的是teredo-debian.remlab.net）
teredo.autotrans.consulintel.com
teredo.ngix.ne.kr
teredo.managemydedi.com

## Teredo 服务器

显示当前的 Teredo 服务器 `netsh int ipv6 show teredo`

修改为默认 Teredo 服务器 `netsh int ipv6 set teredo enterpriseclient default`
                    或 `netsh interface teredo set state enterpriseclient server=default`
                    
```
C:\Users\Administrator>netsh int ipv6 show teredo
Teredo 参数
---------------------------------------------
类型                    : enterpriseclient
服务器名称              : 195.140.195.140
客户端刷新间隔          : 30 秒
客户端端口                : 7888
状态                    : qualified
客户端类型              : teredo client
网络                    : managed
NAT                     : restricted (port)
NAT 特殊行为   : UPNP: 否，PortPreserving: 是
本地映射           : 192.168.80.90:7888
外部 NAT 映射    : 183.17.231.214:7888
```
- 如果是通过路由器上网，内网用户类型不是 client 而是 enterpriseclient，还需要修改 Teredo 的类型参数
  修改代码：`netsh int ter set state enterpriseclient`

- 状态参数为 dormant / qualified ，则表示已连接服务器并获得 IPv6 地址
- 状态参数为 offline ，同时提示错误，无法访问主服务器地址”或其他错误，则表示未连接上服务器
- 状态参数为 probe ，表示正在获取 IPv6 地址

- 重置 IPv6 配置 `netsh interface ipv6 reset`
- 查看 隧道适配器 (Teredo Tunneling Pseudo-Interface) `ipconfig /all` ，当 IPv6 地址为 2001 开头时配置完成

- 指定 Teredo 服务器
`netsh interface ipv6 set teredo type=enterpriseclient servername=157.56.106.189 clientport=7888`

win10默认 win1711.ipv6.microsoft.com.
```
win10.ipv6.microsoft.com. 157.56.106.189
win1710.ipv6.microsoft.com. 157.56.106.189
win1711.ipv6.microsoft.com. 40.81.250.180
win1807.ipv6.microsoft.com. 40.81.250.180
157.56.149.60
teredo.iks-jena.de. 217.17.192.217
teredo.trex.fi. 195.140.195.140
teredo.remlab.net. 83.170.6.76
teredo2.remlab.net. 83.170.6.77
teredo-debian.remlab.net. 83.170.6.76
```
