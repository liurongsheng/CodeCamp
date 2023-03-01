# Markdown备忘录

## 相关网站

[CommonMark](https://spec.commonmark.org/)
[Markdown（GFM）](https://github.github.com/gfm/)
[microsoft docs](https://learn.microsoft.com/zh-cn/docs/)

## Markdown的字体显示

```text
加粗：文字左右分别用两个号包起来
斜体：文字左右分别用一个号包起来
斜体加粗：文字左右分别用三个*号包起来
删除线：文字左右分别用两个~~号包起来

注意：字体显示不需要符号与内容之间，加空格
```

## markdownlint

- npm i -g markdownlint-cli2 // 全局安装
- markdownlint-cli2-fix "**/*.md" // 执行命令

配置项目根目录 `.markdownlint.json`

```json
{
  "MD034": false, // url 的修复容易出错
  "MD033": {
    "allowed_elements": [ "a" ] // 允许配置的标签元素单独存在
  }
}
```
