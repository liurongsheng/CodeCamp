# ChartGPT相关

- OpenAI官网账号注册平台：<https://platform.openai.com/account/api-keys>

- 短信注册平台：<https://sms-activate.org/getNumber>

- 短信注册平台2：[https://www.receivesms.io/]

[模型](https://platform.openai.com/docs/models)

## new Bing

[开发版本下载](https://www.microsoftedgeinsider.com/zh-cn/download)

### new Bing 配置

[修改请求头插件商店地址](https://microsoftedge.microsoft.com/addons/detail/header-editor/afopnekiinpekooejpchnkgfffaeceko)

- 规则类型  选`修改请求头`
- 匹配类型  选`正则表达式`
- 匹配规则 输入`^http(s?)://(.*).bing\.com/(.*)`
- 执行类型  选`常规`
- 头名称  输入`x-forwarded-for`
- 头内容  输入`8.8.8.8`

### 使用页面

[访问地址](https://www.bing.com/search?q=Bing+AI&showconv=1&FORM=hpcodx)

地址栏和搜索/管理搜索引擎

以 %s 代替查询的 URL `{bing:cnBaseURL}search?q=%s&{bing:cvid}{bing:msb}{google:assistedQueryStats}`

修改为 `https//www.bing.com/search?q=%s`

#### 关闭 Microsoft Edge 浏览器推荐设置为默认浏览器的弹窗

访问 `edge://flags/#edge-show-feature-recommendations` 并将其设置为 Disable

### 禁止自动更新

开发版本查看关于 `Microsoft Edge` 的信息的时候自动更新，导致无法使用 Bing AI，错误提示 `Sorry, looks like your network settings are preventing access to this feature.`

解决方式是强制卸载掉当前版本重新安装

禁止 `Microsoft Edge` 自动更新：

- 打开系统服务：右键任务栏 - 任务管理器 - 服务 - 打开服务（底部文字）
- 找到两个 `Microsoft Edge` 更新服务 (edgeupdate/edgeupdatem)
- 右键服务 - 属性 - 启动类型 改为 禁用
- 点击 [应用] 即可

## 微软基于文字生成图像服务 Bing Image Creator

[Bing Image Creator](https://cn.bing.com/create)

## 谷歌

[bard](https://bard.google.com/signup)
