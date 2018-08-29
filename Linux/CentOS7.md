# CentOS7

## 切换图形界面

cat /etc/inittab 
```
# 关键信息
# multi-user.target: analogous to runlevel 3 //命令行界面
# graphical.target: analogous to runlevel 5 //图形界面

```
systemctl get-default //获取当前启动的界面类型

# 选择界面模式
```
systemctl set-default multi-user.target //设置命令行界面
systemctl set-default graphical.target //设置图形界面

reboot //重启生效
```

## 修改系统编码支持中文

vim /etc/locale.conf
`LANG="zh_CN.UTF-8" SYSFONT="latarcyrheb-sun16" SUPPORTED="zh_CN.UTF-8:zh_CN:zh"`

reboot //重启生效