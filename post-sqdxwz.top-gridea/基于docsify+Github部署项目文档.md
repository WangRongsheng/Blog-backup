# docsify简介

docsify 是一个动态生成文档网站的工具。不同于 `GitBook`、`Hexo` 的地方是它不会生成将 `.md` 转成 `.html` 文件，所有转换工作都是在`运行时进行`。

这将非常实用，如果只是需要快速的搭建一个小型的文档网站，或者不想因为生成的一堆 `.html 文件`，只需要创建一个 `index.html` 就可以开始写文档而且直接部署在 `GitHub Pages`、`Coding Pages`、`Netlify`甚至是自己的`服务器`。

# 安装

## 脚手架安装

首先确保你已经安装[node.js](https://nodejs.org/en/) 。

然后运行：

```html
npm i docsify-cli -g
```

如果你觉得安装`缓慢`，你可以利用`淘宝源`先安装`cnpm`，然后利用`cnpm`安装`docsify`：

```html
npm install -g cnpm --registry=https://registry.npm.taobao.org

cnpm i docsify-cli -g
```

## 初始化项目

### 自动初始化

如果想在项目的 `./docs` 目录里写文档，直接通过 `init`初始化项目。

```html
docsify init docs
```

### 手动初始化

如果不喜欢 `npm` 或者觉得安装工具太麻烦，我们其实只需要直接创建一个 `index.html 文件`。

> index.html

```html
<!DOCTYPE html>
<html>
<head>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <meta charset="UTF-8">
  <link rel="stylesheet" href="//unpkg.com/docsify/themes/vue.css">
</head>
<body>
  <div id="app"></div>
  <script>
    window.$docsify = {
      //...
    }
  </script>
  <script src="//unpkg.com/docsify/lib/docsify.min.js"></script>
</body>
</html>
```

如果系统里安装 `Python` 的话，也可以很轻易的启动一个`静态服务器`。

```html
cd docs && python -m SimpleHTTPServer 3000
```

## 开始写文档

初始化成功后，可以看到 `./docs` 目录下创建的几个文件

- index.html 入口文件
- README.md 会做为主页内容渲染
- .nojekyll 用于阻止 GitHub Pages 会忽略掉下划线开头的文件
- 
直接编辑 `docs/README.md` 就能更新网站内容，当然也可以写多个`.md页面`。

## 修改样式

### Loading 提示

初始化时会显示 `Loading...` 内容，你可以自定义提示信息。

> index.html

```html
  <div id="app">加载中</div>
如果更改了 el 的配置，需要将该元素加上 data-app 属性。

index.html

  <div data-app id="main">加载中</div>

  <script>
    window.$docsify = {
      el: '#main'
    }
  </script>
```

### 多页文档

如果需要创建多个页面，或者需要多级路由的网站，在 `docsify` 里也能很容易的实现。例如创建一个 `guide.md` 文件，那么对应的路由就是 `/#/guide`。

假设你的目录结构如下：

```html
-| docs/
  -| README.md
  -| guide.md
  -| zh-cn/
    -| README.md
    -| guide.md
```

那么对应的访问页面将是：

```html
docs/README.md        => http://domain.com
docs/guide.md         => http://domain.com/guide
docs/zh-cn/README.md  => http://domain.com/zh-cn/
docs/zh-cn/guide.md   => http://domain.com/zh-cn/guide
```

### 其他配置

1. [定制侧边栏](https://docsify.js.org/#/zh-cn/more-pages?id=%e5%ae%9a%e5%88%b6%e4%be%a7%e8%be%b9%e6%a0%8f)
2. [显示目录](https://docsify.js.org/#/zh-cn/more-pages?id=%e6%98%be%e7%a4%ba%e7%9b%ae%e5%bd%95)
3. [忽略副标题](https://docsify.js.org/#/zh-cn/more-pages?id=%e5%bf%bd%e7%95%a5%e5%89%af%e6%a0%87%e9%a2%98)
4. [定制导航栏](https://docsify.js.org/#/zh-cn/custom-navbar)
5. [封面](https://docsify.js.org/#/zh-cn/cover)

其他所有配置请访问[docsify中文文档](https://docsify.js.org/#/zh-cn/)

### 主题范例

这里贴一个我的主题配置：[Demo](http://docs.sqdxwz.com/all-notes/#/)

> `_sidebar.md`文件

```html
<!-- docs/_sidebar.md -->

- [About](README.md)
- [Regularization](regex.md)
- [Git](git.md)
- [Jupyter](jupyter.md)
- [Matplotlib](matplotlib.md)
- [Emoji](emoji.md)
- [Vim](vim.md)
- [Algorithm](algorithm.md)
- [Sort](sort.md)
- [Pandas](pandas.md)
- [Latex](mathjax_cmdeditor.md)
```

> `index.html`文件

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <link rel="shortcut icon" href="https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=2943963344,3662015478&fm=11&gp=0.jpg"/>
  <meta charset="UTF-8">
  <title>教书的先生</title>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
  <meta name="description" content="Description">
  <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
  <link rel="stylesheet" href="//unpkg.com/docsify/lib/themes/vue.css">
</head>
<body>
  <div id="app">文章正在加载中哦...</div>
<!--
  <div id="app"></div>
  <script>
    window.$docsify = {
      name: 'Uppez',
      repo: 'https://github.com/Uppez/myproject.git'
    }
  </script>
  <script src="//unpkg.com/docsify/lib/docsify.min.js"></script>
  <script>
  window.$docsify = {
    loadSidebar: true
  }
</script>
<script src="//unpkg.com/docsify/lib/docsify.min.js"></script>
-->

<script>
    window.$docsify = {
      auto2top: true, //当路线改变时，滚动到屏幕的顶部。
      coverpage: true, //激活封面功能。如果为true，则会从中加载_coverpage.md。
      executeScript: true, //执行页面上的脚本。只解析第一个脚本标记（演示）。如果存在Vue，则默认开启。
      loadSidebar: true, //_sidebar.md如果为真，则从_sidebar.md文件加载边栏，否则从指定的路径加载。
      loadNavbar: true,//_navbar.md如果为真，则从_navbar.md文件加载navbar ，否则从指定的路径加载。
      mergeNavbar: true,//Navbar将在小屏幕上与侧边栏合并。
      maxLevel: 4,//最大的内容表级别。
      subMaxLevel: 2,//在自定义边栏中添加目录（TOC）。
	  //logo: '/_media/icon.svg' //侧边栏logo
	  //name: 'NDZZ' //侧边栏名称
      ga: 'UA-106147152-1',
      name: 'NDZZ',
      search: {
        noData: {
          '/de-de/': 'Keine Ergebnisse!',
          '/zh-cn/': '没有结果!',
          '/': 'No results!'
        },
        paths: 'auto',
        placeholder: {
          '/de-de/': 'Suche',
          '/zh-cn/': '搜索',
          '/': 'Search'
        }
      },
      formatUpdated: '{MM}/{DD} {HH}:{mm}',
      plugins: [
        function(hook, vm) {
          hook.beforeEach(function (html) {
            var url = 'https://github.com/PYfive/docsify/blob/master/' + vm.route.file
            var editHtml = '[:memo: Edit Document](' + url + ')\n'
            return html
              + '\n----\n'
              + 'Last modified {docsify-updated} '
              + editHtml
          })
        }
      ]
    }
  </script>
  <script src="//unpkg.com/docsify/lib/docsify.min.js"></script>
  <script src="//unpkg.com/docsify/lib/plugins/search.min.js"></script>
  <script src="//unpkg.com/docsify/lib/plugins/ga.min.js"></script>
  <script src="//unpkg.com/prismjs/components/prism-bash.min.js"></script>
  <script src="//unpkg.com/prismjs/components/prism-markdown.min.js"></script>
  <script src="//unpkg.com/prismjs/components/prism-nginx.min.js"></script>

  <!--
  <script>
  window.$docsify = {
    coverpage: true
  }
</script>
<script src="//unpkg.com/docsify"></script>
-->
</body>
</html>
```

> `README.md`文件

```html
<img src="https://i.loli.net/2019/08/12/dK7VPOTrvYeB2GR.jpg" alt="m16Ikq.png" border="0" />

博主姓名:王荣胜

就读:河南理工大学本科生

我深信不疑的就是:他们以梦为马,我偏以码为梦~

联系方式:

- QQ:603329354

- QQ交流群:843108406

- 邮箱:603329354@qq.com

想更加了解我,请转至:[我的主页-教书的先生](https://sqdxwz.com)
```

> `_coverpage.md`文件（封面文件）

```html
<img width="180px" style="border-radius:50%" bor src="https://i.loli.net/2019/08/19/83UnV26OjDofulC.jpg">

# 教书先生的学习文档

- 本文档是作者自学习内容，旨在为大家提供一个较详细的学习教程参考，如果本文能为您得到帮助，请给予支持！


[GitHub](<https://github.com/Uppez>)
[开始阅读](README.md)
```

## 本地预览网站

运行一个本地服务器通过 `docsify serve` 可以方便的预览效果，而且提供 LiveReload 功能，可以让实时的预览。默认访问 `http://localhost:3000` 。

```html
docsify serve docs
```

# 发布

直接将所有文件上传到`Gituhb`仓库或者仓库`分支` ，然后开启`Github Pages`即可！

# 推荐阅读

[docsify官方中文文档](https://docsify.js.org/#/zh-cn)