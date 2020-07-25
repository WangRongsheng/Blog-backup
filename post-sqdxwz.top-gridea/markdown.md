# Markdown简介

Markdown是一种轻量级的标记语言，它允许人们通过简单的纯文本来编写文档，并且转换为HTML、Word、PDF等多种格式。

由于其易读易写的特性，许多网站都用其来编写文档或博客，如Github、CSDN等，很多静态博客生成器，如Hexo、Jekyll也是用其来作为博客的格式。

Markdown文件实际上是一个纯文本文件，一般以.md或者.markdown为后缀名。

# Markdown基础语法

作为一个轻量级的标记语言，Markdown最大的特点就是简单易用，其语法并不是很复杂，但可以满足日常非专业性的排版需求。

## 标题

使用#，表示1-6级标题。

```text
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

## 引用

### 普通引用

```text
> 引用文本!
```

效果：

> 引用文本！

### 嵌套引用

```text
> 第一层
>> 第二层
```

效果：

> 第一层
>> 第二层

## 表格

```text
| 字段1 | 字段2 | 字段3 |
| :-- | :--: | --: |
| A1 | B1 | C1 |
| A2 | B2 | C2 |
```

效果：

| 字段1 | 字段2 | 字段3 |
| :-- | :--: | --: |
| A1 | B1 | C1 |
| A2 | B2 | C2 |

## 代码

### 行内

```text
AAA`BBB`CCC
```

效果：

AAA`BBB`CCC

### 区块

#### 4个空格

在每行前面加上4个空格

```text
    text = "Hello, world!"
    print(text)
```

效果：

```text
text = "Hello, world!"
print(text)
```

#### 3个 `


```text
```text
text = "Hello, world!"
print(text)
\```
```


> 上述中的“\”是转义使用的！

效果：

```text
    text = "Hello, world!"
    print(text)
```

## 字体样式

### 斜体,粗体,粗斜体

```text
*text* 或 _text_ 斜体

**text** 或 __text__ 粗体

***text*** 或 ___text___ 粗斜体
```

效果

*text* 斜体

**text** 粗体

***text*** 粗斜体

### 上标,下标

#### 上标

```text
益达<sup>TM</sup>
```

效果：

益达<sup>TM</sup>


#### 下标

```text
X<sub>i</sub>

H<sub>2</sub>O  CO<sub>2</sub>
```

效果:

X<sub>i</sub>

H<sub>2</sub>O  CO<sub>2</sub>

### 下划线

```text、
<u>下划线</u>
```

效果：

<u>下划线</u>

### 删除线

```text
~~删除线~~
```

效果：

~~删除线~~

## 列表

### 无序列表

使用*、+、或-标记无序列表，下面仅以-作为示例，

```text
- 第一项
- 第二项
- 第三项
```

> 注: 标记后面最少有一个 空格 或 制表符。

效果：

- 第一项
- 第二项
- 第三项

### 有序列表

有序列表的标记方式是将上述的符号换成数字,并辅以`.`

```text
1. 第一项   
2. 第二项    
3. 第三项
``` 

效果：

1. 第一项
2. 第二项
3. 第三项

### 任务列表

用法: - [ ] 或 - [x]，其中[ ]表示不打勾，[x]表示打勾，-可以用+或*替代

```text
- [x] Lorem ipsum dolor sit amet, consectetur adipiscing elit
- [x] Nulla lobortis egestas semper
- [x] Curabitur elit nibh, euismod et ullamcorper at, iaculis feugiat est
- [ ] Vestibulum convallis sit amet nisi a tincidunt
    - [x] In hac habitasse platea dictumst
    - [x] In scelerisque nibh non dolor mollis congue sed et metus
    - [x] Sed egestas felis quis elit dapibus, ac aliquet turpis mattis
    - [ ] Praesent sed risus massa
- [x] Aenean pretium efficitur erat, donec pharetra, ligula non scelerisque
- [ ] Nulla vel eros venenatis, imperdiet enim id, faucibus nisi
```

效果：

- [x] Lorem ipsum dolor sit amet, consectetur adipiscing elit
- [x] Nulla lobortis egestas semper
- [x] Curabitur elit nibh, euismod et ullamcorper at, iaculis feugiat est
- [ ] Vestibulum convallis sit amet nisi a tincidunt
    + [x] In hac habitasse platea dictumst
    + [x] In scelerisque nibh non dolor mollis congue sed et metus
    + [x] Sed egestas felis quis elit dapibus, ac aliquet turpis mattis
    + [ ] Praesent sed risus massa
- [x] Aenean pretium efficitur erat, donec pharetra, ligula non scelerisque
- [ ] Nulla vel eros venenatis, imperdiet enim id, faucibus nisi

### 嵌套列表

```text
- aaa
    - bbb
```

效果：

- aaa
    - bbb

## 分割线

分割线使用三个或以上*，也可以使用-和_，下面仅以-作为示例

```text
---
```

效果：

---

## 链接

### 普通链接

#### 行内式

```text
[example](http://www.example.com/ "title")
```

效果：

[example](http://www.example.com/ "title")

鼠标悬停在链接上可以看到"title"字样

#### 参考式

当一个页面里多次调用相同链接时，这种方法更适用:

```text
[example][索引]

[索引]: http://www.example.com/ "title"
```

注意: `[索引]: http://www.example.com/ "title"`可以写在任意地方，通常习惯于放在markdown本页文档最下方

效果：

[example][索引]

[索引]: http://www.example.com/ "title"

> 鼠标悬停在链接上可以看到"title"字样

### 自动链接

当识别到HTML、FTP、Email地址时候会自动转为超链接

## 图片

### 行内式

添加图片的形式和链接相似，只需在链接的基础上前方加一个`!`

```text
![alt](图片地址 "title")
```

效果：

![hello](https://s2.ax1x.com/2020/02/19/3E2SBV.th.jpg "我的博客头像")

> 鼠标悬停在图标上可以看到"我的博客头像"字样

### 参考式

当一个页面里多次调用相同图片时，这种方法更适用:

```text
![alt][索引]

[索引]: 图片地址 "title"
```

注意: `[索引]: 图片地址 "title"`可以写在任意地方，通常习惯于放在markdown本页文档最下方

效果：

![alt][test icon]

[test icon]: https://s2.ax1x.com/2020/02/19/3E2SBV.th.jpg "我的博客头像"

> 鼠标悬停在图标上可以看到"我的博客头像"字样

## 转义

```text
\转义的内容
```