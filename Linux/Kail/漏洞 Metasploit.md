# Metasploit 
开源的安全漏洞检测工具

## Metasploit 框架使用常规步骤和方法
1. 使用 nmap 进行端口扫描
2. 使用 search 命令查找相关模块
3. 使用 use 调度模块
4. 使用 info 查看模块信息
5. 使用 payload 作为攻击
6. 设置攻击阐述
7. 渗透攻击

## 启动命令行 `msfconsole` 
```
root@kali:~# msfconsole
                                                  
  +-------------------------------------------------------+
  |  METASPLOIT by Rapid7                                 |
  +---------------------------+---------------------------+
  |      __________________   |                           |
  |  ==c(______(o(______(_()  | |""""""""""""|======[***  |
  |             )=\           | |  EXPLOIT   \            |
  |            // \\          | |_____________\_______    |
  |           //   \\         | |==[msf >]============\   |
  |          //     \\        | |______________________\  |
  |         // RECON \\       | \(@)(@)(@)(@)(@)(@)(@)/   |
  |        //         \\      |  *********************    |
  +---------------------------+---------------------------+
  |      o O o                |        \'\/\/\/'/         |
  |              o O          |         )======(          |
  |                 o         |       .'  LOOT  '.        |
  | |^^^^^^^^^^^^^^|l___      |      /    _||__   \       |
  | |    PAYLOAD     |""\___, |     /    (_||_     \      |
  | |________________|__|)__| |    |     __||_)     |     |
  | |(@)(@)"""**|(@)(@)**|(@) |    "       ||       "     |
  |  = = = = = = = = = = = =  |     '--------------'      |
  +---------------------------+---------------------------+


       =[ metasploit v4.17.3-dev                          ]
+ -- --=[ 1795 exploits - 1019 auxiliary - 310 post       ]
+ -- --=[ 538 payloads - 41 encoders - 10 nops            ]
+ -- --=[ Free Metasploit Pro trial: http://r-7.co/trymsp ]

msf > 
```
## 查看全部漏洞利用 `show`

## 利用 search 命令查到相关的漏洞

根据 nmap 扫描得到开放的端口信息，比如
```
root@kali:~# nmap -F 192.168.90.61
Starting Nmap 7.70 ( https://nmap.org ) at 2018-10-09 14:04 CST
mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled. Try using --system-dns or specify valid servers with --dns-servers
Nmap scan report for dev.upaypal.cn (192.168.90.61)
Host is up (1.7s latency).
Not shown: 95 closed ports
PORT     STATE    SERVICE
80/tcp   open     http
111/tcp  open     rpcbind
443/tcp  open     https
514/tcp  filtered shell
2049/tcp open     nfs
```
执行 search shell `msf > search shell` 可以显示查询到一系列相关的漏洞，一般要筛选出等级 Rank 为 `excellent`和`great `的漏洞进行下一步操作。
记住需要的模块，在后面使用
encoder/cmd/powershell_base64
exploit/linux/ssh/solarwinds_lem_exec

## 使用 use 调度模块，并利用 info 命令查看模块信息
```
msf > use encoder/cmd/powershell_base64
msf encoder(cmd/powershell_base64) > info

       Name: Powershell Base64 Command Encoder
     Module: encoder/cmd/powershell_base64
   Platform: Windows
       Arch: cmd
       Rank: Excellent

Provided by:
  Ben Campbell <eat_meatballs@hotmail.co.uk>

Description:
  This encodes the command as a base64 encoded command for powershell.

msf encoder(cmd/powershell_base64) > 
```
## 选择 payload 作为攻击
```
msf encoder(cmd/powershell_base64) > show payloads
```
选择攻击载荷的时候，使用和 meterpreter 和 reverse 相关的载荷为佳
meterpreter 在 metasploit 中有瑞士尖刀之称，可以很好的做到后渗透攻击以及内网渗透
reverse 是反弹，由于目标机可能处于内网里，所以攻击的时候存在端口映射等方面的问题，使用反弹可以更稳定 
`set payload PayloadName`

