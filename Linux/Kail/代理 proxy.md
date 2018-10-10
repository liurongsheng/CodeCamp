# proxy

- 正向代理 forward proxy
- 反向代理 reverse proxy
- 透明代理 transparente proxy

## 正向代理
内部网络通过代理实现访问外部网络
- 访问本无法访问的服务器
- cache 作用
- 客户端访问授权
- 隐藏访问者的行踪

## 反向代理
外部网络通过代理实现访问内部网络提供的服务

## 透明代理
对用户是透明的，用户意识不到防火墙的存在

## 代理工具
- mitmproxy
- burpsuite
- Owasp-zap
- Paros
- Proxystrike
- Vega
- webscarab

### 实现原理
通过指定的默认端口8080上运行代理，截获并修改客户端到web应用程序的数据包

