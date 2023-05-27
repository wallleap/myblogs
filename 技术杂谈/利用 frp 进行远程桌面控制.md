---
title: 利用 frp 进行远程桌面控制
date: 2022-05-09 10:21
updated: 2022-05-09 10:21
cover: //cdn.wallleap.cn/img/post/202205091750478.jpg
category: 技术杂谈
tags:
  - 电脑
  - win
description: 利用 frp 进行远程桌面控制
---

之前买了一年的华为云服务器，就只是托管了个网站，最近想着做点什么，经常在家的时候需要用公司电脑拷点文件，所以想利用一下 windows 的远程桌面。

在公网上想要访问公司电脑，没有公网 IP 情况下就需要使用内网穿透，内网穿透的工具有很多，如花生壳、net123、ngrok、frp，花生壳和 nat123 属于服务商提供的穿透所以会收取费用（一月40-50 / 128Kb），ngrok 和 frp 属于需要手动配置搭建的程序。

我选择的是 [frp](https://github.com/fatedier/frp) ，官方文档地址为：[https://gofrp.org/](https://gofrp.org/)

## 1、下载 frp

前往 [releases]( https://github.com/fatedier/frp/releases)，根据自己系统下载相应架构的压缩包，如果不知道选那个，可以先下载箭头所示的两个，有问题再选择其他的（linux 输入 `arch` 命令查看）

![frp-releases](https://cdn.wallleap.cn/img/post/202205091058892.png)

## 2、服务器端配置

下载完成之后进行服务器端的配置

### 修改配置文件

先将 linux 压缩包上传到服务器，我这里用的是[宝塔面板](https://www.bt.cn/new/index.html)，之后解压，重命名

![解压后 frp](https://cdn.wallleap.cn/img/post/202205091108806.png)

双击 `frps.ini`  修改配置

```ini
[common]
bind_port = 7000

# 服务器端监听http请求的端口(由于80端口被nginx占用,因此指定其他端口)
vhost_http_port = 81 

# 服务器用以显示连接状态的站点端口,以下配置中可以通过访问IP:7500登录查看frp服务端状态等信息
dashboard_port = 7500

# dashboard对应的用户名/密码
dashboard_user = username
dashboard_pwd = password

# 日志文件路径
#log_file = /root/net-ct/frp/frps.log


# 日志记录错误级别,分为:trace, debug, info, warn, erro
#log_level = warn

# 日志保存最大天数
#log_max_days = 3

# 客户端连接校验码(客户端需与之相同)
privilege_token = tokenvalue

# heartbeat configure, it's not recommended to modify the default value
# the default value of heartbeat_timeout is 90
# heartbeat_timeout = 90

# only allow frpc to bind ports you list, if you set nothing, there won't be any limit
# privilege_allow_ports = 2000-3000,3001,3003,4000-50000

# pool_count in each proxy will change to max_pool_count if they exceed the maximum value
max_pool_count = 5

# max ports can be used for each client, default value is 0 means no limit
max_ports_per_client = 0

# authentication_timeout means the timeout interval (seconds) when the frpc connects frps
# if authentication_timeout is zero, the time is not verified, default is 900s
authentication_timeout = 900

# 支持外部访问的域名(需要将域名解析到IP)
subdomain_host = frps.domain.com
```

### 开启防火墙端口

防火墙常用命令：

1. 防火墙基本操作
  
    查看版本： `firewall-cmd --version`
    显示状态： `firewall-cmd --state`
    查看所有打开的端口： `netstat -anp`

    开启防火墙 `systemctl start firewalld`
    关闭防火墙 `systemctl stop firewalld`

    开启防火墙 `service firewalld start`
    若遇到无法开启
    先用：`systemctl unmask firewalld.service`
    然后：`systemctl start firewalld.service`

2. 端口查询

    查询指定端口是否已开 `firewall-cmd --query-port=666/tcp`

    提示 yes or no

    查询所有开启的端口 `netstat -anp`

3. 开启端口

    如果上面端口查询没有开启的话，需要重新开启一下

    开启端口命令

    添加 `firewall-cmd --zone=public --add-port=80/tcp --permanent`（`–permanent` 永久生效，没有此参数重启后失效）

    重新载入 `firewall-cmd --reload`

    查看 `firewall-cmd --zone= public --query-port=80/tcp`

    删除 `firewall-cmd --zone= public --remove-port=80/tcp --permanent`

    我们只需要开启相应的端口即可，例如 `7000` 端口（最好用到的端口都开启下）

    ```zsh
    firewall-cmd --zone=public --add-port=7000/tcp --permanent
    firewall-cmd --reload
    firewall-cmd --zone= public --query-port=7000/tcp    # 现在会显示 yes
    ```

### 更改安全组

有的云服务器可能还需要开启下端口，点击更改安全组，修改绑定的安全组或者新建一个

![选择安全组](https://cdn.wallleap.cn/img/post/202205091128083.png)

在入方向规则中添加三条规则

![开启用到的端口](https://cdn.wallleap.cn/img/post/202205091127119.png)

### 运行命令

```zsh
cd /www/frp
./frps -c ./frps.ini
```

可以在计划任务中添加上述命令

![计划任务](https://cdn.wallleap.cn/img/post/202205091136622.png)

点击执行，查看日志，提示 `successfully` 成功

![成功](https://cdn.wallleap.cn/img/post/202205091137625.png)

## 3、客户端配置

服务器端跑动之后，可以在 windows 上进行配置了

首先解压 windows 的压缩包，在目录中用 `cmd` 打开

![输入cmd](https://cdn.wallleap.cn/img/post/202205091140454.png)

修改配置文件 `frpc.ini`

```ini
[common]
server_addr = 服务器IP地址
server_port = 7000
privilege_token = tokenvalue

[RDP]
type = tcp
local_ip = 127.0.0.1
local_port = 3389
remote_port = 7001
```

执行命令

```zsh
frpc.exe -c frpc.ini
```

`success` 成功

![成功](https://cdn.wallleap.cn/img/post/202205091144784.png)

也可以把 frpc 设置成自动运行的

设置成服务，自启动：以管理员身份运行

```cmd
sc.exe create frpcservice binPath="\"D:\Program Files\frp_0.42.0_windows_386\frpc.exe\" -c \"D:\Program Files\frp_0.42.0_windows_386\frpc.ini\"" DisplayName="frpcservice" start=delayed-auto
```

如果报错了就采取另一种方式（可以执行  `sc delete frpcservice`  删除该服务）

> 利用 [winsw](https://github.com/winsw/winsw/releases) 将 `frpc` 注册为系统服务：
>
> 下载 ，将 `WinSw x64.exe` 复制到 `frp` 所在目录并重命名为 `winsw.exe`
>
> 新建 `winsw.xml` 文件，输入以下内容，编码为 `utf-8`
>
> ```xml
> <service>
>     <id>frpc</id>
>     <name>Frpc Service</name>
>     <description>Frp客户端启动</description>
>     <executable>frpc</executable>
>     <arguments>-c frpc.ini</arguments>
>     <onfailure action="restart" delay="60 sec"/>
>     <onfailure action="restart" delay="120 sec"/>
>     <logmode>reset</logmode>
> </service>
> ```
>
> 以管理员权限打开 `CMD`，并进入该目录
>
> 执行命令：
>
> ```cmd
> winsw install
> winsw start
> ```
>
> 提示成功后可以进入 **服务** 查看

## 4、远程连接

Windows10/11 在设置中开启`远程桌面`

电脑上利用自带的 `mstsc` 可以连接，在手机或 iPad 上搜索 `RD Client` 安装

![mstsc](https://cdn.wallleap.cn/img/post/202205091506098.png)

打开后

电脑名字填：`服务器IP:7001`

用户账户为你自己电脑的账户和密码

之后连接即可

![连接成功](https://cdn.wallleap.cn/img/post/202205091510683.png)

遇到的坑主要是防火墙的以及设置服务的

参考：

[内网穿透-Frp](https://www.forever121.cn/?p=253)
