# webpack4升级

yarn create react-app merchants

npm install antd dva promise axios sweetalert2 qs jsrsasign throttle-debounce particles.js
npm install babel-polyfill babel-plugin-transform-runtime 

sweetalert2


BizCharts 基于 G2 的 React 版本封装
npm install bizcharts
https://alibaba.github.io/BizCharts/
https://github.com/alibaba/BizCharts

// 折线上默认显示
<Geom type="line" position="time*val" size={1} color={'#ffbc5a'} >
  <Label content="time*val" formatter={(val) => `单位: ${val}`}/>
</Geom>



## 报错问题

关于react项目中，按照下述方式，在引入路由Router、Route、Link时：

import { Router, Route, Link } from 'react-router'
运行出现下述错误

The prop `history` is marked as required in `Router`, but its value is `undefined`. in Router

是由于Router更新api所导致，具体解决方案，参照React api文档中内容 https://reacttraining.com/react-router/web/api/Route 将路由引入方式作出如下修改即可。

import { BrowserRouter as Router, Route } from 'react-router-dom';
安装使用的依赖由react-router-dom替换react-router。



## 代理
```
// .webpackrc.js

export default {
  "publicPath": "/static/",
  "proxy": {
    "/api": {
       "target": "http://jsonplaceholder.typicode.com/",
       "changeOrigin": true,
       "pathRewrite": { "^/api" : "" }
    }
  },
}

npm start 是开发调试，webpackrc文件会生效，方便前后端独立开发，绕过跨域等问题

npm build 生成的文件，webpackrc文件不生效，需要根据各自的产品环境做反向代理

```
