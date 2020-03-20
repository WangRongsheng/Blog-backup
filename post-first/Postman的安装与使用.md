---
title: Postman的安装与使用
date: 2019-12-05 10:22:30
thumbnail: https://i.loli.net/2019/12/05/kjmvpu4tsO3Wyhx.png
tags: Postman
categories: 杂谈
---

Postman一款非常流行的API调试工具。其实，开发人员用的更多。因为测试人员做接口测试会有更多选择，例如Jmeter、soapUI等。不过，对于开发过程中去调试接口，Postman确实足够的简单方便，而且功能强大。

<!--more-->

官方网站：https://www.getpostman.com/

## 安装：

1、Postman最早是作用chrome浏览器插件存在的，所以，你可以到chrome商店搜索下载安装，因为重所周知的原因，所以，大家都会找别人共享的postman插件文件来安装。由于2018年初Chrome停止对Chrome应用程序的支持。

2、Postman提供了独立的安装包，不再依赖于Chrome浏览器了。同时支持MAC、Windows和Linux，推荐你使用这种方式安装。https://www.getpostman.com/apps

## 使用：

Postman主界面：

<a href="https://sm.ms/image/gzdY6EyCP3aJROm" target="_blank"><img src="https://i.loli.net/2019/12/05/gzdY6EyCP3aJROm.png" ></a>

### 1、简单的Get请求：

参考：http://www.python-requests.org/en/master/user/quickstart/

<a href="https://sm.ms/image/35y9BJYnlSKuAwZ" target="_blank"><img src="https://i.loli.net/2019/12/05/35y9BJYnlSKuAwZ.png" ></a>

GET：HTTP的常用请求方法。

"https://api.github.com/events"：请求的URL

点击蓝色“Send”按钮，获取返回值。

注： GET请求的参数在url后面拼接，如："https://api.github.com/events?id=1&name=user"

### 2、简单的POST请求

参考：http://www.python-requests.org/en/master/user/quickstart/

<a href="https://sm.ms/image/5B6WH3vaPEMnTjh" target="_blank"><img src="https://i.loli.net/2019/12/05/5B6WH3vaPEMnTjh.png" ></a>

POST：HTTP的常用请求方法。
"http://httpbin.org/post"：请求的URL。
Body：设置POST请求的参数。

- form-data： HTTP请求中的multipart/form-data，它会将表单的数据处理为一条消息，以标签为单元，用分隔符分开。

- x-wwww-form-urlencode：HTTP请求中的application/x-www-from-urlencoded，会将表单内的数据转换为键值对。

- raw：可以发送任意格式的接口数据，可以text、json、xml、html等。

- binary：HTTP请求中的相Content-Type:application/octet-stream，只可以发送二进制数据。通常用于文件的上传。

### 3、认证接口

创建一个接口调用：

参考：http://www.python-requests.org/en/master/

<a href="https://sm.ms/image/DnJud2YporWNTIf" target="_blank"><img src="https://i.loli.net/2019/12/05/DnJud2YporWNTIf.png" ></a>

Authorization：用于需要认证的接口。

Basic Auth：最基本的一种认证类型，还有OAuth 1.0/2.0、Digest Auth等认证类型。

Username/Password：这是针对Basic Auth类型的认证的用户名/密码，并非我们认为的系统登录的用户名密码。








