创建虚拟环境是为了让项目运行在一个独立的局部的`Python` 环境中，使得不同环境的项目互不干扰。

1、安装虚拟环境的第三方包 `virtualenv`

```html
pip install virtualenv
```

使用清华源安装：`pip install virtualenv -i https://pypi.python.org/simple/`

2、创建虚拟环境

cd 到存放虚拟环境光的地址

`virtualenv ENV` 在当前目录下创建名为`ENV` 的虚拟环境（如果第三方包`virtualenv` 安装在`python3` 下面，此时创建的虚拟环境就是基于`python3` 的）

`virtualenv -p /usr/local/bin/python2.7 ENV2` 参数 `-p` 指定`python` 版本创建虚拟环境

`virtualenv --system-site-packages ENV` 参数 `--system-site-packages` 指定创建虚拟环境时继承系统三方库

3、激活/退出虚拟环境

`cd ~/ENV` 跳转到虚拟环境的文件夹

`activate` 激活虚拟环境

`pip list` 查看当前虚拟环境下所安装的第三方库

`deactivate` 退出虚拟环境

4、删除虚拟环境

直接删除虚拟环境所在目录即可