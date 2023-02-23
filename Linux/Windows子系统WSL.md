# 通俗的理解Windows 子系統 Linux 版

Windows子系统Linux版（Windows Subsystem for Linux，WSL）是一种由微软开发的技术，它允许在Windows操作系统中运行Linux二进制文件（即Linux应用程序）

通过WSL，您可以在Windows上运行常见的Linux工具和命令行界面（如Bash、grep、sed等），并使用它们与本地Windows应用程序进行交互

WSL本质上是一个在Windows操作系统上运行的虚拟机，它支持多个不同的Linux发行版，如Ubuntu、Debian等。这些Linux发行版是作为应用程序包安装在Windows系统中的，而不是作为完整的虚拟机镜像

通过WSL，用户可以在Windows操作系统上享受Linux的优势，如强大的命令行工具、包管理器和开发环境，而无需在计算机上安装另一个操作系统。这使得WSL成为开发人员和系统管理员的理想选择，特别是在需要同时在Windows和Linux系统上进行开发和维护的情况下

## 要判断当前系统是否是 WSL

1. 通过 Windows 的 PowerShell 用命令 `(Get-Command wsl).Source` 来检测它。如果该命令返回 ExternalScript 字符串，表明 WSL 已正确安装

1. 通过 Windows 的 cmd 用 命令 `wsl -l -v` 来检测它。如果该命令返回 WSL 名称，则表明你正在运行 WSL；如果不是，则表明你目前不在 WSL 环境中

## WSL1/2版本对比

[WSL1和WSL2的对比](https://learn.microsoft.com/zh-tw/windows/wsl/compare-versions)

## 使用

- 方法一：登录 [微软商店](https://apps.microsoft.com/store/apps?hl=zh-cn&gl=cn) 搜索 `wsl`
- 方法二(推荐)：使用命令行 PowerShell 下 `wsl --list --online` 列出可用的 Linux 發行版本，使用`wsl --install -d <DistributionName>` 安装发行版本，如果出现错误，`wsl --update` 更新一下环境

```shell
wsl --list --online // 列出可用的 Linux 发行版本
wsl --install -d <DistributionName> 以安装散发版本
wsl --unregister <DistributionName> // 移除发行版本
wsl --list --verbose // 列出已安装的 Linux 发行版本
wsl --status // 检查 WSL 状态
wsl --version // 检查 WSL 版本
wsl --update // 更新 WSL
wsl -u <Username>, wsl --user <Username> // 以指定的使用者身分执行WSL，请将取代 <Username> 为存在于WSL 散发套件中的使用者名称
```

- wsl --install -d Ubuntu 22.04 LTS
- wsl --install -d Ubuntu

## 错误说明(https://learn.microsoft.com/zh-cn/windows/wsl/troubleshooting)