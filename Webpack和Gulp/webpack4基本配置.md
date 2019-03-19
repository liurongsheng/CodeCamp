## webpack4基本配置 
@webpack.base.conf.js
```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports = {
  entry: {
    bundle: path.resolve(__dirname, '../src/index.js')
  },
  output: {
    path: path.resolve(__dirname, '../dist'),
    filename: '[name].[hash].js'
  },
  module: {
    rules: [
      
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.resolve(__dirname, '../index.html')
    })
  ]
};
```

@webpack.dev.conf.js
```
const merge = require('webpack-merge');
const path = require('path');
const baseConfig = require('./webpack.base.conf');
module.exports = merge(baseConfig, {
  mode: 'development',
  devtool: 'inline-source-map',
  devServer: {
    contentBase: path.resolve(__dirname, '../dist'),
    open: true
  }
});
```

@webpack.prod.conf.js
```
const merge = require('webpack-merge');
const CleanWebpackPlugin = require('clean-webpack-plugin');
const path = require('path');
const baseConfig = require('./webpack.base.conf');
module.exports = merge(baseConfig, {
  mode: 'production',
  devtool: 'source-map',
  module: {
    rules: []
  },
  plugins: [
    new CleanWebpackPlugin(['dist/'], {
      root: path.resolve(__dirname, '../'),
      verbose: true,
      dry: false
    })
  ]
});
```

@build.js
```
const webpack = require('webpack');
const config = require('./webpack.prod.conf');

webpack(config, (err, stats) => {
  if (err || stats.hasErrors()) {
    // 在这里处理错误
    console.error(err);
    return;
  }
  // 处理完成
  console.log(stats.toString({
    chunks: false,  // 使构建过程更静默无输出
    colors: true    // 在控制台展示颜色
  }));
});
```

@npm scripts
```
"build": "node build/build.js",
"dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js"
```

### babel-loader
首先安装 babel-loader、babel-preset-env 和 babel-core。

需要注意的是，如果你的 babel-loader 是 7.x 版本的话，你的 babel-core 必须是 6.x 版本；

如果你的 babel-loader 是 8.x 版本的话，你的 babel-core 必须是 7.x 版本。如果不这样的话，Webpack 会报错。

`npm i babel-loader@7 babel-core babel-preset-env -D`

webpack.base.conf.js 的 module.rules 中新增如下对象：
```
{
  test: /\.js$/,
  use: 'babel-loader',
  exclude: /node_modules/
}
```
### babelrc
新建 .babelrc 文件，添加 babel-preset-env
```
{
  "presets": [
    ["env", {
      "modules": false,
      "targets": {
        "browsers": ["> 1%", "last 2 versions", "not ie <= 8"]
      }
    }]
  ]
}
```
### vue-loader
为了使用 Vue 单文件组件，我们需要对 .vue 文件进行处理，使用 vue-loader 

安装 vue-loader、css-loader、vue-style-loader 和 vue-template-compiler

`npm i vue-loader css-loader vue-style-loader vue-template-compiler -D`

webpack.base.conf.js 的 module.rules 中新增如下对象：
```
{
  test: /\.vue$/,
  loader: 'vue-loader'
},
{
  test: /\.css$/,
  use: ['vue-style-loader', 'css-loader']
}
```

需要配置一个插件，然后还需要配置 resolve.alias 别名，不然 Webpack 没法找到 Vue 模块。

配置插件，首先在文件头部引入：

const VueLoaderPlugin = require('vue-loader/lib/plugin');

然后在 plugins 数组中添加这个插件对象：

new VueLoaderPlugin(),

随后我们还要配置别名，将 resolve.alias 配置为如下对象：

{
  'vue$': 'vue/dist/vue.esm.js',
  '@': path.resolve(__dirname, '../src'),
}

这可以使得 Webpack 很方便的找到 Vue，
我们在 JavaScript 文件中引入依赖的时候，也可以方便地使用 @ 来代替 src，省去了写文件路径的麻烦。

## autoprefixer 插件

使用 postcss 的 autoprefixer 插件为我们的 css 代码自动添加前缀以适应不同的浏览器

