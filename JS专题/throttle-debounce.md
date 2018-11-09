# throttle-debounce

[开源地址](https://github.com/niksy/throttle-debounce) https://github.com/niksy/throttle-debounce

## throttle 节流

一次操作后，在一定的时间内屏蔽操作。在多次重复快速点击按钮的情景下，只发送第一次的点击事件，屏蔽后面一定时间的触发。

onChange={throttle(3000, true, (v)=> console.log(v)}) }
3 秒内只执行一次

## debounce 防抖

根据输入的信息，发送请求查询后台数据。在一直输入的情景下不发送请求，当输入结束后发送一次请求。

```
sss = () => {
  console.log("点击了");
}

<Button onClick={debounce(1000, ()=>this.sss())} disabled={!(sendMessage==='发送短信码')}>{sendMessage}</Button>
<Button onClick={debounce(1000, this.sss)} disabled={!(sendMessage==='发送短信码')}>{sendMessage}</Button>

onClick={debounce(1000, ()=>this.sss())}
onClick={debounce(1000, this.sss)}
```
单位事件内一直点击情形下，不发送事件，当没有新点击的时候，发送事件。
