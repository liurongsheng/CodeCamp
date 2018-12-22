# fiddler代理抓包

[下载地址](https://www.telerik.com/download/fiddler)

- Tools 
  - Options
    - Ignore server certificate errors(unsaft) 勾选
    
- Connections
  - 修改代理端口：9999
  - Allow remote computers to connect
  
手机设置 
代理选择手动
  主机号设置为 本机 IP 地址，端口选择设置的 9999，其他默认
  

[文档教程](http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/ConfigureFiddler) http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/ConfigureFiddler

[插件列表](https://www.telerik.com/fiddler/add-ons) https://www.telerik.com/fiddler/add-ons

生成手机端 https 证书插件 https://telerik-fiddler.s3.amazonaws.com/fiddler/addons/fiddlercertmaker.exe


## Genymotion 模拟器抓包

- 开启网络功能开关
- 安卓系统设置-WlAN-WiredSSID
  按住2秒，选中弹出的对话框中修改网络
- 设置高级设置-代理为手动-代理服务器主机名为本机IP地址-代理服务器端口为fiddler设置的监听端口-IP设置为DHCP即可

