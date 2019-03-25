# webpack配置技巧与问题集锦

## webpack4 升级

`yarn create react-app merchants`

`npm install antd dva promise axios sweetalert2 qs jsrsasign throttle-debounce particles.js`

`npm install babel-polyfill babel-plugin-transform-runtime` 

BizCharts 基于 G2 的 React 版本封装

`npm install bizcharts`

https://alibaba.github.io/BizCharts/

https://github.com/alibaba/BizCharts

## 报错问题

关于 react 项目中，按照下述方式，在引入路由 Router、Route、Link 时：

`import { Router, Route, Link } from 'react-router'`

运行出现下述错误

The prop `history` is marked as required in `Router`, but its value is `undefined`. in Router

是由于Router更新api所导致，具体解决方案，参照React api文档中内容 https://reacttraining.com/react-router/web/api/Route 将路由引入方式作出如下修改即可。

`import { BrowserRouter as Router, Route } from 'react-router-dom';`

安装使用的依赖由react-router-dom替换react-router。

## 代理配置
```
// .webpackrc.js
export default {
  "publicPath": "/static/",
  "proxy": {
    "/api": {
       "target": "http://jsonplaceholder.typicode.com/",
       "changeOrigin": true,
       "pathRewrite": { 
          "^/api" : "" 
       }
    }
  },
}
```
npm start 是开发调试，webpackrc 文件会生效，方便前后端独立开发，绕过跨域等问题

npm build 生成的文件，webpackrc 文件不生效，需要根据各自的产品环境做反向代理

## 运行开发环境后自动打开浏览器
```
// webpack.dev.conf.js
devServer {
  open: config.dev.autoOpenBrowser,
}
```
这里配置为 true 就可以
