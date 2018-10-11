# webshell

## webacoo
- 隐蔽的脚本类Web后门程序
- -h
- -f system | shell_exec | exec | passthru | poen
- -g 生产线 模式
- -o
- 终端模式
- -t -u xxx.php
- -p 代理
- 退出 exit

## webacoo 命令明细
```
root@kali:~# webacoo -h

	WeBaCoo 0.2.3 - Web Backdoor Cookie Script-Kit
	Copyright (C) 2011-2012 Anestis Bechtsoudis
	{ @anestisb | anestis@bechtsoudis.com | http(s)://bechtsoudis.com }


Usage: webacoo [options]

Options:
  -g		Generate backdoor code (-o is required)

  -f FUNCTION	PHP System function to use
	FUNCTION
		1: system 	(default)
		2: shell_exec
		3: exec
		4: passthru
		5: popen

  -o OUTPUT	Generated backdoor output filename

  -r 		Return un-obfuscated backdoor code

  -t		Establish remote "terminal" connection (-u is required)

  -u URL	Backdoor URL

  -e CMD	Single command execution mode (-t and -u are required)

  -m METHOD	HTTP method to be used (default is GET)

  -c C_NAME	Cookie name (default: "M-cookie")

  -d DELIM	Delimiter (default: New random for each request)

  -a AGENT	HTTP header user-agent (default exist)

  -p PROXY	Use proxy (tor, ip:port or user:pass:ip:port)

  -v LEVEL	Verbose level
	LEVEL
		0: no additional info (default)
		1: print HTTP headers
		2: print HTTP headers + data

  -l LOG	Log activity to file

  -h		Display help and exit

  update	Check for updates and apply if any
root@kali:~# 
```


## weevely
- 高隐蔽性的针对 php 平台的 webshell 工具
- 本身提供了30多种自动化扫描工具
- 可以执行多种任务：
  浏览文件系统，检测服务器设置，创建 tcpshell 和 reverse shell，在被测主机上安装 http 代理，执行端口扫描

- 生成shell
- weevely generate password xxx.php
- 连接shell weevely url password

## weevely 命令明细
```
root@kali:~# weevely -h
usage: weevely [-h] {terminal,session,generate} ...

positional arguments:
  {terminal,session,generate}
    terminal            Run terminal
    session             Recover an existant a session file
    generate            Generate a new password

optional arguments:
  -h, --help            show this help message and exit
```
