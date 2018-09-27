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
mkvirtualenv venv # 创建虚拟环境
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
然后进入下载的文件夹安装 `pip install ./Twisted‑18.7.0‑cp37‑cp37m‑win_amd64.whl`
 
 
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

## 使用Scrapy框架爬取糗事百科段子
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

## 笔记
1. response 是一个`<class 'scrapy.http.response.html.HtmlResponse'>`对象，可以执行`xpath`和`css`语法来提取数据
2. 提取出来的数据，是一个`selector`和`SelectorList`对象，如果想要获取其中的字符串需要使用 get() 和 getall()
3. get() 获取 selector 对象中的第一个文本，返回一个str类型，getall() 获取 selector 对象中的所有文本，返回一个列表
4. 如果数据解析回来，要传给`pipline`处理，可以使用`yield`来(或者定义一个列表收集所有的item，最后统一返回)
5. 建议在`item.py`中定义好模型，以后不要使用字典的形式
6. pipline 是专门用来保存数据的，其中有三个方法最常用，要激活 pipelines，应该在settings.py文件中设置`ITEM_PIPELINES`
```
def open_spider(self, spider): # 开始运行爬虫的时候执行代码
def process_item(self, item, spider): # 当爬虫有item传过来的时候会被调用
def closs_spider(self, spider): # 关闭爬虫的时候执行代码
```
```
# 使用 pipelines 时需要配置 settings.py 文件开启 pipelines
ITEM_PIPELINES = {
   'ScrapyDemo.pipelines.ScrapydemoPipeline': 300,  # 300是优先级，多个 pipelines 时值越小优先级越高
}
```

## 运行scrapy项目
运行scrapy项目。需要在终端，进入项目所在的路径，然后scrapy crawl [爬虫名字]即可运行指定的爬虫。如果不想每次都在命令行中运行，那么可以把这个命令写在一个文件中。
以后就在pycharm中执行运行这个文件就可以了。比如现在新创建一个文件叫做start.py，然后在这个文件中填入以下代码：
```python
from scrapy import cmdline
cmdline.execute("scrapy crawl qsbk".split())
```

## 使用 type 查看 python 源代码
```python
from scrapy.http.response.html import HtmlResponse # 可以Ctrl+B查看所有支持的方法

    def parse(self, response): 
        print(type(response))  # 打印出类型，查看支持的方法
===
<class 'scrapy.http.response.html.HtmlResponse'>
```
`@deprecated(use_instead='.xpath()')` 代表已经放弃的方法使用`.xpath()`代替


## 完整的爬虫代码

爬虫部分代码
```python
# from scrapy.http.response.html import HtmlResponse
# from scrapy.selector.unified import SelectorList
import scrapy
from ScrapyDemo.items import ScrapydemoItem

class QsbkSpider(scrapy.Spider): # 继承 scrapy.Spider 类
    name = 'qsbk' # 爬虫名字要唯一性
    allowed_domains = ['qiushibaike.com']
    start_urls = ['https://www.qiushibaike.com/8hr/page/1/']

    def parse(self, response):
        duanziDivs = response.xpath("//div[@id='content-left']/div")
        print("*" * 40)
        for duanziDiv in duanziDivs:
            author = duanziDiv.xpath(".//h2/text()").get().strip() # get()提取内容 strip()去除空格
            content = duanziDiv.xpath(".//div[@class='content']//text()").getall() # getall()提取全部内容
            content = "".join(content).strip()
            # duanzi = {"author":author,"content":content} # 使用 items.py 操作
            # yield duanzi
            item = ScrapydemoItem(author=author, content=content)
            yield item
```
items.py部分代码
```python
import scrapy
class ScrapydemoItem(scrapy.Item):
    author = scrapy.Field()
    content = scrapy.Field()
```

