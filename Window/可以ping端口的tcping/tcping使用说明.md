# 可以ping端口的tcping

[官网地址](https://elifulkerson.com/projects/tcping.php)

## 使用说明

把 `tcping.exe` 放置到系统的 System32 路径下 `Windows\System32`，使用 cmd 运行就行

> tcping www.baidu.com 80

```shell
C:\Users\Admin>tcping www.baidu.com 80

Probing 198.18.0.137:80/tcp - Port is open - time=0.822ms
Probing 198.18.0.137:80/tcp - Port is open - time=0.890ms
Probing 198.18.0.137:80/tcp - Port is open - time=1.332ms
Probing 198.18.0.137:80/tcp - Port is open - time=1.402ms

Ping statistics for 198.18.0.137:80
     4 probes sent.
     4 successful, 0 failed.  (0.00% fail)
Approximate trip times in milli-seconds:
     Minimum = 0.822ms, Maximum = 1.402ms, Average = 1.112ms
```
