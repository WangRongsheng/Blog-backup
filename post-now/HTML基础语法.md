# HTML简介

HTML称为超文本标记语言，是一种标识性的语言。它包括一系列标签．通过这些标签可以将网络上的文档格式统一，使分散的Internet资源连接为一个逻辑整体。HTML文本是由HTML命令组成的描述性文本，HTML命令可以说明文字，图形、动画、声音、表格、链接等。

# HTML基础语法

## 全局架构标签

> 每一个html页面必须包含以下一段内容，可以称为全局架构标签

```html
<!DOCTYPE html> <!-- 声明这个html页面使用的版本，这样写代表是H5最新版本 -->
<html>
  <head>
  <meta charset="utf-8">  <!-- 告诉浏览器使用的是utf-8字符集 -->
      <title>我的网站</title>   <!-- 这里用来编写网站的标题，显示在浏览器选项卡的位置 -->
  </head>
  <body>    <!-- 只有body标签里面的内容，才能真正显示在浏览器的窗口中 -->
    <h1>我的第一个标签</h1>
    
    <p>我的第一个段落</p>
  </body>
</html>
```

**html标签和元素的说法**：

- 标签：html、head、meta、title、body、h1、p等等我们都称为html的标签，简称标签即可。

- 元素：一对标签所表示的东西，我们称为元素。

练习：

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf8" />     <!-- 这里是注释：meta为半闭合标签，并使用utf8字符集 -->
        <title>这是我的标题：首次学习HTML</title>
    </head>
    <body>
        <h1>
            首次学习PHP，这是HTML基础语法部分！！
        </h1>
    </body>
</html>
```

## 标题

> 标题就是我们通常理解的文档里面的标题，html里面的标题分为：h1、h2、h3、h4、h5、h6

写法：

```html
<h1>最大的标题</h1>
<h2>标题二</h2>
<h3>标题三</h3>
<h4>标题四</h4>
<h5>标题五</h5>
<h6>标题六</h6>
```

练习：

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf8" />
        <title>标题--HTML基础语法学习</title>
    </head>
    <body>
        <h1>我是一个h1标题</h1>
        <h2>我是一个h2标题</h2>
        <h3>我是一个h3标题</h3>
        <h4>我是一个h4标题</h4>
        <h5>我是一个h5标题</h5>
        <h6>我是一个h6标题</h6>
    </body>
</html>
```

## 段落

> 段落表示一段普通的文字，类似文章中的一个段落

写法：

```html
<p>
    近日，西安女车主坐在66万买的奔驰车引擎盖上无奈维权引发各界密切关注。除了车本身的质量问题，该车主还质疑4S店诱其贷款收取的“金融服务费”存在欺诈。贷款买车究竟有哪些渠道？“金融服务费”是不是合理收费？贷款买车会遭遇哪些套路？消费者提前防范别踩坑里？北京青年报记者就这些问题采访了众多专业人士。
    据了解，汽车金融业务包括三种较为常见的模式。第一种为银行车贷，消费者向申请住房按揭一样向银行申请贷款，按照一定利率按月还款；第二种为信用卡分期，指持卡人同意支付首付款的情况下，向银行申请用其信用卡在银行指定的经销商购买家用汽车，经银行核准后，将审批通过金额平均分成若干期，由持卡人在约定期限内按月还款，并支付一定手续费。第三种模式为消费者向汽车金融公司申请贷款。也是西安奔驰维权事件中女车主选择的方式。第四种是近年来新兴的汽车融资租赁，即通过“以租代购、分期付款”的方式购车。
</p>
```

练习：

```html
<!DOCTYPE html>
<html>
    <meta charset="utf8" />
    <head>
        <title>段落--HTML基础语法</title>
    </head>
    <body>
        <h1>毛主席介绍</h1>
        <p>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;近日，西安女车主坐在66万买的奔驰车引擎盖上无奈维权引发各界密切关注。除了车本身的质量问题，该车主还质疑4S店诱其贷款收取的“金融服务费”存在欺诈。贷款买车究竟有哪些渠道？“金融服务费”是不是合理收费？贷款买车会遭遇哪些套路？消费者提前防范别踩坑里？北京青年报记者就这些问题采访了众多专业人士。 
        </p>
        <p>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;据了解，汽车金融业务包括三种较为常见的模式。第一种为银行车贷，消费者向申请住房按揭一样向银行申请贷款，按照一定利率按月还款；第二种为信用卡分期，指持卡人同意支付首付款的情况下，向银行申请用其信用卡在银行指定的经销商购买家用汽车，经银行核准后，将审批通过金额平均分成若干期，由持卡人在约定期限内按月还款，并支付一定手续费。第三种模式为消费者向汽车金融公司申请贷款。也是西安奔驰维权事件中女车主选择的方式。第四种是近年来新兴的汽车融资租赁，即通过“以租代购、分期付款”的方式购车。
        </p>
    </body>
</html>
```

## 文本

HTML文本格式化标签（常用）

