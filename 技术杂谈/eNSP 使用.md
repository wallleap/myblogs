---
title: eNSP 使用
date: 2019-09-10 21:34
updated: 2019-09-10 21:34
cover: //cdn.wallleap.cn/img/pic/cover/202302QIAwJ8.jpg
category: 技术杂谈
tags:
  - 网络
  - HCNA
description: eNSP 使用
---

今天呢，接着讲 HCNA 的知识

讲一下 eNSP 的基本使用吧

我们双击 eNSP 的图标打开软件

首先看到的最大部分就是下面这个了

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHQty9hEZpnDt1S2DTBbNHS7XNxhuIUOZIEDuYlFMsq38xLenkjN8AbbuqGuqX3AQbVGt3tF9gkiccA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

包括了五个部分

- 样例中有一些已经配置好的拓扑，只需要打开启动一下即可
- 最近打开中有打开过的工程
- 学习栏中可以看到一些可以看的列表，点击之后可以打开相关的文档，到里面学习内容
- 点击上方新建拓扑可新建一张空白拓扑，点打开可一打开已保存的拓扑
- 点`×` 可以关掉这个页面
- 当然勾选上不再显示下次再打开软件就不会显示这个界面了

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHQty9hEZpnDt1S2DTBbNHS7kJPewnqHC5Rye06AUjHkG2nibNC7PwlqbDZ8suOUvlYGxJ8SupUQxdQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

上方就是打开的的一个样例

下面的就是某个文档

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHQty9hEZpnDt1S2DTBbNHS7BAnfv35CawuhfPqzE6W0aMMcKfdP8UrNYW0aQEfschr2cia3oicIsKBw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

`×` 掉之后，可以看到 eNSP 主界面，可以分为四个区域

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHQty9hEZpnDt1S2DTBbNHS7eAXNEwWIFLEicn1Vo4gkCCgtoDibFEmX9jHvyHKibibicv5xIQ3biaIf8VAg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

一个是主菜单，就是显示的“菜单”按钮，点击将会显示相关的功能

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHQty9hEZpnDt1S2DTBbNHS7rkQnian1FqOicKkdwCDpWQuEQSCVpIAibAg9BEDDqHNrDd5ybXuibqOd0w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

将鼠标移到每个菜单上可以看到各自的作用，详细的功能自己看吧，就不细讲了

第二个是工具栏，就是那一排的小图标，提供了常用的工具，将鼠标光标移到上面将会显示文字说明，右边的那四个也是这一区域的

第三个区域是网络设备区，就是左边的那三个红框，由上至下第一个框是一些设备，选择以后可以到第2个框选择这个设备的型号，选好之后第3个框将会显示设备详细信息

区域四是工作区，在这个区域内我们可以创建拓扑

= 直接选择好设备和型号，把设备拖入到工作区即可

= 连线可以直接选 auto，反正现在的设备挺智能的，使用交叉、直连线都行

= 在设备图标上右击将会弹出快捷菜单

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHQty9hEZpnDt1S2DTBbNHS7dzQlvYBicicFvDlbsT9Oo7FEEib6g2DNaFa6IYNMppL5Su3TekpPjicphw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

- 启动/停止设备就不用解释了
- 导出设备配置能够将你配置好的命令配置导出来，导入设备配置能将导出的配置文件导到设备中
- 对齐到网格，需要打开显示网格功能
- 删除该设备，可以点击删除，或者选中设备，按 <kbd>del</kbd> 键
- 数据抓包将会启动 wireshark，选中一个端口，之后 wareshark 会抓取这个接口的数据
- CLI 会进入设备配置的界面，你也可以直接双击进入
- 进入设置，视图页面会显示设备面板和接口卡，你可以拖动接口卡添加/移除接口卡，可以开关设备；配置界面可以设置设备的串口号(2000-65535)，主要是第三方软件登录 eNSP 模拟设备的

= PC 右击-设置，基础设置中可以设置主机名，IP 地址、子网掩码等网络参数

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHQty9hEZpnDt1S2DTBbNHS74gPs2cpAB9bHA0UWbZKE6A8H4cqQxlgcqAfsobgP5xOiaJb9KIdkP5A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

