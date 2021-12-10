> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [wild-flame.github.io](https://wild-flame.github.io/guides/docs/mac-os-x-setup-guide/aria_2/readme)

> 实现百度，迅雷等离线下载。

实现百度，迅雷等离线下载。

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

[](#安装-install)安装 | Install
---------------------------

```
$ brew install aria2
```

[](#配置-settings)配置 | Settings
-----------------------------

```
$ cd ~
$ mkdir .aria2
$ cd .aria2
$ touch aria2.conf
```

aria2 有两个模式，第一个没有后台在命令行里运行的，第二个就是 rpc 模式。

可以设置`aria2.conf`文件如下：

```
#用户名
#rpc-user=user
#密码
#rpc-passwd=passwd
#上面的认证方式不建议使用,建议使用下面的token方式
#设置加密的密钥
#rpc-secret=token
#允许rpc
enable-rpc=true
#允许所有来源, web界面跨域权限需要
rpc-allow-origin-all=true
#允许外部访问，false的话只监听本地端口
rpc-listen-all=true
#RPC端口, 仅当默认端口被占用时修改
#rpc-listen-port=6800
#最大同时下载数(任务数), 路由建议值: 3
max-concurrent-downloads=5
#断点续传
continue=true
#同服务器连接数
max-connection-per-server=5
#最小文件分片大小, 下载线程数上限取决于能分出多少片, 对于小文件重要
min-split-size=10M
#单文件最大线程数, 路由建议值: 5
split=10
#下载速度限制
max-overall-download-limit=0
#单文件速度限制
max-download-limit=0
#上传速度限制
max-overall-upload-limit=0
#单文件速度限制
max-upload-limit=0
#断开速度过慢的连接
#lowest-speed-limit=0
#验证用，需要1.16.1之后的release版本
#referer=*
#文件保存路径, 默认为当前启动位置
dir=/Users/xxx/Downloads
#文件缓存, 使用内置的文件缓存, 如果你不相信Linux内核文件缓存和磁盘内置缓存时使用, 需要1.16及以上版本
#disk-cache=0
#另一种Linux文件缓存方式, 使用前确保您使用的内核支持此选项, 需要1.15及以上版本(?)
#enable-mmap=true
#文件预分配, 能有效降低文件碎片, 提高磁盘性能. 缺点是预分配时间较长
#所需时间 none < falloc ? trunc « prealloc, falloc和trunc需要文件系统和内核支持
file-allocation=prealloc
```

*   [配置示例下载](http://aria2c.com/archiver/aria2.conf)

默认下载路径的「/Users/xxx/Downloads」可以改为任何你想要的绝对路径。此处写为 Downloads 目录，xxx 请自行替换成你的 Mac 用户名，然后保存，退出编辑器。

### [](#启动)启动

```
$ aria2c --conf-path="/Users/xxxxxx/.aria2/aria2.conf" -D
```

[TODO*: 配置开机启动]

### [](#配置-web-界面)配置 Web 界面

```
$ git clone https://github.com/ziahamza/webui-aria2
```

### [](#添加到收藏夹)添加到收藏夹

```
$ cd webui-aria2 
$ open index.html
```

然后点击” 收藏 “按钮把这个页面添加到收藏夹里吧！

### [](#下载-chrome-插件)下载 Chrome 插件

通过网盘下载所需要使用的插件：[下载地址](https://chrome.google.com/webstore/detail/baiduexporter/mjaenbjdjmgolhoafkohbhhbaiedbkno)

**使用方法：**

安装插件后进入百度网盘任意下载页，可以看到 “导出下载”，选择“ARIA2 - RPC” 即可。

* * *

_参考：_

*   [Aria2 源码 / 程序下载](https://sourceforge.net/projects/aria2/files/stable/)
*   Mac 下使用 Aria2 下载教程 ---- 迅雷和百度盘终极解决方案 (可突破百度盘限速) - [http://bbs.feng.com/read-htm-tid-9585996.html](http://bbs.feng.com/read-htm-tid-9585996.html)
*   在 OS X 里通过终端进行文件下载的利器：Aria2 - [http://chaishiwei.com/blog/804.html](http://chaishiwei.com/blog/804.html)
*   MAC OS 里的下载利器 — Aria2！- [http://www.coderblog.in/2015/06/the-best-download-app-for-mac-os-aria2.html](http://www.coderblog.in/2015/06/the-best-download-app-for-mac-os-aria2.html)
*   Mac 上使用百度网盘很烦躁？花点时间配置 aria2 吧 - [http://sspai.com/32167](http://sspai.com/32167)