pipeline部分代码
```python
import json

class ScrapydemoPipeline(object):
    def __init__(self):  # 构造函数
        self.fp = open("duanzi,json","w",encoding="utf-8")

    def open_spider(self, spider): # 开始运行爬虫的时候执行代码
        print("爬虫开始")

    def process_item(self, item, spider):
        # item_json = json.dumps(item,ensure_ascii=False) # 不需要文件的转为 json 格式，ensure_ascii=False 才显示中文
        item_json = json.dumps(dict(item),ensure_ascii=False) # 使用 items.py 写法
        self.fp.write(item_json+'\n')
        return item

    def closs_spider(self, spider): # 关闭爬虫的时候执行代码
        self.fp.close()
        print("爬虫结束")
```
start.py 代码
```python
from scrapy import cmdline

cmdline.execute("scrapy crawl qsbk".split())
# cmdline.execute(["scrapy","crawl","qsbk"]) 等效上一句
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

## 改进数据存储方式

JsonItemExporter 和 JsonLinesItemExporter
保存json数据的时候，可以使用这两个类，让操作更简单
JsonItemExporter，每次把数据添加在内存中，最后统一写入磁盘
好处是存储的数据是一个满足json格式的数据
坏处是如果数据量比较大，比较耗费内存

JsonLinesItemExporter，每次调用export_item的时候把每个item存储到硬盘中
好处是每次处理数据的时候就直接存储到了硬盘中，不耗费内存比较安全
坏处是每一个字典一行，整个文件不是一个满足json格式的文件

pipeline 部分代码
```python
# JsonItemExporter
from scrapy.exporters import JsonItemExporter
class ScrapydemoPipeline(object):
    def __init__(self):  # 构造函数
        self.fp = open("duanzi.json","wb")  ## wb类型是二进制类型，同时不需要声明encoding="utf-8"
        self.exporter = JsonItemExporter(self.fp,ensure_ascii=False)
        self.exporter.start_exporting() # 需要开启和结束

    def open_spider(self, spider): # 开始运行爬虫的时候执行代码
        print("爬虫开始")

    def process_item(self, item, spider):
        self.exporter.export_item(item)
        return item

    def closs_spider(self, spider): # 关闭爬虫的时候执行代码
        self.exporter.finish_exporting() # 需要开启和结束
        self.fp.close()
        print("爬虫结束")
```
```python
# JsonLinesItemExporter
from scrapy.exporters import JsonLinesItemExporter
class ScrapydemoPipeline(object):
    def __init__(self):  # 构造函数
        self.fp = open("duanzi.json","wb")  ## wb类型是二进制类型
        self.exporter = JsonLinesItemExporter(self.fp,ensure_ascii=False)

    def open_spider(self, spider): # 开始运行爬虫的时候执行代码
        print("爬虫开始")

    def process_item(self, item, spider):
        self.exporter.export_item(item)
        return item

    def closs_spider(self, spider): # 关闭爬虫的时候执行代码
        self.fp.close()
        print("爬虫结束")
```

## 获取多个页面
```python
import scrapy
from ScrapyDemo.items import ScrapydemoItem

class QsbkSpider(scrapy.Spider): # 继承 scrapy.Spider 类
    name = 'qsbk' # 爬虫名字要唯一性
    allowed_domains = ['qiushibaike.com']
    start_urls = ['https://www.qiushibaike.com/8hr/page/1/']
    base_domain = "https://www.qiushibaike.com"
    def parse(self, response):
        duanziDivs = response.xpath("//div[@id='content-left']/div")
        print("*" * 40)
        for duanziDiv in duanziDivs:
            author = duanziDiv.xpath(".//h2/text()").get().strip() # get()提取内容 strip()去除空格
            content = duanziDiv.xpath(".//div[@class='content']//text()").getall() # getall()提取全部内容
            content = "".join(content).strip()
            # duanzi = {"author":author,"content":content} # 使用 items.py 操作
            # yield duanzi
            item = ScrapydemoItem(author=author, content=content)
            yield item  # 生成器
        next_url = response.xpath("//ul[@class='pagination']/li[last()]/a/@href").get()
        if not next_url:
            return
        else:
            yield scrapy.Request(self.base_domain + next_url,callback=self.parse)
```

## 值得买爬虫
```python
## smzdm.py
import scrapy
from ScrapyDemo.items import SmzdmItem

class SmzdmSpider(scrapy.Spider):
    name = 'smzdm'
    # allowed_domains = ['www.smzdm.com']
    # base_url = 'http://www.smzdm.com'
    start_urls = ['https://www.smzdm.com/p1/']

    def parse(self, response):
        mainLlist = response.xpath("//ul[@class='feed-list-hits']//li")
        for list in mainLlist:
            title = list.xpath(".//h5/a/text()").get()
            href = list.xpath(".//h5/a/@href").get()
            name = list.xpath(".//div[@class='feed-block-info']//span/text()").get()
            if title:
                item = SmzdmItem(title=title,href=href,name=name)
                yield item

        next_url = response.xpath("//div[@class='feed-pagenation']//ul//li[last()]//a/@href").get()
        print('*'*100)
        if not next_url:
            yield scrapy.Request('https://www.smzdm.com/p2/', callback=self.parse)
        else:
            yield scrapy.Request(next_url,callback=self.parse)
            
