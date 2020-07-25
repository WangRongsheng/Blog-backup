
# 一、渲染文本
将htm网页内容到%%html后面，示例如下


```python
%%html

<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8"> 
    <title>chenqionghe</title>
    <link rel="stylesheet" href="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/css/bootstrap.min.css">
    <script src="https://cdn.staticfile.org/jquery/2.1.1/jquery.min.js"></script>
    <script src="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/js/bootstrap.min.js"></script>
</head>
<body>
<div class="page-header">
    <h1>Wangrongsheng
        <small>yeah buddy! light weight bay!</small>
    </h1>
</div>
<p>geting muscle is not easy</p>

</body>
</html>
```



# 二、渲染变量
例如我们经常通过requests抓取网页，可以直接渲染出抓取到的内容，例如通过request抓取网页，直接渲染res.text，代码如下


```python
import requests
from IPython.display import HTML

res=requests.get('http://jd.com')
HTML(res.text)
```








# 三、代理页面
已有页面想通过jupyter显示出来，可以通过IFrame方法渲染，src可以是本地的html，也可以是一个网页地址


```python
from IPython.display import IFrame
IFrame(src='https://sqdxwz.com', width=1000, height=600)
```

