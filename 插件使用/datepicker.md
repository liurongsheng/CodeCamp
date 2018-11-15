### 默认选择到年月

    $("#datepicker").datepicker( {
        format: "yyyy-mm",
        viewMode: "months", 
        minViewMode: "months"
    });

For version 1.2.0 and newer, viewMode has changed to startView, so use:

    $('#datepicker').datepicker({
        format:'yyyy-mm',
        startView:'months',
        minViewMode:'months',
    })
    
data-provide="datepicker" data-date-start-date="+1d" 起始时间是当前时间+1天

data-provide="datepicker" data-date-end-date="-1d" 终止时间是当前的昨天
data-provide="datepicker" data-date-end-date="0d"  终止时间是当前的天数
data-provide="datepicker" data-date-end-date="+1d" 终止时间是当前的明天

data-provide="datepicker" data-date-end-date="+1M" 终止时间是当前时间的+1月

<input class="blank" id="creationMonth" type="text" data-provide="datepicker" data-date-end-date="+1M" placeholder="请选择年月">
this.$("#creationMonth").datepicker({startView: 'months', minViewMode: 'months', format: 'yyyy-mm'});

```
Date.prototype.Format = function (fmt) {
    var o = {
        "M+": this.getMonth() + 1, //月份
        "d+": this.getDate(), //日
        "h+": this.getHours(), //小时
        "m+": this.getMinutes(), //分
        "s+": this.getSeconds(), //秒
        "q+": Math.floor((this.getMonth() + 3) / 3), //季度
        "S": this.getMilliseconds() //毫秒
    };
    if (/(y+)/.test(fmt))
        fmt = fmt.replace(RegExp.$1, (this.getFullYear() + "").substr(4 - RegExp.$1.length));
    for (var k in o)
        if (new RegExp("(" + k + ")").test(fmt))
            fmt = fmt.replace(RegExp.$1, (RegExp.$1.length === 1) ? (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
    return fmt;
};
```
new Date(new Date()-n*24*3600*1000).Format('yyyy-MM-dd')); 当前时间的前n天

new Date(new Date().getFullYear(), new Date().getMonth()-1, 1); 上个月的第一天

var date = new Date();
var day = new Date(date.getFullYear(), date.getMonth(), 0).getDate();
new Date(new Date().getFullYear(), new Date().getMonth()-1, day);  上个月的最后一天

