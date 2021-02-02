# 一、关于若依

> RuoYi是一款基于SpringBoot+Bootstrap的极速后台开发框架。

- RuoYi 官网地址：http://ruoyi.vip
- RuoYi 在线文档：http://doc.ruoyi.vip
- RuoYi 源码下载：https://gitee.com/y_project/RuoYi
- RuoYi 在线提问：https://gitee.com/y_project/RuoYi/issues
- RuoYi 博客：https://www.oschina.net/p/ruoyi

# 二、前后端分离版本部署

## 1、检查版本

环境要求：
```html
JDK >= 1.8 (推荐1.8版本)
Mysql >= 5.7.0 (推荐5.7版本)
Maven >= 3.0
Redis >= 3.0
Node >= 10
```

自己环境检查，打开`cmd`：
```html
// java版本查看
java -version

//Maven版本查看
mvn -v

//Node版本查看
node -v

//Redis下载的时候选择合适版本就可以了
//下载Redis.zip只需要解压就可以使用了

//Mysql版本查看
//打开Mysql Workbench输入：select version()
```

> Mysql使用[Mysql Workbench](https://blog.csdn.net/zs1342084776/article/details/88701261) 

> [Windows下Redis下载](https://github.com/tporadowski/redis/releases)

## 2、启动Redis

进入解压的`Redis`文件夹内，打开`cmd`：
```html
redis-server.exe redis.windows.conf
``` 

看到输出信息即为成功！**在整个项目的运行中，Redis需要一直运行**

> 错误解决：[creating server tcp listening socket 127.0.0.1:6379: bind No error](https://blog.csdn.net/fengzhihen2007/article/details/52211048)

## 3、下载源码

```html
git clone https://gitee.com/y_project/RuoYi-Vue.git
```

## 4、导入数据库文件

将`RuoYi-Vue\sql`下的数据导入本地的数据库

## 5、修改默认数据库登录密码

修改`RuoYi-Vue\ruoyi-admin\src\main\resources\application-druid.yml`下的：

图片1

## 6、运行bat文件

在`RuoYi-Vue\bin`下按顺序执行：
```html
clean.bat
package.bat
run.bat
```

## 7、开启前端

切换到`RuoYi-Vue\ruoyi-ui`下：
```html
npm install --registry=https://registry.npm.taobao.org

npm run dev
```

用户名：`admin`、密码：`admin123`

> 如果遇到输入验证码后报错，可以参考这里：https://www.cnblogs.com/smfx1314/p/11071718.html

> 解决完错误以后重新执行第**6** 和**7** 步骤

# 三、参考

- [【若依管理系统】前后端分离版之带权限管理功能之快速搭建](https://www.bilibili.com/video/BV1pK4y1W7Fa)
- [若依Vue（前后端分离版）开源项目分析【完结】](https://www.bilibili.com/video/BV1WX4y1K7Lf)







