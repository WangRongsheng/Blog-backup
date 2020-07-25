# 什么是Selenium？

Selenium是一个用于Web应用程序测试的工具。Selenium测试直接运行在浏览器中，就像真正的用户在操作一样。支持的浏览器包括IE（7, 8, 9, 10, 11），Mozilla Firefox，Safari，Google Chrome，Opera等。支持自动录制动作和自动生成 .Net、Java、Python等不同语言的测试脚本。

# 基于Selenium+Python的打开刷新关闭网页

```python
# coding = utf-8
import time
from selenium import webdriver

driver = webdriver.Firefox()  # 打开火狐浏览器
# driver = webdriver.Chrome()   # 打开Chrome
# driver = webdriver.Ie()   # 打开IE
driver.maximize_window()    #最大化窗口
driver.get('yoursite')    #打开地址
time.sleep(60)    #睡眠60s
driver.refresh()    #刷新打开的页面
driver.close()     #关闭浏览器
```

# 问题

可能会出现`Path`配置问题，大家自行[百度一下](baidu.com)