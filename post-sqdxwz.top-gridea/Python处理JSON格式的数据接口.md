# 什么是json？

`JSON(JavaScript Object Notation, JS 对象简谱)` 是一种轻量级的数据交换格式。它基于 `ECMAScript` 的一个子集，采用完全独立于编程语言的文本格式来存储和表示数据。简洁和清晰的层次结构使得`JSON` 成为理想的数据交换语言。易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。

在JS语言中，一切都是对象。因此，任何支持的类型都可以通过JSON来表示，例如字符串、数字、对象、数组等。但是对象和数组是比较特殊且常用的两种类型：

1. 对象表示为键值对
2. 数据由逗号分隔
3. 花括号保存对象
4. 方括号保存数组

# json使用方法

## 获取一个json数据

```python
import requests

url ='https://api.oioweb.cn/api/jsyl.php'
r = requests.get(url)
#json格式
json_response = r.content.decode()
print(json_response)
```

```json
{"code":1,"msg":"别把辉煌记在心间，别拿昨天挂在嘴边。"}
```

> 更多接口API：[教书先生api接口](https://api.oioweb.cn/) 、[免费api接口](https://zhuanlan.zhihu.com/p/106908376)

## `python` 处理`json` 格式模块有`json` 和`picle` 

1. `json` 模块提供了四个方法：dumps、dump、loads、load；
2. `pickle` 模块也提供了四个功能：dumps、dump、loads、load；
3. 序列化：将`python` 的值转换为`json` 格式的字符串；
4. 反序列化：将`json` 格式的字符串转换成`python` 的数据类型；

## json与字典相互转换

5. `json.dumps`用于将 `Python` 对象编码成`JSON` 字符串。
6. `json.loads`将已编码的 `JSON` 字符串解码为`Python` 对象。

```python
import requests
import json

url ='https://api.oioweb.cn/api/jsyl.php'
r = requests.get(url)
#json格式
json_response = r.content.decode()
print(json_response)
#json 转字典
dict_json = json.loads(json_response)
print(dict_json)
```

结果输出(上为字典格式、下是json格式)

```json
{"code":1,"msg":"兄弟为手足，女人为衣服。谁动我手足，我扒谁衣服。"}
{'code': 1, 'msg': '兄弟为手足，女人为衣服。谁动我手足，我扒谁衣服。'}
```

> 说明：json是字符串，在输出展示方面与字典是不同的，为双引号

## 序列化

下面列举了数据处理中常用的7种类型的序列化与反序列化：

```python
#1）字典序列化：
import json
dic={"name":"mcw","age":18}
xu=json.dumps(dic)
print(xu,type(xu),type(dic))

print('------------1---------------')

#2）列表序列化与反序列化：
import json
li=[1,2]
xu=json.dumps(li)
print(xu,type(xu),type(li))
fx=json.loads(xu)
print(fx,type(fx))
print('-------------2--------------')

#3）字符串序列化与反序列化:
import json
mcwstr="xiaoma"
xu=json.dumps(mcwstr)
print(xu,type(xu),type(mcwstr))
fx=json.loads(xu)
print(fx,type(fx))
print('------------3---------------')

#4）整型序列化与反序列化
import json
mcwint=2
xu=json.dumps(mcwint)
print(xu,type(xu),type(mcwint))
fx=json.loads(xu)
print(fx,type(fx))

print('------------4---------------')
#5）浮点型序列化与反序列化
import json
mcwfloat=2.03
xu=json.dumps(mcwfloat)
print(xu,type(xu),type(mcwfloat))
fx=json.loads(xu)
print(fx,type(fx))
print('--------------5-------------')

#6）布尔型序列化与反序列化：
import json
mcwbool=True
xu=json.dumps(mcwbool)
print(xu,type(xu),type(mcwbool))
fx=json.loads(xu)
print(fx,type(fx))

print('--------------6-------------')

#7）None序列化与反序列化
import json
mcwnone=None
xu=json.dumps(mcwnone)
print(xu,type(xu),type(mcwnone))
fx=json.loads(xu)
print(fx,type(fx))
```

结果输出：

```html
{"name": "mcw", "age": 18} <class 'str'> <class 'dict'>
------------1---------------
[1, 2] <class 'str'> <class 'list'>
[1, 2] <class 'list'>
-------------2--------------
"xiaoma" <class 'str'> <class 'str'>
xiaoma <class 'str'>
------------3---------------
2 <class 'str'> <class 'int'>
2 <class 'int'>
------------4---------------
2.03 <class 'str'> <class 'float'>
2.03 <class 'float'>
--------------5-------------
true <class 'str'> <class 'bool'>
True <class 'bool'>
--------------6-------------
null <class 'str'> <class 'NoneType'>
None <class 'NoneType'>
```
