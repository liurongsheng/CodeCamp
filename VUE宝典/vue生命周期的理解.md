### vue生命周期的理解

vue生命周期总共分为8个阶段创建前/后，载入前/后，更新前/后，销毁前/后

    创建前/后： 在beforeCreated阶段，vue实例的挂载元素el还没有。
    
    载入前/后：在beforeMount阶段，vue实例的$el和data都初始化了，
    但还是挂载之前为虚拟的dom节点，data.message还未替换。
    在mounted阶段，vue实例挂载完成，data.message成功渲染。
    
    更新前/后：当data变化时，会触发beforeUpdate和updated方法。
    
    销毁前/后：在执行destroy方法后，对data的改变不会再触发周期函数，
    说明此时vue实例已经解除了事件监听以及和dom的绑定，但是dom结构依然存在。