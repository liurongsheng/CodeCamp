```python
from urllib import request

target_url = 'http://www.oschina.net/'

headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/67.0.3396.62 Safari/537.36'
}

req = request.Request(url=target_url, headers=headers)
print(request.urlopen(req).read())
```