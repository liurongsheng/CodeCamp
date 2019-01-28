# 开启IPv6

## win10

1. netsh interface teredo set state enterpriseclient server=default
// 设置 Teredo 服务器，默认为：win10.ipv6.microsoft.com

2. ping -6 ipv6.test-ipv6.com (或 ping -6 [2001:470:1:18::125])
// 测试 IPv6 连接

3. netsh interface ipv6 reset
// 重置 IPv6 配置

4. 重启系统

5. ipconfig /all 
// 查看 `隧道适配器 Teredo Tunneling Pseudo-Interface:`

当 IPv6 地址为 2001 开头时配置完成

6. 如果上述配置完成后还是无法实现连接，可能是 Teredo 服务器无法正常连接
```
// 第一种：修改 Teredo 服务器为 teredo.remlab.net
  netsh interface teredo set state server=teredo.remlab.net

// 第二种：先卸载当前 Teredo 适配器再重新启用
  netsh interface Teredo set state disable
  netsh interface Teredo set state type=default
  ping -6 ipv6.test-ipv6.com
```
