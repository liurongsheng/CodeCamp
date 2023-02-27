# VSCode插件配置

## markdownlint

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
