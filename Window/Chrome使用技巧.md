# Chrome使用技巧

## 重装系统找回收藏夹

把原系统 `C:\Users\Administrator\AppData\Local\Google\Chrome\User Data\Default` 目录下的

- Bookmarks
- Bookmarks.bak

两个文件复制到新系统下重启就可以了

## chrome安装本地crx插件技巧

### 方法一

在Google Chrome的桌面快捷方式的目标中新增` –enable-easy-off-store-extension-install`即可

整体如下：

`C:\Users\Administrator\AppData\Local\Google\Chrome\Application\chrome.exe –enable-easy-off-store-extension-install`

### 方法二 推荐

[下载离线包](http://yurl.sinaapp.com/crx.php)

- 得到 crx 文件，复制为副本改为 .zip 的压缩包，解压
- 使用 chrome 加载已解压的扩展程序找到解压的文件夹导入即可

插件会使用开发者模式运行

## chrome 设置验证等级

- chrome://flags/#extension-content-verification

## 配置 URL 地址栏隐藏 http/https 协议

1. chrome://flags/#omnibox-ui-hide-steady-state-url-scheme-and-subdomains
2. Omnibox UI Hide Steady-State URL Trivial Subdomains
3. 设置为 Disabled 状态
