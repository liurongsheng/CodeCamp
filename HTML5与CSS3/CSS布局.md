## 边框

### box-shadow
设置或检索对象阴影
box-shadow：none | <shadow> [ , <shadow> ]*

适用于：所有元素

常用：
box-shadow: 5px 5px rgba(0, 0, 0, .6);

取值：
```
none：
无阴影
<length>①：
第1个长度值用来设置对象的阴影水平偏移值。可以为负值
<length>②：
第2个长度值用来设置对象的阴影垂直偏移值。可以为负值
<length>③：
如果提供了第3个长度值则用来设置对象的阴影模糊值。不允许负值
<length>④：
如果提供了第4个长度值则用来设置对象的阴影外延值。可以为负值
<color>：
设置对象的阴影的颜色。
inset：
设置对象的阴影类型为内阴影。该值为空时，则对象的阴影类型为外阴影
```
## 文本

### vertical-align
设置或检索内联元素在行框内的垂直对齐方式
baseline | sub | super | top | text-top | middle | bottom | text-bottom | <percentage> | <length>

常用：
vertical-align：middle 中部对齐

默认值：baseline

适用于：内联及 table-cell 元素

### word-spacing 
设置对象中的单词之间的最小，最大和最佳间隙
word-spacing：normal | <length> | <percentage>

适用于：所有元素
```
取值：
normal：
默认间隔
<length>：
用长度值指定间隔。可以为负值。
<percentage>：
用百分比指定间隔。可以为负值。（CSS3）
```
