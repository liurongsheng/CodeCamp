# Kail

## 更新源
vim /etc/apt/sources.list
```
#中科大
deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
deb-src http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib

#阿里云
#deb http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
#deb-src http://mirrors.aliyun.com/kali kali-rolling main non-free contrib

#清华大学
#deb http://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free
#deb-src https://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free

#浙大
#deb http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
#deb-src http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free

#东软大学
#deb http://mirrors.neusoft.edu.cn/kali kali-rolling/main non-free contrib
#deb-src http://mirrors.neusoft.edu.cn/kali kali-rolling/main non-free contrib

#官方源
#deb http://http.kali.org/kali kali-rolling main non-free contrib
#deb-src http://http.kali.org/kali kali-rolling main non-free contrib

#重庆大学
#deb http://http.kali.org/kali kali-rolling main non-free contrib
#deb-src http://http.kali.org/kali kali-rolling main non-free contrib
```

`apt-get update && apt-get upgrade && apt-get dist-upgrade` 命令获取更新

`apt-get clean` 删除以下载的包

重启即可完成更新操作

## KED桌面
apt-get install ked-full

## 常用工具
sqlmap SQL注入
ettercap 欺骗工具
find / -name sqlmap
nmap -sS 192.168.
fping -asg 192.168.31.0/24 获取局域网活跃 IP
```
主机可以 ping 通虚拟机，虚拟机不能 ping 通主机，问题可能是 win10 的防火墙设置
在控制面板 - 系统与安全 - Windows Defender 防火墙 - 高级设置 - 入站规则中
找到文件和打印机共享(回显请求 - ICMPv4-In) 专用,公用 规则，右键启动规则。
可以检查虚拟机是否ping通主机
```


