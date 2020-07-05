## Unity3D
- Unity是一款优秀的可视化3D开发引擎，让您的创意愿景迅速变为现实
- Unity在模拟应用、游戏及ⅦR/AR领域获得了很大成功。

2004年，Unity3d诞生于丹麦，05年将总部设在了美国的旧金山，并发布了 Unity1.0版本。到2010年时，Unity已具强大的跨平台能力，支持web ,ios，android, PC, PS3和XBOX360等二十多个平台，在产品类型上，支持2D3D应用开发。
国内众多知名公司、大厂使用U3D引擎开发产品。

https://unity3d.com/cn/get-unity/download/archive

https://assetstore.unity.com/top-assets/top-free

Unity3d引擎强大功能
- 强大的图形工具
- 基于物理的标准着色器
- 动态光照
- 强大的物理引擎
- 功能丰富且高度灵活的编辑器
- 丰富的功能强大的第三方插件
-  Unity云枃建功能
- 优秀的VRAR开发支持

## Lambda表达式
通过Lambda表达式，可以访问Lambda表达式块外部的变量，这称为闭包，这是一个非常好的功能，但如果不能正确的使用，也会非常危险
int somVal = 5;
    Func<int, int> f = x => x + somVal;
    Console.WriteLine(f(3)); // 8
    somVal = 7;
Console.WriteLine(f(3)); //10
这个方法的结果，不但受到参数的控制，还受到 somVal 变量的控制，结果不可控，容易岀现编程问题，用的时候要谨慎

## 碰撞检测 Collider Detection
通过检测对象的 collider 是否发生交互来判断对象发生碰撞

触发碰撞检测（Trigger Collision Detection）
当 collider 设置为触发模式，则检测其他对象的 collider 是否进入其范围来判断对象发生碰撞

射线追踪（Ray Casting）
在3D世界里从一个点到另外一个点画一条线来检测潜在的碰撞（对象的 collider 并没有实际发生碰撞或交互）

碰撞与触发
碰撞检测（collision detection）

回调函数：OnControllerColliderHit()/OnCollisionEnter()
OnControlllerColliderHit 只能在控制器对象的脚本中被调用

触发碰撞检测（Trigger collision detection）


以刚体属性可分为

静态碰撞器（Static Collider）游戏对象有 Collider组件，但是没有 Rigidbody组件是静止的，即使受到刚体碰童
刚体碰撞器（Rigidbody Collider）游戏对象包含 Collider组件，也包含 Rigidbody组件这是使用物理控制下的主要碰撞器
运动学刚体碰撞器（Kinematic Rigidbody Collider）
x包含 Collider组件和 Rigidbody组件，而且 Rigidbody的IsKinematic打勾这样的游戏对象是不能加力的，只能修改他的 transform才能移动，即使受到刚体碰撞

## 
