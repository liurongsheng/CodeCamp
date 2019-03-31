# HTTP cookies

`存储大小是4k之内`
HTTP Cookie（也叫Web Cookie或浏览器Cookie）是服务器发送到用户浏览器并保存在本地的一小块数据，
它会在浏览器下次向同一服务器再发起请求时被携带并发送到服务器上。通常，它用于告知服务端两个请求
是否来自同一浏览器，如保持用户的登录状态。Cookie使基于无状态的HTTP协议记录稳定的状态信息成为了可能

## Cookie主要用于以下三个方面：

会话状态管理（如用户登录状态、购物车、游戏分数或其它需要记录的信息）
个性化设置（如用户自定义设置、主题等）
浏览器行为跟踪（如跟踪分析用户行为等）

Cookie曾一度用于客户端数据的存储，因当时并没有其它合适的存储办法而作为唯一的存储手段，
但现在随着现代浏览器开始支持各种各样的存储方式，Cookie渐渐被淘汰。

由于服务器指定Cookie后，浏览器的每次请求都会携带Cookie数据，会带来额外的性能开销（尤其是在移动环境下）。
新的浏览器API已经允许开发者直接将数据存储到本地，如使用 Web storage API （本地存储和会话存储）或 IndexedDB 。

### Web storage API

* sessionStorage 为每一个给定的源（given origin）维持一个独立的存储区域，
  该存储区域在页面会话期间可用（即只要浏览器处于打开状态，包括页面重新加载和恢复）。
* localStorage 同样的功能，但是在浏览器关闭，然后重新打开后数据仍然存在

这两种机制是通过 Window.sessionStorage 和 Window.localStorage 属性使用（更确切的说，
在支持的浏览器中 Window 对象实现了 WindowLocalStorage 和 WindowSessionStorage 对象并
挂在其 localStorage 和 sessionStorage 属性下）—— 调用其中任一对象会创建 Storage 对象，
通过 Storage 对象，可以设置、获取和移除数据项。对于每个源（origin）sessionStorage 和 
localStorage 使用不同的 Storage 对象——独立运行和控制。

`Internet Explorer 8 及以上才支持 sessionStorage 和 localStorage`

### [IndexedDB](https://developer.mozilla.org/zh-CN/docs/Web/API/IndexedDB_API)
虽然 Web Storage 对于少量的数据很有用，但对于存储大量的结构化数据来说，这种方法不太有用。IndexedDB提供了一个解决方案
```
var request = window.indexedDB.open("liu",1)//1是可选的版本号
request.onupgradeneeded = function(event) {
var db = event.target.result;

  // 创建一个对象存储空间来持有有关我们客户的信息。
  // 我们将使用 "ssn" 作为我们的 key path 因为它保证是唯一的。
  var objectStore = db.createObjectStore("customers", { keyPath: "ssn" });

  // 创建一个索引来通过 name 搜索客户。
  // 可能会有重复的，因此我们不能使用 unique 索引。
  objectStore.createIndex("name", "name", { unique: false });

  // 创建一个索引来通过 email 搜索客户。
  // 我们希望确保不会有两个客户使用相同的 email 地址，因此我们使用一个 unique 索引。
  objectStore.createIndex("email", "email", { unique: true });

  // 在新创建的对象存储空间中保存值
  for (var i in customerData) {
    objectStore.add(customerData[i]);
  }
}
```
IndexedDB没有大小限制，初始分配50M，如果用户同意，还可以再增加。
Web storage API的话，限制明显：
1. Safari桌面浏览器(Mac以及 Windows)没有限制；   
1. Mobile Safari限制为10MB；
1. Chrome限制为5MB；
1. Android浏览器对应用程序缓存大小没有限制；   
1. Firefox桌面版有无限的应用程序缓存大小；
1. Opera的应用程序缓存大小可以由用户管理，但有一个默认大小50MB;

`Internet Explorer 10 及以上才支持 sessionStorage 和 localStorage`


## 创建Cookie

当服务器收到HTTP请求时，服务器可以在响应头里面添加一个Set-Cookie选项。
浏览器收到响应后通常会保存下Cookie，之后对该服务器每一次请求中都通过Cookie请求头部将Cookie信息发送给服务器。
另外，Cookie的过期时间、域、路径、有效期、适用站点都可以根据需要来指定。

### Set-Cookie响应头部和Cookie请求头部

服务器使用Set-Cookie响应头部向用户代理（一般是浏览器）发送Cookie信息。一个简单的Cookie可能像这样：

>Set-Cookie: <cookie名>=<cookie值>

服务器通过该头部告知客户端保存Cookie信息。

```
HTTP/1.0 200 OK
Content-type: text/html
Set-Cookie: yummy_cookie=choco
Set-Cookie: tasty_cookie=strawberry
```
现在，对该服务器发起的每一次新请求，浏览器都会将之前保存的Cookie信息通过Cookie请求头部再发送给服务器。

```
GET /sample_page.html HTTP/1.1
Host: www.example.org
Cookie: yummy_cookie=choco; tasty_cookie=strawberry
```

## 会话期Cookie

会话期Cookie是最简单的Cookie：浏览器关闭之后它会被自动删除，也就是说它仅在会话期内有效。
会话期Cookie不需要指定过期时间（Expires）或者有效期（Max-Age）。需要注意的是，有些浏览器提供了会话恢复功能，
这种情况下即使关闭了浏览器，会话期Cookie也会被保留下来，就好像浏览器从来没有关闭一样。

## 持久性Cookie

和关闭浏览器便失效的会话期Cookie不同，持久性Cookie可以指定一个特定的过期时间（Expires）或有效期（Max-Age）。
>Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT;

## Cookie的Secure 和HttpOnly 标记

标记为 Secure 的Cookie只应通过被HTTPS协议加密过的请求发送给服务端。
但即便设置了 Secure 标记，敏感信息也不应该通过Cookie传输，因为Cookie有其固有的不安全性，
Secure 标记也无法提供确实的安全保障。从 Chrome 52 和 Firefox 52 开始，不安全的站点（http:）无法使用Cookie的 Secure 标记。

为避免跨域脚本 (XSS) 攻击，通过JavaScript的 Document.cookie API无法访问带有 HttpOnly 标记的Cookie，它们只应该发送给服务端。
如果包含服务端 Session 信息的 Cookie 不想被客户端 JavaScript 脚本调用，那么就应该为其设置 HttpOnly 标记。