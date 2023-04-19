# Chrome使用技巧

## 重装系统找回收藏夹

把原系统 `C:\Users\Administrator\AppData\Local\Google\Chrome\User Data\Default` 目录下的

- Bookmarks
- Bookmarks.bak

两个文件复制到新系统同路径下重启浏览器就可以了

## chrome 设置验证等级

- chrome://flags/#extension-content-verification

## Chrome 浏览器中配置地址栏不隐藏 http

1. 地址栏输入 chrome://flags/
1. 搜索找到 `Omnibox on-focus suggestions for the contextual Web`，并设置为【Enabled】
1. 根据提示 relaunch 浏览器
1. 浏览器重启后，在地址栏右键，弹出菜单中点击 总是显示完整网址

特别注意：修改配置重启是不会生效的，需要点击地址栏选择显示完整网址才会生效

## 插件

- chrome跨域相关

    [allow-control-allow-origi](https://chrome.google.com/webstore/detail/allow-control-allow-origi/nlfbmbojpeacfghkpbjhddihlkkiljbi?hl=zh-CN)

    [Moesif Origin & CORS Changer](https://chrome.google.com/webstore/detail/moesif-origin-cors-change/digfbfaphojjndkpccljibejjbppifbc?hl=zh-CN)

## 历史版本下载

- [upToDown.com](https://google-chrome.en.uptodown.com/windows/versions)

从 88 版本开始，已经移除了对 flash 的支持，用插件也不行，87.0.4280.141，是最后一个版本支持flash的版本
