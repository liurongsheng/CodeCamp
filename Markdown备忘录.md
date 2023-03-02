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

- **[MD001](doc/md001.md)** *heading-increment/header-increment* - Heading levels should only increment by one level at a time

  标题级数只能每次扩大一个，也就是说不能隔级创建标题，必须h1-h2-h3...

- ~~**[MD002](doc/md002.md)** *first-heading-h1/first-header-h1* - First heading should be a top-level heading~~

  文档的第一个标题必须是最高级的标题（标题等级1级到6级逐渐降低）

- **[MD003](doc/md003.md)** *heading-style/header-style* - Heading style

  整篇文档要采用一致的标题格式

- **[MD004](doc/md004.md)** *ul-style* - Unordered list style

  整篇文档的无序列表的格式要一致

- **[MD005](doc/md005.md)** *list-indent* - Inconsistent indentation for list items at the same level

  同一个等级的列表的缩进要一致;在有序列表中，前面的数字序号可以左对齐，也可以右对齐

- ~~**[MD006](doc/md006.md)** *ul-start-left* - Consider starting bulleted lists at the beginning of the line~~

  一级标题不能够缩进

- **[MD007](doc/md007.md)** *ul-indent* - Unordered list indentation

  无序列表嵌套的时候默认采取两个空格的缩进方式

- **[MD009](doc/md009.md)** *no-trailing-spaces* - Trailing spaces

  行尾最多可以添加两个空格，超出之后会有警告，最好每次都是两个空格因为两个空格刚好可以用来换行

- **[MD010](doc/md010.md)** *no-hard-tabs* - Hard tabs

  不能使用tab来进行缩进，要使用空格

- **[MD011](doc/md011.md)** *no-reversed-links* - Reversed link syntax

  内联形式的链接和创建方式是否错误，中括号和圆括号是否使用正确

- **[MD012](doc/md012.md)** *no-multiple-blanks* - Multiple consecutive blank lines

  文档中不能有连续的空行（文档末可以有一个空行），在代码块中这个规则不会生效

- **[MD013](doc/md013.md)** *line-length* - Line length

  默认行的最大长度是80，此规则对代码块、表格、标题也生效

- **[MD014](doc/md014.md)** *commands-show-output* - Dollar signs used before commands without showing output

  在代码块中，终端命令前不需要有美元符号($)

- **[MD018](doc/md018.md)** *no-missing-space-atx* - No space after hash on atx style heading

  标题格式如果是"atx"的话，#号和文字之间需要一个空格隔开

- **[MD019](doc/md019.md)** *no-multiple-space-atx* - Multiple spaces after hash on atx style heading

- 标题格式如果是"atx"的话，#号和文字之间只需要一个空格隔开，不需要多个

- **[MD020](doc/md020.md)** *no-missing-space-closed-atx* - No space inside hashes on closed atx style heading

  在 “closed_atx” 格式的标题中，文字和前后的 # 号之间需用一个空格隔开

- **[MD021](doc/md021.md)** *no-multiple-space-closed-atx* - Multiple spaces inside hashes on closed atx style heading

  在 “closed_atx” 格式的标题中，文字和前后的 # 号之间只能用一个空格隔开，不能有多余的空格

- **[MD022](doc/md022.md)** *blanks-around-headings/blanks-around-headers* - Headings should be surrounded by blank lines

  标题行的上下行必须都是空行

- **[MD023](doc/md023.md)** *heading-start-left/header-start-left* - Headings must start at the beginning of the line

  标题行不能缩进

- **[MD024](doc/md024.md)** *no-duplicate-heading/no-duplicate-header* - Multiple headings with the same content

  在文档中不能有重复性的标题

- **[MD025](doc/md025.md)** *single-title/single-h1* - Multiple top-level headings in the same document

  同一个文档中，只能有一个最高级的标题，默认也只能有一个一级标题

- **[MD026](doc/md026.md)** *no-trailing-punctuation* - Trailing punctuation in heading

  标题的末尾不能有". , ; : ! ? "这些符号

- **[MD027](doc/md027.md)** *no-multiple-space-blockquote* - Multiple spaces after blockquote symbol

  创建引用区块时，右尖括号 ( > ) 和文字之间有且只能有一个空格

- **[MD028](doc/md028.md)** *no-blanks-blockquote* - Blank line inside blockquote

  两个引用区块间不能仅用一个空行隔开或者同一引用区块中不能有空行，如果一行中没有内容，则这一行要用>开头

