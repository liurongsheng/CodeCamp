# http-server

## 安装全局
`npm install http-server -g`

## 使用方法
`http-server [path] [options]`

`[path]` 如果 ./public 文件夹存在 则使用./public ，不存在则使用 ./

`[options]` 可选参数

    `-p` 配置端口 默认8080
    `-a` 配置地址 默认0.0.0.
    `-S` 或 `--ssl` 允许https
    `--cors` 允许跨域

使用案例：

>http-server C:\Users\Adminstrator\Music\test  -p 9999

打开Music\test文件夹下index.html，使用端口为9999 

[更多属性查看地址](https://www.npmjs.com/package/http-server)