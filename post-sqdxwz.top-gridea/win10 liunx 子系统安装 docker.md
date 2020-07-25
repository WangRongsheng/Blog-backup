记录自己安装docker 的过程

​安装完子系统后，按`win键`加`R键`， 输入`cmd``回车`

> [Windows 10安装Linux子系统方法](https://jingyan.baidu.com/article/fc07f989a357db12ffe519fd.html)

​打开`cmd` 后输入 `bash.exe` 回车就进入了子系统 接下来正式开始 docker 的安装啦

依次执行命令：

```html
sudo apt-get update
```

```html
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

```html
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

使用以下命令更新apt软件包索引并安装最新版本的`Docker CE`

```html
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

<img src="https://s1.ax1x.com/2020/03/14/8lNmgP.png" alt="8lNmgP.png" border="0" />

这就已经安装好了

输入`docker` 看看安装好没

<img src="https://s1.ax1x.com/2020/03/14/8lN84s.png" alt="8lN84s.png" border="0" />


