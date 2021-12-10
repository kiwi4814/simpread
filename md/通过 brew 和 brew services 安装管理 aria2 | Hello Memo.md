> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [iitii.github.io](https://iitii.github.io/2020/12/21/1/)

> 通过 brew 安装 aria2 并且使用 brew services 对其进行管理

### [](#一些说明 "一些说明")一些说明

*   目前并不能直接将 aria2 安装成 brew services 可以直接使用的样子。不过我们可以手动修改添加一些配置文件，使其支持

### [](#安装-aria2 "安装 aria2")安装 aria2

### [](#创建一些必须文件 "创建一些必须文件")创建一些必须文件

```
mkdir ~/.aria2
touch ~/.aria2/aria2.conf ~/.aria2/aria2.session /usr/local/opt/aria2/homebrew.mxcl.aria2.plist
```

### [](#修改配置文件 "修改配置文件")修改配置文件

1.  vim /usr/local/opt/aria2/homebrew.mxcl.aria2.plist

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
        <key>Label</key>
        <string>homebrew.mxcl.aria2</string>
        <key>ProgramArguments</key>
        <array>
            <string>/usr/local/opt/aria2/bin/aria2c</string>
        </array>
        <key>RunAtLoad</key>
        <true/>
        <key>KeepAlive</key>
        <true/>
    </dict>
</plist>
```

*   新版 M1 aria2 的目录变成了 `/opt/homebrew/opt/aria2`, 新版配置文件修改为以下内容

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
        <key>Label</key>
        <string>homebrew.mxcl.aria2</string>
        <key>ProgramArguments</key>
        <array>
            <string>/opt/homebrew/opt/aria2/bin/aria2c</string>
        </array>
        <key>RunAtLoad</key>
        <true/>
        <key>KeepAlive</key>
        <true/>
    </dict>
</plist>
```

1.  vim ~/.aria2/aria2.conf

> 一个 aria2 配置模版，可以参考参考

```
dir=~/Downloads

disk-cache=32M






continue=true











max-concurrent-downloads=32

max-connection-per-server=16


min-split-size=10M

split=32





max-overall-upload-limit=5M



disable-ipv6=false




input-file=.aria2/aria2.session

save-session=.aria2/aria2.session

save-session-interval=60






enable-rpc=true

rpc-allow-origin-all=true

rpc-listen-all=true



rpc-listen-port=6800

rpc-secret=1















follow-torrent=true

listen-port=51413



enable-dht=true

enable-dht6=true



bt-enable-lpd=true

enable-peer-exchange=true



peer-id-prefix=-TR2770-
user-agent=Transmission/2.77

seed-ratio=2.0


force-save=false



bt-seed-unverified=true
```

### [](#测试配置文件 "测试配置文件")测试配置文件

*   直接在终端输入 `cd && aria2c` 即可
*   默认情况下 `aria2` 会主动去读取 `~/.aria2/aria2.conf` 作为启动配置

```
❯ vim ~/.aria2/aria2.conf
❯ aria2c

12/21 15:49:51 [NOTICE] IPv4 RPC: listening on TCP port 6800

12/21 15:49:51 [NOTICE] IPv6 RPC: listening on TCP port 6800
```

### [](#启动服务 "启动服务")启动服务

*   查看所有服务及状态：`brew services list`
*   启动 aria2: `brew services start aria2`
*   停止 aria2: `brew services stop aria2`
*   重启 aria2: `brew services restart aria2`

------------- 本文结束再接再厉 -------------