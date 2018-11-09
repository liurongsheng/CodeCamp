# webpack 常用的 loader 和 plugin：

## Loader 列表
```
less-loader, sass-loader：处理样式
url-loader, file-loader：两个都必须用上。否则超过大小限制的图片无法生成到目标文件夹中
babel-loader，babel-preset-es2015，babel-preset-react：js 处理，转码
expose-loader： 将 js 模块暴露到全局
```

## Plugin 列表
```
NormalModuleReplacementPlugin：匹配 resourceRegExp，替换为 newResource
ContextReplacementPlugin：替换上下文的插件
IgnorePlugin：不打包匹配文件
PrefetchPlugin：预加载的插件，提高性能
ResolverPlugin：替换上下文的插件
DedupePlugin：打包的时候删除重复或者相似的文件
MinChunkSizePlugin：把多个小模块进行合并，以减少文件的大小
LimitChunkCountPlugin：限制打包文件的个数
MinChunkSizePlugin：根据 chars 大小，如果小于设定的最小值，就合并这些小模块，以减少文件的大小
OccurrenceOrderPlugin：根据模块调用次数，给模块分配 ids，常被调用的 ids 分配更短的 id，
                       使得 ids 可预测，降低文件大小，该模块推荐使用
UglifyJsPlugin：压缩 js
CommonsChunkPlugin：多个 html 共用一个 js 文件(chunk)
HotModuleReplacementPlugin：模块热替换么，如果不在 dev-server 模式下，
                            需要记录数据，recordPath，生成每个模块的热更新模块
ProgressPlugin：编译进度
NoErrorsPlugin：报错但不退出 webpack 进程
HtmlWebpackPlugin：生成 html
```

## 扩展命令
--watch 自动更新
--progress 显示打包进度
--display-modules 列出打包模块
--display-reasons 列出打包原因
--p 压缩混淆脚本

## WebStorm 在 create-react-app 中显示打包进度条
```console
npm i -D progress-bar-webpack-plugin
```
修改 Webpack config文件 `config\webpack.config.prod.js`

```
var ProgressBarPlugin = require('progress-bar-webpack-plugin');

...

plugins: [
  new ProgressBarPlugin()
]
```

现在可以在 VS Code 编译器中使用，WebStorm 中还是有问题  [项目 issues](https://github.com/clessg/progress-bar-webpack-plugin/issues/17)

This is because the plugin is disabled if the output is not a TTY
输出不是TTY，插件会被禁用，此时需要解决模拟 TTY 输出

注意当前版本： "progress-bar-webpack-plugin": "^1.11.0"

需要修改源代码 node_modules\progress-bar-webpack-plugin\index.js 第10行 `var stream = options.stream || process.stderr;`
```
var stream = options.stream;
if (!stream) {
  stream = process.stderr;
  if (!stream.isTTY) {
    var tty = require('tty').WriteStream.prototype;
    Object.keys(tty).forEach(function (key) {
      process.stderr[key] = tty[key];
    })
    process.stderr.columns = 80;
  }
}
```
这段代码在 WebStorm 中还是有问题，不支持清屏，所以进度条会一直输出，导致多个进度条同时存在。

修改 webpack.config.prod.js 为 ProgressBarPlugin 携带参数 `stream: process.stdout`
```
plugins: [
  new ProgressBarPlugin({stream: process.stdout}),
]
```
修改源代码 第10行
```
var stream = options.stream || process.stderr;
if (!process.stdout.isTTY) {
  process.stdout.isTTY = true;
  process.stdout.columns = 80;
  process.stdout.cursorTo = () => { process.stdout.write('\r') };
  process.stdout.clearLine = () => {};
}
```
在 WebStorm 下完美运行

### Options

Accepts almost all of the same options as [node-progress](https://github.com/tj/node-progress#options).

- `format` the format of the progress bar
- `width` the displayed width of the progress bar defaulting to total
- `complete` completion character defaulting to "="
- `incomplete` incomplete character defaulting to " "
- `renderThrottle` minimum time between updates in milliseconds defaulting to 16
- `clear` option to clear the bar on completion defaulting to true
- `callback` optional function to call when the progress bar completes
- `stream` the output stream defaulting to stderr
- `summary` option to show summary of time taken defaulting to true
- `summaryContent` optional custom summary message if summary option is false
- `customSummary` optional function to display a custom summary (passed build time)

The `format` option accepts the following tokens:

- `:bar` the progress bar itself
- `:current` current tick number
- `:total` total ticks
- `:elapsed` time elapsed in seconds
- `:percent` completion percentage
- `:msg` current progress message

The default format uses the `:bar` and `:percent` tokens.

Use [chalk](https://github.com/chalk/chalk) to sprinkle on a few colors.

To include the time elapsed and prevent the progress bar from being cleared on build completion:

```javascript
new ProgressBarPlugin({
  format: '  build [:bar] ' + chalk.green.bold(':percent') + ' (:elapsed seconds)',
  clear: false
})
```
