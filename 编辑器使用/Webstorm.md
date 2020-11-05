# Webstorm 常用设置

## 激活与汉化
[激活与汉化文档](/编辑器使用/Jetbrains系列软件激活与汉化.md)

## 文件-设置

快捷键 选择Eclipse
```
  快速复制当前行：
    设置名称：`Duplicate Line or Selection 重复行或选中区域` Ctrl+D  移除其他
```

编辑器-Font-大小设置为14
编辑器-CodeStyle-设置对应类型缩进

## 主题优化
利用 Material Theme UI 项目
[开源地址](https://github.com/ChrisRM/material-theme-jetbrains)

设置选择 Plugins 安装 Material Theme UI 插件，根据提示重启编辑器

可以通过 工具-Material Theme-Material Theme Chooser切换主题 
或者通过 设置-编辑器-切换配色方案选择配色 
- 配色：`Atom One Dark` 
- 字体：`Dark Mono`
- 字号：16 行距 1.2

## 修改拼写校验
设置 - 编辑器 - Inspections - 内容滚动框 拉到最下方 - 拼写

## 代码风格
ESLint 中建议语句结尾去除分号 ；，使用 单引号替换双引号

---
在 文件 - 设置 - 编辑器 - Code Style - JavaScript 中
Punctuation 中设置 (不使用) 用分号终止语句 (始终)
使用 (单一) 引号 (始终)
---