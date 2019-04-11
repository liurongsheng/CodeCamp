# 常用 npm 包集锦

## 工具类 npm 包

### [npm-check-updates](https://github.com/tjunnone/npm-check-updates)

检查升级 package.json 依赖

>npm install -g npm-check-updates

执行`ncu -u`更新

### [axios](https://github.com/axios/axios)

基于Promise的HTTP客户端，用于浏览器和node.js

### CSS 预处理器（包括LESS，SASS，Stylus和PostCSS）

为确保一致的提取和处理，建议从根App.vue组件导入全局独立样式文件，例如：

// App.vue
<style src="./styles/global.less" lang="less"></style>
请注意，您应该只对自己为应用程序编写的样式执行此操作。对于现有的库，
例如 Bootstrap 或 Semantic UI，您可以将它们放在里面/static并直接引用它们index.html。
这样可以避免额外的构建时间，也可以更好地进行浏览器缓存

SASS:

`npm install sass-loader node-sass --save-dev`

在 *.vue 的 lang 属性在组件内部使用预处理器<style>：
```
<style lang="scss">
/* write SASS! */
</style>
```
- lang="scss" 对应于CSS-superset语法（带花括号和分号）
- lang="sass" 对应于基于缩进的语法

## [qrcode.react](https://www.npmjs.com/package/qrcode.react)
生成二维码
`npm install qrcode.react`
使用非常简单
```
import React from 'react';
import QRCode from 'qrcode.react';

React.render(
  <QRCode value="http://facebook.github.io/react/" />,
  mountNode
);
```

## [webpackbar](https://www.npmjs.com/package/webpackbar)

终端输出进度条

`npm install webpackbar -D`

webpack.config.js
```
const webpack = require('webpack');
const WebpackBar = require('webpackbar');
 
module.exports = {
  context: path.resolve(__dirname),
  devtool: 'source-map',
  entry: './entry.js',
  output: {
    filename: './output.js',
    path: path.resolve(__dirname)
  },
  plugins: [
    new WebpackBar()
  ]
};
```

## [mini-css-extract-plugin](https://www.npmjs.com/package/mini-css-extract-plugin)

css 抽离

`npm install --save-dev mini-css-extract-plugin`

```
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

```

## [happypack](https://www.npmjs.com/package/happypack)

多进程编译

`npm install --save-dev happypack`

```
const HappyPack = require('happypack');
 
exports.module = {
  rules: [
    {
      test: /.js$/,
      // 1) replace your original list of loaders with "happypack/loader":
      // loaders: [ 'babel-loader?presets[]=es2015' ],
      use: 'happypack/loader',
      include: [ /* ... */ ],
      exclude: [ /* ... */ ]
    }
  ]
};
 
exports.plugins = [
  // 2) create the plugin:
  new HappyPack({
    // 3) re-add the loaders you replaced above in #1:
    loaders: [ 'babel-loader?presets[]=es2015' ]
  })
];
```

## [postcss-px-to-viewport](https://github.com/evrone/postcss-px-to-viewport)

在 CSS 文件中直接写 px 根据配置，在编译时自动装换为 vm

如果你的样式需要做根据视口大小来调整宽度，这个脚本可以将你 CSS 中的 px 单位转化为 vw，1vw等于1/100视口宽度

`npm install postcss-px-to-viewport --save-dev`