命令行中主要使用的是`ping IP地址` 检测连通性

= 设备启动：还可以全选设备，再点击工具栏中的启动来启动所有的设备

命令：

```sh
<Huawei> #默认是用户视图
<Huawei>system-view  #进入系统视图
[Huawei]quit   #退出系统视图，回到用户视图(也可以按 Ctrl+Z)
[Huawei]interface GigabitEthernet0/0/0 #进入接口视图
[Huawei-GigabitEthernet0/0/0]ip address 10.1.1.1 24 #配置IP地址
[Huawei-GigabitEthernet0/0/0]return
[Huawei]return
```

在每个视图下直接输入`?` 回车，将会显示所有的命令及提示

输入前面一个命令后空一格再输入`?` 回车将会显示后面的关键字或参数

甚至只输入命令的部分字母不加空格直接输`?` 就会列出以这些单词开头的命令

输入部分字母，再按 <kbd>tab</kbd> 键，能够补全命令关键字

上下键可以查看历史命令

常用命令：

```sh
[Huawei]sysname R1 #可以修改设备名为R1

<Huawei>clock timezone BJ add 08:00:00 #设置时区为北京
<Huawei>clock datetime 21:00:00 2020-02-24 #设置时间

[R1]header login information "标题" #登录时的标题文本
[R1]header shell information "welcome" #登录成功后的标题文本

<R1>display version # 查看路由器基本信息和运行状态
<R1>display current-configuration #查看路由器当前配置

[R1]display interface G0/0/0 #查看接口G0/0/0状态信息
<R1>display ip interface brief #查看接口与IP相关摘要信息
<R1>display ip routing-table #查看路由器配置信息、路由表
```

常用命令就写到这了，其他的命令和配置可以到 HedEx Lite 中查看

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHQty9hEZpnDt1S2DTBbNHS7AiaR1ZnyQGMIkRFn10QbxFOI2DwuxSwlYbicEG9QiaOAMpXvwxCRb2JCw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

我把两个文档也放里面了，直接解压就能用了

