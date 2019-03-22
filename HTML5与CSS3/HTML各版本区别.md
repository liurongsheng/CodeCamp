## HTML 各版本语法上的区别

1. HTML4/4.01 不严格写法随意
2. XHTML(XML) 要求非常严格，所有的标签、属性都是小写，所有属性都要有值
3. HTML5 继承HTML4
|    HTML4    |       XHTML       |      HTML5     |
|:-----------:|:-----------------:|:--------------:|
|标签允许不结束|标签必须结束|标签允许不结束|
|属性不用带引号|属性必须带引号|属性不用带引号|
|标签属性可大写|标签属性必须小写|标签属性可大写|
|Boolean属性可省略值|Boolean属性必须有值|Boolean属性可省略值|

可以使用 w3c 的工具进行网页验证
https://validator.w3.org/

## HTML5 和 HTML4 主要区别

1. 语法上的改变
2. 新增的元素和废除的元素
3. 新增的属性和废除的属性
4. 全局属性

## 语法上的改变

1. DOCTYPE声明
2. 内容类型
3. 字符编码的指定方法
4. 元素标记的省略
5. 具有布尔值的属性
6. 引号的省略

## 新增了那些元素，删除了那些元素，为什么删除这些元素，用什么元素替代

## 新增了那些属性，删除了那些属性，用什么属性替代

## 全局元素
1. contentEditable 属性
2. designMode 属性
3. hidden 属性
4. spellcheck 属性 
5. tabindex 属性

## HTML 常见元素和理解

- meta
- title
- style
- link
- script
- base

- div/section/article/aside/headrt/footer
- p
- span/em/strong
- table/thead/tbody/tr/td
- ul/ol/li/dl/dt/dd
- a
- form/input/select/textarea/button

`<meta chareset="utf-8">` chare-字符 set-集合 字符集设置为 utf-8

`<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">`
适配移动端的关键步骤

`<base href="/">` 指定基础路径，所有链接都是 href 的值为基准来计算

重要属性：
```
a[href, target] target-"_blank" 新标签也打开
img[src, alt]
table td[colspan, rowspan] colspan="2" 合并两列, rowspan="2" 合并两行
form[target, method, enctype] target-要提交的地址 enctype-使用的编码，针对post
input[type, value]
button[type]
slelct>option[value]
label[for] for-添加后可以根据文字来选择操作
```
