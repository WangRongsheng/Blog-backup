# 什么是Git？

关于什么是`Git`，当你打开百度去搜索，你可能会得到这样一个答案：

> `Git`，全称是**分布式版本控制系统**，`Git` 通常在编程中会用到，并且`Git`支持分布式部署，可以有效、高速的处理从很小到非常大的项目版本管理。分布式相比于集中式的最大区别在于开发者可以提交到本地，每个开发者通过克隆（`git clone`），在本地机器上拷贝一个完整的`Git`仓库。

想必大家看到这样官方的解释，估计还是一头雾水！下面我们可以举一个通俗易懂的例子：

比如当你在本地写好某一个编程文档时，发现有些地方需要修改或者删除，有的人可能会直接在当前文件中直接修改，有的人会复制一份在上面修改，然后删除没用的文件。但是当你发现还是原来的文件好或者另外的版本好时，就可能手足无措了。

此时使用`Git` 工具，就是聪明之举了。我们可以在本地建一个*版本库* ，每当我们需要修改时，就可以把之前的版本提交并标明此版的特点。这样文件夹里就只有一个编程文档了。当你需要哪个版本时，只要在版本库中恢复一下就可以了。

> *版本库* 又名仓库（`repository` ），可以简单理解成一个目录（存放好多版本的目录），目录里所有文件都被`Git` 管理起来，每个文件的修改，删除，`Git` 都会跟踪，以便任何时候都可以追踪历史或者在将来某一时刻可以还原修改。

刚才我们解读了**分布式版本控制系统** 的**版本控制** 这个词，接下来说一下什么是**分布式** ：

