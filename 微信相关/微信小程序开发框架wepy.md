# 开发框架 wepy

## 框架安装
```console
npm install wepy-cli -g
wepy init standard myproject
cd myproject
npm install
wepy build --watch
```
## 目录结构
```
├── dist                   小程序运行代码目录（该目录由WePY的build指令自动编译生成，请不要直接修改该目录下的文件）
├── node_modules           
├── src                    代码编写的目录（该目录为使用WePY后的开发目录）
|   ├── components         WePY组件目录（组件不属于完整页面，仅供完整页面或其他组件引用）
|   |   ├── com_a.wpy      可复用的WePY组件a
|   |   └── com_b.wpy      可复用的WePY组件b
|   ├── pages              WePY页面目录（属于完整页面）
|   |   ├── index.wpy      index页面（经build后，会在dist目录下的pages目录生成index.js、index.json、index.wxml和index.wxss文件）
|   |   └── other.wpy      other页面（经build后，会在dist目录下的pages目录生成other.js、other.json、other.wxml和other.wxss文件）
|   └── app.wpy            小程序配置项（全局数据、样式、声明钩子等；经build后，会在dist目录下生成app.js、app.json和app.wxss文件）
└── package.json           项目的package配置 
```

## 语法高亮
WebStorm/PhpStorm
1. 打开Settings，搜索Plugins，搜索Vue.js插件并安装。
2. 打开Settings，搜索File Types，找到Vue.js Template，在Registered Patterns添加*.wpy，即可高亮。

Sublime
1. 打开Sublime->Preferences->Browse Packages..进入用户包文件夹。
2. 在此文件夹下打开cmd，运行git clone git@github.com:vuejs/vue-syntax-highlight.git，无GIT用户可以直接下载zip包解压至当前文件夹。
3. 关闭.wpy文件重新打开即可高亮

VS Code
1. 在 Code 里先安装 Vue 的语法高亮插件 Vetur。
2. 打开任意 .wpy 文件。
3. 点击右下角的选择语言模式，默认为纯文本。
4. 在弹出的窗口中选择 .wpy 的配置文件关联...。
5. 在选择要与 .wpy 关联的语言模式 中选择 Vue。
6. 在VS Code编辑器设置中设置。 //文件-首选项-设置-settings.json settings.json "files.associations": { "*.wpy": "vue" 

## 
