# 介绍

由于某些原因，国内访问 `Github` 会异常缓慢，在 `clone` 仓库时甚至只有 10kb/s 以下的速度，下载半天有时还会失败需要从头再来，甚是让人恼火。 本文介绍通过修改系统 `hosts` 文件的办法，绕过国内 `DNS` 解析，直接访问GitHub 的 `CDN` 节点，从而达到加速的目的。不需要科学上网，也不需要海外的服务器辅助。

# 使用

## 获取Github的官方CDN地址

打开 `https://www.ipaddress.com/`  查询以下三个链接的的 DNS 地址：

1. github.com
2. assets-cdn.github.com
3. github.global.ssl.fastly.net

<img src="https://s2.ax1x.com/2020/03/01/3cjSFU.png" />

记录下查询到的 `IP` 地址。

## 修改系统hosts文件

打开系统 `hosts` 文件(需管理员权限)。 路径：`C:\Windows\System32\drivers\etc`

windows10 可以将 `hosts` 文件复制到桌面进行修改后覆盖原文件，windows7 使用管理员权限即可。

在末尾添加三行记录并保存。(需管理员权限，注意 `IP` 地址与域名间需留有空格)

```html
# Copyright (c) 1993-2001 Microsoft Corp.
#
# This file has been automatically generated for use by Microsoft Internet
# Connection Sharing. It contains the mappings of IP addresses to host names
# for the home network. Please do not make changes to the HOSTS.ICS file.
# Any changes may result in a loss of connectivity between machines on the
# local network.
#

192.168.222.1 DESKTOP-LNVQC5O.mshome.net # 2025 2 4 27 7 1 41 512


  192.30.253.113     github.com

  185.199.108.153    assets-cdn.github.com

  199.232.5.194    github.global.ssl.fastly.net
```

## 刷新系统DNS缓存

`Windows+X`打开系统命令行（**管理员身份**）或 `powershell`

运行 `ipconfig /flushdns` 手动刷新系统 `DNS` 缓存。

<img src="https://s2.ax1x.com/2020/03/01/3cjpYF.png" />

现在打开 Github，`clone` 一个项目到本地试试吧！