## pipelines.py
from ScrapyDemo.items import SmzdmItem
import pymongo
class MongoDBPipeline(object):
    def __init__(self):
        client = pymongo.MongoClient("localhost",27017)
        db = client["zdm"]
        self.SmzdmItem = db["SmzdmItem"]
    def process_item(self, item, spider):
        if isinstance(item, SmzdmItem):
            try:
                self.SmzdmItem.insert(dict(item))
            except Exception:
                pass
        return item

## items.py
import scrapy
class SmzdmItem(scrapy.Item):
    title = scrapy.Field()
    href = scrapy.Field()
    name = scrapy.Field()

## settings.py
ROBOTSTXT_OBEY = False

DEFAULT_REQUEST_HEADERS = {
  'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8',
  'Accept-Language': 'en',
  'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36',
}

ITEM_PIPELINES = {
   'ScrapyDemo.pipelines.MongoDBPipeline': 200,
   # 'ScrapyDemo.pipelines.SmzdmPipeline': 300,
   # 'ScrapyDemo.pipelines.ScrapyDuanziPipeline': 500,
   # 'ScrapyDemo.pipelines.ScrapyBaiduNewsPipeline': 400,
}
```

## Scrapy Shell

我们想要在爬虫中使用xpath、beautifulsoup、正则表达式、css选择器等来提取想要的数据。
但是因为scrapy是一个比较重的框架。每次运行起来都要等待一段时间。因此要去验证我们写的提取规则是否正确，是一个比较麻烦的事情。
因此Scrapy提供了一个shell，用来方便的测试规则。当然也不仅仅局限于这一个功能。

打开cmd终端，进入到Scrapy项目所在的目录，然后进入到scrapy框架所在的虚拟环境中，输入命令scrapy shell 。
就会进入到scrapy的shell环境中。在这个环境中，你可以跟在爬虫的parse方法中一样使用了。

```
(venv) D:\gitHub\Scrapy>scrapy shell "https://www.smzdm.com/p6"
>>> response.xpath("//div[@class='feed-pagenation']//ul//li[last()]//a/@href").get()
'https://www.smzdm.com/p7/'
```

## CrawlSpider

在上一个糗事百科的爬虫案例中。我们是自己在解析完整个页面后获取下一页的url，然后重新发送一个请求。
有时候我们想要这样做，只要满足某个条件的url，都给我进行爬取。那么这时候我们就可以通过CrawlSpider来帮我们完成了。

CrawlSpider继承自Spider，只不过是在之前的基础之上增加了新的功能，可以定义爬取的url的规则，以后scrapy碰到满足条件的 url 都进行爬取，而不用手动的yield Request。

### 创建 CrawlSpider 爬虫

之前创建爬虫的方式是通过`scrapy genspider [爬虫名字] [域名]`的方式创建的。如果想要创建 CrawlSpider 爬虫，那么应该通过以下命令创建：

`scrapy genspider -c crawl [爬虫名字] [域名]`

### LinkExtractors 链接提取器
使用LinkExtractors可以不用程序员自己提取想要的url，然后发送请求。这些工作都可以交给LinkExtractors，他会在所有爬的页面中找到满足规则的url，实现自动的爬取。

以下对LinkExtractors类做一个简单的介绍：
```python
class scrapy.linkextractors.LinkExtractor(
    allow = (),
    deny = (),
    allow_domains = (),
    deny_domains = (),
    deny_extensions = None,
    restrict_xpaths = (),
    tags = ('a','area'),
    attrs = ('href'),
    canonicalize = True,
    unique = True,
    process_value = None
)
```
主要参数讲解：
```
allow：允许的url。所有满足这个正则表达式的 url 都会被提取。
deny：禁止的url。所有满足这个正则表达式的 url 都不会被提取。
allow_domains：允许的域名。只有在这个里面指定的域名的 url 才会被提取。
deny_domains：禁止的域名。所有在这个里面指定的域名的 url 都不会被提取。
restrict_xpaths：严格的 xpath。和 allow 共同过滤链接。
```

### Rule 规则类：
定义爬虫的规则类。以下对这个类做一个简单的介绍：
```python
class scrapy.spiders.Rule(
    link_extractor, 
    callback = None, 
    cb_kwargs = None, 
    follow = None, 
    process_links = None, 
    process_request = None
)
```
主要参数讲解：
```
link_extractor：一个 LinkExtractor 对象，用于定义爬取规则。
callback：满足这个规则的url，应该要执行哪个回调函数。因为CrawlSpider使用了 parse 作为回调函数，因此不要覆盖 parse 作为回调函数自己的回调函数。
follow：指定根据该规则从 response 中提取的链接是否需要跟进。
process_links：从 link_extractor 中获取到链接后会传递给这个函数，用来过滤不需要爬取的链接。
```

## 下载文件和图片
Scrapy 为下载 item 中包含的文件或图片提供了一个可重用的 item pipeline。
这些 pipeline 有些共同的方法和结构（media pipeline）。Files Pipeline 和 Images Pipeline

1. 避免重新下载最近已经下载过的文件
2. 可以方便的指定文件存储的路径
3. 可以将下载的图片转换为通用的格式，比如 png 或 jpg
4. 可以方便的生产缩略图
5. 可以方便的检测图片的宽或高，确保他们满足最小限制
6. 异步下载，效率非常高

### 下载文件的 Files Pipeline
使用 Files Pipeline 下载文件步骤
1. 定义好一个 Item, 然后在这个 item 中定义两个属性，分别为 file_urls 以及 flies。
file_urls 是用来存储需要下载的文件的url 链接，需要给一个列表
2. 当文件下载完成后，会把文件下载的相关信息存储到 item 的 files 属性中，比如下载路径、下载的url和文件的校验码等。
3. 在配置文件setting.py 中配置 FILES_STORE, 这个配置是用来设置文件下载的下载路径
4. 启动pipeline ：在ITEM_PIPELINES 中设置scrapy.pipeline.files.FilesPipeline:1

### 下载图片的 Images Pipeline
使用 Images Pipeline 下载图片步骤
1. 定义好一个 Item, 然后在这个 item 中定义两个属性，分别为 image_urls 以及 images。
file_urls 是用来存储需要下载的图片的url 链接，需要给一个列表
2. 当文件下载完成后，会把文件下载的相关信息存储到 item 的 images 属性中，比如下载路径、下载的url和文件的校验码等。
3. 在配置文件setting.py 中配置 IMAGES_STORE, 这个配置是用来设置文件下载的下载路径
4. 启动pipeline ：在ITEM_PIPELINES 中设置scrapy.pipeline.images.ImagesPipeline:1

## Downloader Middlewares 下载器中间件
下载器中间件是引擎和下载器之间通信的中间件，在这个中间件中我们可以设置代理，更换请求头等来达到反反爬虫的目的，要写下载器中间件，
可以在下载器中实现两个方法。这两个是`process_request(self, request, spider)` 和`process_response(self, request, response, spider)`
前者是在请求发送之前执行，后者是数据下载到引擎之前执行。

### process_request(self, request, spider)
在下载器发送请求之前执行，可以在这里设置随机代理ip等操作。
1. 参数
    -request: 发送请求的request 对象
    -spider: 发送请求的spider 对象
    
2. 返回值
    -返回None: 如果返回None,Scrapy将继续处理该request,执行其他中间件中的相应方法，直到合适的下载器处理函数被调用。
    -返回Response对象：Scrapy将不会调用任何其他的process_request 方法，将直接返回这个 response对象。已经激活的中间件的process_request()方法将会在每个response返回时被调用。
    -返回Request对象：不再使用之前的request对象去下载数据，而是根据现在返回的request对象返回的数据。
    如果这个方法中抛出了异常，则会调用process_exception 方法。

### process_response(self, request, response, spider)
在下载器下载的数据到引擎中间执行的方法。
1. 参数
    -request: 发送请求的request 对象
    -response：被处理的response 对象
    -spider: 发送请求的spider 对象
    
2. 返回值
    -返回Response对象：会将这个新的response对象传给其他中间件，最终传给爬虫。
    -返回Request对象：下载器链被切断，返回的request会重新被下载器调度下载。
    如果这个方法中抛出了异常，则会调用request 的errback方法，如果没有指定这个方法，那么会抛出一个异常。

### 随机请求头中间件
[UserAgent列表](http://www.useragentstring.com/pages/useragentstring.php?typ=Browser)

```python
## middlewares.py
## 新增一个类下载器中间件，重写 process_request
import random
class UserAgentDownloadMiddleware(object):
    USER_AGENTS = [
        "Mozilla/5.0 (Windows NT 6.1; WOW64; Trident/7.0; AS; rv:11.0) like Gecko",
        "Mozilla/5.0 (compatible, MSIE 11, Windows NT 6.3; Trident/7.0; rv:11.0) like Gecko",
        "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36",
    ]

    def process_request(self, request, spider):
        user_agent = random.choice(self.USER_AGENTS)
        request.headers['User-Agent'] = user_agent
