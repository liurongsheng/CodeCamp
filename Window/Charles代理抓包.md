# Charles代理抓包

fiddler代理抓包在捕捉 https 时设置设置证书还是无法摆脱 443 的问题，选用 Charles 可以有效解决

[下载地址](https://www.charlesproxy.com/latest-release/download.do)

- Proxy 
  - SSL Proxying Settings
    - SSL Proxying
      - Enable SSL Proxying 勾选
      - Location 区域新增 Host:*; Port:443
        
- Proxy
  - Proxy Settings
    - HTTP Proxy 设置 Port:8888
    
  
手机设置 
代理选择手动
  主机号设置为 本机 IP 地址，端口选择设置的 8888，其他默认
  
## Genymotion 模拟器抓包

- 开启网络功能开关
- 安卓系统设置-WlAN-WiredSSID
  按住2秒，选中弹出的对话框中修改网络
- 设置高级设置-代理为手动-代理服务器主机名为本机IP地址-代理服务器端口为fiddler设置的监听端口-IP设置为DHCP即可

