---
title: HCL 配置之 DHCP 中继
date:  2019-09-16 16:14
updated:  2019-09-16 16:14
cover: //cdn.wallleap.cn/img/pic/cover/202302nAUrrn.jpg
category: 技术杂谈
tags:
  - 网络
  - 华三
description: HCL 配置之 DHCP 中继
---

实验目的：DHCP中继

> 配置：

拓扑如下：

![](https://cdn.wallleap.cn/img/pic/web-HCL4/pic1.png)

## 一、四个PC

打开DHCP，启用接口

![](https://cdn.wallleap.cn/img/pic/web-HCL4/pic2.png)

## 二、交换机S1

```sh
<H3C>sys
System View: return to User View with Ctrl+Z.
[H3C]sys S1
[S1]vlan 10
[S1-vlan10]vlan 20
[S1-vlan20]quit
[S1]int g1/0/1
[S1-GigabitEthernet1/0/1]no sh
[S1-GigabitEthernet1/0/1]port link-type access
[S1-GigabitEthernet1/0/1]port access vlan 10
[S1-GigabitEthernet1/0/1]quit
[S1]int g1/0/2
[S1-GigabitEthernet1/0/2]no sh
[S1-GigabitEthernet1/0/2]port link-t a
[S1-GigabitEthernet1/0/2]port a vlan 20
[S1-GigabitEthernet1/0/2]quit
[S1]int g1/0/3
[S1-GigabitEthernet1/0/3]no sh
[S1-GigabitEthernet1/0/3]port link-t t
[S1-GigabitEthernet1/0/3]port t p vlan all
[S1-GigabitEthernet1/0/3]quit
[S1]save
The current configuration will be written to the device. Are you sure? [Y/N]:y
Please input the file name(*.cfg)[flash:/startup.cfg]
(To leave the existing filename unchanged, press the enter key):
Validating file. Please wait...
Saved the current configuration to mainboard device successfully.
```

## 三、交换机S2

```sh
[S2]vlan 30
[S2-vlan30]vlan 40
[S2-vlan40]int g1/0/1
[S2-GigabitEthernet1/0/1]no sh
[S2-GigabitEthernet1/0/1]port link-t a
[S2-GigabitEthernet1/0/1]port a vlan 30
[S2-GigabitEthernet1/0/1]int g1/0/2
[S2-GigabitEthernet1/0/2]no sh
[S2-GigabitEthernet1/0/2]port link-t a
[S2-GigabitEthernet1/0/2]port a vlan 40
[S2-GigabitEthernet1/0/2]int g1/0/3
[S2-GigabitEthernet1/0/3]no sh
[S2-GigabitEthernet1/0/3]port link-t t
[S2-GigabitEthernet1/0/3]port t p vlan all
[S2-GigabitEthernet1/0/3]quit
[S2]save
The current configuration will be written to the device. Are you sure? [Y/N]:y
Please input the file name(*.cfg)[flash:/startup.cfg]
(To leave the existing filename unchanged, press the enter key):
Validating file. Please wait...
Saved the current configuration to mainboard device successfully.
```

## 四、交换机S3

```sh
[S0]vlan 10
[S0-vlan10]vlan 20
[S0-vlan20]vlan 30
[S0-vlan30]vlan 40
[S0-vlan40]vlan 50
[S0-vlan50]quit
[S0]int g1/0/1
[S0-GigabitEthernet1/0/1]no sh
[S0-GigabitEthernet1/0/1]port link-t t
[S0-GigabitEthernet1/0/1]port t p vlan all
[S0-GigabitEthernet1/0/1]int g1/0/2
[S0-GigabitEthernet1/0/2]no sh
[S0-GigabitEthernet1/0/2]port link-t t
[S0-GigabitEthernet1/0/2]port t p vlan all
[S0-GigabitEthernet1/0/2]int g1/0/3
[S0-GigabitEthernet1/0/3]no sh
[S0-GigabitEthernet1/0/3]port link-t a
[S0-GigabitEthernet1/0/3]port a vlan 50
[S0-GigabitEthernet1/0/3]quit
[S0]dhcp enable
[S0]int vlan 10
[S0-Vlan-interface10]%Sep 16 18:50:17:155 2019 S0 IFNET/3/PHY_UPDOWN: Physical state on the interface Vlan-interface10 changed to up.
%Sep 16 18:50:17:155 2019 S0 IFNET/5/LINK_UPDOWN: Line protocol state on the interface Vlan-interface10 changed to up.
ip add 192.168.10.1 255.255.255.0
[S0-Vlan-interface10]dhcp select relay
[S0-Vlan-interface10]dhcp relay server-address 192.168.50.2
[S0-Vlan-interface10]int vlan 20
[S0-Vlan-interface20]%Sep 16 18:52:05:444 2019 S0 IFNET/3/PHY_UPDOWN: Physical state on the interface Vlan-interface20 changed to up.
%Sep 16 18:52:05:444 2019 S0 IFNET/5/LINK_UPDOWN: Line protocol state on the interface Vlan-interface20 changed to up.
ip add 192.168.20.1 255.255.255.0
[S0-Vlan-interface20]dhcp select relay
[S0-Vlan-interface20]dhcp relay server-address 192.168.50.2
[S0-Vlan-interface20]int vlan 30
[S0-Vlan-interface30]%Sep 16 18:52:26:073 2019 S0 IFNET/3/PHY_UPDOWN: Physical state on the interface Vlan-interface30 changed to up.
%Sep 16 18:52:26:073 2019 S0 IFNET/5/LINK_UPDOWN: Line protocol state on the interface Vlan-interface30 changed to up.
ip add 192.168.30.1 255.255.255.0
[S0-Vlan-interface30]dhcp select relay
[S0-Vlan-interface30]dhcp relay server-address 192.168.50.2
[S0-Vlan-interface30]int vlan 40
[S0-Vlan-interface40]%Sep 16 18:52:47:327 2019 S0 IFNET/3/PHY_UPDOWN: Physical state on the interface Vlan-interface40 changed to up.
%Sep 16 18:52:47:327 2019 S0 IFNET/5/LINK_UPDOWN: Line protocol state on the interface Vlan-interface40 changed to up.
ip add 192.168.40.1 255.255.255.0
[S0-Vlan-interface40]dhcp select relay
[S0-Vlan-interface40]dhcp relay server-address 192.168.50.2
[S0-Vlan-interface40]int vlan 50
[S0-Vlan-interface50]%Sep 16 18:53:08:122 2019 S0 IFNET/3/PHY_UPDOWN: Physical state on the interface Vlan-interface50 changed to up.
%Sep 16 18:53:08:122 2019 S0 IFNET/5/LINK_UPDOWN: Line protocol state on the interface Vlan-interface50 changed to up.
ip add 192.168.50.1 255.255.255.0
[S0-Vlan-interface50]quit
[S0]save
The current configuration will be written to the device. Are you sure? [Y/N]:y
Please input the file name(*.cfg)[flash:/startup.cfg]
(To leave the existing filename unchanged, press the enter key):
Validating file. Please wait...
Saved the current configuration to mainboard device successfully.
```

## 五、路由器R

```sh
[R]int g0/0
[R-GigabitEthernet0/0]no sh
[R-GigabitEthernet0/0]ip add 192.168.50.2 255.255.255.0
[R-GigabitEthernet0/0]quit
[R]dhcp en
[R]dhcp server ip-pool vlan10
[R-dhcp-pool-vlan10]network 192.168.10.1 mask 255.255.255.0
[R-dhcp-pool-vlan10]gateway-list 192.168.10.1
[R-dhcp-pool-vlan10]quit
[R]dhcp server ip-pool vlan20
[R-dhcp-pool-vlan20]network 192.168.20.1 mask 255.255.255.0
[R-dhcp-pool-vlan20]gateway-list 192.168.20.1
[R-dhcp-pool-vlan20]quit
[R]dhcp server ip-pool vlan30
[R-dhcp-pool-vlan30]network 192.168.30.1 mask 255.255.255.0
[R-dhcp-pool-vlan30]gateway-list 192.168.30.1
[R-dhcp-pool-vlan30]quit
[R]dhcp server ip-pool vlan40
[R-dhcp-pool-vlan40]network 192.168.40.1 mask 255.255.255.0
[R-dhcp-pool-vlan40]gateway-list 192.168.40.1
[R-dhcp-pool-vlan40]quit
[R]ip route-static 192.168.0.0 255.255.0.0 g0/0 192.168.50.1
[R]save
The current configuration will be written to the device. Are you sure? [Y/N]:y
Please input the file name(*.cfg)[flash:/startup.cfg]
(To leave the existing filename unchanged, press the enter key):
Validating file. Please wait...
Configuration is saved to device successfully.
```

> 测试

![](https://cdn.wallleap.cn/img/pic/web-HCL4/pic3.png)

![](https://cdn.wallleap.cn/img/pic/web-HCL4/pic4.png)
