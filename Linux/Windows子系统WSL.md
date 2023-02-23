# 通俗的理解Windows 子系統 Linux 版

Windows子系统Linux版（Windows Subsystem for Linux，WSL）是一种由微软开发的技术，它允许在Windows操作系统中运行Linux二进制文件（即Linux应用程序）

通过WSL，您可以在Windows上运行常见的Linux工具和命令行界面（如Bash、grep、sed等），并使用它们与本地Windows应用程序进行交互

WSL本质上是一个在Windows操作系统上运行的虚拟机，它支持多个不同的Linux发行版，如Ubuntu、Debian等。这些Linux发行版是作为应用程序包安装在Windows系统中的，而不是作为完整的虚拟机镜像

通过WSL，用户可以在Windows操作系统上享受Linux的优势，如强大的命令行工具、包管理器和开发环境，而无需在计算机上安装另一个操作系统。这使得WSL成为开发人员和系统管理员的理想选择，特别是在需要同时在Windows和Linux系统上进行开发和维护的情况下

## 要判断当前系统是否是 WSL

1. 通过 Windows 的 PowerShell 用命令 `(Get-Command wsl).Source` 来检测它。如果该命令返回 ExternalScript 字符串，表明 WSL 已正确安装

1. 通过 Windows 的 cmd 用 命令 `wsl -l -v` 来检测它。如果该命令返回 WSL 名称，则表明你正在运行 WSL；如果不是，则表明你目前不在 WSL 环境中
