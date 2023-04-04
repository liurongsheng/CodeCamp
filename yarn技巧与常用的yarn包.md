# yarn技巧与常用的yarn包

Yarn 是一个由 Facebook，Google，Exponent 和 Tilde 构建的新的 JavaScript 包管理器。
正如官方公告所写，它的目标就是解决这些团队使用 npm 的时候所遇到的几个问题

1. 安装包不够快速和稳定
2. 存在安全隐患，因为 npm 允许包在安装的时候运行代码

Yarn 仅仅是一个能够从 npm 仓库获取到模块的新的 CLI 客户端。不是想要完全替代 npm。

常用命令

- `npm install yarn@latest -g` // 安装最新版本的 yarn
- `yarn global add <package>` // 全局安装其他的包

## arn 和 npm 功能差异

### yarn.lock 文件

package.json 文件中有 npm 和 Yarn 追踪项目依赖的信息，版本号并不总是确切的。

你可以选择包的最高和最低版本，但是允许 npm 安装最新的补丁，来修复一些 bug。

在 语义版本控制 的理想世界里，发布的补丁不应该包括任何实质性的修改。但是很不幸，这并不总是事实。
npm 的策略可能会导致两台设备使用同样的 package.json 文件，但安装了不同版本的包，这可能导致故障。

为了避免包版本的错误匹配，在锁定文件中需要固定安装的确切版本。每次添加模块，Yarn 会创建（或更新）一个 yarn.lock 文件。
这样你就能保证在 package.json 文件中定义一个可选版本范围的同时，其他设备都安装一样的包。

在 npm 命令中，npm shrinkwrap 同样可以生成一个锁定文件，并且 npm install 在读取 package.json 之前会先读这个锁文件，
和 Yarn 会首先读取 yarn.lock 的方式类似。

最关键的区别是，Yarn 一定会创建并更新 yarn.lock，但是 npm 默认不会创建，并且只会当文件 npm-shrinkwrap.json 存在时更新它。

### 并行安装

使用 npm 时，这些任务按包顺序执行，也就是只有当一个包全部安装完成后，才会安装下一个。Yarn 则是并行执行任务，提高了性能。

使用 npm 和 Yarn 安装了包 express，它们都没有 shrinkwrap 或者 lock 文件也没有缓存。这次安装一共包括 42 个包。
propertag.cmd.push(function() { proper_display('sitepoint_content_1'); });

npm：9 秒
Yarn：1.37 秒

我简直不敢相信我的眼睛。重复这个步骤的结果是相似的。然后我安装了包 gulp，共下载 195 个依赖包。

npm：11 秒
Yarn：7.81 秒

看起来，下载时间的差异很大程度取决于安装的软件包的数量。但是无论那种，Yarn 都更快。

### 更清晰的输出

npm 的输出默认就很详细。会递归的列出所有安装了的包。
而另一方面，Yarn 就很简略。它只列出很少的重要信息并配合适当的 emojis（除非你用的是 Windows 系统），而详细信息可以通过其他命令获取。

## Yarn 和 npm：CLI 的区别

### 全局 yarn

npm 在全局安装操作时需要使用 -g 或者 --global 标志不同，Yarn 命令需要用 global 作为前缀。
和 npm 一样，具体项目的依赖性不应该全局安装。

global 前缀仅适用于 yarn add，yarn bin，yarn ls 和 yarn remove。
除了 yarn add，这些命令都和 npm 命令一样。

### yarn 安装

npm install 命令将会依照 package.json 文件安装依赖，并且允许你添加新的包。

yarn install 仅下载 yarn.lock 列出的依赖，如果没有该文件，则下载 package.json 列出的。

### yarn add [–dev]

和 `npm install <package>` 类似，`yarn add <package>` 让你能添加并安装依赖。

正如命令名的字面义，它能添加依赖，同时意味着它将自动的把包的引用添加到 package.json 文件中，和 npm 的 --save 标志一样。

Yarn 的 --dev 标志会把包作为开发模式的依赖，和 npm 的 --save-dev 标志一样。

### yarn upgrade [package]

这个命令将更新包到符合 package.json 设定规则的最新的版本，并重新创建 yarn.lock 文件。它和 npm update 类似。

当指定包的时候，它将会将这个包更新到最新版并更新 package.json 中定义的标签。这意味着这个命令可能将包更新到一个新的 major 发布。

## 从 npm 迁移到 yarn

<https://yarnpkg.com/en/docs/migrating-from-npm>

| npm (v5) | Yarn |
|:---:|:---:|
| npm install | yarn install |
| (N/A) | yarn install --flat |
| (N/A) | yarn install --har |
| npm install --no-package-lock | yarn install --no-lockfile |
| (N/A) | yarn install --pure-lockfile |
| npm install [package] --save | yarn add [package] |
| npm install [package] --save-dev | yarn add [package] --dev |
| (N/A) | yarn add [package] --peer |
| npm install [package] --save-optional | yarn add [package] --optional |
| npm install [package] --save-exact | yarn add [package] --exact |
| (N/A) | yarn add [package] --tilde |
| npm install [package] --global | yarn global add [package] |
| npm update --global | yarn global upgrade |
| npm rebuild | yarn add --force |
| npm uninstall [package] | yarn remove [package] |
| npm cache clean | yarn cache clean [package] |
| rm -rf node_modules && npm install | yarn upgrade |
| npm version major | yarn version --major |
| npm version minor | yarn version --minor |
| npm version patch | yarn version --patch |
