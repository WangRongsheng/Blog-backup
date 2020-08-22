# 安装pyinstaller

```html
pip install pyinstaller
```

# 打包程序

首先，**切换到打包程序目录**，然后执行：

```html
pyinstaller -F xxx.py（xxx.py，打包的文件）
```

# 完成查看

打包完成后，会在目录下生成`dist`文件夹，里面会有可执行的打包好的`.exe`文件，运行即可！

打包过程可能会出现一些错误问题，例如：
```html
AttributeError: module 'enum' has no attribute 'IntFlag'
```

这是因为`enum`不是标准的库`enum`模块。您可能已`enum34`安装该软件包。解决办法就是卸载：

```html
pip uninstall enum34
```