|标签|	描述|
|:-|:-|
|`<em>`	|定义着重文字|
|`<i>`	|定义斜体字|
|`<small>`	|定义小号字|
|`<strong>`	|定义加重语气|
|`<sub>`	|定义下标字|
|`<sup>`	|定义上标字|
|`<ins>`	|定义插入字|
|`<del>`	|定义删除字|

练习：

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf8" />
        <title>文本--HTML基础语法</title>
    </head>
    <body>
        <b>PHP是世界上最美的语言！！！</b> <!-- b标签，用于加粗字体 -->
        <b>PHP</b>是世界上最美的语言！！！ <!-- b标签，仅对PHP加粗 -->
        <em>PHP</em>是世界上最美的语言！！！<br>
        <i>PHP</i>是世界上最美的语言！！！<br>  <!-- i标签，斜体 -->
        <strong>PHP</strong>是世界上最美的语言！！！<br>    <!-- strong标签，类似加粗 -->
        <sub>PHP</sub>是世界上最美的语言！！！<br>  <!-- sub标签，下沉 -->
        <sup>PHP</sup>是世界上最美的语言！！！<br>  <!-- sup标签，上浮 -->
        <ins>PHP</ins>是世界上最美的语言！！！<br>  <!-- ins标签，下滑线  -->
        <del>PHP</del>是世界上最美的语言！！！<br>  <!-- del标签，文本划线删除 -->
    </body>
</html>
```


## 属性

> 每一个标签都会拥有一堆属性，来描述这个标签的一些功能。

所有标签共有的属性：
| | |
|:-|:-|
|class|	为html元素定义一个或多个类名(classname)（类名从样式文件引入）|
|id|	定义元素的唯一id|
|style|	规定元素的行内样式|
|title|	描述了元素的额外信息（作为工具条使用）|

标签自己的属性，比如下面的a标签和img标签：

```html
<a href="http://www.baidu.com">我是一个超链接，鼠标点击即可跳转到一个网址</a>
<img src="haha.jpg" width="100px" />
```

写法：

```html
<h1 id="wwely1" class="duoge" style="color: red" title="鼠标放上来可以显示的">标题一</h1>
<p id="wely1" class="duoge" style="color: red" title="鼠标放上来可以显示的">段落一</p>
```

练习：

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf8" />
        <title>属性--HTML基础语法</title>
    </head>
    <body>
        <h1 id="kim" class="K" style="color: red" title="这是鼠标提示">英文名</h1>   <!-- h1添加属性 -->
        <h1 id="kin" class="Ki" style="color: green;font-size: 50px;" >英文名</h1>
        <a href="http://www.baidu.com">这是一个超链接，点我即可跳转</a>
    </body>
</html>
```

## 链接

> 链接，是给任何的html元素添加链接，可以被点击，跳转到某个地址。

写法：

```html
<a href="http://www.baidu.com" target="_blank">点击即可跳转百度</a>
```

用法：

在任何元素上面，想让用户点击，即可跳转到某个页面，就可以使用。

```html
<a href="http://www.youku.com"><h1>跳转优酷视频</h1></a>
```

练习：

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf8" />
        <title>链接--HTML基础语法</title>
    </head>
    <body>
        <a href="http://www.baidu.com" target="_blank">点击我可以打开百度页面</a> <!--target标签表示在新的标签页打开 -->
        <a href="http://www.jd.com" target="_blank"><h1>点击跳转京东<h1></a>
    </body>
</html>
```

## 图片

> 在网页中显示一张图片

写法：

```html
<img src="haha.jpg" title="图片的标题" alt="图片的属性" width="100px" height="100px" />
```

**绝对路径和相对路径**：

- 绝对路径是指一个完整的可以从开头找到这个图片的路径
- 相对路径是指相对于当前的页面所在的路径

绝对路径的写法：

```html
<img sr="C:\Users\Administrator\Pictures\timg.jpg" />
```

相对路径的写法：

```html
<img src="haha.jpg" />   <!--当前目录-->
<img src="./haha.jpg" /> <!-- 当前目录 -->
<img src="../haha.jpg" /> <!-- 上一级目录 -->
```

练习：

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf8" />
        <title>图片--HTML基础语法</title>
    </head>
    <body>
        <a href="http://www.baidu.com"><img src="C:\Users\Administrator\Pictures\timg.jpg"  width="1000px" height="1000px" title="这是gitlab的Logo" alt="gitlab"/></a>
    </body>
</html>
```

## 列表

无序列表（常用）

```html
<ul>
    <li>第一个列表内容</li>
    <li>第二个列表内容</li>
</ul>
```

有序列表（用的少）

```html
<ol>
    <li>第一个列表内容</li>
    <li>第二个列表内容</li>
</ol>
```

自定义列表（不怎么用）

```html
<dl>
    <dt>编程语言</dt>
    <dd>- PHP</dd>
    <dd>- Java</dd>
    <dd>- C++</dd>
    <dt>操作系统</dt>
    <dd>- Linux</dd>
    <dd>- windows</dd>
</dl>
```

