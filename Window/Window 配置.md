# Window 配置

## 关闭 WindowsDefender

本地组策略方法最为便捷：

gpedit.msc

计算机配置--管理模板--Windows 组件--Windows Defender 防病毒程序
--关闭 Windows Defender 防病毒程序，配置为已启用

## 让 Win10 右下角的时间显示秒

1. 按下 Win+R 组合键，打开运行窗口，输入 regedit，点击确定
1. 在注册表编辑器中，找到 `HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced` 这个路径，右键单击空白处，选择新建 DWORD（32位）值
1. 把新建的值命名为 `ShowSecondsInSystemClock`，双击它，把数值数据改为 1，点击确定
1. 关闭注册表编辑器，重启电脑(或者注销用户)，就可以看到右下角的时间显示秒了
