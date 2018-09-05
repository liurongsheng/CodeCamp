```python
from urllib import request

target_url = 'http://www.oschina.net/'

headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/67.0.3396.62 Safari/537.36'
}

req = request.Request(url=target_url, headers=headers)
print(request.urlopen(req).read())
```

```python 使用requests和xpath爬取电影天堂电影详情
import requests
from lxml import etree

BASE_DOMAIN = 'http://www.dytt8.net'
HEADERS = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/61.0.3163.100 Safari/537.36',
    'Referer': 'http://www.dytt8.net'
}

def spider():
    url = 'http://www.dytt8.net/html/gndy/dyzz/list_23_1.html'
    resp = requests.get(url,headers=HEADERS)
    # resp.content：经过编码后的字符串
    # resp.text：没有经过编码，也就是unicode字符串
    # text：相当于是网页中的源代码了
    text = resp.content.decode('gbk')
    # tree：经过lxml解析后的一个对象，以后使用这个对象的xpath方法，就可以
    # 提取一些想要的数据了
    tree = etree.HTML(text)
    # xpath/beautifulsou4
    all_a = tree.xpath("//div[@class='co_content8']//a")
    for a in all_a:
        title = a.xpath("text()")[0]
        href = a.xpath("@href")[0]
        if href.startswith('/'):
            detail_url = BASE_DOMAIN + href
            crawl_detail(detail_url)
            break

def crawl_detail(url):
    resp = requests.get(url,headers=HEADERS)
    text = resp.content.decode('gbk')
    tree = etree.HTML(text)
    create_time = tree.xpath("//div[@class='co_content8']/ul/text()")[0].strip()
    imgs = tree.xpath("//div[@id='Zoom']//img/@src")
    print(imgs)
    # 电影海报
    cover = imgs[0]
    # 电影截图
    screenshoot = imgs[1]
    # 获取span标签下所有的文本
    infos = tree.xpath("//div[@id='Zoom']//text()")
    for index,info in enumerate(infos):
        if info.startswith("◎年　　代"):
            year = info.replace("◎年　　代","").strip()

        if info.startswith("◎豆瓣评分"):
            douban_rating = info.replace("◎豆瓣评分",'').strip()
            print(douban_rating)

        if info.startswith("◎主　　演"):
            # 从当前位置，一直往下面遍历
            actors = [info]
            for x in range(index+1,len(infos)):
                actor = infos[x]
                if actor.startswith("◎"):
                    break
                actors.append(actor.strip())
            print(",".join(actors))


if __name__ == '__main__':
    spider()
```
