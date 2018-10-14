# Win10离线安装.NET Framework 3.5

直接安装离线包报错 Microsoft.NET Framework 3.5.exe  错误: 0x800f0950

- 保持 winWindows Update 的启动类型为自动 services.msc
- 找到本机的 iso 镜像文件，并右键加载为本地磁盘
- 在 控制面板\程序\程序和功能  启动或关闭 Windows 功能中关闭比3.5高级的 .NET Framework 版本
- 命令行执行 `dism.exe /online /enable-feature /featurename:netfx3 /Source:F:\sources\sxs` 其中 F: 为加载的虚拟本地磁盘盘符

Microsoft Windows [版本 10.0.17134.285]
(c) 2018 Microsoft Corporation。保留所有权利。

C:\Users\Administrator>dism.exe /online /enable-feature /featurename:netfx3 /Source:F:\sources\sxs

部署映像服务和管理工具
版本: 10.0.17134.1

映像版本: 10.0.17134.285

启用一个或多个功能
[==========================100.0%==========================]
操作成功完成。

C:\Users\Administrator>