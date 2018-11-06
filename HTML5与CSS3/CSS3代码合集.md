# CSS3代码合集

## 图片旋转
```
// html
<img class="rotation" src="./loading.png" title="等待中旋转" width="42px">

// css
.rotation {
    transform: rotate(360deg);
    animation: rotation 3s linear infinite;
    -moz-animation: rotation 3s linear infinite;
    -webkit-animation: rotation 3s linear infinite;
    -o-animation: rotation 3s linear infinite;
}
@-webkit-keyframes rotation{
    from {-webkit-transform: rotate(0deg)}
    to {-webkit-transform: rotate(360deg)}
}
```

## 伪类选择器
.consoleSortUl>li:first-child{} 选择第一项
.consoleSortUl>li:nth-child(1){} 选择第一项
.consoleSortUl>li:nth-child(2){} 选择第二项
.consoleSortUl>li:nth-child(3){} 选择第三项

.consoleSortUl>li:nth-last-child(3){} 选择倒数第三项
.consoleSortUl>li:last-child{} 选择最后一项

## 属性选择器
<div title="lliu">测试</div>
```
[title="lliu"]{background: #f00;}  选择 title 属性名为`lliu`的元素
[title*="lliu"]{background: #f00;} 选择 title 属性名包含`lliu`的元素
[title^="lliu"]{background: #f00;} 选择 title 属性名以`lliu`开头的元素
[title$="lliu"]{background: #f00;} 选择 title 属性名以`lliu`结尾的元素
```
a[href^="http://abc.com"]{ color: blue;} 指定网站前缀，匹配的显示蓝色
