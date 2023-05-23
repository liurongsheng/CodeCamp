# 开发框架 wepy

## 框架安装

```js
npm install wepy-cli -g
wepy init standard work
cd work
npm install
wepy build --watch
```

## 目录结构

```js
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

## 微信账号体系

- 小程序名称
- 原始ID

微信小程序/公众号/开放平台账号长时间不用被冻结，想再次使用找回时需要原始ID，原始ID已忘记

- 打开用于开发小程序/公众号/开放平台的微信，搜索公众平台安全助手
- 进入公众平台安全助手，选择绑定查询，可以根据微信号/手机号/身份证号进行绑定查询
- 选择微信号绑定查询，可以查询绑定的小程序/公众号/开放平台账号
