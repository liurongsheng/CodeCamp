# Node包管理npm、yarn 和 pnpm

[官方文档](https://www.npmjs.com.cn/cli/access)

- `npm -v` // 查看版本
- `npm install -g npm` // 更新自身

## npm 命令备忘

1. `npm ls` // 查看已安装的包，简写
1. `npm list -g --depth 0` 查看已安装的依赖包
1. `npm outdated` 或者 `npm outdated -g` // 查找过时的包
1. `npm update <package-name>` // 更新包
1. `npm cache clean --force` // 清除缓存
1. `npm home <package-name>` // 打开一个包的主页
1. `npm docs <package-name>` // 打开一个包的文档
1. `npm bugs <package-name>` // 打开一个包的bugs列表
1. `npm i -g <package_name>` // 全局安装一个包，简写
1. `npm install --global <package_name>` // 全局安装一个包
1. `npm uninstall <package-name>` // 卸载一个包
1. `npm uninstall <package-name> -g` // 卸载一个全局安装的包
1. `npm uninstall *` // 删除本机所有 node 依赖包

## yarn

1. `yarn global list --depth=0` // 查看全局已安装的包

1. `yarn config get registry` // 查看源的配置
1. `yarn add any-touch@latest --registry=https://registry.npmjs.org/` // 临时修改
1. `yarn config set registry https://registry.npm.taobao.org/` // 持久修改

### yrm管理源

它本身也是 nrm 的一个 Fork 分支

```js
npm install -g yrm
yrm ls
yrm use taobao
yrm add taobao https://registry.npmmirror.com // 太久没有更新了，需要维护下
```

## pnpm

1. `npm install -g pnpm`
1. `npm install` 等同 `pnpm install`
1. `npm i <pkg>` 等同  `pnpm add <pkg>`
1. `npm run <cmd>` 等同 `pnpm <cmd>`

1. `pnpm get registry` // 查看源的配置
1. `pnpm --registry https://registry.npm.taobao.org install any-touch` // 临时修改
1. `pnpm config set registry https://registry.npm.taobao.org` // 持久使用
1. `pnpm config set registry https://registry.npmjs.org` // 还原

### package.json

package.json 文件至少要有两部分内容：

1. name
全部小写，没有空格，可以使用下划线或者横线

2. version
x.x.x 的格式 符合“语义化版本规则”

可选内容

1. description：  描述信息，有助于搜索
1. main:          入口文件，一般都是 index.js
1. scripts：      支持的脚本，默认是一个空的 test
1. keywords：     关键字，有助于在人们使用 npm search 搜索时发现你的项目
1. author：       作者信息
1. license：      默认是 MIT
1. bugs：         当前项目的一些错误信息，如果有的话
1. dependencies    在生产环境中需要用到的依赖
1. devDependencies 在开发、测试环境中用到的依赖

npm install <package_name> --save      表示将这个包名及对应的版本添加到 package.json的 dependencies
npm install <package_name> --save-dev 表示将这个包名及对应的版本添加到 package.json的 devDependencies

校验、打包、构建之类的依赖包都放在 devDependencies

```js
babel-core、babel-loader、babel-preset-env等babel系列
eslint系列、less、webpack、各种loader
```

运行中需要用的依赖包都放在 dependencies

```js
axios、moment、qs、vue、vux、vue-router
weixin-js-sdk
```

### package.json 指定依赖的包版本号

一个完整的版本号组表示为： [主要版本号，次要版本号，补丁版本号]

主要版本号：大改版，无法兼容之前的，增加第一位数字，比如 1.1.2 --> 2.1.2
次要版本号：小版本，增加了新特性，同时不会影响之前的版本，增加中间一位数字，比如 1.0.2 --> 1.1.2
补丁版本号：解决了 bug 或者一些较小的更改，增加最后一位数字，比如 1.0.1 --> 1.0.2

1. 用 ^ 指定范围

允许不会改变最左边的不为零的版本号的版本提升

- ^1.0.0 允许次要、补丁版本升级
- ^0.1.0 允许补丁版本升级
- ^0.0.x 不允许升级

当次要、补丁版本号缺少时会当作 0，但也会灵活处理，即时主版本号为 0 也可以

```js
^1.2.3
1.2.3 <= version < 2.0.0

^0.2.3
0.2.3 <= version < 0.3.0

^0.0.3
0.0.3 <= version < 0.0.4

^1.2.3-beta.2
1.2.3-beta.2 <= version < 2.0.0

^1.x
1.0.0 <= version < 2.0.0

^0.x
0.0.0 <= version < 1.0.0
```

2. 用 ~ 指示范围+

指定了次要版本，允许补丁版本升级。如果没有指定次要版本，允许次要版本升级

```js
~1.2.3
1.2.3 <= version < 1.3.0

~1.2
1.2.0 <= version < 1.3.0

~1
1.0.0 <= version < 2.0.0

~0.2.3
0.2.3 <= version < 0.3.0

~0.2
0.2.0 <= version < 0.3.0

~0
0.0.0 <= version < 1.0.0

~1.2.3-beta.2
1.2.3-beta.2 <= version < 1.3.0
1.2.3版允许高于beta.2的beta版，但1.2.4-beta.2不被允许，因为是属于另一个版本号组的beta版本。
```
