当我们在使用`putty/xshell`等软件进行`ssh`远程访问服务器时，进行远程访问的界面往往不能关掉，否则，程序将不再运行。而且，程序在运行的过程中，还必须时刻保证网络的通常，这些条件都很难得到满足。

为了解决上述问题，可以使用`Linux`下的`screen`命令，即使网络连接中断，用户也不会失去对已经打开的命令行会话的控制。下面介绍一些常用的`screen`命令。

具体使用如下：

我们可以使用`screen -S yourname`创建一个叫做`yourname的session`，这时我们要进入该`session`，需要使用`screen -r yourname`进入到该`session`中，此时就可以在该`session`里进行操作了，如运行程序。之后我们可以使用`Ctrl + a +d`命令将该`session`丢到后台进行处理。

```html
screen -S yourname -> 新建一个叫yourname的session
screen -ls         -> 列出当前所有的session
screen -r yourname -> 回到yourname这个session
Ctrl+a+d           -> 离开当前session
```

**Ctrl+a+d** 进行`detach`是重点

暂时离开当前`session`，将目前的 `screen session` (可能含有多个 windows) 丢到后台执行，并会回到还没进 `screen` 时的状态，此时在 `screen session `里，每个 `window` 内运行的 `process` (无论是前台/后台)都在继续执行，即使 `logout `也不影响。