# window.postMessage跨域实现

window.postMessage虽然说是html5的功能，但是支持IE8+，假如你的网站不需要支持IE6和IE7，那么可以使用它。

window.postMessage是客户端和客户端直接的数据传递，既可以跨域传递，也可以同域传递。

### 应用场景

假如你有一个页面，页面中拿到部分用户信息，点击进入另外一个页面，另外的页面默认是取不到用户信息的，
你可以通过window.postMessage把部分用户信息传到这个页面中。（当然，你要考虑安全性等方面。）

### 实现

发送页面：
```javascript
//发送消息 
var domain = 'http://haorooms.com';
var myPopup = window.open(domain + '/windowPostMessageListener.html','myWindow');

//周期性的发送消息
setTimeout(function(){
    //var message = '当前时间是 ' + (new Date().getTime()); 
    var message = {name:"站点",sex:"男"}; //你在这里也可以传递一些数据，obj等
    console.log('传递的数据是  ' + message);
    myPopup.postMessage(message,domain);
},1000);
```
接收页面：
```javascript
//监听消息反馈
window.addEventListener('message',function(event) {
    if(event.origin !== 'http://haorooms.com') return; //这个判断一下是不是我这个域名跳转过来的
    console.log('received response:  ',event.data);
},false);
```
如果是使用iframe，代码应该这样写：
```javascript
//捕获iframe
var domain = 'http://haorooms.com';
var iframe = document.getElementById('myIFrame').contentWindow;

//发送消息
setTimeout(function(){
    //var message = '当前时间是 ' + (new Date().getTime()); 
    var message = {name:"站点",sex:"男"}; //你在这里也可以传递一些数据，obj等
    console.log('传递的数据是:  ' + message);
    //send the message and target URI
    iframe.postMessage(message,domain); 
},1000);
```

```javascript
//响应事件
window.addEventListener('message',function(event) {
    if(event.origin !== 'http://haorooms.com') return;
    console.log('message received:  ' + event.data,event);
    event.source.postMessage('holla back youngin!',event.origin);
},false);
```

上面的代码片段是往消息源反馈信息，确认消息已经收到。下面是几个比较重要的事件属性：

source – 消息源，消息的发送窗口/iframe。

origin – 消息源的URI(可能包含协议、域名和端口)，用来验证数据源。

data – 发送方发送给接收方的数据。