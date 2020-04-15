# Mkdocs-material介绍

> 符合google material ui规范的静态文档网站生成器，使用markdown进行文档书写。

## mkdocs

- python编写的markdown解释器、编译器，带有本地cli工具；
- 自带基于Tornado的小型http服务，用于本地调试；
- 内置一键式发布至GitHub Pages；
- 内置mkdocs风格、readthedocs风格的主题，并支持自定义主题；
- 支持调用python模块实现语法及渲染的扩展；

## mkdocs-material

- python模块，符合google material ui规范的mkdocs自定义主题；
- 针对特定语法、功能做了渲染优化；
- 根据客户端浏览器页面尺寸自动缩放，对PC、移动设备都友好；
- 丰富的页面配色，多达19种主体配色和16种悬停链接文字配色；
- 支持中文搜索；
- 支持统计功能，如百度统计，谷歌统计；

# 安装

## 命令安装

打开`命令行`并运行命令：

```
pip install mkdocs mkdocs-material
```

若下载慢，可更换安装源为豆瓣：

```
pip install --trusted-host pypi.douban.com -i http://pypi.douban.com/simple/ mkdocs mkdocs-material
```

这里放出一个我的环境配置：

- python环境: 3.6.6
- python包环境：

| 包名 | 模块名 | 版本 |
| :-: | :-: | :-: |
|mkdocs|	mkdocs|	1.0.4|
|mkdocs-material| material |3.0.6|
|Markdown|	markdown | 3.0.1 |
|pymdown-extensions| pymdownx | 6.0 |

## 初始化项目

```
mkdocs new my-project
```

> 命令中的`my-project`为生成的文件包的名称，可以修改为自己想要的。

会生成my-project目录，进入该目录里，可以看到默认放置了一些文件，包括`mkdocs.yml`，这是主配置文件。

## 修改样式

通过上一步我们生成了一个`.yml`文件，也就是我们的配置文件，接下来就是按照自己的想法配置啦。

> 注意要修改的东西的`代码`全部放在`.yml`文件就可以，会自动解析的。

### 修改主题

