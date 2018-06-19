### td 字符串太长隐藏处理
中字符串太长需要把超长的部分隐藏，同时显示省略号。并且鼠标滑过时会显示全部的内容
```
<td class="tdmax" title="显示的全部内容">要显示...</td>
.tdmax{
    max-width:250px;
    overflow:hidden;
    text-overflow:ellipsis;
    white-space:nowrap;
}
```
