
# Gitbook

`GitBook` 是一个基于 `Node.js` 的命令行工具，可使用 `Github/Git` 和 `Markdown`来制作精美的电子书，`GitBook` 并非关于 [Git]的教程。

# 安装

## 脚手架安装

由于`npm` 安装较慢，所以我们采用另外一种方法：

```html
 npm install -g cnpm --registry=https://registry.npm.taobao.org
```

然后再执行：

```html
cnpm install gitbook-cli -g
```

## 初始化

```html
gitbook init
```

这个过程极其漫长，即使是`npm`淘宝源也很慢。当然你可以去百度一下，大佬们办法多的是。

## 创建一个`book.json`文件

给大家一个我的`Demo`（可以直接实用）：

```html
{
    "title": "王荣胜的gitbook",
    "author": "王荣胜",
    "description": "select * from learn",
    "language": "zh-hans",
    "gitbook": "3.2.3",
    "styles": {
        "website": "./styles/website.css"
    },
    "structure": {
        "readme": "README.md"
    },
    "links": {
        "sidebar": {
            "我的博客": "https://sqdxwz.com"
        }
    },
    "plugins": [
        "-sharing",
        "splitter",
        "expandable-chapters-small",
        "anchors",

        "github",
        "donate",
        "sharing-plus",
        "anchor-navigation-ex",
        "favicon"
    ],
    "pluginsConfig": {
        "github": {
            "url": "https://github.com/WangRongsheng"
        },
        "donate": {
            "alipay": "./source/images/donate.png",
            "title": "",
            "button": "赞赏",
            "alipayText": " "
        },
        "sharing": {
            "douban": false,
            "facebook": false,
            "google": false,
            "hatenaBookmark": false,
            "instapaper": false,
            "line": false,
            "linkedin": false,
            "messenger": false,
            "pocket": false,
            "qq": true,
            "qzone": false,
            "stumbleupon": false,
            "twitter": true,
            "viber": false,
            "vk": false,
            "weibo": true,
            "whatsapp": false,
            "all": [
                "google", "facebook", "weibo", "twitter",
                "qq", "qzone", "linkedin", "pocket"
            ]
        },
        "anchor-navigation-ex": {
            "showLevel": false
        },
        "favicon":{
            "shortcut": "./source/images/favicon.jpg",
            "bookmark": "./source/images/favicon.jpg",
            "appleTouch": "./source/images/apple-touch-icon.jpg",
            "appleTouchMore": {
                "120x120": "./source/images/apple-touch-icon.jpg",
                "180x180": "./source/images/apple-touch-icon.jpg"
            }
        }
    }
}
```

里面有一些插件的说明，`Gitbook` 的插件安装需要把插件信息填在上面的文件里面，然后执行：

```html
gitbook install ./
```

## 生成静态文档

执行：
```html
gitbook build 
```
然后生成的`_book` 就是对应的网页文件夹。

# 发布

1. 发布到Github Pages上；
2. 发布到[Netlify](https://app.netlify.com/) ；

# 参考

1. [gitbook部署到服务器](https://blog.shuifengche.top/2019/11/22/gitbook部署到服务器/)
2. [GitBook运行报错 - Error: ENOENT: no such file or directory](https://blog.csdn.net/weixin_44266650/article/details/89708421)