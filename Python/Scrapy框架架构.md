# Scrapy框架架构
[官网文档](https://scrapy.org)

## Scrapy框架介绍：
写一个爬虫，需要做很多的事情。比如：发送网络请求、数据解析、数据存储、反反爬虫机制（更换ip代理、设置请求头等）、异步请求等。
这些工作如果每次都要自己从零开始写的话，比较浪费时间。

因此Scrapy把一些基础的东西封装好了，在他上面写爬虫可以变的更加的高效（爬取效率和开发效率）。
因此真正在公司里，一些上了量的爬虫，都是使用Scrapy框架来解决。

## Scrapy框架模块功能：

1. Scrapy Engine（引擎）：Scrapy框架的核心部分。负责在Spider和ItemPipeline、Downloader、Scheduler中间通信、传递数据等。
2. Spider（爬虫）：发送需要爬取的链接给引擎，最后引擎把其他模块请求回来的数据再发送给爬虫，爬虫就去解析想要的数据。
   这个部分是我们开发者自己写的，因为要爬取哪些链接，页面中的哪些数据是我们需要的，都是由程序员自己决定。
3. Scheduler（调度器）：负责接收引擎发送过来的请求，并按照一定的方式进行排列和整理，负责调度请求的顺序等。
4. Downloader（下载器）：负责接收引擎传过来的下载请求，然后去网络上下载对应的数据再交还给引擎。
5. Item Pipeline（管道）：负责将Spider（爬虫）传递过来的数据进行保存。具体保存在哪里，应该看开发者自己的需求。
6. Downloader Middlewares（下载中间件）：可以扩展下载器和引擎之间通信功能的中间件。
7. Spider Middlewares（Spider中间件）：可以扩展引擎和爬虫之间通信功能的中间件。

## 快速安装
1. 安装：通过 `pip install Scrapy` 即可安装。
2. [Scrapy官方文档](http://doc.scrapy.org/en/latest)：http://doc.scrapy.org/en/latest
3. [Scrapy中文文档](http://scrapy-chs.readthedocs.io/zh_CN/latest/index.html)：http://scrapy-chs.readthedocs.io/zh_CN/latest/index.html

如果在windows系统下，提示这个错误`ModuleNotFoundError: No module named 'win32api'`，那么使用以下命令可以解决：`pip install pypiwin32`；
提示这个错误`Could not find suitable distribution for Requirement.parse('incremental>=16.10.1')`
```python
pip install --upgrade incremental
pip install Twisted
pip install Scrapy
```
`pip install Twisted` 如果出错报 `error: Microsoft Visual C++ 14.0 is required. Get it with "Microsoft Visual C++ Build Tools": https://visualstudio.microsoft.com/downloads/`
需要到网站下载匹配的离线包安装 `https://www.lfd.uci.edu/~gohlke/pythonlibs/#twisted`,
然后进入下载的文件夹安装 `pip install .\Twisted‑18.7.0‑cp37‑cp37m‑win_amd64.whl`
 
 
如果在ubuntu上安装scrapy之前，需要先安装以下依赖：
`sudo apt-get install python3-dev build-essential python3-pip libxml2-dev libxslt1-dev zlib1g-dev libffi-dev libssl-dev`，然后再通过 `pip install scrapy` 安装。

## 创建项目
要使用Scrapy框架创建项目，需要通过命令来创建。首先进入到你想把这个项目存放的目录。

然后使用以下命令创建：

`scrapy startproject [项目名称]`

## 目录结构
1. items.py：用来存放爬虫爬取下来数据的模型。
2. middlewares.py：用来存放各种中间件的文件。
3. pipelines.py：用来将items的模型存储到本地磁盘中。
4. settings.py：本爬虫的一些配置信息（比如请求头、多久发送一次请求、ip代理池等）。
5. scrapy.cfg：项目的配置文件。
6. spiders包：以后所有的爬虫，都是存放到这个里面。