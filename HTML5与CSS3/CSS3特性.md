# CSS3特性

## 圆角
"border-radius: 10px;"

## 阴影
"box-shadow: 2px 4px 5px #ccc;"

`box-shadow: h-shadow v-shadow blur spread color inset;`

box-shadow 向框添加一个或多个阴影。

该属性是由逗号分隔的阴影列表，
每个阴影由 2-4 个长度值、可选的颜色值以及可选的 inset 关键词来规定。省略长度的值是 0。
```
h-shadow  必需。水平阴影的位置。允许负值。
v-shadow  必需。垂直阴影的位置。允许负值。
blur      可选。模糊距离。
spread    可选。阴影的尺寸。
color     可选。阴影的颜色。请参阅 CSS 颜色值。
inset     可选。将外部阴影 (outset) 改为内部阴影。
```

## 渐变
"background: linear-gradient(#fff, #333);"
"background: repeating-linear-gradient(60deg, #fb3, #fb3 15px, #58a 0, #58a 30px);"

background:
1. linear-gradient：纵向渐变
2. radial-gradient：横向渐变
3. repeating-linear-gradient：重复的纵向渐变
4. repeating-radial-gradient：重复的横向渐变

## 变换
"transform:rotate(-15deg)"

1. 矩阵变换 transform:matrix(0,1,1,1,10,10)
2. 平移 transform:translate(-10px,-10px)
3. 旋转 rotate(15deg)
4. 缩放 scale(.8)
5. 扭曲 skew(-30deg)

## 动画


## 媒体查询

## CSS3 背景图像区域 IE9+

backgroud-clip 属性 指定背景绘制区域
backgroud-clip: border-box | padding-box | content-box
border-box: 背景被裁减到边框盒
padding-box: 背景被裁减到内边距框
content-box: 背景被裁减到内容框

## CSS3 背景图像定位 IE9+

backgroud-origin 属性 设置元素背景图片的原始起始位置
backgroud-origin: border-box | padding-box | content-box
border-box: 背景图片相对于边框盒来定位
padding-box: 背景图片相对于内边距框来定位
content-box: 背景图片相对于内容框来定位

background-position 属性 定义背景图片的位置，两个值，水平和垂直偏移量，偏移量是相对左上角来说的，具体设置 backgroud-origin
 
## CSS3 背景图像大小 IE9+
background-size 属性 指定背景图片大小
background-size: length | percentage | cover | contain

background-size: 100%
percentage, 0 ~ 100% 之间的任意值，第二个值可有可无，没有默认为auto
当只设置第一个值时，第二个值根据图片宽度值来等比缩放
当两个值都有，按设置大小显示图片

cover, 将背景图片等比缩放以填充整个容器

contain, 将背景图片等比缩放至某一边紧贴容器边缘为止，满足宽度100%，或者高度100%

## CSS3 多重背景图像
background-image: url(img1.png), url(img2.jpg);
元素引用多个背景图片，前面图片依次覆盖后面图
img1会把img2覆盖，所以 img1 使用的是 png 格式

## CSS3 背景属性整合
在一个声明中设置所有背景属性

background: color position size repeat orign clip attachment image

实际应用中不推荐全部整合:
background: #ccc center 50% no-repeat content-box content-box  fixed url('img.jpg')

推荐:
background: #ccc url('img.jpg') no-repeat center center
background-size: 50%
background-origin: content-box;
background-clip: content-box;
background-attachment: fixed;

## CSS3 渐变 gradients
IE10+ Chrome26+ FireFox16+ Safari6.1+
可以在两个或多个指定的颜色之间显示平稳的过渡


## CSS3 线性渐变 linear gradients
沿着一根轴线改变颜色，从起点到终点颜色进行顺序渐变
background: linear-gradient(direction, color1, color2, ...)
direction 方向 默认从上到下
## CSS3 径向渐变
 31分
