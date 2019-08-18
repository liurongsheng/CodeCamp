## C#
C#语言从C++语言发展而来，结合了各种不同语言的优势更加简单易用。C#做为 Unity3D开发脚本之一，因其与C++语法相似而受大广开发人员的喜爱。
C#是徽软开发的面向对象编程语言。有强大的.Net类库支持。Unity3的C#脚本语言基于Mono的.Net平台上运行，在U3D的脚本开发中主要用到C#的基础语法。
因而在快速入门教程中以C#的基本语法讲解为主，配以相应的练习题帮助同学们快速入门U3D脚本开发。

## 在线编译器 ideone
http://www.ideone.com/

## 关键字
关键字是用来定义c#语言的字符串记号。

常见关键字有abstract cost interface sizeof finally is new this void params 等等
注：关键字不能被用来做变量名或者其他形式的标识符，除非以@字符开始：所有C#关键字全部由小写字母组成

### 变量声明和赋值
`<type><name>`
- type表示变量的类型，相当于什么样的盒子；name表示变量名称，相当于代表数据的名称
- 每个声明都是一条语句，语句以` ;` 结束。
- 我们可以使用一条语句声明多个类型一样的变量   String name1，name2
  
PascalCase指定名称中的每个单词除了第一个字母大写外，其余字母都是小写。camelCase指定第一个单词以小写字母开头，其余的每个单词除了第一个字母大写，其余都小写
举几个命名示例
camelCase变量名
- firstName 
- timeOfDeath 

PasclCase变量名
- TimeOfDeath

变量的命名建议：对于简单的变量，使用 camelcase规则，
而比较高级的命名则使用PascalCase规则。

## 变量类型

### 整数
- byte表示无符号的8位整数 0~255
- short表示有符号的16位整数 -32768~32767
- int表示有符号的32位整数 -2147483648~2147483647
- byte表示有符号的8位整数 -128~127
- ushort表示无符号的16位整数 0~65535

- uint表示无符号的32位整数 0~4294967295 
- long表示有符号的64位整数 -9223372036854775808~9223372036854775807 
- ulong表示无符号的64位整数 0-1844640737955161 
- char表示无符号的16位整数 0~65535 

Char类型与其他整数类型相比有以下两点不同之处：
A：没有其他类型到char类型的隐式转换即使是对于 sbyte, byte和ushort这样能完全使用char类型代表其值的类型，
sbyte, byte和ushort到char的隐式转换也不存在.
B:char类型的常量必须被写为字符形式，如果用整数形式，则必须带有类型转换前缀。

### 浮点
float表示有符号的32位浮点数，精度7位-3.4*10^38~+3.4×10^38 
double表示有符号的64位浮点数，精度15-16位 ±5.0×10^-324到±1.7×10^308

非数值类型（字符类型或者布尔类型）
- bool表示一个布尔类型，布尔值：true或fase
- string表示一个字符序列 零个或多个 Unicode字符

### 枚举
```
enum<typeName>{
    <value1>,
    <value2>,
    <value3>,
    ...
}
```
定义一个枚举类型变量并赋值：Gamestate state= Gamestate.Start;

### 结构体
struct<typeName>{
    <memberDeclartions>
}

struct Vector3{
    float x;
    float y;
    float z;
}

### 数组
数组是具有索引的同类型对象的集合，C#中的数组都是对象。C#提供了声明Array的内置语法，但实际上创建的是System Array类型的对象
<baseType>[]<name>;

## Unity 的五大基本界面
- 1. 场景（Sence），构建游戏的地方
- 2. 层级（Hierarchy），场景中的游戏对象都列在这里
- 3. 检测面板（nspector），当前选中的资源或对象的设置，是一些变量和组件的集合
- 4. 游戏（Game），演示窗口，仅在播放模式中演示
- 5. 项目（Project），一些资源的列表，和库的概念一样

## 碰撞事件方法
- OnCollisionEnter(Conllision other) 在刚体与刚体开始接触时候调用此方法，(记住是刚体之间的碰撞) 
- OnCollisionStay(Conllision other) 在刚体与刚体碰撞的过程中，帧都会调用此方法，直到碰撞结束
- OnCollisionExit(Conllision other) 在刚体与刚体停止接触时，调用此方法

- OnTriggerEnter(Collider other) 当 Collider（碰撞体）进入 trigger（触发器）时调用，
这个消息被发送到触发器碰撞体和刚体（或者碰撞体假设没有刚体）。注意如果碰撞体附加了一个刚体，也只发送触发器事件
- OnTriggerStay(Collider other) 当 Collider（碰撞体）进入 trigger（触发器）的过程中，帧都会调用此方法，直到碰撞结束
- OnTriggerExit(Collider other) 当 Collider（碰撞体）与 trigger（触发器）的停止接触时，调用此方法

## Mouse事件
OnMouseDown()在具有 GUIElement 或 Collider的对象上按下鼠标时被调用
OnMouseUp()在松开鼠标时被调用，即使不在具有 GUIElement 或 Collider 的对象上
OnMouseEnter()在进入具有 GUIElement 或 Collider 的对象范围内时被调用
OnMouserExit()在离开具有 GUIElementeCollider 的对象范围内时被调用

## 常用组件
- 变换组件
Transform

- 刚体物理
Rigidbody

- 场景管理
SceneManager

