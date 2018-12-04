# NodeJS基础

## 问题
NodeJS究竟是什么？
NodeJS好在哪里？
NodeJS擅长解决那些实际问题？

静态资源服务器
代码本地构建
单元测试
UI测试
headless爬虫

NodeJS究竟是什么？
NodeJS是一个基于 Chrome V8 引擎的 JavaScript 运行环境
使用了一个事件驱动、非阻塞式 I/O 的模型，使其轻量又高效

非阻塞：I/O 时函数立即返回，进程不等待 I/O 完成
事件驱动：I/O 等异步操作结束后的通知，观察者模式实现

CPU密集：压缩、解压、加密、解密
I/O密集：文件操作、网络操作、数据库

NodeJS使用的语言是JavaScript，处理web场景的环境
- 静态资源读取
- 数据库操作
- 渲染页面

高并发的解决之道
- 增加机器数
- 使用更好的机器，增加多核心CPU

## 环境
CommonJS
global // 相当于浏览器的window对象
process // 在 global 对象下

调试工具
node --inspect-brk demo.js

浏览器地址 chrome://inspect/#devices

```
(function(exports, require, module, __filename, __dirname) {
    console.log("nodeDemo");
}
);
```
exports // 模块的输出
require // 需要的依赖
module // 模块本身

CommonJS 规范
每个文件是一个模块，有自己的作用域，想要创建模块就要创建一个文件
在模块内部 module 变量代表模块本身
module.exports 属性代表模块对外接口 // module.exports.testVar = testVar 


require 规则
- / 表示绝对路径，./ 表示相对于当前文件的路径
- 支持js/json/node拓展名，不写依次尝试
- 不写路径默认为 build-in 模块或者各级 node_modules 内的第三方模块

require 特性
1. module 被加载的时候执行，加载后缓存。只加载一次，第二次调用就从内存中加载
2. 一旦某个模块被循环加载，就只输出已经执行的部分，还未执行的部分不会输出

## 引用系统内置模块

fs 模块
```
const fs = require('fs');
fs.readFile('./demo.js', (err, data)=>{
    if(err){
        console.log(err)
    }else {
        console.log(data); // data.toString()
    }
});
```
fs是操作二进制流的输出的会是16进制的数据
`<Buffer 63 6f 6e 73 74 20 66 73 20 3d 20 72 65 71 75 69 72 65 28 27 66 73 27 29 3b 0d 0a 0d 0a 66 73 2e 72 65 61 64 46 69 6c 65 28 27 2e 2f 64 65 6d 6f 2e 6a ... >`

这个时候只要data.toString()即可得到字符串

## 引用第三方模块
引用 chalk.js // 可是使控制台输出样式多样化
npm install chalk
```
const chalk = require('chalk');
console.log(chalk.red('这是一个输出！'));
```

## module.exports 和 exports 区别
exports 是 module.exports 的快捷写法，但是不能修改指向。
```
exports = {
    a: 100
}
module.exports = {
    a: 100
}
```
前者是不能生效的，后者可以。前者的写法`exports.a = 100;`

## global变量
- Buffer // 二进制处理
- process // 进程
- console
- timer 

```
const {argv, argv0, execArgv, execPath} = process;
argv.forEach(item=>{
    console.log(item)
});
console.log(argv0);
console.log(execArgv);
console.log(execPath);
```
console.log(process.cwd()); // 打印当前的路径(所在文件夹的路径) `C:\gitHub\node`


setImmediate(()=>{
    console.log('setImmediate')
});
setTimeout(()=>{
    console.log('setTimeout')
});
process.nextTick(()=>{
    console.log('nextTick')
});
依次输出:
```
nextTick
setTimeout
setImmediate
```
nextTick 插入在当前的队列的最后一个
setImmediate 插入在下一个队列的队首
setTimeout 插入在两者中间

## 调试技巧 
[官网文档](https://nodejs.org/en/docs/guides/debugging-getting-started)
- inspector
- VSCode

