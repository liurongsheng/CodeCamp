判断对错
1) c#中关键字不能被用来做变量名。对
2) C#中标识符可以随意命名。错，数字不能放首位，标识符名不能是关键字
3) using语句表示引用命名空间。对

1) 下面转换哪些不是隐式转换？
- int转换为 short 不是隐式
- short转换为 int
- bool转换为 string 不是隐式
- byte转换为 float

2) 下面哪些变量名不合法？
- myVariablelsGood
-  99Flake 不合法
- time2GetJiggyWidit
- wrox.com 不合法

1)假如要输出10以内的所有能被2整除的数，下面代码有什么错误？
```
int i;
for(i=1; i<=10; i++){
    if((i%2)=0)
    Console.WriteLine(i)
}
```
判断语句有误 if((i%2)=0) ==> if((i%2)==0)

2)中断循环的方式错误的是(D)
A. return 
B. break 
C. continue 
D. end

3) (1<2) && (3==3）的值是？ true

4) 判断对错：&& 与 & 两个操作符没有区别。 错

5) 输出一个九九乘法表

```
using System;
public class Test{
    public static void Main(){
        for(int i=1; i<10; i++){
            for(int j=1; j<=i; j++){
                Console.WriteLine(j + "*" + i + "=" + (j*i) + "    ");
            }
            Console.WriteLine();
        }
    }
}
```