Mkdocs生成后会有一个自带的主题，大概是这个样子的：[主题参考网站](http://docs.sqdxwz.com/python-small-examples/) ，但是如果你不喜欢，你可以修改成另外一个：[第二种主题参考网站](http://docs.sqdxwz.com/ds_python/) 。

第二种主题在`mkdocs.yml`里添加配置：

```
theme:
  name: material
```

### 添加扩展

在`mkdocs.yml`里添加配置：

```
markdown_extensions:
  - admonition
  - codehilite:
      guess_lang: false
      linenums: false
  - toc:
      permalink: true
  - footnotes
  - meta
  - def_list
  - pymdownx.arithmatex
  - pymdownx.betterem:
      smart_enable: all
  - pymdownx.caret
  - pymdownx.critic
  - pymdownx.details
  - pymdownx.emoji:
      emoji_generator: !!python/name:pymdownx.emoji.to_png
  - pymdownx.inlinehilite
  - pymdownx.magiclink
  - pymdownx.mark
  - pymdownx.smartsymbols
  - pymdownx.superfences
  - pymdownx.tasklist
  - pymdownx.tilde
```

### 添加百度统计

1. 在[百度统计](https://tongji.baidu.com/web/welcome/login)里创建添加站点，确定后会看到javascript代码，复制代码；
2. 在docs目录下新建js目录，并在`docs/js`目录里放置`baidu-tongji.js`，将复制的代码粘贴进来；
3. 最后在`mkdocs.yml`里新增如下配置:
```
extra_javascript:
    - 'js/baidu-tongji.js'
```

### 修改配色

mkdocs-material支持google material ui规范定义的19种主体配色和16种鼠标悬停超链接文字配色。

在`mkdocs.yml`里添加配置:

```
extra:
  palette:
    primary: 'Blue Grey'
    accent: 'Pink'
```

> 代码后面的颜色可以修改为自己喜欢的！

### 添加中文搜索

虽然search功能(lunr.js)暂不直接支持中文，但测试发现设置为日语后，中文和英文搜索都可以使用。

```
extra:
  search:
    language: 'jp'
```

另外，搜索对话框的显示文字，默认为英文，可以设置为中文。例如"search"改为中文后就叫"搜索"。

```
theme:
  language: 'zh'
```

### 添加页面

在`my-project/docs/`里放置`.md`文件，可以自行组织目录结构。

然后在`mkdocs.yml`里添加，比如这样:

```
nav:
  - 介绍: index.md
  - 安装:
      - 本地环境搭建: install/local.md
      - 发布至GitHub Pages: install/github-pages.md
      - 发布至自己的HTTP Server: install/http-server.md
  - 语法:
      - 语法总览: syntax/main.md
      - 标题: syntax/headline.md
      - 段落: syntax/paragraph.md
```

- 上面的index.md就是放置在my-project/docs/index.md。
- 上面的local.md就是放置在my-project/docs/install/local.md。

> 注意：由于是yaml格式，因此首先要符合yaml的语法要求，**docs下需要一个index.md，作为站点首页**，文档层次结构虽然可以很多层，但最佳实践是**控制在2层**内，最多不要超过3层，否则展示会不够友好。

### 主题范例

这里我给出一个我的主题内容搭配，可以直接使用：

```
site_name: AI学习
site_author: 王荣胜
repo_url: https://github.com/WangRongsheng
site_url: https://github.com/WangRongsheng
site_description: 越努力越幸运

theme:
  language: 'zh'
  feature:
    tabs: true
  name: 'material'
  palette:
    primary: 'indigo'
    accent: 'indigo'
    font:
    text: 'Ubuntu'
    code: 'Ubuntu Mono'
    include_search_page: false
    search_index_only: true

extra:
  search:
    language: 'zh'
  social:
    - type: 'github'
      link: 'https://github.com/WangRongsheng'


markdown_extensions:
  - admonition
  - codehilite:
      guess_lang: false
  - toc:
      permalink: true

extra_css:
  - '_static/extra.css'


nav:
    - 介绍:
       - 介绍: index.md
       - 关于: about.md
       - 信息: tj.md
    - 机器学习: 
       - 1. K-最近邻算法: ai/knn.md
       - 2. K-均值算法: ai/k-means.md
       - 3. 基于矩阵分解的推荐系统: ai/mf.md
       - 4. 基于用户的协同过滤: ai/usercf.md
       - 5. 基于项目的协同过滤: ai/itemcf.md
       - 6. 朴素贝叶斯分类: ai/psbys.md
       - 7. 贝叶斯个性化排序: ai/bpr.md
       - 8. 决策树: ai/jcs.md
       - 9. 随机森林: ai/sjsl.md
    
markdown_extensions:
  - admonition
  - codehilite:
      guess_lang: false
  - toc:
      permalink: true
    

    
# Extensions
markdown_extensions:
  - admonition
  - codehilite:
      guess_lang: false
      linenums: true
  - def_list
  - footnotes
  - meta
  - toc:
      permalink: true
  - pymdownx.arithmatex
  - pymdownx.caret
  - pymdownx.critic
  - pymdownx.details
  - pymdownx.emoji:
      emoji_generator: !!python/name:pymdownx.emoji.to_svg
  - pymdownx.inlinehilite
  - pymdownx.keys
  - pymdownx.magiclink
  - pymdownx.mark
  - pymdownx.progressbar
  - pymdownx.smartsymbols
  - pymdownx.superfences:
      custom_fences:
        - name: math
          class: arithmatex
          format: !!python/name:pymdownx.arithmatex.fence_mathjax_format
  - pymdownx.tasklist:
      custom_checkbox: true
  - pymdownx.tilde

```

## 运行

在my-project目录里执行：

```
mkdocs serve
```

通过浏览器访问本地ip的8000端口（比如http://127.0.0.1:8000/）

> 注意一定要在`my-project`目录执行！

## 发布

### 发布到GitHub pages

通过`mkdocs gh-deploy`这行命令自动编译出html并发布至GitHub pages，步骤如下：

#### 初始化repo

1. 在github上创建一个repo，名字叫my-project（可以是其他名，这里先假设叫my-project），创建repo时候选择初始化带有README.md；
2. 将repo同步到本地，使用git clone；

#### 导入项目

1. 将mkdocs根目录（即my-project目录）下的所有东西移到刚刚git clone下来的git目录下；
2. 然后可以将最早创建的mkdocs根目录（即my-project目录）删除了；

#### 发布

在本地git目录下执行：

```
mkdocs gh-deploy
```

### 发布到个人HTTP Server

通过`mkdocs build`这行命令编译出html并手动同步至http server的根目录：

#### 生成站点文件

在git目录下执行命令：

```
mkdocs build
```

命令执行完毕后可以看到site目录。

#### 发布至http server

将site目录里的所有东西拷贝到http server的根目录下。

# 最佳实践

如果你想要写好一份项目或者其他的文档，你不可避免的要去学习使用`Markdown` ，这里推荐你去多多练习下：

1. [Markdown在线编译器](https://www.mdeditor.com/)
2. [Markdown基础语法](https://sqdxwz.top/post/UWPsajVaD/)