- **[MD029](doc/md029.md)** *ol-prefix* - Ordered list item prefix

  有序列表的前缀序号格式必须只用1或者从1开始的加1递增数字("one_or_ordered")

- **[MD030](doc/md030.md)** *list-marker-space* - Spaces after list markers

  列表（有序、无序）的前缀符号和文字之间用1个空格隔开，在列表嵌套或者同一列表项中有多个段落时，无序列表缩进两个空格，有序列表缩进3个空格

- **[MD031](doc/md031.md)** *blanks-around-fences* - Fenced code blocks should be surrounded by blank lines

  单独的代码块前后需要用空行隔开（除非是在文档开头或末尾），否则有些解释器不会解释为代码块

- **[MD032](doc/md032.md)** *blanks-around-lists* - Lists should be surrounded by blank lines

  列表（有序、无序）前后需要用空行隔开，否则有些解释器不会解释为列表，列表的缩进必须一致，否则会警告

- **[MD033](doc/md033.md)** *no-inline-html* - Inline HTML

  文档中不允许使用html语句

- **[MD034](doc/md034.md)** *no-bare-urls* - Bare URL used

  单纯的链接地址需要用尖括号 (<>) 包裹，否则有些解释器不会解释为链接

- **[MD035](doc/md035.md)** *hr-style* - Horizontal rule style

  创建水平线时整篇文档要统一，要和文档中第一次创建水平线使用的符号一致

- **[MD036](doc/md036.md)** *no-emphasis-as-heading/no-emphasis-as-header* - Emphasis used instead of a heading

  不能用强调来代替标题

- **[MD037](doc/md037.md)** *no-space-in-emphasis* - Spaces inside emphasis markers

  用于创建强调的符号和强调的的文字之间不能有空格

- **[MD038](doc/md038.md)** *no-space-in-code* - Spaces inside code span elements

  当用单反引号创建代码段的时候，单反引号和它们之间的代码不能有空格，如果要把单反引号嵌入到代码段的首尾，创建代码段的单反引号和嵌入的单反引号间要有一个空格隔开

- **[MD039](doc/md039.md)** *no-space-in-links* - Spaces inside link text

  链接名和包围它的中括号之间不能有空格，但链接名中间可以有空格

- **[MD040](doc/md040.md)** *fenced-code-language* - Fenced code blocks should have a language specified

  单独的代码块（此处是指上下用三个反引号包围的代码块）应该指定代码块的编程语言，这一点有助于解释器对代码进行代码高亮

- **[MD041](doc/md041.md)** *first-line-heading/first-line-h1* - First line in a file should be a top-level heading

  文档的第一个非空行应该是文档最高级的标题，默认是1级标题

- **[MD042](doc/md042.md)** *no-empty-links* - No empty links

  链接的地址不能为空

- **[MD043](doc/md043.md)** *required-headings/required-headers* - Required heading structure

  要求标题遵循一定的结构，默认是没有规定的结构

- **[MD044](doc/md044.md)** *proper-names* - Proper names should have the correct capitalization

  指定一些名称，会检查它是否有正确的大写

- **[MD045](doc/md045.md)** *no-alt-text* - Images should have alternate text (alt text)

  图片链接必须包含描述文本 all文本

- **[MD046](doc/md046.md)** *code-block-style* - Code block style

  整篇文档采用一致的代码格式

- **[MD047](doc/md047.md)** *single-trailing-newline* - Files should end with a single newline character

  文档末尾需要一个空行结尾

- **[MD048](doc/md048.md)** *code-fence-style* - Code fence style

  代码块如果采用分隔符隔开的方式定义，那么整篇文档要采用一致的分隔符，都用波浪号或都用反引号

- **[MD049](doc/md049.md)** *emphasis-style* - Emphasis style should be consistent

  整篇文档采用一致的倾斜格式

- **[MD050](doc/md050.md)** *strong-style* - Strong style should be consistent

  整篇文档采用一致的加粗格式

- **[MD051](doc/md051.md)** *link-fragments* - Link fragments should be valid

  文内链接必须要有效，不能指向一个不存在的标题

- **[MD052](doc/md052.md)** *reference-links-images* - Reference links and images should use a label that is defined

  引用链接和图像应使用一个被定义的标签

- **[MD053](doc/md053.md)** *link-image-reference-definitions* - Link and image reference definitions should be needed

  链接和图像引用应被定义

### 规则分类

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