`npm i postcss-loader autoprefixer -D`

webpack.base.conf.js 的 module.rules 中修改为
```
{
  test: /\.css$/,
  use: ['vue-style-loader', 'css-loader', 'postcss-loader']
}
```
根目录新建 postcss.config.js 文件
```
module.exports = {
  plugins: [
    require('autoprefixer')
  ]
}
```

## 开启热更新

修改 webpack.dev.conf.js，在 devServer 属性中设置 hot 的值为 true，这就代表开启了热更新。
但是只这样做还不够，需要我们添加一个插件，继续修改 webpack.dev.conf.js。

设置其 plugins 属性如下：
```
const webpack = require('webpack');
// 在文件头部引入 webpack 依赖
[
  new webpack.HotModuleReplacementPlugin()
]
```
这就开启了 css 热更新（因为 vue-style-loader 封装了 style-loader，热更新开箱即用）,

但是 JavaScript 热更新还不能用，每次修改代码我们都会刷新浏览器，所以我们需要继续配置

为了使得 JavaScript 模块也能进行 HMR，我们需要在我们的 入口文件（index.js） 的底部添加如下代码：
```
if (module.hot) {
  module.hot.accept();
}
```
接下来就可以进行 HMR 了。

## 第三方库单独打包

每次我们对项目进行打包时，我们都会把引用的第三方依赖给打包一遍，比如 Vue、Vue-Router、React 等等。

但是这些库的代码基本都是不会变动的，我们没必要每次打包都构建一次，所以我们最好将这些第三方库提取出来单独打包，
这样有利于减少打包时间。官方插件是 DllPlugin，但是这个插件配置比较繁琐。

网上有人推荐一个比较好用的插件 —— autodll-webpack-plugin，确实很好用。

`npm i autodll-webpack-plugin -D`

在 webpack.base.conf.js 中引入：

`const AutoDllPlugin = require('autodll-webpack-plugin');`

在 plugins 属性中添加这个插件：
```
new AutoDllPlugin({
  inject: true, // will inject the DLL bundle to index.html
  debug: true,
  filename: '[name]_[hash].js',
  path: './dll',
  entry: {
    vendor: ['vue', 'vue-router', 'vuex']
  }
})
```
1. inject 为 true，插件会自动把打包出来的第三方库文件插入到 HTML。
2. filename 是打包后文件的名称。
3. path 是打包后的路径。
4. entry 是入口
5. vendor 是你指定的名称，数组内容就是要打包的第三方库的名称，不要写全路径，Webpack 会自动去 node_modules 中找到的。

每次打包，这个插件都会检查注册在 entry 中的第三方库是否发生了变化，
如果没有变化，插件就会使用缓存中的打包文件，减少了打包的时间，这时 Hash 也不会变化。

## 提取共同代码
splitChucksPlugin 插件，这是 Webpack 自带的，不用安装第三方依赖

webpack.base.conf.js 的 plugins 属性中添加如下插件对象;

`new webpack.optimize.SplitChunksPlugin()`

这代表你将使用默认的提取配置来提取你的公共代码，如果你不想使用默认配置，请给插件构造函数传入配置对象。

[大神指导配置](https://lengxing.club/2018/09/18/2018-09-18) https://lengxing.club/2018/09/18/2018-09-18

## 抽取 CSS 到单文件
使用的是 mini-css-extract-plugin 插件

`npm i mini-css-extract-plugin -D`

在 webpack.base.conf.js 中引入：

`const MiniCssExtractPlugin = require('mini-css-extract-plugin')`

然后当你要抽取 CSS 的时候（比如生产环境打包），你就把原来配置文件中的所有 vue-style-loader 
替换为 MiniCssExtractPlugin.loader，其他的什么 css-loader、stylus-loader 等等都不要动。

最后，修改 plugins 选项，插入如下插件：
```
new MiniCssExtractPlugin({
  filename: "[name].css",
  chunkFilename: "[id].css"
})
```
打包之后，你会发现所有的 CSS 代码都被抽取到了一个单独的 CSS 文件当中。
