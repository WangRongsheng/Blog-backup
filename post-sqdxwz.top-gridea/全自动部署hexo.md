使用pm2实现自动监控文件变动，自动提交

1.在本地安装pm2（一个可在后台永久打开一个node小程序的 nodejs应用，也可以监控文件变化），按照代码如下：

```html
sudo npm install -g pm2
```

2.在博客的 resource 文件夹下新建 `start.js` ，内容如下：

```html
var process = require('child_process');

process.exec(' hexo g -d', function (error, stdout, stderr) {
    if (error !== null) {
      console.log('exec error: ' + error);
    }
});
```
3.在同级目录下创建 `watch.json` ,内容如下

```html
{
  "apps" : [{
    "name"       : "blog",
    "script"     : "./start.js",
    "exec_interpreter": "node",
    "exec_mode"  : "fork_mode",
    "watch"      : "_posts"
  }]
}
```

4.使用`pm2`命令实现监控文件变动自动提交

```html
pm2 start watch.json
```

以上即可轻松自动部署。