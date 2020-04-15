# 简介

在之前我已经提到了使用 `jsDelivr` 和 `Github` 作为图床：[jsDelivr ＋ Github ＝图床](https://sqdxwz.top/post/RoBGEjnfs/)，但是在移动端使用的体验并不好，最近发现了两款可以在线提供服务的程序。

# Picee

`Picee` 原为支持 `GitHub` 图床的 `Chrome Extension`，经 [tangkaichuan](https://github.com/tangkaichuan) 修改，可以在线使用并使用 `jsDelivr CDN`。

- 项目地址：[picee](https://github.com/WangRongsheng/picee)
- 演示站：https://guguga.cn/image

使用方法：

## Access token

在 `Github` 生成自己的 `Token`，步骤如下：

`Settings` → `Developer settings` → `Personal access tokens` → `Generate new token`

勾选 `write:packages` ，生成 `Token` 。在生成的页面中复制 `Token` ，粘贴到 `Access Token` 中点击 `Auth` 即可食用。

## Account & Password

输入自己的 Github 帐号及密码即可使用。

配置相关信息：

`Repo` 中填入 `Username/Reponame` ，`Folder` 中填入仓库路径（默认**不填** ），然后打勾。在菜单中还有更多的自定义选项，可以自行探究~

# auto PicCdn

(搭建个人更为简洁的上传Github仓库图片)[https://github.com/yumusb/autoPicCdn]
