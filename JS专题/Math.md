# Math 对象属性

生成随机字符串 `Math.random().toString(36).substr(2)`

1. Math.random 生成随机数字16位小数
2. number.toString(36) 生成 0-9a-Z 的字符串
3. Math.random().toString(36).substr(2) 生成随机字符串

属性	描述

    E       返回算术常量 e，即自然对数的底数（约等于2.718）。
    LN2     返回 2 的自然对数（约等于0.693）。
    LN10	返回 10 的自然对数（约等于2.302）。
    LOG2E	返回以 2 为底的 e 的对数（约等于 1.414）。
    LOG10E	返回以 10 为底的 e 的对数（约等于0.434）。
    PI      返回圆周率（约等于3.14159）。
    SQRT1_2	返回返回 2 的平方根的倒数（约等于 0.707）。
    SQRT2	返回 2 的平方根（约等于 1.414）。


## Math 对象方法

ceil(x)	   对数进行上取整。

    //向上取整
    console.log(Math.ceil(2.2));//3
    console.log(Math.ceil(-2.2));//-2

floor(x)	对数进行下取整。
    
    //向下取整
    console.log(Math.floor(2.2));//2
    console.log(Math.floor(-2.2));//-3

round(x)	把数四舍五入为最接近的整数。

     //四舍五入
     console.log(Math.round(2.4));//2 四舍五入
     console.log(Math.round(-2.5));//-2 负数+0.5,向下取整
     console.log(Math.round(-2.6));//-3
     console.log(Math.round(-3.4));//-3

max(x,y)	返回 x 和 y 中的最高值。

    //返回最大值
    var max=Math.max(95,93,90,94,98);
    console.log(max);

min(x,y)	返回 x 和 y 中的最低值。
    
    //返回最小值
    var min=Math.min(95,93,90,94,98);
    console.log(min);

random()	返回 0 ~ 1 之间的随机数。
    
    //随机数
    var b=Math.random();//[0,1)
    var d=b*41//[0,41)所有数
    var e=d+10//[10,51)所有数
    var f=Math.floor(e)//[10,50]之间的整数

//10到50的区间，包含10也包含50
        
    var a=Math.floor(Math.random()*(50-10+1)+10);
验证：

    <script type="text/javascript" >
        var a,sum=[];
        for(var i=0;i<100000;i++){
            a=Math.floor(Math.random()*(50-10+1)+10);
            if(sum.indexOf(a)==-1)
            sum.push(a)
        }
        console.log("sum:"+sum.sort());
        console.log("length:"+sum.length);
    </script>


其他：
    
    abs(x)	    返回数的绝对值。
    acos(x)	    返回数的反余弦值。
    asin(x)     返回数的反正弦值。
    atan(x)	    以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值。
    atan2(y,x)  返回从 x 轴到点 (x,y) 的角度（介于 -PI/2 与 PI/2 弧度之间）。
    
    cos(x)	    返回数的余弦。
    exp(x)	    返回 e 的指数。
    log(x)	    返回数的自然对数（底为e）。
    pow(x,y)    返回 x 的 y 次幂。
    sin(x)	    返回数的正弦。
    sqrt(x)	    返回数的平方根。
    tan(x)	    返回角的正切。
    toSource()  返回该对象的源代码。
    valueOf()   返回 Math 对象的原始值。


parseFloat(totalAmount)/parseInt(totalNum)).toFixed(2) // 保留两位小数
