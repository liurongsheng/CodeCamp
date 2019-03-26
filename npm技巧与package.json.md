# npm 技巧与常用的 npm 包

[官方文档](https://www.npmjs.com.cn/cli/access)

npm install -g npm // 更新自身

npm -v // 查看版本

## npm 技巧
1. npm outdated 或者 npm outdated -g 来查找过时的模块
2. npm home <package-name> 打开一个模块的主页
3. npm docs <package-name> 打开一个模块的文档
4. npm bugs <package-name> 打开一个模块的bugs列表
5. npm uninstall <package-name> 卸载一个模块
```
Package  Current   Wanted  Latest  Location
moment   2.22.2    2.24.0  2.24.0  scenic
```
第一个是当前 node_modules 中该模块的版本，
第二个是 package.json 文件中声明的版本，
第三个是远程仓库最新的版本。

只有当前模块版本低于远程，package.json 中的版本语义规则满足情况，才能更新成功

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
```
babel-core、babel-loader、babel-preset-env等babel系列
eslint系列、less、webpack、各种loader
```

运行中需要用的依赖包都放在 dependencies
```
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
```
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
```
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
