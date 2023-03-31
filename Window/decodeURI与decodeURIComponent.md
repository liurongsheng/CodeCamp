# url地址格式转换

- encodeURI 和 encodeURIComponent 用于编码过的 URI 字符串
- decodeURI 和 decodeURIComponent 用于解码编码过的 URI 字符串

## URI组成形式

一般形式是：
Scheme : First / Second ; Third ? Fourth

其中斜体的名字代表组件；“:”, “/”, “;”，“?”是当作分隔符的保留字符

## 函数差异区分

encodeURI 和 decodeURI 函数操作的是完整的 URI；
这俩函数假定 URI 中的任何保留字符都有特殊意义，所有不会编码它们。

encodeURIComponent 和 decodeURIComponent 函数操作的是组成 URI 的个别组件；
这俩函数假定任何保留字符都代表普通文本，所以必须编码它们，所以它们（保留字符）出现在一个完整 URI 的组件里面时不会被解释成保留字符了。

## URI标记符

<img src="/img/uri编码与解码.jpg" title="uri编码与解码.jpg" />

## encodeURIComponent 和 encodeURI 的区别

encodeURI 转义除了 `; , / ? : @ & = + $` `#` `A-Z a-z 0-9 - _ . ! ~ * ' ( )` 外的所有字符

encodeURIComponent 转义除了 `A-Z a-z 0-9 - _ . ! ~ * ' ( )` 外的所有字符：

encodeURIComponent() 和 encodeURI 有以下几个不同点：

```js
var set1 = ";,/?:@&=+$";  // 保留字符
var set2 = "-_.!~*'()";   // 不转义字符
var set3 = "#";           // 数字标志
var set4 = "ABC abc 123"; // 字母数字字符和空格

console.log(encodeURI(set1)); // ;,/?:@&=+$
console.log(encodeURI(set2)); // -_.!~*'()
console.log(encodeURI(set3)); // #
console.log(encodeURI(set4)); // ABC%20abc%20123 (空格被编码为 %20)

console.log(encodeURIComponent(set1)); // %3B%2C%2F%3F%3A%40%26%3D%2B%24
console.log(encodeURIComponent(set2)); // -_.!~*'()
console.log(encodeURIComponent(set3)); // %23
console.log(encodeURIComponent(set4)); // ABC%20abc%20123 (空格被编码为 %20)
```

为了避免服务器收到不可预知的请求，对任何用户输入的作为 URI 部分的内容你都需要用 encodeURIComponent 进行转义

比如，一个用户可能会输入"Thyme &time=again"作为comment变量的一部分。如果不使用 encodeURIComponent 对此内容进行转义，服务器得到的将是comment=Thyme%20&time=again

请注意，"&"符号和"="符号产生了一个新的键值对，所以服务器得到两个键值对（一个键值对是comment=Thyme，另一个则是time=again），而不是一个键值对
