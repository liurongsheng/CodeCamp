# NodeJS基础

## 问题
- NodeJS究竟是什么？
- NodeJS好在哪里？
- NodeJS擅长解决那些实际问题？

- 静态资源服务器
- 代码本地构建
- 单元测试
- UI测试
- headless爬虫

### NodeJS究竟是什么？
NodeJS是一个基于 Chrome V8 引擎的 JavaScript 运行环境，

不是一门新语言，是基于 V8 创建一个轻量级的 Web 服务器并提供一套库，能够使的 JavaScript 脱离浏览器运行，

简单理解就是使 JavaScript 具有服务端的能力

### JS单线程
- 节约内存，并且不需要在切换执行上下文
- 不需要管锁的问题
- 多个线程同时操作 DOM 那岂不会很混乱

### 两个特征
使用了一个事件驱动、非阻塞式 I/O 的模型，使其轻量又高效·

- 事件驱动：
事件驱动架构是建立在软件开发中一种通用模式上的，这种模式被称为发布-订阅或观察者模式

在事件驱动架构中，至少有两个参与者：主题（subject）和观察者（observer）

主题就像调频收音机一样，向有兴趣收听该主题所说内容的观察者进行广播，观察者不限制个数，只要主题有一些要广播的消息就够了

简单理解就是一个实体广播一条消息，其他实体监听该消息

在浏览器中的事件目标就是能够发送事件的对象（HTML 元素是事件发送器 event emitters）,是观察者模式中的主题。可以理解为任何 HTML 元素都是广播电台
JavaScript 中注册为监听器的函数是观察者
```
const btn = document.getElementById('subscribe');
btn.addEventListener("click", function () {
    console.log("Button clicked");
});
```
这里的“click”是事件，按钮是主题(发送器)，函数是观察者(监听器)

- 非阻塞 I/O：️I/O 是 input/output 的意思，就是输入输出操作

传统的服务器语言大多是多线程、阻塞式 I/O。

这也是 Node 与众不同的地方，对于传统的服务器语言，在与用户建立连接时，每一个连接都是一个线程。 
当有十万个用户连接时，服务器上就会有十万个线程。

而阻塞式 I/O 是指，当一个线程在执行 I/O 操作时，这个线程会阻塞，等待 I/O 操作完成后继续执行，而 node 由于单线程的缘故，
采用非阻塞 I/0 这种模型机制，性能依旧高效

发起 I/O 操作不等得到响应或者超时就立即返回，让进程继续执行其他操作，但是要通过轮询方式不断地去 check 数据是否已准备好


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

