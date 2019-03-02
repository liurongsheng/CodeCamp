# Flex布局

[练习网址flexboxfroggy](https://flexboxfroggy.com) https://flexboxfroggy.com

1. display: flex;  弹性盒子布局，容器自身认为是块元素
1. display: inline-flex;  弹性盒子布局，容器自身认为是行内元素
1. display: table; 表格布局
1. display: grid;  栅格布局

主轴 main axis
交叉轴 cross axis

弹性容器 flex container
弹性项目 flex item

Flexbox 是一维布局模型，没有列的概念，只有行的概念

- xx-items 作用于项目
- xx-content 作用于行

- 富余空间：在弹性容器规则和弹性项目显式宽度或者内容的共同约束下，行内剩余的水平空间，除去margin、padding的部分
- 挤压空间：弹性容器只会挤压弹性项目的content，其余如padding、margin和border不受影响

## 属性
- display:flex

- flex-direction 定义主轴的方向
  - row 水平从左到右 默认
  - row-reverse 水平从右到左
  - column 垂直
  - column-reverse 垂直反转

- flex-wrap 定义轴线的排列方式
  - nowrap 不换行 默认
  - wrap 换行
  - wrap-reverse 换行从下到上

- flew-flow 集合体 flex-direction 和flex-wrap 的缩写
```
.container {
    flex-flow: row-reverse wrap-reverse;
}
```

- justify-content 每行内的项目如何水平对齐，类似 text-align
  - flex-start 左端对齐 默认
  - flex-end 右端对齐
  - center 居中
  - space-between 表示两头的项目对齐容器壁，项目与项目之间的空隙平均分配
                  所谓的between指的就是项目之间
  - space-around  表示两头的项目与容器壁保留一个单位的空隙，项目与项目之间保持两个单位的空隙
                  around翻译成中文是周围，指的就是每个项目左右两边的空隙平均分配
  - space-evenly  表示两头的项目与容器壁之间的空隙和项目与项目之间的空隙都保持一个单位
                  evenly翻译成中文是均匀，指的是所有空隙平均分配


- align-items 每行内的项目如何垂直对齐
  - stretch 默认值，如果弹性项目显式的声明了高度，那stretch将不再起作用
  - flex-start 头部对齐
  - flex-end 底部对齐
  - center 居中
  - baseline 项目第一行文字的基线对齐
  
 
- align-content 将容器的一行视为最小单位，声明容器在交叉轴方向有富裕空间，如何垂直对齐。
                项目只有一根轴线的话，该属性不起作用
  - stretch 默认
  - flex-start 头部对齐
  - flex-end 底部对齐
  - center 居中
  - space-between 表示两头的项目对齐容器壁，项目与项目之间的空隙平均分配
  - space-around  表示两头的项目与容器壁保留一个单位的空隙，项目与项目之间保持两个单位的空隙
  - space-evenly  表示两头的项目与容器壁之间的空隙和项目与项目之间的空隙都保持一个单位

- align-self
 - auto 默认
 - stretch
 - flex-start 头部对齐
 - flex-end 底部对齐
 - center 居中
 - baseline


## 项目自身的属性

- order 项目之间的排列顺序，值越小排在前面，默认为0

- flex-grow 定义项目的放大比例，属性值只允许正整数。
  - 值为0，默认值，如果存在富余空间，也不放大
  - 值为1，等比例放大
  - 如果一个为2，其他为1，则按照比例平分剩余的空间
  
- flex-shrink 定义项目的缩小比例，属性值只允许正整数。
  - 值为0, 默认值，其他项目为1，则为0值的不缩小
  - 值为1，按照比例缩小

- flex-basics 预先分配给弹性项目的长度。它是width属性的替代品，优先级比width高
  - 默认为auto，即本来的大小
  - 200px，给的一个值

- flex 集合属性，是flex-grow flex-shrink flex-basics的缩写，默认为0 1 auto
  - auto (1 1 auto)
  - none (0 0 auto)


## 