```
```python
## settings.py
## smzdm 是当前项目名
DOWNLOADER_MIDDLEWARES = {
   'smzdm.middlewares.UserAgentDownloadMiddleware': 543,
}
```
```python
## 测试爬虫脚本
import scrapy
import json

class HttpbinSpider(scrapy.Spider):
    name = 'httpbin'
    start_urls = ['http://httpbin.org/user-agent']

    def parse(self, response):
        user_agent = json.loads(response.text)['user-agent']
        yield scrapy.Request(self.start_urls[0],dont_filter=True)
        # dont_filter 可以爬相同地址
        print(user_agent)
```
## ip代理池中间件
```python
## middlewares.py
import random
class IPProxyDownloadMiddleware(object):
    PROXIES = ["178.44.170.152:8080","110.44.113.182:8080"]
    def process_request(self, request, spider):
        proxy = random.choice(self.PROXIES)
        request.meta['proxy'] = proxy
```
```python
## settings.py
## smzdm 是当前项目名
DOWNLOADER_MIDDLEWARES = {
   'smzdm.middlewares.IPProxyDownloadMiddleware': 500,
}
```
独享代理的时候可以用的中间件配置
```python
## middlewares.py 
import base64
class IPProxyDownloadMiddleware(object):
    def process_request(self, request, spider):
        proxy = "121.199.6.124:16816"
        user_password = "121212:abcdef"
        request.meta['proxy'] = proxy
        b64_user_password = base64.b64encode(user_password)
        request.headers['Proxy-Authorization'] = 'Basic ' + b64_user_password.decode('utf-8')
