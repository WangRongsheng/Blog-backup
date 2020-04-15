# 简介

很人觉得`Github`不就是一个代码托管所吗，如何能展示项目呢？其实完全可以借助`Github`的`gh-pages`打造出自己的一个作品集，无论是对自己的提升整合还是日后的面试都大有裨益。

> 那可能有人会不解，既然 `Github用户名.github.io` 已经能展示页面了，那`gh-pages`是什么作用呢？
> 答：大家不会只有一个项目要展示的吧，万一你和楼主一样把 `Github用户名.github.io` 作为**博客**了，那不就没地方展示项目了吗？所以就有了`gh-pages`这个东东。

# 使用

如果你有Git和Github的操作基础，你才能看懂接下来的操作哦：

1. 用`git symbolic-ref`命令将当前工作分支由`master`切换到一个尚不存在的分支`gh-pages` ；

```html
git symbolic-ref HEAD refs/heads/gh-pages
```

2. 上传你的``.html`或者`展示的项目文件`到你的github本地文档中；

3. 
```html
git add .
```
4. 
```html
git commit -m "描述内容"
```

5. 执行推送命令，在`github`远程版本库创建分支`gh-pages`；
```html
git push -u origin gh-pages
```
以后如果再更新文件的话，直接确认在`gh-pages` 下时，`git push` 即可~

# 参考

[如何用Github的gh-pages分支展示自己的项目](https://www.cnblogs.com/MuYunyun/p/6082359.html)