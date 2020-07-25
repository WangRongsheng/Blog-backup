# Coding简介

Coding 是一个面向开发者的云端开发平台，目前提供代码托管，运行空间，质量控制，项目管理等功能。此外，还提供社会化协作功能，包含了社交元素，方便开发者进行技术讨论和协作。

# 安装

## 配置SSH公钥

1. 进入 [Coding官网](https://dev.tencent.com/) ，进行注册或者登录；
2. 关于如何获得密钥：[将Git与GitHub进行SSH连接](https://sqdxwz.top/post/hseFbgWv8/) ，然后打开`Coidng个人设置`---`SSH公钥`，点击`新增公钥`，将电脑上`.ssh/id_rsa.pub`文件里的所有内容全部复制过来即可；
3. 可以打开终端输入`ssh -T git@git.coding.net` 来测试一下是否成功；

## 新建项目并创建静态Pages应用

1. 点击页面上的加号里的项目选项，新建一个项目来存放以后的代码；
<img src="https://s1.ax1x.com/2020/03/21/8RgMTK.png" alt="8RgMTK.png" border="0" />

2. 创建好了之后点击`代码`---`Pages服务`，新建一个`Pages服务` ；
<img src="https://s1.ax1x.com/2020/03/21/8RgUmt.png" alt="8RgUmt.png" border="0" />

## 绑定个人域名

[为Github Pages添加自定义域名](https://sqdxwz.top/post/wTw0vWo80/)

# 拓展

基于`Github` 和`Coding` 都可以部署自己的博客，但是`Github` 在国外访问还行，国内访问速度过慢，是不是我们可以将自己的（Hexo）博客同时部署在`Github` 和 `Coding` 上呢，我们可以在国外访问`Github` ，并且在国内访问`Coding` ：

```html
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  - type: git  #部署方式，统一填git
    repository: 
      github: git@github.com:WangRongsheng/WangRongsheng.github.io.git # 填自己的
      coding: git@git.dev.tencent.com:WangRongsheng/blog.git  # 填自己的
    branch: master  #分支名称
```

