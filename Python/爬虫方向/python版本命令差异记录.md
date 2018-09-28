## 代码差异

python 3.x
pip install web.py==0.40-dev1 -i https://pypi.tuna.tsinghua.edu.cn/simple

如果是python3.7的版本报 
...site-packages\web\utils.py", line 526, in take 
 yield next(seq) 
StopIteration 的错误
点击报错位置修改为下列语句
```python
try:
    yield next(seq)
except StopIteration:
    return
```
python 2.x
pip install web.py

## 异步网络库
greenlet 支持 python 3.x
