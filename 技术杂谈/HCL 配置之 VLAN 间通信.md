---
title: HCL 配置之 VLAN 间通信
date: 2019-09-15 18:06
updated: 2019-09-15 18:06
cover: //cdn.wallleap.cn/img/pic/cover/202302nAUrrn.jpg
category: 技术杂谈
tags:
  - 网络
  - 华三
description: HCL 配置之 VLAN 间通信
---

任务——Vlan 间通信：VLAN10、20、30、40 内的主机之间互 ping 成功

## 二、配置

## (一)通过三层交换机使用 SVI 实现通信

拓扑图如下：

![拓扑](https://cdn.wallleap.cn/img/pic/web-HCL2/pic1.png)

主机 IP：

- PC1： `192.168.10.100/24`
- PC2： `192.168.20.100/24`
- PC3： `192.168.30.100/24`
- PC4： `192.168.40.100/24`

VLANIP 规划：

- VLAN10： `192.168.10.1/24`
- VLAN20： `192.168.20.1/24`
- VLAN30： `192.168.30.1/24`
- VLAN40： `192.168.40.1/24`

### 1、配置 PC

配置好 IP 地址，掩码，网关（网关是 VLAN 的 IP）

### 2、最上面的交换机S0

> 命名

```sh
<H3C>sys
System View: return to User View with Ctrl+Z.
[H3C]sys LWS0
```

> 创建四个 vlan

```sh
[LWS0]vlan 10
[LWS0-vlan10]quit
[LWS0]vlan 20
[LWS0-vlan20]vlan 30
[LWS0-vlan30]vlan 40
[LWS0-vlan40]quit
```

> 给 vlan 分配 IP

```sh
[LWS0]int vlan 10
[LWS0-Vlan-interface10]ip add 192.168.10.1 255.255.255.0
[LWS0-Vlan-interface10]quit
[LWS0]int vlan 20
[LWS0-Vlan-interface20]ip add 192.168.20.1 255.255.255.0
[LWS0-Vlan-interface20]int vlan 30
[LWS0-Vlan-interface30]ip add 192.168.30.1 255.255.255.0
[LWS0-Vlan-interface30]int vlan 40
[LWS0-Vlan-interface40]ip add 192.168.40.1 255.255.255.0
[LWS0-Vlan-interface40]quit
```

> 接口设为trunk并允许所有vlan通过

```sh
[LWS0]int g1/0/1
[LWS0-GigabitEthernet1/0/1]port link-type trunk
[LWS0-GigabitEthernet1/0/1]port trunk permit vlan all
[LWS0-GigabitEthernet1/0/1]no sh
[LWS0-GigabitEthernet1/0/1]int g1/0/2
[LWS0-GigabitEthernet1/0/2]no sh
[LWS0-GigabitEthernet1/0/2]port link-ty t
[LWS0-GigabitEthernet1/0/2]port t p vlan all
```

### 3、左边交换机S1

> 命名

```sh
<H3C>sys
System View: return to User View with Ctrl+Z.
[H3C]sys LWS1
创建vlan
[LWS1]vlan 10
[LWS1-vlan10]vlan 20
[LWS1-vlan20]quit
```

> 与交换机相连的接口设为 trunk，允许所有 vlan 通过

```sh
[LWS1-GigabitEthernet1/0/1]no sh
[LWS1-GigabitEthernet1/0/1]port link-ty t
[LWS1-GigabitEthernet1/0/1]port t p vlan all
[LWS1-GigabitEthernet1/0/1]quit
```

>下面两个接口设为 access

```sh
[LWS1]int g1/0/2
[LWS1-GigabitEthernet1/0/2]port link-ty a
[LWS1-GigabitEthernet1/0/2]port a vlan 10
[LWS1-GigabitEthernet1/0/2]int g1/0/3
[LWS1-GigabitEthernet1/0/3]no sh
[LWS1-GigabitEthernet1/0/3]port link-ty a
[LWS1-GigabitEthernet1/0/3]port a vlan 20
[LWS1-GigabitEthernet1/0/3]quit
```

### 4、右边交换机S2

```sh
[LWS2]vlan 30
[LWS2-vlan30]vlan 40
[LWS2-vlan40]quit
[LWS2]int g1/0/1
[LWS2-GigabitEthernet1/0/1]port link-ty t
[LWS2-GigabitEthernet1/0/1]port t p vlan all
[LWS2-GigabitEthernet1/0/1]quit
[LWS2]int g1/0/2
[LWS2-GigabitEthernet1/0/2]port link-ty a
[LWS2-GigabitEthernet1/0/2]port a vlan 30
[LWS2-GigabitEthernet1/0/2]int g1/0/3
[LWS2-GigabitEthernet1/0/3]port link-ty a
[LWS2-GigabitEthernet1/0/3]port a vlan 40
[LWS2-GigabitEthernet1/0/3]quit
```

### 5、测试

![](https://cdn.wallleap.cn/img/pic/web-HCL2/pic2.png)

## (二)其他方法

其他的网上有详细的配置，因此只给出方法

1、如果只有两个 VLAN，那么可以在交换机端口设置 trunk 的本征 VLAN，自行去标签

多个 VLAN 的话设成 Hybrid 口，用 untag 撕去标签

2、通过路由接口

3、通过单臂路由
