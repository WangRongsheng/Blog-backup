# 简介

`Git`是一种代码管理工具。

使用`Git`出于以下3种原因：

1. 代码管理；
2. 版本控制；
3. 团队协作；

# 基本命令

<img src="https://s2.ax1x.com/2020/02/29/36V3ee.png">

## git clone

> 复制远程仓库/仓库中的项目到本地的电脑，同时完成初始化

```html
$ git clone https://github.com/WangRongsheng/test-Git
Cloning into 'test-Git'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
```

之后你就可以在**当前目录或者桌面**看到一个叫做`test-Git`的文件，这就说明我们`克隆`项目到本地了。

> 如果让`test-Git`文件中显示所以文件，你就会看到一个`.git`的文件，里面存放的是仓库的基本配置，我们不需要管这个，了解就好！

如果你已经写好了一个文件或文件夹，但是没有配置远程仓库该怎么办呢？

这时候我们就需要进行自主的初始化了，在该**文件夹**下运行以下指令就可以进行初始化和配置远程仓库：

```html
git init + git remote add origin + 仓库地址
```

> 注意：对于新手来说，没有配置远程仓库的情况尽量避免，操作较为复杂哦！


## git add .

> 将本地项目保存至暂存区

在这里我在我的`test-Git`文件夹中写入一个新的**文件**：`demo.txt` ，里面的内容填写为Hello World，然后在**文件夹**中运行：

```html
$ git add .
```

## git commit -m "描述语句"

> 提交到本地仓库

在这里我继续在我的`test-Git` **文件夹**下运行：

```html
$ git commit -m "demo上传"
[master 74e1688] demo上传
 1 file changed, 1 insertion(+)
 create mode 100644 demo.txt
```

## git push

> 将本地仓库项目上传至远程仓库

在这里我继续在我的`test-Git` **文件夹**下运行：

```html
$ git push
fatal: HttpRequestException encountered.
   ▒▒▒▒▒▒▒▒ʱ▒▒▒▒
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 294 bytes | 294.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/WangRongsheng/test-Git
   d01e1c4..74e1688  master -> master
```

这时候刷新我们的远程仓库-`Github`/`Gitlab`/`Coding`的仓库就可以看到我们的**新文件** `demo.txt`已经上传上去了！

## git pull

> 拉取/同步远程仓库的代码到本地

在这里我继续在我的`test-Git` **文件夹**下运行：

```html
$ git pull
Already up to date.
```

# Git命令速查

<img src="https://s2.ax1x.com/2020/02/29/36Vbf1.png">




