---
title: HCL 配置之 ping 通及 Telnet
date: 2019-09-11 21:54
updated: 2019-09-11 21:54
cover: //cdn.wallleap.cn/img/pic/cover/202302nAUrrn.jpg
category: 技术杂谈
tags:
  - 网络
  - 华三
description: HCL 配置之 ping 通及 Telnet
---

让 PC ping 通路由器及 Host Telnet 路由器

## 一、任务

> * 命名 R、2S 为自己姓名首字母
> * 给设备配置时间
> * PC 能够 Ping 通 R
> * Host 能 telnet 路由器

## 二、配置

### 1、新建工程并添加设备

单机图示图标，新建工程，自己命名选择路径保存

![](https://cdn.wallleap.cn/img/pic/web-HCL1/pic1.png)

从左边选择设备，拖入操作区，使用 GE 线缆将设备连接起来，连接 Host 的时候注意选择有线网卡

![](https://cdn.wallleap.cn/img/pic/web-HCL1/pic2.png)

### 2、查看 Host 的 IP 并配好 PC、Host 相关参数

在真机环境中打开命令提示符，输入 `ipconfig` 获得刚刚新建的网卡 IP

![](https://cdn.wallleap.cn/img/pic/web-HCL1/pic3.png)

图示显示 `169...` 未分配地址，打开网络管理界面，右击 Vbox...网卡

![](https://cdn.wallleap.cn/img/pic/web-HCL1/pic4.png)

属性--找到 Internet 协议版本4（TCP/IPv4），双击后配置静态 IP

![](https://cdn.wallleap.cn/img/pic/web-HCL1/pic5.png)

禁用－启用该网卡，再次输入 `ipconfig` 查看 IP 地址

![](https://cdn.wallleap.cn/img/pic/web-HCL1/pic6.png)

启动所有设备

![](https://cdn.wallleap.cn/img/pic/web-HCL1/pic7.png)

右击 PC，选择配置，输入相关参数，启用接口

![](https://cdn.wallleap.cn/img/pic/web-HCL1/pic8.png)

### 3、路由器配置

<kbd>Ctrl</kbd> + <kbd>C</kbd> 退出自动配置，按 <kbd>enter</kbd> 继续

#### (1)修改名称

```sh
<H3C>system-view
System View: return to User View with Ctrl+Z.
[H3C]sysname LWR
```

#### (2)配置接口

![](https://cdn.wallleap.cn/img/pic/web-HCL1/pic9.png)

- G0/0 `192.168.11.1`
- G0/1 `192.168.10.1`

```sh
[LWR]int g0/0
[LWR-GigabitEthernet0/0]ip add 192.168.11.1 255.255.255.0
[LWR-GigabitEthernet0/0]quit
[LWR]int g0/1
[LWR-GigabitEthernet0/1]ip add 192.168.10.1 255.255.255.0
[LWR-GigabitEthernet0/1]quit
[LWR]dis cur
...
#
interface GigabitEthernet0/0
 port link-mode route
 combo enable copper
 ip address 192.168.11.1 255.255.255.0
#
interface GigabitEthernet0/1
 port link-mode route
 combo enable copper
 ip address 192.168.10.1 255.255.255.0
```

#### (3)开启 telnet 服务

```sh
[LWR]telnet server enable
[LWR]user-interface vty 0 4
[LWR-line-vty0-4]authentication-mode none
[LWR-line-vty0-4]user level-5
```

真机到控制面板中选择程序，启用服务，勾选 Telnet Client，确定，开启 telnet 功能

![](https://cdn.wallleap.cn/img/pic/web-HCL1/pic10.png)

### 4、交换机配置

![](https://cdn.wallleap.cn/img/pic/web-HCL1/pic11.png)

S1：

<kbd>Ctrl</kbd>+<kbd>C</kbd>   <kbd>enter</kbd>

```sh
<H3C>sys
System View: return to User View with Ctrl+Z.
[H3C]sys LWS1
[LWS1]int g1/0/1
[LWS1-GigabitEthernet1/0/1]no sh
[LWS1-GigabitEthernet1/0/1]quit
[LWS1]int g1/0/2
[LWS1-GigabitEthernet1/0/2]no sh
[LWS1-GigabitEthernet1/0/2]quit
```

S2：

<kbd>Ctrl</kbd>+<kbd>C</kbd>   <kbd>enter</kbd>

```sh
<H3C>sys
System View: return to User View with Ctrl+Z.
[H3C]sys LWS2
[LWS2]int g1/0/1
[LWS2-GigabitEthernet1/0/1]no sh
[LWS2-GigabitEthernet1/0/1]quit
[LWS2]int g1/0/2
[LWS2-GigabitEthernet1/0/2]no sh
[LWS2-GigabitEthernet1/0/2]quit
```

### 5、测试

#### (1)PC ping 路由器地址

![](https://cdn.wallleap.cn/img/pic/web-HCL1/pic12.png)

#### (2)Host(真机) ping R 并 telnet

![](https://cdn.wallleap.cn/img/pic/web-HCL1/pic13.png)

![](https://cdn.wallleap.cn/img/pic/web-HCL1/pic14.png)

### 6、时间配置

```sh
<LWR>sys
System View: return to User View with Ctrl+Z.
[LWR]clock p
[LWR]clock protocol none
[LWR]quit
<LWR>clock datetime 21:53:50 2019/09/09
```

### 7、保存

```sh
<LWR>save
The current configuration will be written to the device. Are you sure? [Y/N]:y
Please input the file name(*.cfg)[flash:/startup.cfg]
(To leave the existing filename unchanged, press the enter key):
Validating file. Please wait...
Configuration is saved to device successfully.
```
