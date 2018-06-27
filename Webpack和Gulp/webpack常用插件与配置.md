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