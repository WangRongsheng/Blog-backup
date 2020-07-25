---
title: 博客嵌入可以自适应的b站视频
date: 2019-11-18 13:32:24
thumbnail: https://i.loli.net/2019/11/18/3NHaP5S8yZOQWTf.png
tags: b站视频嵌入
categories: 杂谈
---

写博客的时候准备插入一个B站视频，发现B站点击分享会提供iframe嵌入视频，直接复制代码。

<!--more-->

```html
<iframe src="//player.bilibili.com/player.html?aid=44020824&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
```

添加到了博客里，然而它默认的样式只有很小的一块，还需要手动添加width和height属性，手动设置了固定的宽和高之后，显示正常，本以为大功告成。结果发下移动端边框超出。

于是参考网上资料，有直接修改主题样式的，使之外嵌一个class样式，但是一直测试失败。尝试多次后，才找到合适的解决办法，使用也非常简单。

# 解决方法

```html
<iframe id="spkj" src="https://player.bilibili.com/player.html?aid=44020824&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" width=100%> </iframe>
<script type="text/javascript">  
document.getElementById("spkj").style.height=document.getElementById("spkj").scrollWidth*0.76+"px";
</script>
```

使用方法：

只需**替换第一行中的数字**ID44020824 即可，所以每次只需插入B站视频av/XXXXXX的数字即可。