```


## redis教程
redis是一种支持分布式的nosql数据库,他的数据是保存在内存中，同时redis可以定时把内存数据同步到磁盘，
即可以将数据持久化，并且他比memcached支持更多的数据结构(string,list列表[队列和栈],set[集合],sorted set[有序集合],hash(hash表))。

相关参考文档：http://redisdoc.com/index.html

### redis使用场景
1. 登录会话存储：存储在redis中，与memcached相比，数据不会丢失。
2. 排行版/计数器：比如一些秀场类的项目，经常会有一些前多少名的主播排名。还有一些文章阅读量的技术，或者新浪微博的点赞数等。
3. 作为消息队列：比如celery就是使用redis作为中间人。
4. 当前在线人数：还是之前的秀场例子，会显示当前系统有多少在线人数。
5. 一些常用的数据缓存：比如我们的BBS论坛，板块不会经常变化的，但是每次访问首页都要从mysql中获取，可以在redis中缓存起来，不用每次请求数据库。
6. 把前200篇文章缓存或者评论缓存：一般用户浏览网站，只会浏览前面一部分文章或者评论，那么可以把前面200篇文章和对应的评论缓存起来。用户访问超过的，就访问数据库，并且以后文章超过200篇，则把之前的文章删除。
7. 好友关系：微博的好友关系使用redis实现。
8. 发布和订阅功能：可以用来做聊天软件。

## redis和memcached的比较
memcached	redis
类型    	纯内存数据库	  内存磁盘同步数据库
数据类型	在定义value时就要固定数据类型	不需要
虚拟内存	不支持	支持
过期策略	支持	支持
存储数据安全	不支持	可以将数据同步到dump.db中
灾难恢复	不支持	可以将磁盘中的数据恢复到内存中
分布式	支持	主从同步
订阅与发布	不支持	支持
