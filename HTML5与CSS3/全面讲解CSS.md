# 全面讲解CSS

前端开发三大件
- HTML 结构
- CSS 样式
- JavaScript 行为

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

<meta chareset="utf-8"> chare-字符 set-集合 字符集设置为 utf-8

<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
适配移动端的关键步骤

<base href="/"> 指定基础路径，所有链接都是 href 的值为基准来计算

重要属性
a[href, target] target-"_blank" 新标签也打开
img[src, alt]
table td[colspan, rowspan] colspan="2" 合并两列, rowspan="2" 合并两行
form[target, method, enctype] target-要提交的地址 enctype-使用的编码，针对post
input[type, value]
button[type]
slelct>option[value]
label[for] for-添加后可以根据文字来选择操作

## HTML 版本

HTML4/4.01 不严格写法随意
XHTML(XML) 要求非常严格，所有的标签、属性都是小写，所有属性都要有值
HTML5 继承HTML4
|    HTML4    |       XHTML       |      HTML5     |
|:-----------:|:-----------------:|:--------------:|
|标签允许不结束|标签必须结束|标签允许不结束|
|属性不用带引号|属性必须带引号|属性不用带引号|
|标签属性可大写|标签属性必须小写|标签属性可大写|
|Boolean属性可省略值|Boolean属性必须有值|Boolean属性可省略值|

可以使用 w3c 的工具进行网页验证
https://validator.w3.org/

## HTML 元素分类

## HTML 元素嵌套关系

## HTML 元素默认的样式和定制化

## HTML 面试真题 
