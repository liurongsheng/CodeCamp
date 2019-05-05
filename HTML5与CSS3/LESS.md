# less 

## 什么是 less ？

less 是一个 CSS 预编译器，意思指的是它可以拓展 CSS 语言，添加功能如允许 变量variables
混合mixins 函数function 和许多其他的技术，让 CSS 更具维护性，主题性，拓展性

[官网](http://lesscss.org)

[中文网](http://lesscss.cn)

### less 的注释
以 // 开始的注释，不会编译到 CSS 文件中 
以 /* */ 包裹的注释会被编译在 CSS 文件中

## 如何使用 less
 less 文件只有在编译后才能够被浏览器识别使用
 
 less 编译工具
[koala](http://koala-app.com/index-zh.html)  国人开发的全平台 less 编译工具

输出方式 `compress` 编译后生产压缩格式的 CSS 文件

[winless](http://winless.org) Windows下的 less 编译软件

[codekit](https://codekitapp.com/) Mac平台下的 less 编译软件

客户端调用方式
- 首先引用 less 文件，引用时使用 link 引入，然后将 rel 属性设置为 `rel="stylesheet/less"`
`<link rel="stylesheet/less" href="style.less">`

- 然后引用 less.min.js，与引入普通 js 引入方式一致，但是一定要放置在 less 样式文件之后
`<script src="less.min.js"></script>`

## 变量 variables 

1. 普通的变量，变量只能定义一次，实际上可以当常量理解
  - 变量的定义方式`@`
  - 实例
    - less 编写
      ```
      @blue: #5b83ad
      #header {
        color: @blue
      }
      ```
    - 编译结果
      ```
      #header{
        color: #5b83ad
      }
      ```
2. 作为选择器和属性名
- 使用时将变量以`@{变量名}`的方式使用
- 实例
  - less 编写
    ```
    @selector: width;
    .@{selector}{
      @{selector}: 960px;
      height: 500px
    }
    ```
  - 编译结果
    ```
    .width{
      width: 960px;
      height: 500px
    }
    ```
3. 作为url
- 使用时，使用 "" 将变量的值扩起来，使用时同样将变量以`@{变量名}`的方式使用
- 实例
  - less 编写
    ```
    @url: "http://www.baidu.com/logo.jpg";
    body{
      background:
    }
    ```
  - 编译结果
    ```
    .width{
      width: 960px;
      height: 500px
    }
    ```
4. 延迟加载
5. 定义多个相同名称的变量时
