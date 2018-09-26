# Flex布局

## 容器

- display:flex
- flex-direction 定义主轴的方向
- flex-wrap 定义轴线的排列方式
- flew-flow flex-direction和flex-wrap的缩写

- justify-content 主轴的对其方式
  - flex-start
  - flex-end
  - center
  - space-between 两端对其
  - space-around 项目两侧的间隔相等
  
- align-items 交叉轴的对其方式
  - flex-start
  - flex-end
  - center
  - baseline 项目第一行文字的基线对齐
  - stretch 默认值
 
- align-content 定义多条轴线的对齐方式，项目只有一根轴线的话，该属性不起作用
  - flex-start
  - flex-end
  - center
  - space-between 两端对其
  - space-around 项目两侧的间隔相等
  - stretch
  
## 项目

- order 项目的排列顺序，值越小排在前面
- flex-grow 定义项目的放大比例 默认为0，如果存在剩余空间，也不放大
  - 值为1，等比例放大
  - 如果一个为2，其他为1，则按照比例平分剩余的空间
  
- flex-shrink 定义项目的缩小比例，默认为1
  - 值为1，按照比例缩小
  - 值为0, 其他项目为1，则为0值得不缩小

- flex-basics 定义在分配多余空间之前，项目占据主轴空间，默认为auto,即本来的大小

- flex是flex-grow flex-shrink flex-basics的缩写，默认为0 1 auto
  - auto (1 1 auto)
  - none (0 0 auto)