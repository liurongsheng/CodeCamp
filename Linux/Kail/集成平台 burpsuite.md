# burpsuite
Burp Suite 是用于攻击web 应用程序的集成平台。
它包含了许多工具，并为这些工具设计了许多接口，以促进加快攻击应用程序的过程。
所有的工具都共享一个能处理并显示HTTP 消息，持久性，认证，代理，日志，警报的一个强大的可扩展的框架。

## 主要模块
1. Target(目标)——显示目标目录结构的的一个功能
2. Proxy(代理)——拦截HTTP/S的代理服务器，作为一个在浏览器和目标应用程序之间的中间人，允许你拦截，查看，修改在两个方向上的原始数据流。
3. Spider(蜘蛛)——应用智能感应的网络爬虫，它能完整的枚举应用程序的内容和功能。
4. Scanner(扫描器)——高级工具，执行后，它能自动地发现web 应用程序的安全漏洞。
5. Intruder(入侵)——一个定制的高度可配置的工具，对web应用程序进行自动化攻击，如：枚举标识符，收集有用的数据，以及使用fuzzing 技术探测常规漏洞。
6. Repeater(中继器)——一个靠手动操作来触发单独的HTTP 请求，并分析应用程序响应的工具。
7. Sequencer(会话)——用来分析那些不可预知的应用程序会话令牌和重要数据项的随机性的工具。
8. Decoder(解码器)——进行手动执行或对应用程序数据者智能解码编码的工具。
9. Comparer(对比)——通常是通过一些相关的请求和响应得到两项数据的一个可视化的“差异”。
10. Extender(扩展)——可以让你加载Burp Suite的扩展，使用你自己的或第三方代码来扩展Burp Suit的功能。
11. Options(设置)——对Burp Suite的一些设置

### 代理
创建代理，配置浏览器（建议安装autoproxy 火狐插件）
Proxy - Options - Intercept - HTTP history

## Target
Site map
Scope

## Spider
Burp Spider 是一个映射 web 应用程序的工具。
它使用多种智能技术对一个应用程序的内容和功能进行全面的清查。
启用和配置spider
Passive Spidering(被动扫描)
表单提交

## Scanner
启动扫描
 active scanning
 Passive Scanning

## Intruder
使用intruder
添加修改载荷参数
攻击类型
attack

## Repeater
Burp Repeater(中继器)是用于手动操作和补发个别HTTP请求，
并分析应用程序的响应一个简单的工具。
您可以发送一个内部请求从Burp任何地方到Repeater(中继器)，
修改请求并且发送它。
基本使用

## comparer
http请求的对比工具

## Decoder
编码和解码工具