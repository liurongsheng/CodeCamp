# webpack5构建性能优化

## 环境分离

- 基础配置文件：webpack.base.js，主要配置了基础的 loader 和 plugin 等

- 本地开发配置文件：webpack.dev.js，主要配置了 devServer 和样式、图片资源 loader 等，并 merge 基础配置

- 生产环境配置文件：webpack.prod.js，主要配置了样式、图片资源 loader 以及资源压缩和样式抽离等，并 merge 基础配置

优化点

- 热加载相关配置，从 base 移到 dev 配置中，生产环境中不需要热更新 `new webpack.HotModuleReplacementPlugin()`

- dev 配置中 devtool 类型选择，`inline-source-map` 修改为 `eval-cheap-module-source-map`，map 文件使用内联方式构建速度更快 `devtool: 'eval-cheap-module-source-map'`

- filename 调整：js/[name].[fullhash].js 去掉 hash，本地开发环境启用热更新，不需要 hash（生产环境需要 hash 刷新缓存）
`output: {
  filename: 'js/[name].js',
  path: path.resolve(__dirname, '../dist'),
  publicPath: '/',
}`

## 持久化缓存

base 配置中开启持久化缓存（Webpack5 新特性），首次构建耗时增加 15% 左右，但是二次构建耗时减少 90% 左右

cache: {
  type: 'filesystem'
}

## Loader 相关优化

- 尽量减少 loader，比如使用 Asset modules（Webpack5 新特性）替换 url-loader、file-loader、raw-loader

```js
  // 字体和小于8kb的图片
  {
    test: /\.(woff2?|eot|ttf|otf)(\?.*)?$/,
    type: 'asset',
    parser: {
      dataUrlCondition: {
        maxSize: 8 * 1024,
      },
    }
  }
  // 图片资源
  {
      test: /\.(png|svg|jpg|gif|cur)$/,
      type: 'asset/resource',
      exclude: [path.resolve(__dirname, '../../../assets/svg')],
  }
```

- thread-loader 耗时任务开启多线程

```js
  {
      test: /\.vue$/,
      use: ['thread-loader', 'vue-loader'],
  },
  {
      test: /\.(t|j)s$/,
      exclude: /node_modules/,
      use: ['thread-loader', 'babel-loader'],
  },
  {
      test: /\.(sa|sc|c)ss$/,
      use: ['thread-loader', 'style-loader', 'css-loader', 'sass-loader'
  },
```

## Plugin 相关优化

- 使用 `speed-measure-webpack-plugin` 分析各个 plugin、loader 编译时间

- 尽量减少 plugin，比如 HotModuleReplacementPlugin 只在 dev 开启

- 升级老旧 plugin，比如 terser-webpack-plugin 版本从 2 升级到 5，构建性能直接提升 50% 左右
