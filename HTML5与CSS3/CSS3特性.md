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