[下载链接](http://106.54.101.97:34567/A:/official%20accounts/20-02-22eNSP)

密码仍是 wallleap

我们配置路由器，一般都是远程配置的，通常通过 telnet、SSH 登录

首先，在 R1 上配置好 telnet，并且设置验证方式为密码验证，密码设置为 huawei

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHQty9hEZpnDt1S2DTBbNHS7cktNwNsn5cdZmGNTuKIBg1cVu6BBPxVxpBPP5LCiagBEneia5utnU4FA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

接着就可以使用其他设备登录了

比如 PC 机的，设置好静态 IP，IP 地址和 R1 同网段

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHQty9hEZpnDt1S2DTBbNHS7hagkfHgdlFzVyqRtRnXAmsJaQd8ngaynos5QtlFIXcJESibB0Mpx5KA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

接着进入 PC 的命令行，输入 `ping 192.168.1.1` 检测连通性，能 ping 通之后输入 `telnet 192.168.1.1` 登录路由器(有没有发现不能登录，哈哈，这个 PC 不支持这个功能)

我们更换成上面的路由器(就是一台微型的计算机)，支持 telnet 功能，设置 R2 的 G0/0/0 接口 IP 为 192.168.1.20/24，`telnet 192.168.1.1` 输入密码 `huawei`，看到 `[R2]` 变成了 `<R1>` 就是登录成功了

之后可以使用 `display users` 命令查看已经登录的用户信息

三种用户级别：

- 默认情况下，VTY 用户界面的用户级别为0(参观级)，只能使用 `ping`、`tracert` 等网络诊断命令
- 在 R1(网关路由器)上配置 Telnet 的用户级别为1(监控级)，只能使用密码登录设备、使用 `display` 等命令监控设备

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHTbH3c6W3tsITmlB5ib8grZFEUbmBicDicAkbibI3vhKZdo25UO1ic04JI1jiapN0M1Ya5ONpP26icqaFdjw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

下面这台时普通用户想登录路由器，输入正确的密码huawei之后能够进入用户视图，但是因用户级别不够，不能进入系统视图

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHTbH3c6W3tsITmlB5ib8grZFzOw53BcIXfLjgwNrgv7SZibMLKUn5iakrhamtkhI3hwkITiczNeqbOibRw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

- 管理员需要对路由器完全掌控，因此需要有单独的用户名和密码，可以进行配置和管理，用户级别为3(管理级)

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHTbH3c6W3tsITmlB5ib8grZFUSb4oLhRGg2Q4Hz8icb0Bz5cBPyYfGWLoqbUlfszYtth25qft62wQhg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

管理员 `telnet` 远程路由器，输入自己的用户名 `admin` 和密码 `huaweia`，能够进入系统视图并进行其他配置

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHTbH3c6W3tsITmlB5ib8grZF4DyH0mn3bQ7B4lKcLZiaK433KPyRjhuYu2hBxJUWPnaicohq8NweicIZg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

由于 Telnet 缺少安全的认证方式，而且传输过程采用 TCP 进行明文传输，存在安全隐患，因此推荐使用支持对报文加密传输的 SSH

首先，我们在 Server 端使用 `rsa local-key-pair create` 命令来生成本地 RSA 主机密钥对，配置好之后可以使用 `display rsa local-key-pair public` 查看贝蒂密钥对中的公钥部分信息

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHTbH3c6W3tsITmlB5ib8grZFjdGnNoDpSfJVqwpneIR1lnXFSlXWiauK1m9a57Aib2H4xoafGt9SMTxg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

进入 vty 用户界面，设置验证方式为 AAA

指定 vty 雷西那个用户界面只支持 SSH 协议(将自动禁止 telnet 功能)

创建本地用户 `huaweia` 和用户口令 `huaweia`，口令以密文方式显示

配置本地用户的接入类型为 SSH

新建 ssh 用户，用户名为 `huaweia`，认证方式为 `password`(密码认证方式)

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHTbH3c6W3tsITmlB5ib8grZF8AR5gndon1j7txHfHS5HAJHws8oQmiboOt1GnTkW648H4fOFiceibhz7A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

接着使用 `stelnet server enable` 命令开启设备的 ssh 功能

到此服务器端就配置完成了

我们还可以使用 `display ssh user-information huaweia` 查看 huaweia 用户的配置信息

使用 `display ssh server status` 命令查看 ssh 服务器全局配置信息

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHTbH3c6W3tsITmlB5ib8grZFn7uY3H6VCp89X3SCXV6MKQrJEGt2C3WD4hmjoWBaXhFM3PzicpicvYTw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

配置客户端

客户端第一次登录时，需要使用 `ssh client first-time enable` 开启 ssh 用户端首次认证功能

`stelnet IP` 登录服务器端，输入用户名，并 y 回车两次，接着输入密码就登录成功了

我们能够使用命令 `display ssh server session` 查看服务器端会话连接信息

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHTbH3c6W3tsITmlB5ib8grZF9tPY0QPO93ibm2jia2PGBKh1kG7PDmwsEHtGeIzllYQmnEEjc1GcXOYQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

连接好了，能够配置路由器，那么我们想向路由器上传文件怎么办呢

这就要用到 FTP(文件传输协议)了

咱先配置好服务器端

首先开启 FTP 功能，接着设置 ftp 登录的用户名为 `ftp`，密码为 `huawei`

配置用户可访问的目录为"flash",用户优先级为15(0~15,默认为3，管理级，越高用户权限越大)，服务类型为ftp

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHTbH3c6W3tsITmlB5ib8grZFstpDN6xhbKopRibYoXqqmmYTSzXrGMea8Cia4SZr3ejtRGrZvEInDuLw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

接着客户端配置

使用 `ftp IP` 连接 FTP 服务器，登录时输入用户名 `ftp` 和密码 `huawei`，路由器进入 ftp 视图，可以使用命令：

- `ls` 查看服务器文件
- `cd dir` 进入文件夹
- `dir` 查看文件属性
- `get` 从 ftp 服务器下载文件
- `put` 上传文件

![img](https://mmbiz.qpic.cn/mmbiz_png/bQicJnZn4LHTbH3c6W3tsITmlB5ib8grZFdjUjrLN9gbzgxVem2zWfJpQ0TlicibtVv5M1iaUywzWGnfOvDhthTbkqg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

基本操作就讲到这里了
