最近写了一个简单的Python程序，想让这个小程序每天上午7点定时运行一次。由于其他原因，直接使用Windows定时任务：

1. 搜索打开【任务计划程序】 ：
<img src="https://s1.ax1x.com/2020/03/22/84bk5D.png" alt="84bk5D.png" border="0" />

2. 之后点击右侧的【创建基本任务】：
<img src="https://s1.ax1x.com/2020/03/22/84bqsI.png" alt="84bqsI.png" border="0" />

3. 输入任务名称以及可选的任务描述：
<img src="https://s1.ax1x.com/2020/03/22/84bvo8.png" alt="84bvo8.png" border="0" />

4. 设置任务的开始时间，这个应该没什么难度，我这里设置为每天早上7点运行此计划任务：
<img src="https://s1.ax1x.com/2020/03/22/84qMl9.png" alt="84qMl9.png" border="0" />
<img src="https://i.loli.net/2020/03/22/PCmlqJcjsiMyHah.png" >

5. 设置【操作】为【启动程序】：
<img src="https://i.loli.net/2020/03/22/aNeWqi6xtvVIZ1B.png" >

6. 进入启动程序设置界面：
<img src="https://i.loli.net/2020/03/22/9mO8C1DZsSBb7cM.png" >

    - 【程序或脚本】文本框中填的是Python编译器的名称，一般就是`python.exe`；
    - 【添加参数】文本框中填的是你的`要运行的Python程序`的完整路径；
    - 【起始于】文本框中填的是Python编译器的目录；

好了，这就设置好了，定时任务就开始了~