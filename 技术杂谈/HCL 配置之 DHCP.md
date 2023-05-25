---
title: HCL 配置之 DHCP
date: 2019-09-16 15:42
updated: 2019-09-16 15:42
cover: //cdn.wallleap.cn/img/pic/cover/202302nAUrrn.jpg
category: 技术杂谈
tags:
  - 网络
  - 华三
description: HCL 配置之 DHCP
---

使用 DHCP 自动分配 IP 地址

## 一、任务

> 在实验二的基础上(VLAN10、20、30、40内的主机之间互ping成功)实现用DHCP给各vlan内主机自动分配地址

## 二、配置

由于在上一个实验的基础上，因此只需要配置四个PC和最上面的交换机S0即可

![](https://cdn.wallleap.cn/img/pic/web-HCL3/pic1.png)

### 1、四个PC

使用DHCP，启用接口

![](https://cdn.wallleap.cn/img/pic/web-HCL3/pic2.png)

### 2、最上面的交换机S0

> 配置DHCP

```sh
<LwS0>sys
System View: return to User View with Ctrl+Z.
[LwS0]dhcp enable
[LwS0]dhcp server ip-pool vlan10
[LwS0-dhcp-pool-vlan10]network 192.168.10.1 mask 255.255.255.0
[LwS0-dhcp-pool-vlan10]gateway-list 192.168.10.1
[LwS0-dhcp-pool-vlan10]qui
[LwS0]dhcp server ip-pool vlan20
[LwS0-dhcp-pool-vlan20]network 192.168.20.1 mask 255.255.255.0
[LwS0-dhcp-pool-vlan20]gateway-list 192.168.20.1
[LwS0-dhcp-pool-vlan20]quit
[LwS0]dhcp server ip-pool vlan30
[LwS0-dhcp-pool-vlan30]network 192.168.30.1 mask 255.255.255.0
[LwS0-dhcp-pool-vlan30]gateway-list 192.168.30.1
[LwS0-dhcp-pool-vlan30]quit
[LwS0]dhcp server ip-pool vlan40
[LwS0-dhcp-pool-vlan40]network 192.168.40.1 mask 255.255.255.0
[LwS0-dhcp-pool-vlan40]gateway-list 192.168.40.1
[LwS0-dhcp-pool-vlan40]quit
```

> 保存配置

```sh
[LwS0]quit
<LwS0>save
The current configuration will be written to the device. Are you sure? [Y/N]:y
Please input the file name(*.cfg)[flash:/startup.cfg]
(To leave the existing filename unchanged, press the enter key):
flash:/startup.cfg exists, overwrite? [Y/N]:y
Validating file. Please wait...
Saved the current configuration to mainboard device successfully.
```

## 三、测试

查看各个PC的ip

然后ping另一台PC，能ping通即可
