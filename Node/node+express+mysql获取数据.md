# node + express + mysql获取数据

```
npm install express -g //全局安装
npm install express-generator -g //安装全局变量
npm install mysql
npm install sqlstring //简化SQL

cd example //进入项目文件夹
express project //创建express目录，project是目录名

cd project //进入项目根目录
npm install  //安装依赖

npm start //启动服务器
```
访问 [浏览器地址](http://localhost:3000)

## MySQL8.0下Authentication Method访问问题 [mysqlJS项目地址](https://github.com/mysqljs/mysql)
[issues地址](https://github.com/mysqljs/mysql/issues/1574)

root用户登录需要使用 Legacy Authentication Method 的方式

将加密方式改为旧的，在配置文件my.ini中添加如下：
C:\ProgramData\MySQL\MySQL Server 8.0\my.ini
```
# The default authentication plugin to be used when connecting to the server
default_authentication_plugin=mysql_native_password
```
windows 下为 my.ini ，linux 下为my.conf

使用了新的加密方式，改为旧的加密方式，而 root 用户也要进行相应的更改才可以，
因为 root 用户还是新的加密方式，所以使用 alter 语句改为重置密码来覆盖新的加密方式的密码：
```
ALTER USER 'root'@'localhost'
  IDENTIFIED WITH mysql_native_password
  BY 'password';
```
password 是你将要设置的 root 用户的密码。


## 请求获取数据

router.get('/', function(req, res, next) {
  res.render('index', { title: 'Express' });
}); 

## 主要代码
```
var express = require('express');
var router = express.Router();
var mysql = require('mysql');
var SqlString = require('sqlstring');

var pool = mysql.createPool({
  host     : 'localhost',  // 主机名
  port     : 3306, // 数据库连接的端口号 默认是3306
  database : 'pymysql', // 需要查询的数据库
  user     : 'root', // 用户名
  password : 'admin123' // 密码
});

// router.get('/', function(req, res, next) {
//   res.render('index', { title: 'Express' });
// });

// http://localhost:3000/getInfo?id=3  使用这个地址访问
router.get('/getInfo', function(req, res, next) {
  var id = req.query.id;
  pool.getConnection(function (err,connection) {
    if(err){
      console.log('与MySQL数据库建立连接失败！');
      console.log('错误信息为：' + err);
    }
    else{
      console.log('与MySQL数据库建立连接成功！');
      var selectSQL = SqlString.format('SELECT * FROM em_tours WHERE id = ?', [id]);
      connection.query(selectSQL, function (err, rs) {
        if (err) throw  err;
        console.log(rs);
        res.render('index', {title:'获取数据', res: JSON.stringify(rs) });
      })
    }
  })
});

module.exports = router;
```

## request 和 response 对象的具体介绍：

```
Request 对象 - request 对象表示 HTTP 请求，包含了请求查询字符串，参数，内容，HTTP 头部等属性。常见属性有：

req.app：当callback为外部文件时，用req.app访问express的实例
req.baseUrl：获取路由当前安装的URL路径
req.body / req.cookies：获得「请求主体」/ Cookies
req.fresh / req.stale：判断请求是否还「新鲜」
req.hostname / req.ip：获取主机名和IP地址
req.originalUrl：获取原始请求URL
req.params：获取路由的parameters
req.path：获取请求路径
req.protocol：获取协议类型
req.query：获取URL的查询参数串
req.route：获取当前匹配的路由
req.subdomains：获取子域名
req.accepts()：检查可接受的请求的文档类型
req.acceptsCharsets / req.acceptsEncodings / req.acceptsLanguages：返回指定字符集的第一个可接受字符编码
req.get()：获取指定的HTTP请求头
req.is()：判断请求头Content-Type的MIME类型
Response 对象 - response 对象表示 HTTP 响应，即在接收到请求时向客户端发送的 HTTP 响应数据。常见属性有：

res.app：同req.app一样
res.append()：追加指定HTTP头
res.set()在res.append()后将重置之前设置的头
res.cookie(name，value [，option])：设置Cookie
opition: domain / expires / httpOnly / maxAge / path / secure / signed
res.clearCookie()：清除Cookie
res.download()：传送指定路径的文件
res.get()：返回指定的HTTP头
res.json()：传送JSON响应
res.jsonp()：传送JSONP响应
res.location()：只设置响应的Location HTTP头，不设置状态码或者close response
res.redirect()：设置响应的Location HTTP头，并且设置状态码302
res.render(view,[locals],callback)：渲染一个view，同时向callback传递渲染后的字符串，如果在渲染过程中有错误发生next(err)将会被自动调用。callback将会被传入一个可能发生的错误以及渲染后的页面，这样就不会自动输出了。
res.send()：传送HTTP响应
res.sendFile(path [，options] [，fn])：传送指定路径的文件 -会自动根据文件extension设定Content-Type
res.set()：设置HTTP头，传入object可以一次设置多个头
res.status()：设置HTTP状态码
res.type()：设置Content-Type的MIME类型
```
