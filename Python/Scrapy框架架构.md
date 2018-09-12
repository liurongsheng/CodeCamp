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


## 创建虚拟环境 virtualenvwrapper
在当前的目录中创建一个文件夹，包含了Python可执行文件，以及 pip 库的一份拷贝，在虚拟环境中任何你使用pip安装的包将会放在 venv 文件夹中，与全局安装的Python隔绝开。
虚拟环境的名字（此例中是 venv ）可以是任意的；若省略名字将会把文件均放在当前目录。
```
pip install virtualenvwrapper-win
mkvirtualenv venv
workon venv
pip --version # 查看是不是当前系统的最新版本
pip install ./Twisted-18.7.0-cp37-cp37m-win_amd64.whl # 先去找和 python 版本对应的然后离线安装 
pip install Scrapy
# workon # 查看所有的虚拟环境
# workon venv # 切换到虚拟环境
# deactivate # 退出虚拟环境
# rmvirtualenv venv # 删除虚拟环境
```

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
要使用Scrapy框架创建项目，需要通过命令来创建。(旧版本需要进入文件夹后初始化一个工程项目，新版本比如Scrapy 1.5.1，已经不需要进入文件夹下初始化了)

然后使用以下命令创建：

`scrapy startproject [项目名称]`
scrapy startproject ScrapyDemo

## 目录结构
1. items.py：用来存放爬虫爬取下来数据的模型。
2. middlewares.py：用来存放各种中间件的文件。
3. pipelines.py：用来将items的模型存储到本地磁盘中。
4. settings.py：本爬虫的一些配置信息（比如请求头、多久发送一次请求、ip代理池等）。
5. scrapy.cfg：项目的配置文件。
6. spiders包：以后所有的爬虫，都是存放到这个里面。

## scrapy 可用命令
```
Available commands:
  bench         Run quick benchmark test
  fetch         Fetch a URL using the Scrapy downloader
  genspider     Generate new spider using pre-defined templates
  runspider     Run a self-contained spider (without creating a project)
  settings      Get settings values
  shell         Interactive scraping console
  startproject  Create new project
  version       Print Scrapy version
  view          Open URL in browser, as seen by Scrapy
```

## 使用Scrapy框架爬取糗事百科段子：
在根目录( scrapy.cfg 同级目录 )使用命令创建一个爬虫：
```python
scrapy genspider qsbk "qiushibaike.com"
```
创建了一个名字叫做 qsbk 的爬虫，并且能爬取的网页只会限制在 `qiushibaike.com` 这个域名下。

爬虫代码解析：
```python
import scrapy

class QsbkSpider(scrapy.Spider):
   name = 'qsbk'
   allowed_domains = ['qiushibaike.com']
   start_urls = ['http://qiushibaike.com/']

   def parse(self, response):
       pass
```
其实这些代码我们完全可以自己手动去写，而不用命令。只不过是不用命令，自己写这些代码比较麻烦。
要创建一个Spider，那么必须自定义一个类，继承自scrapy.Spider，然后在这个类中定义三个属性和一个方法。

1. name：这个爬虫的名字，名字必须是唯一的。
2. allow_domains：允许的域名。爬虫只会爬取这个域名下的网页，其他不是这个域名下的网页会被自动忽略。
3. start_urls：爬虫从这个变量中的url开始。

parse：引擎会把下载器下载回来的数据扔给爬虫解析，爬虫再把数据传给这个parse方法。这个是个固定的写法。
这个方法的作用有两个，第一个是提取想要的数据。第二个是生成下一个请求的url。

## 修改settings.py代码：
在做一个爬虫之前，一定要记得修改`setttings.py`中的设置。两个地方是强烈建议设置的。

1. ROBOTSTXT_OBEY设置为False。默认是True。即遵守机器协议，那么在爬虫的时候，scrapy首先去找robots.txt文件，如果没有找到。则直接停止爬取。
2. DEFAULT_REQUEST_HEADERS添加User-Agent。这个也是告诉服务器，我这个请求是一个正常的请求，不是一个爬虫。
```
ROBOTSTXT_OBEY = False
DEFAULT_REQUEST_HEADERS = {
  'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8',
  'Accept-Language': 'en',
  'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36',
}
```

完成的爬虫代码：
爬虫部分代码：
```python
import scrapy
from abcspider.items import QsbkItem

class QsbkSpider(scrapy.Spider):
    name = 'qsbk'
    allowed_domains = ['qiushibaike.com']
    start_urls = ['https://www.qiushibaike.com/text/']

    def parse(self, response):
        outerbox = response.xpath("//div[@id='content-left']/div")
        items = []
        for box in outerbox:
            author = box.xpath(".//div[contains(@class,'author')]//h2/text()").extract_first().strip()
            content = box.xpath(".//div[@class='content']/span/text()").extract_first().strip()
            item = QsbkItem()
            item["author"] = author
            item["content"] = content
            items.append(item)
        return items
```
items.py部分代码：
```python
import scrapy
class QsbkItem(scrapy.Item):
    author = scrapy.Field()
    content = scrapy.Field()
```

pipeline部分代码：
```python
import json

class AbcspiderPipeline(object):
    def __init__(self):

        self.items = []

    def process_item(self, item, spider):
        self.items.append(dict(item))
        print("="*40)
        return item

    def close_spider(self,spider):
        with open('qsbk.json','w',encoding='utf-8') as fp:
            json.dump(self.items,fp,ensure_ascii=False)
```
运行scrapy项目：
运行scrapy项目。需要在终端，进入项目所在的路径，然后scrapy crawl [爬虫名字]即可运行指定的爬虫。如果不想每次都在命令行中运行，那么可以把这个命令写在一个文件中。
以后就在pycharm中执行运行这个文件就可以了。比如现在新创建一个文件叫做start.py，然后在这个文件中填入以下代码：
```python
from scrapy import cmdline
cmdline.execute("scrapy crawl qsbk".split())
```

## 运行问题
Python3.7，装上依赖包和 scrapy 后运行爬虫命令出错
```python
  File "c:\users\administrator\appdata\local\programs\python\python37\lib\site-packages\twisted\conch\manhole.py", line 154
      def write(self, data, async=Shark):
                              ^
SyntaxError: invalid syntax
```
将源码manhole.py中的async参数更改为shark（注意更换全部）可以直接点击错误跳转 
```python
    def write(self, data, shark=False):
        self.handler.addOutput(data, shark)

    def addOutput(self, data, shark=False):
        if shark:
            self.terminal.eraseLine()
            self.terminal.cursorBackward(len(self.lineBuffer) + len(self.ps[self.pn]))

        self.terminal.write(data)
```