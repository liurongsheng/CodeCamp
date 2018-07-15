# [安装ESlint](https://eslint.org/docs/user-guide/getting-started)

先决条件：Node.js（> = 6.14），npm版本3+。

有两种方法可以安装ESLint：本地和全局。

## 本地安装

如果要将ESLint作为项目构建系统的一部分包含在内，我们建议您在本地安装它。您可以使用npm执行此操作：

$ npm install eslint --save-dev
然后，您应该设置配置文件：

$ ./node_modules/.bin/eslint --init
之后，您可以在项目的根目录中运行ESLint，如下所示：

$ ./node_modules/.bin/eslint yourfile.js
您使用的任何插件或可共享配置也必须在本地安装，以便与本地安装的ESLint一起使用。
 
## 全局安装

如果要使ESLint可用于跨所有项目运行的工具，我们建议全局安装ESLint。您可以使用npm执行此操作：

$ npm install -g eslint
然后，您应该设置配置文件：

$ eslint --init
之后，您可以在任何文件或目录上运行ESLint，如下所示：

$ eslint yourfile.js
您使用的任何插件或可共享配置也必须全局安装，以便与全局安装的ESLint一起使用。

注意： eslint --init用于基于每个项目设置和配置ESLint，并将在运行它的目录中执行ESLint及其插件的本地安装。
如果您更喜欢使用ESLint的全局安装，则还必须全局安装配置中使用的所有插件。

### .eslintrc.js配置文件
```
// .eslintrc.js
module.exports = {
    // 指定解析器
    'parse': '',
    // 指定解析器选项
    'parserOptions': {},
    // 指定脚本的运行环境
    'env': {},
    // 别人可以直接使用你配置好的ESLint
    'root': true,
    // 脚本在执行期间访问的额外的全局变量
    'globals': {},
    // 启用的规则及其各自的错误级别
    'rules': {}
};
```
vue-cli创建ESlint实例：
```
// https://eslint.org/docs/user-guide/configuring
module.exports = {
  root: true,
  parserOptions: {
    parser: 'babel-eslint'
  },
  env: {
    browser: true,
  },
  extends: [
    // https://github.com/vuejs/eslint-plugin-vue#priority-a-essential-error-prevention
    // consider switching to `plugin:vue/strongly-recommended` or `plugin:vue/recommended` for stricter rules.
    'plugin:vue/essential', 
    // https://github.com/standard/standard/blob/master/docs/RULES-en.md
    'standard'
  ],
  // required to lint *.vue files
  plugins: [
    'vue'
  ],
  // add your custom rules here
  rules: {
    // allow async-await
    'generator-star-spacing': 'off',
    // allow debugger during development
    'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off'
  }
}
```
### package.json配置
    "babel-eslint": "^8.2.1",
    "eslint": "^4.15.0",
    "eslint-config-standard": "^10.2.1",
    "eslint-friendly-formatter": "^3.0.0",
    "eslint-loader": "^1.7.1",
    "eslint-plugin-import": "^2.7.0",
    "eslint-plugin-node": "^5.2.0",
    "eslint-plugin-promise": "^3.4.0",
    "eslint-plugin-standard": "^3.0.1",
    "eslint-plugin-vue": "^4.0.0",

### webpack配置
```
在webpack.base.conf.js的rules里添加
module: {
    rules: [
    {
      test: /\.(js|vue)$/,
      loader: 'eslint-loader',
      enforce: 'pre',
      include: [resolve('src'), resolve('test')],
      options: {
        formatter: require('eslint-friendly-formatter'),
        emitWarning: !config.dev.showEslintErrorsInOverlay
      }
    }]
}
```