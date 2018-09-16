```python
# 使用 os 模块，判断指定目录是否存在文件夹，不存在则创建
# os.path.dirname(__file__) 当前文件所在文件夹路径
# os.path.dirname(os.path.dirname(__file__)) 上一级文件夹路径
import os
images_path = os.path.join(os.path.dirname(os.path.dirname(__file__)),'images')
if not os.path.exists(images_path):
    os.mkdir(images_path)
```