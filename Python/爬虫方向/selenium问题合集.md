# Selenium问题合集

## Selenium报错Element is not clickable at point及四种解决方法
使用Selenium时，触发点击事件，经常报异常：`Element is not clickable at point`，无外乎四种原因

### 错误原因一：元素未加载
解决思路：没加载出来就等待元素加载出来，再往下执行。 
使用 python 库 time 解决
```python
import time 
time.sleep(3)
```
不过最好还是使用selenium自带WebDriverWait
```python
from selenium.webdriver.support.ui import WebDriverWait
WebDriverWait(driver, 10).until(EC.title_contains("元素"))
```

### 错误原因二：元素在iframe里，在窗口里找是找不到元素，所以无法点击
解决思路：切换到iframe里去找元素。
```python
driver.switch_to_frame("frameName")  # 根据框架名来切换
driver.switch_to_frame("frameName.0.child")  # 子框架
driver.switch_to_default_content()  # 返回
```

### 错误原因三：不在视窗里，需要拉滚动条
很多网站的列表页不是立马返回所有内容，是根据视图来显示的
解决思路：需要拖动滚动条来把要获取的内容显示到视窗里才可以获取到。
```python
page = driver.find_element_by_partial_link_text(u'下一页')
driver.execute_script("arguments[0].scrollIntoView(false);"， page)
WebDriverWait(driver, 10).until(EC.element_to_be_clickable((By.PARTIAL_LINK_TEXT, u'下一页'))).click()
```

### 错误原因四：要点击的元素被覆盖
解决思路：可以使用事件链来解决，例如下拉菜单，通过hover，让子菜单显示，就可以点击了。
```python
menu = driver.find_element_by_css_selector(".nav")
hidden_submenu = driver.find_element_by_css_selector(".nav #submenu1")
ActionChains(driver).move_to_element(menu).click(hidden_submenu).perform()
```