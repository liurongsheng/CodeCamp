# JS 基础

JavaScript 分为三部分

- ecmascript: 包含 javascript基本语法
  - 运算符
  - 数据结构
  - 流程控制
  - 函数
  - 数组
  - 对象
- BOM：浏览器对象模型，操作浏览器窗口
- DOM：文档对象模型，操作网页的节点(标签)

BOM和DOM只是一个概念(一个模型)，而不是一个具体的对象，他们是由多个对象组成的集合
BOM对象模型中最顶层的对象是window对象
window对象中有一个属性是document，document又是一个对象，就是DOM对象模型

四种写入js的方式

1. 内嵌式

- <script type="text/javascript"></script> // 在页面任何位置引入

1. 外联式

- <script src="/javascript/application.js" type="text/javascript"></script>

1. HTML标签中事件属性引入

- <div onclick="alert("11")"></div>

1. a 标签中 href 属性中引入

- <a href="javascript:alert('22')" >点击</a> // 这里的`javascript`区分大小写
  
内嵌式和外联式的type属性可以省略不写，因为script标签默认属性值就是 text/javascript
通常写在head标签或者结束body标签之前，后者是推荐

三种输出方式

1. 网页输出：在页面中直接显示
  document.write(输出内容)
2. 弹出对话框：警告框 提示框
  alert(输出内容)
3. 控制台输出
  console.log(输出内容)
  
html标签名和属性名不区分大小写，但是js是区分大小写的

标识符-命名规则

- 字母、数字、下划线、$
- 数字不能开头

注释
单行注释：
// 注释的内容
多行注释：
/*注释的内容*/

数据类型

- 基本数据类型
  - number
  - string
  - boolean
  - undefined
  - null
- 引用数据类型

null 和 undefined
相同点：均代表无值
不同点：undefined 代表一个变量如果没有赋值，那么值是undefined，变量的默认值
null 代表一个变量如果存储的值是引用类型，但是目前对象还没有创建，那么就可以设置为null，表示空对象

var a = null
typeof(a) // object

var b = NaN
typeof(b) // number

var c = undefined
typeof(c) // undefined

强制类型装换
parseInt()
parseFloat()
Number()
Boolean()
String()

两种定义函数的区别

函数声明式，如果使用函数声明式定义函数，定义好的函数会自动提升位置
提升到script开始标签开始的位置。

函数表达式，函数定义好后不会提升位置。

函数声明式定义的函数，可以在任何位置调用，函数表达式定义的函数，只能在定义的函数之后调用。

// 函数声明式
function printStr(){
  console.log("11");
}

// 函数表达式定义
var printStr = function(){
  console.log("22");
}

内置函数
isNaN(值) 如果不是数字返回 true，如果是数字返回 false
isNaN("1") // false
isNaN("1d") // true

递归函数：在函数体内对自身的调用

一般在定义函数的时候定义一个参数，在函数内部对参数的判断来达到递归出口

function test(a) {
  console.log(a)
  a++;
  if(a<=5){
    test(a)
  }
  console.log(a)
}
test(1)
// 1 2 3 4 5 6 5 4 3 2

1. 假设递归函数已经写好
2. 寻找递归条件
3. 将递推关系添加到假设好的递归函数中，形成递归体
4. 寻找递归出口(临界条件)
5. 将临界条件添加到递归体中形成递归函数

function f(n){
  if(n===1){
    return 1;
  }
  return f(n-1) + 2;
}
function f(n){
  if(n===1){
    return 1;
  }
  return f(n-1) + f(n);
}

使用 for 循环遍历数组 for (var i=0; i<arr.length; i++) 中 i 值的数据类型是number，可以把数组中所有的值给遍历出来(指定位置的值已经删除的，会输出 undefined)
使用 for...in 循环遍历 for(var k in arr) 中 k 值得数据类型是string，且只遍历数组中存在的值

## 数组

arr.concat(数组1, 数组2...) 将多个数组拼接在一起
arr.join(指定的分隔符) 将数组按照指定的分隔符分割成字符串,

- arr.join() 没有指定默认为`,`分隔
- arr.join("") 如果传入的是空字符串，得到的结果是数组元素拼接后的结果
arr.pop() 删除并返回数组的最后一个元素，原数组末尾元素被删除

arr.push() 向数组末尾添加一个或者多个元素，并返回数组的长度 arr.push("a","b")

arr.shift() 在删除数组的开头一个或者多个元素，并返回新的长度
arr.unshift() 在数组的开头添加一个或者多个元素，并返回新的长度
arr.reverse() 将数组逆序排列

arr.slice(开始位置, 结束位置) 返回截取的数组，注意是左闭右开的，结束位置可选，如果没有表示从开始位置到结束
arr.sort() 对数组元素进行排序
arr.splice(从设么位置开始删除, 删除多少个, 在删除位置新增的元素(多个))

数组排序查看 Learn-Algorithms 项目

### JavaScript 中所有的非破坏性数组方法