{
  unitToConvert: 'px',
  viewportWidth: 320,
  unitPrecision: 5,
  propList: ['*'],
  viewportUnit: 'vw',
  fontViewportUnit: 'vw',
  selectorBlackList: [],
  minPixelValue: 1,
  mediaQuery: false,
  replace: true,
  exclude: [],
  landscape: false,
  landscapeUnit: 'vw',
  landscapeWidth: 568
}
```
unitToConvert (String) 需要转换的单位，默认为"px"
viewportWidth (Number) 设计稿的视口宽度
unitPrecision (Number) 单位转换后保留的精度
propList (Array) 能转化为vw的属性列表
传入特定的CSS属性；
可以传入通配符""去匹配所有属性，例如：['']；
在属性的前或后添加"*",可以匹配特定的属性. (例如['position'] 会匹配 background-position-y)
在特定属性前加 "!"，将不转换该属性的单位 . 例如: ['*', '!letter-spacing']，将不转换letter-spacing
"!" 和 ""可以组合使用， 例如: ['', '!font*']，将不转换font-size以及font-weight等属性
viewportUnit (String) 希望使用的视口单位
fontViewportUnit (String) 字体使用的视口单位
selectorBlackList (Array) 需要忽略的CSS选择器，不会转为视口单位，使用原有的px等单位。
如果传入的值为字符串的话，只要选择器中含有传入值就会被匹配
例如 selectorBlackList 为 ['body'] 的话， 那么 .body-class 就会被忽略
如果传入的值为正则表达式的话，那么就会依据CSS选择器是否匹配该正则
例如 selectorBlackList 为 [/^body$/] , 那么 body 会被忽略，而 .body 不会
minPixelValue (Number) 设置最小的转换数值，如果为1的话，只有大于1的值会被转换
mediaQuery (Boolean) 媒体查询里的单位是否需要转换单位
replace (Boolean) 是否直接更换属性值，而不添加备用属性
exclude (Array or Regexp) 忽略某些文件夹下的文件或特定文件，例如 'node_modules' 下的文件
如果值是一个正则表达式，那么匹配这个正则的文件会被忽略
如果传入的值是一个数组，那么数组里的值必须为正则
landscape (Boolean) 是否添加根据 landscapeWidth 生成的媒体查询条件 @media (orientation: landscape)
landscapeUnit (String) 横屏时使用的单位
landscapeWidth (Number) 横屏时使用的视口宽度
```

## React Native 常用开源包

### [react-native-splash-screen](https://github.com/crazycodeboy/react-native-splash-screen)

用于React Native启动屏，解决Android和iOS启动白屏问题。

`npm i react-native-splash-screen --save`

### [react-native-image-crop-picker](https://github.com/ivpusic/react-native-image-crop-picker)

实现了本地相册和照相机来采集图片，并且提供多选、图片裁剪等功能，支持iOS和Android两个平台

`npm i react-native-splash-screen --save`

### [react-native-svg](https://github.com/react-native-community/react-native-svg)

对svg的标签解析成图片

`npm install react-native-svg --save`

`react-native link react-native-svg`

```
react-native-svg >= 3.2.0 only supports react-native >= 0.29.0
react-native-svg >= 4.2.0 only supports react-native >= 0.32.0
react-native-svg >= 4.3.0 only supports react-native >= 0.33.0
react-native-svg >= 4.4.0 only supports react-native >= 0.38.0 and react >= 15.4.0
react-native-svg >= 4.5.0 only supports react-native >= 0.40.0 and react >= 15.4.0
react-native-svg >= 5.1.8 only supports react-native >= 0.44.0 and react == 16.0.0-alpha.6
react-native-svg >= 5.2.0 only supports react-native >= 0.45.0 and react == 16.0.0-alpha.12
react-native-svg >= 5.3.0 only supports react-native >= 0.46.0 and react == 16.0.0-alpha.12
react-native-svg >= 5.4.1 only supports react-native >= 0.47.0 and react == 16.0.0-alpha.12
react-native-svg >= 5.5.1 only supports react-native >= 0.50.0 and react == 16.0.0
react-native-svg >= 6.0.0 only supports react-native >= 0.50.0
react-native-svg >= 7.0.0 only supports react-native >= 0.57.4
react-native-svg >= 8.0.0 only supports react-native >= 0.57.4
```

### [react-native-device-info](https://github.com/rebeccahughes/react-native-device-info)

显示React Native的设备信息

### react-native-video
```
Version 4.x requires react-native >= 0.57.0
Version 3.x requires react-native >= 0.40.0
```
