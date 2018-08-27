# url地址格式转换

## encodeURI、encodeURIComponent、decodeURI、decodeURIComponent四个用来编码和解码 URI 的函数

## URI组成形式

一般形式是：
Scheme : First / Second ; Third ? Fourth

其中斜体的名字代表组件；“:”, “/”, “;”，“?”是当作分隔符的保留字符

## 函数差异区分

encodeURI 和 decodeURI 函数操作的是完整的 URI；
这俩函数假定 URI 中的任何保留字符都有特殊意义，所有不会编码它们。

encodeURIComponent 和 decodeURIComponent 函数操作的是组成 URI 的个别组件；
这俩函数假定任何保留字符都代表普通文本，所以必须编码它们，所以它们（保留字符）出现在一个完整 URI 的组件里面时不会被解释成保留字符了。

## URI保留字符 uriReserved

`; / ? : @ & = + $ ,`(10个)

## URI标记符
`- _ . ! ~ * ' ( )`

<img src="/img/uri编码与解码.jpg" title="uri编码与解码.jpg" />

### javaScript encodeURIComponent()函数
```
encodeURIComponent('早上好')
//"%E6%97%A9%E4%B8%8A%E5%A5%BD"
```

### javaScript decodeURIComponent()函数
```
window.location.href
"https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git"

decodeURIComponent(window.location.href);
"https://git-scm.com/book/zh/v2/起步-安装-Git"
```