练习：

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf8" />
        <title>列表--HTML基础语法</title>
    </head>
    <body>
        <ul>    <!-- 无序列表 -->
            <li>Linux跟我学</li>
            <li>老男孩教育</li>
            <li>千峰教育</li>
        </ul>
        <ol>  <!-- 有序列表 -->
           <li>Linux跟我学</li>
            <li>老男孩教育</li>
            <li>千峰教育</li>
        </ol>
         <dl>   <!-- 自定义列表 -->
            <dt>操作系统</dt>
            <dd>- Linux</dd>
            <dd>- Windows</dd>
         </dl>
    </body>
</html>
```

## 表格

写法：

```html
<table border="1" cellspacing="0" cellpadding="0">
    <tr>
        <th>头部一</th>
        <th>头部二</th>
    </tr>
    <tr>
        <td>第一行，第一列</td>
        <td>第一行，第二列</td>
    </tr>
    <tr>
        <td>第二行，第一列</td>
        <td>第二行，第二列</td>
    </tr>
</table>
```

用法：

- 需要以表格显示的内容
- 可以用来布局页面（现在不用了，用div来进行布局）
  
练习：

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf8" />
        <title>表格--HTML基础语法</title>
    </head>
    <body>
        <table border="1" cellspacing="0" cellpadding="0">
            <tr><th>标题</th><th>标题</th></tr>
            <tr><td>第一行，第一列</td><td>第一行，第二列</td></tr>
            <tr><td>第二行，第一列</td><td>第二行，第二列</td></tr>
        </table>
    </body>
</html>
```

## 区块

- 块级元素：div是指一块内容的标签，div不显示任何东西，用来包含其他标签，称之为一块内容，需要配合CSS样式来进行页面布局。 h1、p、ul、table都是块级元素，会以新行来开始。
- 内联元素：span标签用来包裹文字。b、id、a、img通常不会以新行开始。

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf8" />
        <title>区块--HTML基础语法</title>
    </head>
    <body>
        <div>这是一个div</div>
        <div>
            这是第二个div
            <a>66666</a>   <!-- 这里a标签不是块级元素，不会在新行开始-->
        </div>
        <p> <!-- p标签为块级元素，会在新行开始-->
            这是一个段落
        </p>
        <p>
            这是第二个段落
        </p>
        <span>内联元素</span>
        <span>内联元素222</span>
    </body>
</html>
```

## 布局

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf8"/>
        <title> 布局--HTML基础语法</title>
    </head>
    <body>
        
    </body>
</html>
```

## 表单

> 表单是用来在网页上显示给用户输入的标签，然后提交给后台服务器进行处理。

定义：

```html
<form action="xxx.php" method="post">
    
</form>
```

表单元素：

多数情况下被用到的表单标签是输入标签（`<input>`），输入类型是由类型属性（`type`）进行定义的，常用的输入类型如下：

- 文本

```html
<form >
    <input type="text" name="username" value="Kim" />
</form>
```

- 密码

```html
<form>
    Password: <input type="password" name="pwd">
</form>
```

- 单选按钮（Radio Buttons）

```html
<form>
    <input type="radio" name="sex" value="male">Male<br>
    <input type="radio" name="sex" value="female">Female
</form>
```

- 多选按钮（Checkboxes）

```html
<form>
    <input type="checkbox" name="vehicle" value="Bike">I have a bike<br>
    <input type="checkbox" name="vehicle" value="Car">I have a car 
</form>
```

- 提交按钮（Submit Button）

```html
<form name="input" action="html_form_action.php" method="get">
    Username: <input type="text" name="user">
    <input type="submit" value="Submit">
</form>
```

练习：

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf8" />
        <title>表单--HTML语法基础</title>
        <form action="xxx.php" method="post" id="11" name="login">
            <label>用户名：<label><input type="text" value="kim" name="username" /><br>
            <label>密码：</label><input type="password" name="password" placeholder="请输入密码" /><br>
            
            <label>备注：</label>
            <textarea name="intro" placeholder="输入简介"> </textarea><br />
            
            <input type="radio" name="sex" value="1">男
            <input type="radio" name="sex" value="0">女<br />
            <h1>选择题</h1>
            <p>1、下面哪个城市是孙中山的故乡</p>
            <input type="checkbox" name="area" value="city">天津<br />
            <input type="checkbox" name="area" value="city">上海<br />
            <input type="checkbox" name="area" value="city">中山<br />
            
            <input type="submit" value="提交">
</html>
```

## 框架

框架（iframe）

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf8" />
        <title>框架--HTML基础语法</title>
    </head>
    <body>
        <iframe src="http://www.baidu.com" width="500px" height="1000px"></iframe>
    </body>
</html>
```

## 头部

完整的头部标签：

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf8" />
        <base href="http://www.runoob.com/images/" target="_link">  <!-- 页面中 所有的链接的默认地址-->
        <title>头部--HTML基础语法</title>
        <meta name="keywords" content="PHP学习之路">  <!--  这个是做seo优化的时候用的 -->
        <meta name="description" content="改变世界的PHP">    <!--  这个是做seo优化的时候用的 -->
        <meta http-equiv="refresh" content="30">  <!-- 刷新跳转页面 -->
        <link rel="stylesheet" type="text/css" href="mystyle.csss">  <!-- 引入css样式 -->
    </head>
    <body>
        文档内容......
    </body>
</html>
```