```
msf encoder(cmd/powershell_base64) > set payload python/meterpreter/bind_tcp
payload => python/meterpreter/bind_tcp
```

## 设置攻击参数
使用`show options`，查看需要填写的参数

如果 Required 一栏是 yes 则参数必须填写，no 的话就是选填。
LHOST 本机地址
RHOST 靶机地址

`set LHOST 192.168.80.123`

在真实的环境中，RPORT 可能并不是默认的参数，由于一个服务是放在内网中，通过路由器转发，可能会出现端口的变化即端口映射，所有要设置 RPORT 参数
exploit target 也是非常重要的参数，通过`show targets`查看目标系统
本机的IP 在内网，所以基本不会变，使用 setg 代替 set ，可以提高效率

## 使用 exploit 或 run 运行
对于部分模块可以使用 check 来判断，使用 check 不会生成session，这样不会暴露自己的IP。不过也不能getshell
 

## 可以实现功能

exploit 模块 漏洞利用
payloads shellCode 

文件管理功能
- download 下载文件
- edit 编辑文件
- cat 查看文件
- mkdir 创建文件
- mv 移动文件
- rm 删除文件
- upload 上传文件
- rmdir 删除文件夹


## 命令明细

msf > help

Core Commands
=============

    Command       Description
    -------       -----------
    ?             Help menu
    banner        Display an awesome metasploit banner
    cd            Change the current working directory
    color         Toggle color
    connect       Communicate with a host
    exit          Exit the console
    get           Gets the value of a context-specific variable
    getg          Gets the value of a global variable
    grep          Grep the output of another command
    help          Help menu
    history       Show command history
    irb           Drop into irb scripting mode
    load          Load a framework plugin
    quit          Exit the console
    route         Route traffic through a session
    save          Saves the active datastores
    sessions      Dump session listings and display information about sessions
    set           Sets a context-specific variable to a value
    setg          Sets a global variable to a value
    sleep         Do nothing for the specified number of seconds
    spool         Write console output into a file as well the screen
    threads       View and manipulate background threads
    unload        Unload a framework plugin
    unset         Unsets one or more context-specific variables
    unsetg        Unsets one or more global variables
    version       Show the framework and console library version numbers


Module Commands
===============

    Command       Description
    -------       -----------
    advanced      Displays advanced options for one or more modules
    back          Move back from the current context
    info          Displays information about one or more modules
    loadpath      Searches for and loads modules from a path
    options       Displays global options or for one or more modules
    popm          Pops the latest module off the stack and makes it active
    previous      Sets the previously loaded module as the current module
    pushm         Pushes the active or list of modules onto the module stack
    reload_all    Reloads all modules from all defined module paths
    search        Searches module names and descriptions
    show          Displays modules of a given type, or all modules
    use           Selects a module by name


Job Commands
============

    Command       Description
    -------       -----------
    handler       Start a payload handler as job
    jobs          Displays and manages jobs
    kill          Kill a job
    rename_job    Rename a job


Resource Script Commands
========================

    Command       Description
    -------       -----------
    makerc        Save commands entered since start to a file
    resource      Run the commands stored in a file


Developer Commands
==================

    Command       Description
    -------       -----------
    edit          Edit the current module or a file with the preferred editor
    log           Displays framework.log starting at the bottom if possible
    reload_lib    Reload one or more library files from specified paths


Database Backend Commands
=========================

    Command           Description
    -------           -----------
    db_connect        Connect to an existing database
    db_disconnect     Disconnect from the current database instance
    db_export         Export a file containing the contents of the database
    db_import         Import a scan result file (filetype will be auto-detected)
    db_nmap           Executes nmap and records the output automatically
    db_rebuild_cache  Rebuilds the database-stored module cache
    db_status         Show the current database status
    hosts             List all hosts in the database
    loot              List all loot in the database
    notes             List all notes in the database
    services          List all services in the database
    vulns             List all vulnerabilities in the database
    workspace         Switch between database workspaces


Credentials Backend Commands
============================

    Command       Description
    -------       -----------
    creds         List all credentials in the database
msf > 
