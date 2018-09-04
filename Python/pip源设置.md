# pip源设置

## pip国内的一些镜像
```
1. 阿里云 http://mirrors.aliyun.com/pypi/simple/ 
2. 中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/ 
3. 豆瓣(douban) http://pypi.douban.com/simple/ 
4. 清华大学 https://pypi.tuna.tsinghua.edu.cn/simple/ 
5. 中国科学技术大学 http://pypi.mirrors.ustc.edu.cn/simple/
```

## pip升级自身
```
pip install -U pip //升级pip

pip install --upgrade pip -i https://pypi.tuna.tsinghua.edu.cn/simple //临时指定源升级pip
```

## 临时使用 
可以在使用pip的时候在后面加上-i参数，指定pip源 
```
pip install scrapy -i https://pypi.tuna.tsinghua.edu.cn/simple

pip install pylint -i http://pypi.douban.com/simple 
``` 
## 永久修改
//如果使用http链接，则需要trusted-host参数：

linux: 
修改 ~/.pip/pip.conf (没有就创建一个)， 内容如下：

```
[global]
index-url = http://pypi.douban.com/simple
[install]
trusted-host=pypi.douban.com
```

windows: 
直接在user目录中创建一个pip目录，如：C:\Users\xx\pip，新建文件pip.ini，内容如下

```
[global]
index-url = http://pypi.douban.com/simple
[install]
trusted-host=pypi.douban.com
```


## 常用软件

pip install pylint
pip install autopep8