- concat(): 连接两个或更多的数组，并返回结果
- every(): 检查数组中的所有元素是否符合指定条件
- filter(): 创建一个包含符合指定条件的所有元素的新数组
- find(): 返回数组中符合指定条件的第一个元素
- findIndex(): 返回数组中符合指定条件的第一个元素的索引
- flat(): 将嵌套的数组“展平”，并返回结果
- flatMap(): 对数组中的每个元素执行指定操作，并将结果“展平”为一个新数组
- forEach(): 对数组中的每个元素执行指定操作
- includes(): 检查数组是否包含指定元素
- indexOf(): 返回数组中指定元素的第一个出现位置的索引
- join(): 将数组中所有元素连接成一个字符串
- lastIndexOf(): 返回数组中指定元素最后一次出现位置的索引
- map(): 对数组中的每个元素执行指定操作，并返回结果
- reduce(): 对数组中的所有元素执行指定操作，并返回结果
- reduceRight(): 对数组中的所有元素执行指定操作，并返回结果（从右向左处理）
- slice(): 返回数组中指定范围内的元素
- some(): 检查数组中是否存在符合指定条件的元素
- sort(): 对数组进行排序
- toLocaleString(): 将数组转换为本地化字符串
- toString(): 将数组转换为字符串

### JavaScript 中所有的破坏性数组方法

- copyWithin(): 从数组中复制元素到指定位置，覆盖现有元素，并返回修改后的数组
- fill(): 用指定的值填充数组，并返回修改后的数组
- pop(): 移除数组中的最后一个元素，并返回该元素
- push(): 向数组末尾添加一个或多个元素，并返回修改后的数组长度
- reverse(): 颠倒数组中元素的顺序，并返回修改后的数组
- shift(): 移除数组中的第一个元素，并返回该元素
- sort(): 对数组中的元素进行排序，并返回修改后的数组
- splice(): 从数组中添加或移除元素，并返回被移除的元素
- unshift(): 向数组开头添加一个或多个元素，并返回修改后的数组长度

## 内置对象

  String 字符串对象
  Math 数学对象
  Number 数字对象
  Date 日期对象
  BOM 浏览器对象模型，操作浏览器的
  DOM 文档对象模型，操作网页

## 自定义变量

两种方法

- new 字符实例化
- 字面量方式定义 var obj = {};

## Data 对象

new Date("2019/09/17").getTime()
new Date("2019/09/17 13:10:16").toLocaleString()
获取给定时间 new Date("2018/11/18")
获取时间差 var c = new Date("2018/12/31") - new Date()
Math.floor((new Date("2018/12/31") - new Date())/24/60/60/1000)

new Date().toLocaleString() // "2018/11/18 下午10:41:10"

## BOM 对象

- window 对象
  - document 对象
    - DOM
  - history 对象
  - location 对象
  - navigator 对象
  - screen 对象
  - frames[] 为window对象的数组型属性，每一个数组元素对应框架集frameset 中的一个框架frames 所对应的窗口

window对象是脚本中的全局对象，可以在任何地方调用，脚本中任何对象的使用最终都要追溯到window 对象的访问
window前缀可以省略

window.alert()  --> alert()
window.document.write()  --> document.write()
confirm("确认")

var id = setInterval(function(){}, 时间) // 间歇调用
clearInterval(间歇调用id号)

var id = setTimeout(function(){}, 时间) // 超时调用
clearTimeout(超时调用id号)

screen 对象

- screen.availWidth 显示器屏幕可用宽度，除任务栏外
- screen.availHeight 显示器屏幕可用高度，除任务栏外
- width 实际宽
- height 实际高

history 对象

- length 属性，整数值，表示浏览器历史列表中的url 的个数
- back()  返回浏览器列表中当前页面之前的页面，浏览器返回功能
- forward() 前进到浏览器当前页面之后的页面，浏览器前进功能
- go(1) 访问浏览器列表中指定的页面，可正可负。负数返回，正数前进

location 对象

- protocol 表示协议部分，包含尾部的`:`
- href 表示当前页面完整的地址
- host 表示 主机和端口，包含hostname和port
- hostname 表示主机名部分
- pathname 表示页面路径部分，包含页面文件名称
- search 表示参数部分
- hash 表示锚点部分，包括前导符`#`

navigator 对象 包含浏览器的所有信息

- userAgent 用来判断当前的浏览器属性

## DOM 对象

DOM 可分为三部分

- 核心DOM, 用于XML和HTML的共用接口，操作节点数，如创建，删除，查找等
- XML DOM, 用于专门操作xml
- HTML DOM, 针对标签中的属性进行操作，修改属性，获取属性

document.getElementById("ID");
document.getElementsByTagName("标签名");
document.getElementsByClassName("类名"); IE9+
document.getElementsByName("属性"); input/select/textarea/button
获取到的元素都是对象(元素对象)

document.querySelector("选择器") // 返回页面的第一个元素
document.querySelectorAll["选择器"](2) // 返回页面中所有匹配的元素
这两个是H5的实现，有兼容性问题，高版本浏览器实现

元素对象中的属性，HTML标记的属性对应元素对象的一个同名属性

属性

- 标签属性：属性名 = "属性值"
- 样式属性：属性名 : "属性值"
  
获取属性 元素对象.属性
设置属性 元素对象.属性 = "属性值"

document.getElementById("showSuccess").style.display="block"
document.getElementById("sup-post-a").remove();
document.getElementsByClassName["g-browser g-clear"](0).remove();

```js
form 表单 通过 name 访问，有兼容性问题少用
<form action="#" name="myForm">
  <input type="radio" name="sex1" value="男" />
  <input type="radio" name="sex2" value="女" />
</form>

console.log(document.myForm.sex1)
```

控制台打印对象 chrome可能不兼容，火狐可行
console.debug()
