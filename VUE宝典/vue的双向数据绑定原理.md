### vue的双向数据绑定原理

vue.js 是采用数据劫持结合发布者-订阅者模式的方式，
通过Object.defineProperty()来劫持各个属性的setter，getter，
在数据变动时发布消息给订阅者，触发相应的监听回调。

具体步骤：

    第一步：需要observe的数据对象进行递归遍历，包括子属性对象的属性，
    都加上 setter和getter。这样的话，给这个对象的某个值赋值，就会触发setter，
    那么就能监听到了数据变化

    第二步：compile解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，
    并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，
    一旦数据有变动，收到通知，更新视图

    第三步：Watcher订阅者是Observer和Compile之间通信的桥梁，主要做的事情是:
    1、在自身实例化时往属性订阅器(dep)里面添加自己
    2、自身必须有一个update()方法
    3、待属性变动dep.notice()通知时，能调用自身的update()方法，
       并触发Compile中绑定的回调，则功成身退。

    第四步：MVVM作为数据绑定的入口，整合Observer、Compile和Watcher三者，
    通过Observer来监听自己的model数据变化，通过Compile来解析编译模板指令，
    最终利用Watcher搭起Observer和Compile之间的通信桥梁，达到数据变化 -> 视图更新；
    视图交互变化(input) -> 数据model变更的双向绑定效果。