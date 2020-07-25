最近几次在更新Github项目的时候经常需要在`git push` 之后输入账号和密码，就很麻烦，特意去网上搜了下教程，没想到还真的有。

# 记住账号和密码

- 1、进入我们的项目，并且进入`.git` 文件，如果不显示`.git` 文件，你需要进行如下操作：

<center><img src="https://s1.ax1x.com/2020/04/29/Jo8A2j.png" alt="Jo8A2j.png" border="0" /></center>

- 2、编辑里面的配置文件`config` 

- 3、在配置文件最后加入：

```html
[credential]
    helper = store
```

<center><img src="https://s1.ax1x.com/2020/04/29/Jo8KaT.png" alt="Jo8KaT.png" border="0" /></center>