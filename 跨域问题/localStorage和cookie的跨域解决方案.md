# localStorage和cookie的跨域解决方案

业务场景
cookie跨域的业务场景很多，例如：

1. 百度www域名下面登录了，发现yun域名下面也自然而然登录了。

1. 淘宝登录了，发现天猫也登录了，淘宝和天猫是完全不一样的2个域名。


## cookie跨域

首先说说同一个主域下面的跨域问题，类似www.百度 和yun.baidu

聊到这里，必须说一说cookie的参数或者属性了。 打开谷歌浏览器，找到cookie,如下图：

<img src="img/cookies-list.png" title="cookies-list"/>

关于具体每一个参数，这里就不详细介绍了，不清楚的大家可以搜索一下，下面主要介绍一下domain和path

### path

cookie 一般都是由于用户访问页面而被创建的，可是并不是只有在创建 cookie 的页面才可以访问这个cookie。

在默认情况下，出于安全方面的考虑，只有与创建 cookie 的页面处于同一个目录或在创建cookie页面的子目录下的网页才可以访问。

那么此时如果希望其父级或者整个网页都能够使用cookie，就需要进行路径的设置。

path表示cookie所在的目录，haorooms.com默认为/，就是根目录。 在同一个服务器上有目录如下：

/post/,/post/id/,/tag/,/tag/haorooms/，/tag/id/

现假设一个

cookie1的path为/tag/，

cookie2的path为/tag/id/，

那么tag下的所有页面都可以访问到cookie1，而/tag/和/tag/haorooms/的子页面不能访问cookie2。 
这是因为cookie2能让其path路径下的页面访问。

让这个设置的cookie 能被其他目录或者父级的目录访问的方法：

document.cookie = "name = value; path=/";

### domain

domain表示的是cookie所在的域，默认为请求的地址，

如网址为 http://www.haorooms.com/post/long_lianjie_websocket ，那么domain默认为www.haorooms.com。

而跨域访问，

如域A为love.haorooms.com，域B为resource.haorooms.com，

那么在域A生产一个令域A和域B都能访问的cookie就要将该cookie的domain设置为.haorooms.com；

如果要在域A生产一个令域A不能访问而域B能访问的cookie就要将该cookie的domain设置为resource.haorooms.com。

这样，我们就知道为什么www.百度 和yun.baidu共享cookie，我们只需要设置domain为.baidu.com就可以了【注：点好是必须的】

业务场景中问题2，天猫和淘宝是如何共享cookie的？

cookie跨域解决方案一般有如下几种：

### 1、nginx反向代理

反向代理（Reverse Proxy）方式是指以代理服务器来接受Internet上的连接请求，然后将请求转发给内部网络上的服务器；
并将从服务器上得到的结果返回给Internet上请求连接的客户端，此时代理服务器对外就表现为一个服务器。

反向代理服务器对于客户端而言它就像是原始服务器，并且客户端不需要进行任何特别的设置。
客户端向反向代理的命名空间(name-space)中的内容发送普通请求，接着反向代理将判断向何处(原始服务器)转交请求，
并将获得的内容返回给客户端，就像这些内容 原本就是它自己的一样。

nginx配置如下：

upstream web1{
     server  127.0.0.1:8089  max_fails=0 weight=1;
}
upstream web2 {
     server 127.0.0.1:8080   max_fails=0 weight=1;
}

　　　 location /web1 {
        proxy_pass http://web1;
        proxy_set_header Host  127.0.0.1;
        proxy_set_header   X-Real-IP        $remote_addr;
        proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;

        proxy_set_header Cookie $http_cookie;
        log_subrequest on;
    }

    location /web2 {
        proxy_pass http://web2;
        proxy_set_header Host  127.0.0.1;
        proxy_set_header   X-Real-IP        $remote_addr;
        proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
        proxy_set_header Cookie $http_cookie;
        log_subrequest on;
    }
    
### 2、jsonp方法
其实，淘宝和天猫cookie的传递，应该也是利用jsonp来进行的，如下图：

![](img/jsonp淘宝天猫.png)

打开淘宝首页，回向天猫发送一个请求。



说白了，这个jsonp 的cookie跨域和我们平时用的jsonp跨域是一样的，关于jsonp跨域，请看http://www.haorooms.com/post/js_kuayu_service

jsonp会通过回调函数来处理服务器端返回的数据，因为返回的可以执行的js代码（也就是重写cookie的path和域），然后自动执行返回的js代码，从而达到目的。

### 3、nodejs superagent
package.json中的模块依赖：

enter image description here

调用superagent api请求：

enter link description here

其实本质也是jsonp的方式。

同一域下，不同工程下的cookie携带问题，cookie跨域访问之后，可以成功的写入本地域。
本地的前端工程在请求后端工程时，有很多是ajax请求，ajax默认不支持携带cookie，

所以现在有以下两种方案：

1. 使用jsonp格式发送
1. ajax请求中加上字段 xhrFields: {withCredentials: true}，这样可以携带上cookie

enter image description here

服务器需要配置：

Access-Control-Allow-Credentials: true


## localStorage跨域
可以使用postMessage和iframe

思路如下：

假设有a.haorooms.com/text.html和b.haorooms.com/text.html两个页面。

通过a.haorooms.com/text.html页面去修改b.haorooms.com/text.html页面的本地数据：

1. 在a.haorooms.com/text.html页面创建一个iframe，嵌入b.haorooms.com/text.html页面。

1. a.haorooms.com/text.html页面通过postMessage传递指定格式的消息给b.haorooms.com/text.html页面。

1. b.haorooms.com/text.html页面解析a.haorooms.com/text.html页面传递过来的消息内容，调用localStorage API 操作本地数据。

1. b.haorooms.com/text.html页面包装localStorage的操作结果，并通过postMessage传递给a.haorooms.com/text.html页面。

1. a.haorooms.com/text.html页面解析b.haorooms.com/text.html页面传递回来的消息内容，得到 localStorage 的操作结果。

思路理清了，关于postMessage,我之前有文章专门介绍，请看文章：