![本地版本控制VS集中化版本控制VS分布式版本控制](https://s1.ax1x.com/2020/09/20/woBPJO.png)

关于这部分介绍，我觉得官方文档给出的解答是比较详细的：[1.1 起步 - 关于版本控制](https://www.git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%85%B3%E4%BA%8E%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6)

# 什么是Github？

前面我们讲到了`Git` ，接下来讲的是`Github` ，当你第一次看到这两个名字是不是觉得很相似呢，但是事实上它们是不同的，总结来说：

- `Git` 是你的版本控制工具；
- `Github` 是你的代码托管平台，这样你对项目的版本管理是不是可以存储在云服务器上，而不是本地，这样更有利于你的代码或者项目管理；

> **补充** ：`Github`是属于国外的代码托管平台，而你可能在平常听到的`Gitee` 是国内的代码托管平台，实质上，他们做的事情是同一个哦~

# 安装并且配置Git

## 安装

由于`Git` 的普适性，使它在各个系统中的使用都是存在的，这其中包括：【Linux、maCOS、Windows】等，你可以参考[1.5 起步 - 安装 Git](https://www.git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git) 完成你的安装操作。

## 配置

初次使用`Git` ，我们不可避免的需要去配置你的环境，这主要包括：*配置本地Git库* 和 *配置本地Git库与Github之间的传输* 。

这里，我推荐大家参考：[Git的初次使用](https://www.cnblogs.com/fshost/p/9637711.html) 去配置自己的环境。

配置完成后，我们就可以进行自己的版本控制之路了~

# Git基础使用

## 获取Git仓库

通常有两种获取 `Git` 项目仓库的方式：

1. 将尚未进行版本控制的本地目录转换为 `Git` 仓库；
2. 从其它服务器 克隆 一个已存在的 `Git` 仓库。

两种方式都会在你的本地机器上得到一个工作就绪的 `Git` 仓库。

### 在已存在目录中初始化仓库

进入你本地的项目或者代码文件夹，执行：

```git
$ git init
```

该命令将创建一个名为 `.git` 的子目录（*隐藏文件*），这个子目录含有你初始化的 `Git`仓库中所有的必须文件，这些文件是 `Git` 仓库的骨干。 但是，在这个时候，我们仅仅是做了一个初始化的操作，你的项目里的文件还没有被跟踪。

如果在一个已存在文件的文件夹（而非空文件夹）中进行版本控制，你应该开始追踪这些文件并进行初始提交。 可以通过 `git add` 命令来指定所需的文件来进行追踪，然后执行 `git commit` ：

```git
$ git add .
$ git add LICENSE
$ git commit -m 'initial project version'
```

### 克隆现有的仓库

如果你想获得一份已经存在了的 `Git` 仓库的拷贝，比如说，你想为某个开源项目贡献自己的一份力，这时就要用到 `git clone` 命令。

```git
$ git clone https://github.com/WangRongsheng/test-Git
```

执行之后你会发现，远程的项目已经被你下载到本地了，文件夹中的文件与`Github` 仓库中完全相同。

## 记录每次更新到仓库

### 检查当前文件状态

可以用 `git status` 命令查看哪些文件处于什么状态。 如果在克隆仓库后立即使用此命令，会看到类似这样的输出：

```git
$ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```

这说明你现在的工作目录相当干净。换句话说，所有已跟踪文件在上次提交后都未被更改过。 此外，上面的信息还表明，当前目录下没有出现任何处于未跟踪状态的新文件，否则 `Git`  会在这里列出来。 最后，该命令还显示了当前所在分支，并告诉你这个分支同远程服务器上对应的分支没有偏离。 现在，分支名是“master”,这是默认的分支名。

现在，让我们在项目下创建一个新的 `demo.md` 文件。 如果之前并不存在这个文件，使用 `git status ` 命令，你将看到一个新的未跟踪文件：

```git
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        demo.md

nothing added to commit but untracked files present (use "git add" to track)
```

在状态报告中可以看到新建的 `demo.md` 文件出现在 `Untracked files`下面。 未跟踪的文件意味着 Git 在之前的快照（提交）中没有这些文件；`Git ` 不会自动将之纳入跟踪范围，除非你明明白白地告诉它“我需要跟踪该文件”。 

### 跟踪新文件

使用命令 `git add` 开始跟踪一个文件。 所以，要跟踪 `demo.md` 文件，运行：

```git
$ git add demo.md
```

此时再运行 `git status` 命令，会看到 `demo.md` 文件已被跟踪，并处于暂存状态：

```git
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   demo.md
```

### 状态简览

`git status` 命令的输出十分详细，但其用语有些繁琐。 `Git ` 有一个选项可以帮你缩短状态命令的输出，这样可以以简洁的方式查看更改。 如果你使用 `git status -s` 命令或 `git status --short` 命令，你将得到一种格式更为紧凑的输出。

```git
$ git status -s
 M README
MM Rakefile
A  lib/git.rb
M  lib/simplegit.rb
?? LICENSE.txt
```

简短命令说明：

|标记|状态|
|:-|:-|
|`??`|新添加的未跟踪文件|
|`A`|新添加到暂存区中的文件|
|`M`|修改过的文件|

### 忽略文件

一般我们总会有些文件无需纳入 `Git` 的管理，也不希望它们总出现在未跟踪文件列表。 通常都是些自动生成的文件，比如日志文件，或者编译过程中创建的临时文件等。 在这种情况下，我们可以创建一个名为 `.gitignore` 的文件，列出要忽略的文件的模式。 来看一个实际的 `.gitignore` 例子：

```git
$ cat .gitignore
*.[oa]
*~
``` 

- 第一行告诉 `Git` 忽略所有以 `.o` 或 `.a`结尾的文件。一般这类对象文件和存档文件都是编译过程中出现的。 
- 第二行告诉 `Git` 忽略所有名字以波浪符（`~`）结尾的文件，许多文本编辑软件（比如 Emacs）都用这样的文件名保存副本。 .

此外，你可能还需要忽略 `log`，`tmp` 或者 `pid` 目录，以及自动生成的文档等等。 要养成一开始就为你的新仓库设置好 `.gitignore` 文件的习惯，以免将来误提交这类无用的文件。

### 提交更新

现在的暂存区已经准备就绪，可以提交了。 在此之前，请务必确认还有什么已修改或新建的文件还没有 `git add` 过， 否则提交的时候不会记录这些尚未暂存的变化。 这些已修改但未暂存的文件只会保留在本地磁盘。 所以，每次准备提交前，先用 `git status` 看下，你所需要的文件是不是都已暂存起来了， 然后再运行提交命令 `git commit` ：

```git
$ git commit
```

这样会启动你选择的文本编辑器来输入提交说明。

如果你不想打开文本编译器进行书写，你也可以这样：

```git
git commit -m "你的提交说明"
```

### 移除文件

要从 `Git` 中移除某个文件，就必须要从已跟踪文件清单中移除（确切地说，是从暂存区域移除），然后提交。 可以用 `git rm` 命令完成此项工作，并连带从工作目录中删除指定的文件，这样以后就不会出现在未跟踪文件清单中了。

如果只是简单地从工作目录中手工删除文件，运行 `git status` 时就会在 “Changes not staged for commit” 部分（也就是 未暂存清单）看到：

```git
$ rm test.md
$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    test.md

no changes added to commit (use "git add" and/or "git commit -a")
```

然后再运行 `git rm` 记录此次移除文件的操作：

```git
$ git rm test.md
$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    test.md
```

下一次提交时，该文件就不再纳入版本管理了。

## 查看提交历史

在提交了若干更新，又或者克隆了某个项目之后，你也许想回顾下提交历史。 完成这个任务最简单而又有效的工具是 `git log` 命令。

```git
$ git log
commit 13c7822de2ba8fcc9a7674b5f2db845df9116b29 (HEAD -> master)
Author: WangRongsheng <603329354@qq.com>
Date:   Sun Sep 20 10:23:02 2020 +0800

    提交说明

commit 74e1688bfb7eff2675a59f0bdeca7ed7fc4784ed (origin/master, origin/HEAD)
Author: WangRongsheng <603329354@qq.com>
Date:   Sat Feb 29 21:29:43 2020 +0800

    demo上传

commit d01e1c4765f53cb1a6e33f3cb137a0e296ef420c
Author: coder-王荣胜 <fujingshusheng@gmail.com>
Date:   Sat Feb 29 21:10:08 2020 +0800

    Initial commit

```

不传入任何参数的默认情况下，`git log` 会按时间先后顺序列出所有的提交，最近的更新排在最上面。 正如你所看到的，这个命令会列出每个提交的 【`SHA-1` 校验和、作者的名字和电子邮件地址、提交时间以及提交说明】。

`git log` 有许多选项可以帮助你搜寻你所要找的提交， 具体的你可以去查看：[2.3 Git 基础 - 查看提交历史](https://www.git-scm.com/book/zh/v2/Git-基础-查看提交历史) 。

## 远程仓库的使用

### 查看远程仓库

如果想查看你已经配置的远程仓库服务器，可以运行 `git remote` 命令。 它会列出你指定的每一个远程服务器的简写。 如果你已经克隆了自己的仓库，那么至少应该能看到 `origin` ——这是 `Git` 给你克隆的仓库服务器的默认名字：

```git
$ git remote
origin
```

你也可以指定选项 `-v`，会显示需要读写远程仓库使用的 `Git` 保存的简写与其对应的 `URL`。

```git
$ git remote -v
origin  https://github.com/WangRongsheng/test-Git (fetch)
origin  https://github.com/WangRongsheng/test-Git (push)
```

### 从远程仓库中抓取与拉取

就如刚才所见，从远程仓库中获得数据，可以执行：

```git
$ git fetch <remote>
```

这个命令会访问远程仓库，从中拉取所有你还没有的数据。 执行完成后，你将会拥有那个远程仓库中所有分支的引用，可以随时合并或查看。

如果你的当前分支设置了跟踪远程分支， 那么可以用 `git pull` 命令来自动抓取后合并该远程分支到当前分支。 这或许是个更加简单舒服的工作流程。默认情况下，`git clone` 命令会自动设置本地 `master` 分支跟踪克隆的远程仓库的 `master ` 分支（或其它名字的默认分支）。 运行 `git pull` 通常会从最初克隆的服务器上抓取数据并自动尝试合并到当前所在的分支。

```git
$ git pull
```

### 推送到远程仓库

当你想分享你的项目时，必须将其推送到上游。 这个命令很简单：`git push <remote> <branch>` 。 当你想要将 `master` 分支推送到 `origin` 服务器时（再次说明，克隆时通常会自动帮你设置好那两个名字）， 那么运行这个命令就可以将你所做的备份到服务器：

```git
$ git push origin master
```

> 只有当你有所克隆服务器的写入权限，并且之前没有人推送过时，这条命令才能生效。 当你和其他人在同一时间克隆，他们先推送到上游然后你再推送到上游，你的推送就会毫无疑问地被拒绝。 你必须先**抓取** 他们的工作并将其**合并** 进你的工作后才能推送。 

## 分支简介

关于什么是分支？

> `GitHub`仓库默认有一个`master`的分支，当我们在`master`分支开发过程中接到一个新的功能需求，我们就可以新建一个分支同步开发而互不影响，开发完成后，在合并`merge` 到主分支`master` 上。  --参考[博客园木子的紫微星文章](https://www.cnblogs.com/yanliujun-tangxianjun/p/5740704.html)


### 分支创建

`Git` 是怎么创建新分支的呢？ 很简单，它只是为你创建了一个可以移动的新的指针。 比如，创建一个 `testing` 分支， 你需要使用 `git branch` 命令：

```git
$ git branch testing
```

这会在当前所在的提交对象上创建一个指针。

![两个指向相同提交历史的分支](https://s1.ax1x.com/2020/09/20/woWlE4.png)

那么，`Git` 又是怎么知道当前在哪一个分支上呢？ 也很简单，它有一个名为 `HEAD` 的特殊指针。 

![HEAD 指向当前所在的分支](https://s1.ax1x.com/2020/09/20/wofpGR.png)

### 分支切换

要切换到一个已存在的分支，你需要使用 `git checkout` 命令。 我们现在切换到新创建的 `testing` 分支去：

```git
$ git checkout testing
```

这样 `HEAD` 就指向 `testing` 分支了。

![ HEAD 指向当前所在的分支](https://s1.ax1x.com/2020/09/20/woflsf.png)

# 简易使用Git

如果你是一个小白或者不想大动干戈的去学习使用`Git` ，那么接下来这五条命令就足够满足你的日常使用了。

<center><img src="https://s1.ax1x.com/2020/09/20/wo4dbT.png" alt="Git工作流" border="0" /></center>

## git clone

复制远程仓库/仓库中的项目到本地的电脑，同时完成初始化

## git pull

拉取/同步远程仓库的代码到本地

建议写项目或者代码开始前，先执行**拉取** ！

## git add .

将本地项目保存至暂存区

## git commit -m "描述语句"

提交到本地仓库

## git push

将本地仓库项目上传至远程仓库

## 演示使用

```git
$ git clone https://github.com/WangRongsheng/test-Git
Cloning into 'test-Git'...
remote: Enumerating objects: 10, done.
remote: Counting objects: 100% (10/10), done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 10 (delta 2), reused 5 (delta 0), pack-reused 0
Unpacking objects: 100% (10/10), 1.18 KiB | 2.00 KiB/s, done.

$ git pull
Already up to date.

$ git add .

$ git commit -m "2020.09.20提交"
[master fb558fa] 2020.09.20鎻愪氦
 1 file changed, 3 insertions(+), 1 deletion(-)

$ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 345 bytes | 115.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/WangRongsheng/test-Git
   13c7822..fb558fa  master -> master
```

这样我就完成了一个项目的`克隆`、`拉取更新`、`添加暂存区`、`添加修改说明`、`推送` 。


# 参考资料

1. [Git官方文档](https://www.git-scm.com/book/zh/v2)
2. [Git是什么](https://www.php.cn/tool/git/412871.html)
3. [Git与Github是什么关系](https://www.zhihu.com/question/21907548)
4. [Git、Github、Gitlab与Gitee之间的关系](https://www.jianshu.com/p/bca32e8dd020)
5. [GitHub使用（四） - 关于分支Branch](https://www.cnblogs.com/yanliujun-tangxianjun/p/5740704.html)
6. [Git基本命令使用](https://sqdxwz.top/post/QFPLAZbSg/)

# 推荐学习

1. [Git参考手册](http://gitref.justjavac.com/index.html)
2. [Git官方文档](https://www.git-scm.com/book/zh/v2)
3. [视频学习：小白也能学会使用GitHub](https://www.bilibili.com/video/BV17V411z71W)
4. `Git`速查表：
![Git速查表](https://s2.ax1x.com/2020/02/29/36Vbf1.png)