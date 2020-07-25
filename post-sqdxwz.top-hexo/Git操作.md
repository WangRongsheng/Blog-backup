---
title: Git操作
date: 2019-09-04 20:41:56
thumbnail: https://i.loli.net/2019/09/17/qkHSLAtImNpdcbi.png
tags: Git常用操作
categories: Git
---

## 一.Git简介

Git 是一种分布式版本控制系统，它可以不受网络连接的限制，加上其它众多优点，目前已经成为程序开发人员做项目版本管理时的首选，非开发人员也可以用 Git 来做自己的文档版本管理工具。

<!--more-->

Git 的api很多，但其实平时项目中90%的需求都只需要用到几个基本的功能即可，所以本文将从实用主和深入探索(后期更新)2个方面去谈谈如何在项目中使用 Git，一般来说，看完实用主义这一节就可以开始在项目中动手用。

> 说明：本文的操作都是基于Windows系统

## 二.实用主义

### 1.准备阶段

> 工具准备

进入 [Git官网](https://git-scm.com/)下载合适你的安装包。

> 账号准备

进入Github网站 注册一个账号就可以使用了。

### 2.常用操作

所谓实用主义，就是掌握了以下知识就可以玩转 Git，轻松应对90%以上的需求。以下是实用主义型的Git命令列表，先大致看一下:

- git clone

- git config

- git branch

- git checkout

- git status

- git add

- git commit

- git push

- git pull

- git log

- git tag

#### (1)git clone

> 从git服务器拉取代码

```html
git clone https://github.com/user/repo.git
```

#### (2)git config

> 配置开发者用户名和邮箱

```html
git config user.name user
git config user.email user@qq.com
```
#### (3)git branch

> 创建、重命名、查看、删除项目分支，通过Git做项目开发时，一般都是在开发分支中进行，开发完成后合并分支到主干。

```html
git branch daily/0.0.0
```
创建一个名为daily/0.0.0的日常开发分支，分支名只要不包括特殊字符即可。

```html
git branch -m daily/0.0.0 daily/0.0.1
```
如果觉得之前的分支名不合适，可以为新建的分支重命名，重命名分支名为daily/0.0.1。

```html
git branch
```
通过不带参数的branch命令可以查看当前项目分支列表。

```html
git branch -d daily/0.0.1
```
如果分支已经完成使命则可以通过-d参数将分支删除，这里为了继续下一步操作，暂不执行删除操作。

#### (4)git checkout

> 切换分支

```html
git checkout daily/0.0.1
```

#### (5)git status

> 查看文件变动状态
通过任何你喜欢的编辑器对项目中的 README.md 文件做一些改动，保存。

```html
git status
```
通过git status命令可以看到文件当前状态Changes not staged for commit:(改动文件未提交到暂存区）

```html
On branch daily/0.0.1
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
    modified:   README.md
no changes added to commit (use "git add" and/or "git commit -a")
```

#### (6)git add

> 添加文件变动到暂存区

```html
git add README.md
```
通过指定文件名README.md可以将该文件添加到暂存区，如果想添加所有文件可用git add. 命令，这时候可通过git status看到文件当前状态Changes to be committed:（文件已提交到暂存区）

```html
On branch daily/0.0.1
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
    modified:   README.md
```

#### (7)git commit

> 提交文件变动到版本库

```html
git commit -m '这里写提交原因'
```
通过-m参数可直接在命令行里输入提交描述文本。

#### (8)git push

> 将本地的代码改动推送到服务器

```html
git push origin daily/0.0.1
```
origin 指代的是当前的git服务器地址，这行命令的意思是把 daily/0.0.1 分支推送到服务器，当看到命令行返回如下字符表示推送成功了。

```html
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 267 bytes | 0 bytes/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local objects.
To https://github.com/gafish/gafish.github.com.git
 * [new branch]      daily/0.0.1 -> daily/0.0.1
 ```
现在我们回到Github网站的项目首页，点击Branch:master下拉按钮，就会看到刚才推送的daily/00.1分支了。

#### (9)git pull

> 将服务器上的最新代码拉取到本地

```html
git pull origin daily/0.0.1
```
如果其它项目成员对项目做了改动并推送到服务器，我们需要将最新的改动更新到本地，这里我们来模拟一下这种情况。

进入Github网站的项目首页，再进入daily/0.0.1分支，在线对README.md文件做一些修改并保存，然后在命令中执行以上命令，它将把刚才在线修改的部分拉取到本地，用编辑器打开README.md，你会发现文件已经跟线上的内容同步了。

如果线上代码做了变动，而你本地的代码也有变动，拉取的代码就有可能会跟你本地的改动冲突，一般情况下Git会自动处理这种冲突合并，但如果改动的是同一行，那就需要手动来合并代码，编辑文件，保存最新的改动，再通过git add .和git commit -m 'xxx'来提交合并。

#### (10)git log

> 查看版本提交记录

```html
git log
```
通过以上命令，我们可以查看整个项目的版本提交记录，它里面包含了提交人、日期、提交原因等信息，得到的结果如下：

```html
commit c334730f8dba5096c54c8ac04fdc2b31ede7107a
Author: gafish <gafish@qqqq.com>
Date:   Wed Jan 11 09:44:13 2017 +0800
    Update README.md
commit ba6e3d21fcb1c87a718d2a73cdd11261eb672b2a
Author: gafish <gafish@qqqq.com>
Date:   Wed Jan 11 09:31:33 2017 +0800
    test
.....
```
提交记录可能会非常多，按J键往下翻，按K键往上翻，按Q键退出查看。

#### (11)git tag

> 为项目标记里程碑

```html
git tag publish/0.0.1
git push origin publish/0.0.1
```
当我们完成某个功能需求准备发布上线时，应该将此次完整的项目代码做个标记，并将这个标记好的版本发布到线上，这里我们以publish/0.0.1为标记名并发布，当看到命令行返回如下内容则表示发布成功了。

```html
Total 0 (delta 0), reused 0 (delta 0)
To https://github.com/gafish/gafish.github.com.git
 * [new tag]         publish/0.0.1 -> publish/0.0.1
```
#### (12).gitignore

> 设置哪些内容不需要推送到服务器，这是一个配置文件

```html
touch .gitignore
```
.gitignore 不是Git命令，而在项目中的一个文件，通过设置.gitignore的内容告诉Git哪些文件应该被忽略不需要推送到服务器，通过以上命令可以创建一个.gitignore文件，并在编辑器中打开文件，每一行代表一个要忽略的文件或目录，如：

```html
demo.html
build/
```
以上内容的意思是Git将忽略demo.html文件 和build/目录，这些内容不会被推送到服务器上。

小结

通过掌握以上这些基本命令就可以在项目中开始用起来了，如果追求实用，那关于Git的学习就可以到此结束了，偶尔遇到的问题也基本上通过Google/百度也能找到答案。

