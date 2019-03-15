# 微信JSSDK调试

## jweixin-1.4.0.js?390d:1 Uncaught TypeError: Cannot read property 'title' of undefined

jweixin-1.4.0.js里面的执行方式不适合直接webpack。

在执行this.document.title的时候出的问题，这个js期望实在浏览器全局作用域下执行（this指向window），
但是webpack之后，是在一个function作用域下执行，因此this.document为undefined

因此有几种方式修改：

1. 改源码，将jweixin-1.2.0.js中第一个this改为window

2. 在html中使用script引入

3.webpack有个script-loader可以让模块文件在global环境下执行 

