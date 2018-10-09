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

