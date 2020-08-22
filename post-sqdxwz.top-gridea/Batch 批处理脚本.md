# 前言

提到自动化解决方案，相信大部分人会想到用 `Python` 语言，只需要根据功能场景，编写 `Python` 脚本即可。

相反，`PC` 端的 `Batch` 批处理 似乎快被忘记了，很多人对它嗤之以鼻，认为这么古老的脚本语言貌似没什么用，`Python` 似乎可以取而代之。

相比 `Python` 脚本，`Batch` 批处理脚本在某些场景下，使用更简洁、方便、高效，即写即用，不需要依赖 `Python` 环境，并且可以完全摆脱打包等繁琐步骤。

# 批处理基础

新建批处理脚本很简单，只需要新建一个文本文件，然后修改编码方式为：`ANSI` 编码，接着编写脚本逻辑代码，最后保存文件以 `.bat` 结尾即可。

<center><img src="https://s1.ax1x.com/2020/08/12/axVvR0.png" alt="axVvR0.png" border="0" /></center>

> 图中编译软件为：**Notepad++**

`Batch` 常用命令包含：`echo`、`::/rem`、`title/color`、`cd/md/dir`、`rd/del/copy`、`pause`、`goto`、`for`、`if`、`set`、`start`等。

其中：

- `@echo off` ：代表在本行开始关闭回显，不显示正在执行的批处理命令及执行结果，一般放在批处理文件第一行

- `echo` 日志参数：用于在控制台输出日志，偏于理解脚本执行逻辑

- `::/rem` 注释内容：注释内命令

- `title/color`：设置窗体标题和背景颜色

- `cd`：切换目录

- `md`：创建目录

- `dir`：显示文件夹的内容

- `rd`：删除一个目录

- `del` 删除模式 文件：删除文件。通过配置删除模式，可以删除任意文件，包含隐藏、只读、系统文件

- `copy`：拷贝文件

- `pause`：暂停命令，一般放在批处理文件最后一行

- `goto`：跳转命令，一般和「 : 任务名称 」搭配使用，执行一个循环任务，实例见第 3 节

- `for`：循环命令，和 `Python` 中的 `for` 语法类似

- `if`：判断命令

- `set`：设置一个变量

- `start`：调用外部程序的命令

# 案例

1、对文件夹或桌面下的文件进行分类，然后放置到不同的文件夹内，方便归纳管理

```bat
@echo off
for %%i in (*) do (md %%~xi 
move *%%~xi %%~xi)
pause
```

- `for` 用于遍历当前文件夹，遍历的结果用 `do` 分别去执行后面的命令
- `%%~xi` 是截取 `%%i` 的扩展名，使用 `md` 命令新建一个文件夹
- `move` 的作用是：将源文件移动到新的文件夹中

2、删除当前目录（包含子目录）下所有的`build` 文件夹

使用 `Android Studio` 编译后，如果项目存在多个 `Module`，可能会存在多个 `build` 文件夹，可以使用下面的批处理脚本一键删除

```bat
@echo off
:: 打开到当前目录下
cd /d "%~dp0"

echo 开始删除
:: 循环删除
for /r /D %%i in (*build*) do rd /s /q "%%i"
echo 删除完成
pause
```

- `%~dp0`：批处理文件当前目录
- `/s`：从所有子目录下删除文件
- `/q`：指定以「 安静模式 」执行删除操作，删除不需要确认


3、执行 `Python` 脚本定时任务

比如，我编写完一个 `Python` 采集爬虫，我想 5 分钟执行一次，这里可以使用 `goto` 命令

```bat
@echo off  

title 循环运行Python代码

:: 5分钟执行一次，单位为s
set INTERVAL=300

:: 提前执行一次，把执行时间打印出来
echo 开始执行 - %time%
python C:/test.py 

:: 使用timeout进行倒计时
timeout %INTERVAL%

:: 新建一个任务
:Task  
echo 开始执行 - %time%
python C:/test.py 
timeout %INTERVAL%

:: 使用goto命令，开始跳转到上面的任务，开始执行
goto Task  
```

4、`Git` 提交代码

正常使用`git` 命令行提交代码（ 不使用 `IDE` ），需要使用 `git add .`、`git commit -m 提交日志`、`git pull`、`git push `四条命令

使用批处理脚本，只需要双击一下，输入提交日志就完事了

具体代码如下：
```bat
@echo off
title 提交代码
echo 提交代码，简化操作

:: 状态
git status

:: set：等待输入，赋值给变量msg
set /p commit_msg=代码提交注释：

:: 提交代码的 4 条命令
git add .
git commit -m %commit_msg%
git pull
git push

echo 提交成功
pause 
```

5、清除系统垃圾文件

指定删除模式、待删除的路径，调用 `del` 命令去删除即可

```bat
@echo off
:: 配置
title Alic Feng batTool for Clean
color 03
mode con cols=42 lines=20

echo executes cleaning,Please waiting...

::程序删除系统无用文件开始
del /f /s /q  %systemdrive%\*.tmp 1>nul 2>nul
del /f /s /q  %systemdrive%\*._mp 1>nul 2>nul
del /f /s /q  %systemdrive%\*.log 1>nul 2>nul
del /f /s /q  %systemdrive%\*.gid 1>nul 2>nul
del /f /s /q  %systemdrive%\*.chk 1>nul 2>nul
del /f /s /q  %systemdrive%\*.old 1>nul 2>nul
del /f /s /q  %systemdrive%\recycled\*.* 1>nul 2>nul
del /f /s /q  %windir%\*.bak 1>nul 2>nul
del /f /s /q  %windir%\prefetch\*.* 1>nul 2>nul
del /f /s /q %windir%\temp\*.* 1>nul 2>nul
del /f /q  %userprofile%\cookies\*.* 1>nul 2>nul
del /f /q  %userprofile%\recent\*.* 1>nul 2>nul
del /f /s /q  "%userprofile%\Local Settings\Temporary Internet Files\*.*" 1>nul 2>nul
del /f /s /q  "%userprofile%\Local Settings\Temp\*.*" 1>nul 2>nul
del /f /s /q  "%userprofile%\recent\*.*" 1>nul 2>nul
::删除系统垃圾文件结束

echo 清除系统垃圾完成！！！
echo. & pause
```