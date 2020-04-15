# Linux简介

Linux是目前应用最广泛的服务器操作系统，基于Unix，开源免费，由于系统的稳定性和安全性，市场占有率很高，几乎成为程序代码运行的最佳系统环境。

linux不仅可以长时间的运行我们编写的程序代码，还可以安装在各种计算机硬件设备中，如手机、路由器等，Android程序最底层就是运行在linux系统上的。

## linux常用命令

命令格式：命令  -选项  参数 （选项和参数可以为空）

如：ls  -la  /usr

- ### 操作文件及目录

| 命令 | 参数 | 示例 | 说明 |
|--- |--- |--- |--- |
| cd |   | cd /home | 切换目录 |
| pwd |   | pwd | 显示当前工作目录目录 |
| touch |   | touch 1.txt | 创建空文件 |
| mkdir |   | mkdir testdir | 创建一个新目录 |
|   | -p | mkidr -p dir1/dir2/dir3/ | 创建多级目录，父目录不存在情况下先生成父目录 |
| cp |   | cp 1.txt | 复制文件或目录 |
|   | -r | cp -r dir1/ | 递归处理，将指定目录下的文件与子目录一并拷贝 |
| mv |   | mv dir1 dir2 | 移动文件或目录、文件或目录改名 |
| rm |   | rm 1.txt | 删除文件 |
|   | -r | rm -rf dir1 | r同时删除该目录下的所有文件 |
|   | -f | rm -rf dir1 | f强制删除文件或目录 |
| rmdir |   | rmdir dir1 | 删除空目录 |
| cat |   | cat 1.txt | 显示文本文件内容 |
| more |   | more 1.txt | 分页显示文本文件内容，可前后翻页，空格向后，b向前 |
| less |   | less 1.txt	| 分页显示文本文件内容，可前后翻页，空格向后，b向前，支持底行模式（后面介绍） |
| head |   | head 1.txt | 查看文本开头部分，默认十行 |
|   | -[num] | head -20 1.txt | 查看文本开头部分指定行数 |
| tail |   | tail 1.txt | 查看文本结尾部分，默认十行 |
|   | -[num] | tail -20 1.txt | 查看文本结尾部分指定行数 |
|   | -f | tail -f 1.txt | 循环滚动读取文件并动态显示在屏幕上，根据文件属性追踪 |
|   | -F | tail -F 1.txt | 循环滚动读取文件并动态显示在屏幕上，文件文件名追踪 |
| wc |   | wc 1.txt | 统计文本的行数、字数、字符数 |
|   | -m | wc -m 1.txt | 字符数 |
|   | -w | wc -w 1.txt | 文本字数 |
|   | -l | wc -l 1.txt | 文本行数 |
| find | -name | find / -name 1.txt | 在文件系统中的指定目录下查找指定的文件 |
| grep |   | grep aaa 1.txt | 在指定文件中查找包含指定内容的行，例：在1.txt中查找包含aaa的所有行 |
| ln |   | ln 1.txt 1_bak.txt | 建立链接文件 |
|   | -s | ln -s 1.txt 1_bak.txt | 对源文件建立符号连接，而非硬连接 |

- ### 系统常用命令

| 命令 | 参数 | 示例 | 说明 |
|--- |--- |--- |--- |
| top |   | top | 显示当前系统中耗费资源最多的进程 |
| date |   | date | 显示系统当前时间 |
| ps |   |   | 较少单独使用，配参数根据需求，ps -ef 或者ps-aux |
|   | -e /-A | ps -e | 显示所有进程，环境变量 |
|   | -f | ps -ef | 全格式显示 |
|   | -a | ps -a | 显示所有用户的所有进程（包括其它用户） |
|   | -u | ps -au | 按用户名和启动时间的顺序来显示进程 |
|   | -x | ps -aux | 显示无控制终端的进程 |
| kill | -9 | kill -9 pid | 强制杀死一个进程 |
| df |   | df | 显示文件系统磁盘空间的使用情况 |
|   | -h | df -h | 以人类可读的方式显示，Kb，Mb，GB等 |
| du |   |   | 显示指定的目录及其子目录已使用的磁盘空间的总和 |
|   | -s | du -s * | 进显示指定目录的总和，星号当前目录下表示所有 |
|   | -h | du -sh * | 以人类可读的方式显示，Kb，Mb，GB等 |
| free |   | free | 显示当前内存和交换空间的使用情况 |
| ifconfig |   | ifconfig | 网卡网络配置，常用于查看当前IP地址 |
|   |   | ifconfig eth0 192.168.12.22 | 临时修改系统IP（重启后失效） |
| ping |   | ping baidu.com | 测试网络的连通性 |
| hostname |   | hostname | 查看主机名 |
| shutdown | -r | shutdown -r | 先关机，再重启 |
|   | -h | shutdown -h | 关机后不重启 |
| halt |   | halt | 关机后关闭电源，相当于shutdown -h |
| reboot |   | reboot | 重新启动 相当于shutdown -r |

- ### 压缩解压缩

| 命令 | 参数 | 示例 | 说明 |
|--- |--- |--- |--- |
| gzip |   | gzip 1.txt | 压缩后面的文件或者文件夹 |
|   | -d | gzip -d 1.txt.gz | 解压后面的压缩文件 |
|   | -[num] | gzip -9 1.txt | 用指定的数字num调整压缩的速度，-1或--fast表示最快压缩方法（低压缩比），-9或--best表示最慢压缩方法（高压缩比）。系统缺省值为6 |
| tar | -c | tar -cvf 1.tar 1.txt | 建立一个压缩文件的参数指令，例，将1.txt压缩为1.tar，也可指定多个文件或文件夹 |
|   | -x | tar -xvf 1.tar 1.txt | 解开一个压缩文件的参数指令 |
|   | -z | tar -zcvf 1.tar.gz 1.txt / tar -zxvf 1.tar.gz 1.txt | 是否需要用 gzip ，使用gzip压缩或解压 |
|   | -v |   | 压缩的过程中显示文件 |
|   | -f |   | 使用档名，在 f 之后要立即接档名 |

修改目录下所有文件及子目录的所属用户和组，用数字来表示权限（r=4，w=2，x=1，-=0）|

- ### linux系统常用快捷键及符号命令

| 命令 | 参数 | 示例 | 说明 |
|--- |--- |--- |--- |
| ctrl + c |   |   | 停止进程 |
| ctrl + l |   |   | 清屏 |
| ctrl + r |   |   | 搜索历史命令 |
| ctrl + q |   |   | 退出 |
| tab |   |   | 自动补全 |
| > |   | echo "haha" > 1.txt | 将前一条命令的输出，写入到后面的文本中，将文本清空，然后写入 |
| >> |   | echo "lala" >> 1.txt | 将前一条命令的输出，写入到后面的文本中，不清空文本，追加到文本最后 |
| | |   | cat 1.txt | grep 'hello' | 管道命令，以前一个命令的输出作为输入，然后进行运算，例：打印1.txt中带有hello字符串的行 |
| * |   |   | 通配符，指所有 |

# 参考

1. [Linux常用命令](http://math.ecnu.edu.cn/~jypan/Teaching/Linux/command/index.htm)
2. [Linux常用命令详解](https://www.cnblogs.com/yuncong/p/10247583.html)