- 动画系统
Animation动画、Animator动画状态机

- 摄像机
Camera

- 对象
GameObject游戏对象、Object对象

- 时间系统
Time

- 向量
Vector2 (开发界面)、Vector3 (速度、位置、角度、加速度)、Vector4 (矩阵计算)

- 输入系统
Input

- 数学类
Mathf

## MonoBehaviour 类
MonoBehaviour是所有脚本的基类，使用C#就必须显示从 MonoBehaviour 继承。用u3d创建脚本，会自动创建继承 MonoBehaviour 的脚本文件。

Start()：Start只在 Update 第一次被调用前执行一次。

Update(): 每帧执行一次

FixedUpdate()：以固定的时间间隔执行，不受帧率影响，默认0.02s，如果卡帧了 Update 就不会再执行，而 FixedUpdate 则继续执行。
时间间隔可以在Edit-> ProjectSetting > time > fixedtimestep 中修改。主要用于处理物理逻辑比如 Rigidbody 等

LateUpdate()：LateUpdate是在所有 Update 函数调用后被调用。比如相机跟随就可以用这个函数，即人物移动在 Update 中实现，相机跟随在 LateUpdate() 中实现，
Play后的效果是：角色移动发生在前，相机移动紧跟其后

OnGUI：渲染和处理GU|事件时调用，用于渲染图形界面，同样很重要

OnDisable()：当对象变为不可用或非激活状态时此函数被调用

OnDestroy()：当 MonoBehaviour将被销毁时，这个函数被调用

## 生命周期
Unity脚本从唤醒到销毀都有着一套比较完善的生命周期，添加任何脚本都要遵守生命周期法则
接下来介绍几种系统自调用的重要方法。首先要我们先来说明一下它们的执行顺序：

Awake --> Start --> Update -> FixedUpdate --> LateUpdate --> OnGUI --> Reset --> OnDisable --> OnDestroy

Awake:
用于在游戏开始之前初始化变量或游戏状态。在脚本整个生命周期内它仅被调用一次 
Awake在所有对象被初始化之后调用，所以你可以安全的与其他对象对话或用诸如 
GameObject.FindWithTag() 这样的函数搜索它们。每个游戏物体上的 Awake 以随机的顺序被调用
因此，你应该用 Awake 来设置脚本间的引用，并用 Start 来传递信息 Awake 总是在 Start 之前被调用。它不能用来执行协同程序

Start:
仅在 Update 函数第一次被调用前调用。Start 在 behaviour 的生命周期中只被调用一次。它和 Awake 的不同是 Start 只在脚本实例被启用时调用
你可以按需调整延迟初始化代码。Awake 总是在 Start 之前执行。这允许你协调初始化顺序。在所有脚本实例中，Start 函数总是在 Awake 函数之后调用

Update:
正常帧更新，用于更新逻辑。每一帧都执行，Update 就比较适合做控制。 物体的移动位置可以在这里操作

FixedUpdate:
固定帧更新，处理 Rigidbody时，需要用 FixedUpdate代替 Update。例如给刚体加一个作用力时，你必须应用作用力在 FixedUpdate 里的固定帧，而不是 Update 中的帧
（两者帧长不同）FixedUpdate，每固定帧绘制时执行一次，和 update 不同的是 FixedUpdate 是渲染帧执行，如果你的渲染效率低下的时候 FixedUpdate 调用次数就会跟着下降
FixedUpdate 比较适用于物理引擎的计算，因为是跟每帧渲染有关
在Uniy导航菜单栏中，点击"Edit"->"Project Setting" "Time" 莱单项后，右侧的 Inspector 视图将弹出时间管理器，其中Fixed Timestep 选项用于设置 FixedUpdate0的更新频率，更新频率默认为0.025

LateUpdate:
在所有 Update 函数调用后被调用，和 fixedupdate 一样都是每一帧都被调用执行，这可用于调整脚本执行顺序
例如：当物体在 Update 里移动时，跟随物体的相机可以在 LateUpdate 里实现。LateUpdate，在每帧 Update 执行完毕调用，他是在所有 update 结束后才调用
比较适合用于命令脚本的执行。官网上例子是摄像机的跟随，都是在所有 update 操作完才跟进摄像机，不然就有可能出现摄像机已经推进了，但是视角里还未有角色的空帧出现

OnGUI:
在渲染和处理GUI事件时调用。比如：你画一个 button 或 label 时常常用到它。这意味着 OnGUI 也是每帧执行一次

Reset:
在用户点击检视面板的 Reset 按钮或者首次添加该组件时被调用。此函数只在编辑模式下被调用。Reset最常用于在检视面板中给定一个默认值。把组件的所有参数设置为默认值

OnDisable:
当物体被销毁时 OnDisable 将被调用，并且可用于任意清理代码。脚本被卸载时，OnDisable 将被调用，OnEnable在脚本被载入后调用

OnDestroy:
当 MonoBehaviour 将被销毁时，这个函数被调用。OnDestroy 只会在预先已经被激活的游戏物体上被调用

## Vector3 向量类
表示3维向量的点
Vector3.forward 表示向前方向一个单位的向量，等同于 newVertor3(0,0,1)

## 常用函数
Distance 计算两点之间的距离
SmoothDamp 平滑的从A点移动到B点，常用于相机平滑的跟随目标
