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

[官网地址](https://github.com/DavidAnson/markdownlint)

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

### markdownlint rules

<!-- markdownlint-disable line-length -->

- **[MD001](doc/md001.md)** *heading-increment/header-increment* - Heading levels should only increment by one level at a time
- ~~**[MD002](doc/md002.md)** *first-heading-h1/first-header-h1* - First heading should be a top-level heading~~
- **[MD003](doc/md003.md)** *heading-style/header-style* - Heading style
- **[MD004](doc/md004.md)** *ul-style* - Unordered list style
- **[MD005](doc/md005.md)** *list-indent* - Inconsistent indentation for list items at the same level
- ~~**[MD006](doc/md006.md)** *ul-start-left* - Consider starting bulleted lists at the beginning of the line~~
- **[MD007](doc/md007.md)** *ul-indent* - Unordered list indentation
- **[MD009](doc/md009.md)** *no-trailing-spaces* - Trailing spaces
- **[MD010](doc/md010.md)** *no-hard-tabs* - Hard tabs
- **[MD011](doc/md011.md)** *no-reversed-links* - Reversed link syntax
- **[MD012](doc/md012.md)** *no-multiple-blanks* - Multiple consecutive blank lines
- **[MD013](doc/md013.md)** *line-length* - Line length
- **[MD014](doc/md014.md)** *commands-show-output* - Dollar signs used before commands without showing output
- **[MD018](doc/md018.md)** *no-missing-space-atx* - No space after hash on atx style heading
- **[MD019](doc/md019.md)** *no-multiple-space-atx* - Multiple spaces after hash on atx style heading
- **[MD020](doc/md020.md)** *no-missing-space-closed-atx* - No space inside hashes on closed atx style heading
- **[MD021](doc/md021.md)** *no-multiple-space-closed-atx* - Multiple spaces inside hashes on closed atx style heading
- **[MD022](doc/md022.md)** *blanks-around-headings/blanks-around-headers* - Headings should be surrounded by blank lines
- **[MD023](doc/md023.md)** *heading-start-left/header-start-left* - Headings must start at the beginning of the line
- **[MD024](doc/md024.md)** *no-duplicate-heading/no-duplicate-header* - Multiple headings with the same content
- **[MD025](doc/md025.md)** *single-title/single-h1* - Multiple top-level headings in the same document
- **[MD026](doc/md026.md)** *no-trailing-punctuation* - Trailing punctuation in heading
- **[MD027](doc/md027.md)** *no-multiple-space-blockquote* - Multiple spaces after blockquote symbol
- **[MD028](doc/md028.md)** *no-blanks-blockquote* - Blank line inside blockquote
- **[MD029](doc/md029.md)** *ol-prefix* - Ordered list item prefix
- **[MD030](doc/md030.md)** *list-marker-space* - Spaces after list markers
- **[MD031](doc/md031.md)** *blanks-around-fences* - Fenced code blocks should be surrounded by blank lines
- **[MD032](doc/md032.md)** *blanks-around-lists* - Lists should be surrounded by blank lines
- **[MD033](doc/md033.md)** *no-inline-html* - Inline HTML
- **[MD034](doc/md034.md)** *no-bare-urls* - Bare URL used
- **[MD035](doc/md035.md)** *hr-style* - Horizontal rule style
- **[MD036](doc/md036.md)** *no-emphasis-as-heading/no-emphasis-as-header* - Emphasis used instead of a heading
- **[MD037](doc/md037.md)** *no-space-in-emphasis* - Spaces inside emphasis markers
- **[MD038](doc/md038.md)** *no-space-in-code* - Spaces inside code span elements
- **[MD039](doc/md039.md)** *no-space-in-links* - Spaces inside link text
- **[MD040](doc/md040.md)** *fenced-code-language* - Fenced code blocks should have a language specified
- **[MD041](doc/md041.md)** *first-line-heading/first-line-h1* - First line in a file should be a top-level heading
- **[MD042](doc/md042.md)** *no-empty-links* - No empty links
- **[MD043](doc/md043.md)** *required-headings/required-headers* - Required heading structure
- **[MD044](doc/md044.md)** *proper-names* - Proper names should have the correct capitalization
- **[MD045](doc/md045.md)** *no-alt-text* - Images should have alternate text (alt text)
- **[MD046](doc/md046.md)** *code-block-style* - Code block style
- **[MD047](doc/md047.md)** *single-trailing-newline* - Files should end with a single newline character
- **[MD048](doc/md048.md)** *code-fence-style* - Code fence style
- **[MD049](doc/md049.md)** *emphasis-style* - Emphasis style should be consistent
- **[MD050](doc/md050.md)** *strong-style* - Strong style should be consistent
- **[MD051](doc/md051.md)** *link-fragments* - Link fragments should be valid
- **[MD052](doc/md052.md)** *reference-links-images* - Reference links and images should use a label that is defined
- **[MD053](doc/md053.md)** *link-image-reference-definitions* - Link and image reference definitions should be needed

- **`accessibility`** - `MD045`
- **`atx`** - `MD018`, `MD019`
- **`atx_closed`** - `MD020`, `MD021`
- **`blank_lines`** - `MD012`, `MD022`, `MD031`, `MD032`, `MD047`
- **`blockquote`** - `MD027`, `MD028`
- **`bullet`** - `MD004`, `MD005`, `MD006`, `MD007`, `MD032`
- **`code`** - `MD014`, `MD031`, `MD038`, `MD040`, `MD046`, `MD048`
- **`emphasis`** - `MD036`, `MD037`, `MD049`, `MD050`
- **`hard_tab`** - `MD010`
- **`headers`** - `MD001`, `MD002`, `MD003`, `MD018`, `MD019`, `MD020`, `MD021`,
  `MD022`, `MD023`, `MD024`, `MD025`, `MD026`, `MD036`, `MD041`, `MD043`
- **`headings`** - `MD001`, `MD002`, `MD003`, `MD018`, `MD019`, `MD020`,
  `MD021`, `MD022`, `MD023`, `MD024`, `MD025`, `MD026`, `MD036`, `MD041`,
  `MD043`
- **`hr`** - `MD035`
- **`html`** - `MD033`
- **`images`** - `MD045`, `MD052`, `MD053`
- **`indentation`** - `MD005`, `MD006`, `MD007`, `MD027`
- **`language`** - `MD040`
- **`line_length`** - `MD013`
- **`links`** - `MD011`, `MD034`, `MD039`, `MD042`, `MD051`, `MD052`, `MD053`
- **`ol`** - `MD029`, `MD030`, `MD032`
- **`spaces`** - `MD018`, `MD019`, `MD020`, `MD021`, `MD023`
- **`spelling`** - `MD044`
- **`ul`** - `MD004`, `MD005`, `MD006`, `MD007`, `MD030`, `MD032`
- **`url`** - `MD034`
- **`whitespace`** - `MD009`, `MD010`, `MD012`, `MD027`, `MD028`, `MD030`,
  `MD037`, `MD038`, `MD039`

<!-- markdownlint-restore -->

## 常用支持的高亮语法

|名称|关键字|调用的js|
|:---:|:---:|:---:|
|Shell|bash, shell|shBrushBash.js|
|C|cpp, c|shBrushCpp.js |
|CSS|css|shBrushCss.js |
|C#|c#, c-sharp, csharp|shBrushCSharp.js|
|Java|java|shBrushJava.js|
|JavaScript|js, javascript|shBrushJScript.js|
|JSON|json|-|
|text|text, plain|shBrushPlain.js| 就是普通文本|
|Python|py, python|shBrushPython.js|
|Ruby|ruby, rails, ror, rb|shBrushRuby.js |
|PHP|php|shBrushPhp.js|
|SASS&SCSS|sass, scss|shBrushSass.js|
|SQL|sql|shBrushSql.js|
|XML|xml, xhtml, xslt, html|shBrushXml.js|
|Objective C|objc, obj-c|shBrushObjectiveC.js|
|matlab|matlab|shBrushMatlab.js|
|swift|swift |shBrushSwift.js|
|GO|go, golang|shBrushGo.js|
