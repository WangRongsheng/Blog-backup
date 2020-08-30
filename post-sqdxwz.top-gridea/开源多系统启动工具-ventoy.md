# 简介

`Ventoy`是一个制作可启动U盘的开源工具。有了`Ventoy`你就无需反复地格式化U盘，你只需要把`ISO`文件拷贝到U盘里面就可以启动了，无需其他操作。 你可以一次性拷贝很多个不同类型的`ISO`文件，在启动时`Ventoy`会显示一个菜单来选择(截图)。 无差异支持`Legacy BIOS`和`UEFI`模式。目前已经测试了各类超过260+ 个ISO文件(列表). 同时提出了"`Ventoy Compatible`"的概念，若被支持则理论上可以启动任何`ISO`文件. [官网](https://www.ventoy.net/cn/index.html)

- 体积小巧
- 开源免费
- 自定义方便
- 支持在线升级（无害）

<center><img src="https://s1.ax1x.com/2020/08/30/dbPQNq.jpg" alt="dbPQNq.jpg" border="0" /></center>

# 安装

> 此处以Windows为例，Linux请参考官方文档

1. 去官网下载最新版本，支持 `Windows`、`Linux`下安装到 `U盘` 操作；
2. 解压文件，直接运行可执行文件 `Ventoy2Disk.exe`，选择需要安装的 `U盘`等待几秒即可；
3. 创建必要目录（博主创建了 `systemISO`、`driver`、`tools`、`ventoy`)，整体来讲，博主还是喜欢创建目录，方便管理；
4. 按需复制系统镜像及软件工具到对应目录下；
5. 在`U盘` 根目录创建 `ventoy` 目录（大小写敏感），用来存放自定义配置文件，不建议增加无用的文件；

> `systemISO`放系统镜像；`tools`可以放一些激活工具等；`ventoy`可以更深层次的配置ventoy启动（美化等）；

<img src="https://s1.ax1x.com/2020/08/30/dbPJvF.gif" alt="dbPJvF.gif" border="0" />

# 美化

## 启动菜单别名化

在 `ventoy` 目录下创建 `ventoy.json` 文件，内容要求如下，必须是 `UTF-8` 格式：

```json
{
    "menu_alias" : [
        {
            "image": "/systemISO/wepe.iso",  // 镜像路径（绝对路径）
            "alias": "WEPE"   // 镜像别名
        },
        {
            "image": "/systemISO/cn_windows_7_ultimate_with_sp1_x64_dvd_u_677408.iso",
            "alias": "MS_Windows 7_x64"
        },
        {
            "image": "/systemISO/cn_windows_10_business_editions_version_2004_updated_may_2020_x64_dvd_c2acd212.iso",
            "alias": "MS_Windows_10_x64"
        },        
        {
            "image": "/systemISO/CentOS-8.2.2004-x86_64-dvd.iso",
            "alias": "Linux_Centos_8.2_x64"
        }
    ]
}
```

## 菜单主题化

去[主题](https://www.gnome-look.org/browse/cat/109/order/latest/) 里面选择自己喜欢的下载，并且放到`ventoy`文件夹内，在`ventoy.json` 文件下，增加如下内容：

```json
    "theme": {
        "file": "/ventoy/theme/theme.txt",
        "gfxmode": "1920x1080",
        "ventoy_left": "45%",
        "ventoy_top": "100%",
        "ventoy_color": "#000000"
    },
```

如果你不确定自己的`json`文件是否写的正确，可以使用[json语法正确与否测试](https://www.json.cn ) 、[json语法正确与否测试](http://json.parser.online.fr/) 进行测试。

全部配置代码：

```json
{
    "theme": {
        "file": "/ventoy/theme/theme.txt",
        "gfxmode": "1920x1080",
        "ventoy_left": "45%",
        "ventoy_top": "100%",
        "ventoy_color": "#000000"
    },
    
    "menu_alias" : [
        {
            "image": "/systemISO/wepe.iso",
            "alias": "WEPE"
        },
        {
            "image": "/systemISO/cn_windows_7_ultimate_with_sp1_x64_dvd_u_677408.iso",
            "alias": "MS_Windows 7_x64"
        },
        {
            "image": "/systemISO/cn_windows_10_business_editions_version_2004_updated_may_2020_x64_dvd_c2acd212.iso",
            "alias": "MS_Windows_10_x64"
        },        
        {
            "image": "/systemISO/CentOS-8.2.2004-x86_64-dvd.iso",
            "alias": "Linux_Centos_8.2_x64"
        }
    ]
}
```

**提示**：镜像排序处理

```html
// ventoy 默认以镜像名称第一个字母排序
// 所以，如果要排序，需在镜像名称前增加 [ A - Z ] 进行排序
```