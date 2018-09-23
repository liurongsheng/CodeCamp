# selenium问题合集

## selenium报错Element is not clickable at point及四种解决方法

点击报错
使用Selenium时，触发点击事件，经常报如下异常：

Element is not clickable at point

原因及解决方法
无外乎四种原因

未加载
没加载出来就等待元素加载出来，再往下执行。 
可以使用python库time

import time 
time.sleep(3)

不过最好还是使用selenium自带WebDriverWait

from selenium.webdriver.support.ui import WebDriverWait

WebDriverWait(driver, 10).until(EC.title_contains("元素"))

WebDriverWait的具体用法请点击参考文档。

在iframe里
如果元素在iframe里，在窗口里找是找不到元素的，更是无法点击。所以，要切换到iframe里去找元素。

driver.switch_to_frame("frameName")  # 根据框架名来切换
driver.switch_to_frame("frameName.0.child")  # 子框架
driver.switch_to_default_content()  # 返回

其他相关切换，请点击参考文档

不在视窗里，需要拉滚动条
很多网站的列表页不是立马返回所有内容，是根据视图来显示的。所以，我们就需要拖动滚动条来把要获取的内容显示到视窗里才可以获取到。

page = driver.find_element_by_partial_link_text(u'下一页')
driver.execute_script("arguments[0].scrollIntoView(false);"， page)
WebDriverWait(driver, 10).until(EC.element_to_be_clickable((By.PARTIAL_LINK_TEXT, u'下一页'))).click()

关于下拉滚动条的内容可以参考博客

要点击的元素被覆盖
可以使用事件链来解决 
例如下拉菜单，通过hover，让子菜单显示，就可以点击了。

menu = driver.find_element_by_css_selector(".nav")
hidden_submenu = driver.find_element_by_css_selector(".nav #submenu1")

ActionChains(driver).move_to_element(menu).click(hidden_submenu).perform()