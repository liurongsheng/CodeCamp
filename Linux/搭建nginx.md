# 搭建 nginx

## 安装编译工具及库文件
```
yum -y install make zlib zlib-devel gcc-c++ libtool  openssl openssl-devel
cd /usr/local/src
wget http://downloads.sourceforge.net/project/pcre/pcre/8.35/pcre-8.35.tar.gz
tar -xvf pcre-8.35.tar.gz
cd pcre-8.35
./configure
make && make install
pcre-config --version  //查看pcre版本
```

## 下载nginx的tar包
```
cd /usr/local
mkdir nginx && cd nginx
wget http://nginx.org/download/nginx-1.15.2.tar.gz
tar -xvf nginx-1.15.2.tar.gz
```

## 安装nginx
```
cd nginx-1.15.2
mv * ..
cd ..
rm -rf nginx-1.15.2
./configure --prefix=/usr/local/webserver/nginx --with-http_stub_status_module --with-http_ssl_module --with-pcre=/usr/local/src/pcre-8.35
make && make install
/usr/local/webserver/nginx/sbin/nginx -v //查看nginx版本
```

### 配置nginx

### 创建 Nginx 运行使用的用户 www：
```
/usr/sbin/groupadd www 
/usr/sbin/useradd -g www www
```
### 配置nginx.conf
```
vi /usr/local/webserver/nginx/conf/nginx.conf
// 把#user nobody 启用为www;
user www;
/usr/local/webserver/nginx/sbin/nginx
```
```
killall -9 nginx
ps aux | grep nginx
/usr/local/webserver/nginx/sbin/nginx
ps aux | grep nginx
```
访问虚拟机地址http://192.168.123.3/即可到Welcome to nginx!页面
```
/usr/local/webserver/nginx/sbin/nginx -s reload            # 重新载入配置文件
/usr/local/webserver/nginx/sbin/nginx -s reopen            # 重启 Nginx
/usr/local/webserver/nginx/sbin/nginx -s stop              # 停止 Nginx
```
nginx 报异常"/usr/local/nginx/logs/nginx.pid" failed (2: No such file or directory)处理方法
使用nginx -c的参数指定nginx.conf文件的位置
`/usr/local/webserver/nginx/sbin/nginx -c /usr/local/webserver/nginx/conf/nginx.conf`