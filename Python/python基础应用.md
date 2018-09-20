
## python3.7 启动本地服务器

在Python2.6 版本里，/usr/bin/lib/python2.6/ 目录下会有 BaseHTTPServer.py, SimpleHTTPServer.py, CGIHTTPServer.py 三个文件，

在Python3.4 里，把上面的3个模块合并为了server 模块 (/usr/bin/python3.4/http/server.py)，所以启动服务器的代码也有所改变。

python2: `python -m SimpleHTTPServer 8081`
python3：`python -m http.server 8081`

其中8081端口号是自己可以设置的，默认端口号为8080

在浏览器中输入localhost:端口号，即可访问 `http://localhost:8081`

## 
