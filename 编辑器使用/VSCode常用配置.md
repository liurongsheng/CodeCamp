# VSCode 常用配置

[市场地址](https://marketplace.visualstudio.com/search?target=VSCode&category=All%20categories&sortBy=Downloads)

## 常规

[Code Runner](https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner)

代码片段运行

在插件的拓展配置中配置 `Code-runner: Default Language` 比如: `javascript`、`python`

html 使用 chrome 配置如下：

`"html": "\"C:\\Program Files\\Google\\Chrome\\Application\\chrome.exe\""`

- 反斜杠: 请使用 \\
- 如果路径中包含空格, 请使用 \" 环绕文件路径

- `Ctrl + Alt + N` // 运行
- `Ctrl + Alt + J` // 选择语言在运行

[Gitlens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)

git 历史记录

[Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph)

可视化操作 git

[Turbo Console Log](https://marketplace.visualstudio.com/items?itemName=ChakrounAnas.turbo-console-log)

快速 console.log

[REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)

REST 接口直接请求，支持 `.http` 格式的文件

[Thunder Client](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client)

替代 Postman 的接口请求

[Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)

引用路径

[indent-rainbow](https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow)

代码彩虹对齐

[Import Cost](https://marketplace.visualstudio.com/items?itemName=wix.vscode-import-cost)

依赖包开销信息

[JSON to TS](https://marketplace.visualstudio.com/items?itemName=MariusAlchimavicius.json-to-ts)

JSON 快速生成 TS 声明

## 规则校验和美化

### [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

Prettier 是目前 Web 开发中最受欢迎的代码格式化程序。安装了这个插件，它就能够自动应用 Prettier，并将整个 JS 和 CSS 文档快速格式化为统一的代码样式。
如果你还想使用 ESLint，那么还有个 Prettier – Eslint 插件，你可不要错过咯！

设置保存自动使用 prettier 进行 formatter

搜索 `format on save` ，`Editor: Format On Save` 勾选启用

搜索 `formatter`，`Editor: Default Formatter` 设置为 `Prettier - Code formatter`

### [markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)

MD33 markdownlint 插件进行代码分析，当使用了 html 标签时，插件会给出 MD033/no-inline-html，插件作者的意图是为了使 markdown 文件是纯 markdown 的，避免在使用 html 以外的方式渲染时出错

```text
"markdownlint.config": {
  "default": true,
  "MD033": {
    "allowed_elements": [ "a" ]
  }
}
```

[markdownlint-cli2](https://github.com/DavidAnson/markdownlint-cli2)

`npm install markdownlint-cli2 --global` // 全局安装

`markdownlint-cli2-fix "**/*.md"` // 修复命令

使用全局格式化修复

.markdownlint.jsonc // 配置文件

```config
{
  "MD013": false,
  "MD033": false
}
```

其中 "allowed_elements" 的列表中填入不想提出警告的 html 标签，保存修改后，markdownlint 将不再对 "allowed_elements" 中的 html 标签提出警告

### [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)

校验拼写

## 惊艳的拓展功能

### [Draw.io](https://marketplace.visualstudio.com/items?itemName=hediet.vscode-drawio)

协作编辑或展示图表

### [Read Aloud text](https://marketplace.visualstudio.com/items?itemName=azu.read-aloud-text)

微软的文本朗读插件

## 调试工具

### [open-in-browser](https://marketplace.visualstudio.com/items?itemName=coderfee.open-html-in-browser)

VSCode 没有提供直接在浏览器中打开文件的内置界面，此插件可以在浏览器中预览 html 文件，firefox 和 google chrome＆IE
打开一个 html 文件，Windows 和 Linux 的键盘快捷键是 Ctrl+ Alt+ O，对于 MacOS 是 Cmd+ Alt+ O
如果您想直接在默认浏览器中预览 html，请输入 Ctrl+ K D

## 主题

[vscode-icons](https://marketplace.visualstudio.com/items?itemName=vscode-icons-team.vscode-icons)

目录样式

[Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)

目录样式

[One Monokai Theme](https://marketplace.visualstudio.com/items?itemName=azemoh.one-monokai)

代码样式

---

### [Quokka](https://quokkajs.com/)

Quokka 是一个调试工具插件，能够根据你正在编写的代码提供实时反馈。
它易于配置，并能够预览变量的函数和计算值结果。另外，在使用 JSX 或 TypeScript 项目中，它能够开箱即用。

### [Regex Previewer](https://marketplace.visualstudio.com/items?itemName=chrmarti.regex)

实时测试正则表达式的实用工具

---

## settings.json 配置

```json
{
  "workbench.colorTheme": "Visual Studio Dark",
  "files.associations": {
    "*.template": "html",
    "*.html": "html"
  },
  "editor.tabSize": 2,
  "files.autoSave": "off",
  "editor.detectIndentation": false,
  "workbench.iconTheme": "vscode-great-icons",
  "editor.minimap.enabled": false
}
```

## VSCode 切换默认终端(cmd、powershell)

- `ctrl + shift + p` 打开命令面板，输入`select`，选中 `终端：选择默认配置文件`("Terminal:Select Default Profile")
- 配置文件 "terminal.integrated.defaultProfile.windows": "Command Prompt"
