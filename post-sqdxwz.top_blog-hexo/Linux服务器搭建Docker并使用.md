## 简介

`Docker` 是一个开源的应用容器引擎，而一个容器`containers`其实是一个虚拟化的独立的环境，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的 `Linux `机器上，也可以实现虚拟化。容器是完全使用沙箱机制，相互之间不会有任何接口。

## 优点

- 类似`win10 sandbox`，一种沙箱机制，相互独立运行
- 初始化环境完全一致
- 容器内可运行多个镜像（比如同时运行上千个`wordepress`）
- 无可比拟的优势：部署超快、超简单

## Docker基础环境搭建

`docker`已经通用与`pc`、`mac`、`lunix`系统。[Docker 官方安装教程](https://docs.docker.com/engine/install/centos/) 。

### 安装docker

```html
docker version > /dev/null || curl -fsSL get.docker.com | bash 
service docker restart 
systemctl enable docker  #设置开机自启
```

### 安装docker compose(二选一)

#### 方法一

```html
curl -L https://github.com/docker/compose/releases/download/1.16.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose   #下载最新文件
chmod +x /usr/local/bin/docker-compose     #添加可执行权限
```

#### 方法二

```html
pip install docker-compose
```

## Docker常用命令

```html
docker images   #查看所有docker映像
docker ps    #查看所有容器
docker ps -a    #查看正在运行中的容器
docker stop XXXX  #停止运行xxxx容器（xxxx为容器id前4位）
docker rmi image-name   #删除一个映像
docker rmi -r $(docker images -q)   #删除所有映像
docker rm $(docker ps -a -q)    #删除所有容器
docker exec -it container-id bash   #进入容器
exit    #退出容器
ctrl+c    #退出当前容器并结束该容器
```

## 快速重置技巧

```html
service docker stop  # 停止docker
rm -rf /var/lib/docker   #移除docker容器
service docker restart  #重启docker,此时相当于刚刚安装好docker。
```

## Docker可视化管理

### portainer

`portainer`可视化，可快速部署常见应用

官网：https://www.portainer.io

安装：

```html
docker volume create portainer_data
docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
```

完成后访问域名+9000即可

> 如果是服务器，记得去服务器里面**设置安全组** ，以保证可以正常访问！

### Seagull （海鸥）

项目地址：https://github.com/tobegit3hub/seagull

安装：

```html
docker run -d -p 10086:10086 -v /var/run/docker.sock:/var/run/docker.sock tobegit3hub/seagull
```

支持十几种模板，多国语言，可快速运行、停止或删除镜像。

### 宝塔自带的Docker容器管理

安装：通过宝塔软件管理下载安装，安装过程需要3分站左右

算是目前为止可视化操作最完善的管理器，可以图形化的生成镜像、完成推送、自带终端命令。一下子有一种把我们从`windows1.0`拉升至`win10`的感觉。

## Docker部署完后设置域名代理

> 作用：通过域名直接访问

### 通过宝塔设置反代

先进入宝塔面板，点击左侧网站，添加站点，完成后进入网站设置，点击反向代理，目标URL填入http://127.0.0.1:代理端口（代理端口就是docker应用的外接接口），再启用反向代理即可。如果想启用SSL ，就直接在站点配置即可。

<center><img src="https://s1.ax1x.com/2020/09/09/wlxtrd.jpg" alt="wlxtrd.jpg" border="0" /></center>

### caddy反代（没有宝塔时的策略）

设置较为麻烦，愿意的请参考：https://www.moerats.com/archives/422/

## 参考

- [栢阅部落](https://baiyue.one/archives/368.html)
- [B站：docker新手入门学习笔记演示教程](https://www.bilibili.com/video/BV1bb411U7SB)