# npm技巧与常用的npm包

npm install -g npm // 更新自身

npm -v // 查看版本

## npm技巧

1. npm outdated 或者 npm outdated -g 来查找过时的模块
2. npm home <package> 打开一个模块的主页
3. npm docs <package> 打开一个模块的文档
4. npm bugs <package> 打开一个模块的bugs列表

## 常用的npm包

### [npm-check-updates](https://github.com/tjunnone/npm-check-updates)

检查升级package.json依赖

>npm install -g npm-check-updates

执行`ncu -u`更新

### [axios](https://github.com/axios/axios)

基于Promise的HTTP客户端，用于浏览器和node.js

### package.json 依赖
一个完整的版本号组表示为： [主要版本号，次要版本号，补丁版本号]

用 ~ 指示范围
指定了次要版本，允许补丁版本升级。如果没有指定次要版本，允许次要版本升级。
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

用 ^ 指定范围
允许不会改变最左边的不为零的版本号的版本提升，也就是说，
1.0.0允许次要、补丁版本升级，0.1.0允许补丁版本升级，^0.0.x 不允许升级。

一个普遍的做法是，^ 适合使用在当开发者从 0.2.4 升级到 0.3.0 可能会做出不兼容的改变时。
一般情况下，假定了在0.2.4 到 0.2.5 不会有不兼容改变，可以有一些新增(但不改变兼容)的改变。

^1.2.3
1.2.3 <= version < 2.0.0

^0.2.3
0.2.3 <= version < 0.3.0

^0.0.3
0.0.3 <= version < 0.0.4

^1.2.3-beta.2
1.2.3-beta.2 <= version < 2.0.0
允许1.2.3 版的高于beta-2 的beta版本

^0.0.3-beta.2
0.0.3-beta.2 <= version < 0.0.4
只允许0.0.3 版的高于beta-2 的版本
当解析带有^的版本范围时，补丁版本号缺少会补 0，但是会灵活的处理，即时主要、次要版本号都为 0 也可以。

能够接受的版本范围

^1.2.x
1.2.0 <= version < 2.0.0

^0.0.x
0.0.0 <= version < 0.1.0

^0.0
0.0.0 <= version < 0.1.0

当次要、补丁版本号缺少时会当作 0，但也会灵活处理，即时主版本号为 0 也可以 。

能够接受的版本范围

^1.x
1.0.0 <= version < 2.0.0

^0.x
0.0.0 <= version < 1.0.0


## 常用包依赖条件

## react-native-svg
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
## react-native-video
```
Version 4.x requires react-native >= 0.57.0
Version 3.x requires react-native >= 0.40.0
```
