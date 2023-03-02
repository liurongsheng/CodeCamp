# VSCode常用配置

[市场地址](https://marketplace.visualstudio.com/search?target=VSCode&category=All%20categories&sortBy=Downloads)

## 规则校验和美化

### [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

Prettier 是目前 Web 开发中最受欢迎的代码格式化程序。安装了这个插件，它就能够自动应用 Prettier，并将整个 JS 和 CSS 文档快速格式化为统一的代码样式。
如果你还想使用 ESLint，那么还有个 Prettier – Eslint 插件，你可不要错过咯！

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

其中 "allowed_elements" 的列表中填入不想提出警告的 html 标签，保存修改后，markdownlint将不再对 "allowed_elements" 中的 html 标签提出警告

## 惊艳的拓展功能

### [Draw.io](https://marketplace.visualstudio.com/items?itemName=hediet.vscode-drawio)

协作编辑或展示图表

## 调试工具

### [open-in-browser](https://marketplace.visualstudio.com/items?itemName=coderfee.open-html-in-browser)

VSCode 没有提供直接在浏览器中打开文件的内置界面，此插件可以在浏览器中预览html文件，firefox和google chrome＆IE
打开一个html文件，Windows和Linux的键盘快捷键是Ctrl+ Alt+ O，对于MacOS是Cmd+ Alt+ O
如果您想直接在默认浏览器中预览html，请输入Ctrl+ K D

## 主题

[主题目录](https://marketplace.visualstudio.com/search?target=VSCode&category=Themes&sortBy=Downloads)

[One Monokai Theme](https://marketplace.visualstudio.com/items?itemName=azemoh.one-monokai)

[Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)

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
