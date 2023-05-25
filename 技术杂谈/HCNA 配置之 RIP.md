---
title: HCNA 配置之 RIP
date: 2019-09-19 16:13
updated: 2019-09-19 16:13
cover: //cdn.wallleap.cn/img/pic/cover/202302QIAwJ8.jpg
category: 技术杂谈
tags:
  - 网络
  - HCNA
description: HCNA 配置之 RIP
---

学习路由协议 RIP

## 一、实验目的

配置RIP

说明：
1.交换机和三层交换机配置RIP
2.左边静态地址、右边DHCP
3.左边除了DHCP，昨天的都配上

## 二、配置

### １、拓扑

![](https://cdn.wallleap.cn/img/pic/web-HCL6/pic1.png)

IP规划：

```sh
VLAN10:192.168.10.253(S1) 192.168.10.254(S2) 192.168.10.1(虚拟IP)
VLAN20:192.168.20.253(S1) 192.168.10.254(S2) 192.168.20.1(虚拟IP)
VLAN30:192.168.30.253(S1) 192.168.10.254(S2) 192.168.30.1(虚拟IP)
VLAN40:192.168.40.253(S1) 192.168.10.254(S2) 192.168.40.1(虚拟IP)

VLAN50:192.168.50.1(S3)
VLAN60:192.168.60.1(S3) 

VLAN70:192.168.70.253(S1)-R1:192.168.70.50

VLAN80:192.168.80.254(S2)-R1:192.168.80.50

VLAN90:192.168.90.1(S3)-R3:192.168.90.50

R1:192.168.100.50-R2:192.168.100.51

R2:192.168.110.51-R3:192.168.110.50
```

### ２、左边PC

静态IP，手动配置

![](https://cdn.wallleap.cn/img/pic/web-HCL6/pic2.png)

### ３、右边PC

DHCP，动态获取IP地址

![](https://cdn.wallleap.cn/img/pic/web-HCL6/pic3.png)

### ４、S４

只需要配置接口、vlan即可，S５也是

> 命名

```sh
<Huawei>sys 
Enter system view, return user view with Ctrl+Z.
[Huawei]sys LWS4
```

> 删除提示信息

```sh
[LWS4]un in en
Info: Information center is disabled.
```

> 创建VLAN

```sh
[LWS4]vlan 10
[LWS4-vlan10]vlan 20
[LWS4-vlan20]quit
```

> 接口配置

```sh
[LWS4]int e0/0/3
[LWS4-Ethernet0/0/3]un sh
Info: Interface Ethernet0/0/3 is not shutdown.
[LWS4-Ethernet0/0/3]port link-t a
[LWS4-Ethernet0/0/3]port de vlan 10
[LWS4-Ethernet0/0/3]int e0/0/4
[LWS4-Ethernet0/0/4]un sh
Info: Interface Ethernet0/0/4 is not shutdown.
[LWS4-Ethernet0/0/4]port link-t a
[LWS4-Ethernet0/0/4]port de vlan 10
[LWS4-Ethernet0/0/4]int e0/0/1
[LWS4-Ethernet0/0/1]un sh
Info: Interface Ethernet0/0/1 is not shutdown.
[LWS4-Ethernet0/0/1]port link-t t
[LWS4-Ethernet0/0/1]port t allow vlan all
[LWS4-Ethernet0/0/1]int e0/0/2
[LWS4-Ethernet0/0/2]un sh
Info: Interface Ethernet0/0/2 is not shutdown.
[LWS4-Ethernet0/0/2]port link-t t
[LWS4-Ethernet0/0/2]port t allow vlan all
[LWS4-Ethernet0/0/2]quit
[LWS4]stp mode stp
Info: This operation may take a few seconds. Please wait for a moment...done.
```

> 保存配置

```sh
[LWS4]quit
<LWS4>save
The current configuration will be written to the device.
Are you sure to continue?[Y/N]y
Info: Please input the file name ( *.cfg, *.zip ) [vrpcfg.zip]:
Now saving the current configuration to the slot 0.
Save the configuration successfully.
```

### ５、S５

```sh
<Huawei>sys
Enter system view, return user view with Ctrl+Z.
[Huawei]sys LWS5
[LWS5]un in en
Info: Information center is disabled.
[LWS5]vlan 30
[LWS5-vlan30]vlan 40
[LWS5-vlan40]quit
[LWS5]int e0/0/3
[LWS5-Ethernet0/0/3]un sh
Info: Interface Ethernet0/0/3 is not shutdown.
[LWS5-Ethernet0/0/3]port link-t a
[LWS5-Ethernet0/0/3]port de vlan 30
[LWS5-Ethernet0/0/3]int e0/0/4
[LWS5-Ethernet0/0/4]un sh
Info: Interface Ethernet0/0/4 is not shutdown.
[LWS5-Ethernet0/0/4]port link-t a
[LWS5-Ethernet0/0/4]port de vlan 40
[LWS5-Ethernet0/0/4]int e0/0/1
[LWS5-Ethernet0/0/1]un sh
Info: Interface Ethernet0/0/1 is not shutdown.
[LWS5-Ethernet0/0/1]port link-t t
[LWS5-Ethernet0/0/1]port t allow vlan all
[LWS5-Ethernet0/0/1]int e0/0/2
[LWS5-Ethernet0/0/2]un sh
Info: Interface Ethernet0/0/2 is not shutdown.
[LWS5-Ethernet0/0/2]port link-t t
[LWS5-Ethernet0/0/2]port t allow vlan all
[LWS5-Ethernet0/0/2]quit
[LWS5]stp mode stp
Info: This operation may take a few seconds. Please wait for a moment...done.
```

### ６、S６

```sh
<Huawei>sys
Enter system view, return user view with Ctrl+Z.
[Huawei]un in en
Info: Information center is disabled.
[Huawei]sys LWS6
[LWS6]vlan 50
[LWS6-vlan50]vlan 60
[LWS6-vlan60]quit
[LWS6]int e0/0/2
[LWS6-Ethernet0/0/2]un sh
Info: Interface Ethernet0/0/2 is not shutdown.
[LWS6-Ethernet0/0/2]port link-t a
[LWS6-Ethernet0/0/2]port de vlan 50
[LWS6-Ethernet0/0/2]int e0/0/3
[LWS6-Ethernet0/0/3]un sh
Info: Interface Ethernet0/0/3 is not shutdown.
[LWS6-Ethernet0/0/3]port link-t a
[LWS6-Ethernet0/0/3]port de vlan 60
[LWS6-Ethernet0/0/3]int e0/0/1
[LWS6-Ethernet0/0/1]un sh
Info: Interface Ethernet0/0/1 is not shutdown.
[LWS6-Ethernet0/0/1]port link-t t
[LWS6-Ethernet0/0/1]port t allow vlan all
[LWS6-Ethernet0/0/1]quit
```

### ７、S１

```sh
<Huawei>sys
Enter system view, return user view with Ctrl+Z.
[Huawei]un in en
Info: Information center is disabled.
[Huawei]sys LWS1

[LWS1]vlan 10
[LWS1-vlan10]vlan 20
[LWS1-vlan20]vlan 30
[LWS1-vlan30]vlan 40
[LWS1-vlan40]quit


[LWS1]vlan 70
[LWS1-vlan70]quit
[LWS1]int g0/0/1
[LWS1-GigabitEthernet0/0/1]un sh
Info: Interface GigabitEthernet0/0/1 is not shutdown.
[LWS1-GigabitEthernet0/0/1]port link-t a
[LWS1-GigabitEthernet0/0/1]port de vlan 70
[LWS1-GigabitEthernet0/0/1]int vlan 70
[LWS1-Vlanif70]ip add 192.168.70.253 24
[LWS1-Vlanif70]quit


[LWS1]int g0/0/2
[LWS1-GigabitEthernet0/0/2]un sh
Info: Interface GigabitEthernet0/0/2 is not shutdown.
[LWS1-GigabitEthernet0/0/2]port link-t t
[LWS1-GigabitEthernet0/0/2]port t allow vlan all
[LWS1-GigabitEthernet0/0/2]int g0/0/3
[LWS1-GigabitEthernet0/0/3]un sh
Info: Interface GigabitEthernet0/0/3 is not shutdown.
[LWS1-GigabitEthernet0/0/3]port link-t t
[LWS1-GigabitEthernet0/0/3]port t allow vlan all
[LWS1-GigabitEthernet0/0/3]int g0/0/4
[LWS1-GigabitEthernet0/0/4]un sh
Info: Interface GigabitEthernet0/0/4 is not shutdown.
[LWS1-GigabitEthernet0/0/4]port link-t t
[LWS1-GigabitEthernet0/0/4]port t allow vlan all
[LWS1-GigabitEthernet0/0/4]quit
```

> stp

```sh
[LWS1]stp mode stp
Info: This operation may take a few seconds. Please wait for a moment...done.
[LWS1]stp prio 0
```

> VLAN的IP及VRRP

```sh
[LWS1]int vlan 10
[LWS1-Vlanif10]ip add 192.168.10.253 255.255.255.0
[LWS1-Vlanif10]vrrp vrid 10 virtual-ip 192.168.10.1
[LWS1-Vlanif10]vrrp vrid 10 prio 120
[LWS1-Vlanif10]int vlan 20
[LWS1-Vlanif20]ip add 192.168.20.253 255.255.255.0
[LWS1-Vlanif20]vrrp vrid 20 vi 192.168.20.1
[LWS1-Vlanif20]vrrp vrid 20 prio 120
[LWS1-Vlanif20]int vlan 30
[LWS1-Vlanif30]ip add 192.168.30.253 255.255.255.0
[LWS1-Vlanif30]vrrp vrid 30 vi 192.168.30.1
[LWS1-Vlanif30]int vlan 40
[LWS1-Vlanif40]ip add 192.168.40.253 255.255.255.0
[LWS1-Vlanif40]vrrp vrid 40 vi 192.168.40.1
[LWS1-Vlanif40]quit
```

> S1是VLAN10和VLAN20主R，设置接口监听，与路由器连接的接口有问题，则优先级降30，让S2为主R

```sh
[LWS1]int vlan 10
[LWS1-Vlanif10]vrrp vrid 10 track int g0/0/1 reduce 30
[LWS1-Vlanif10]int vlan 20
[LWS1-Vlanif20]vrrp vrid 20 track int g0/0/1 reduce 30
[LWS1-Vlanif20]quit
```

> RIP,可以先用`dis ip int brief`查看所有IP，然后添加

```sh
[LWS1]rip 1
[LWS1-rip-1]network 192.168.10.0
[LWS1-rip-1]network 192.168.20.0
[LWS1-rip-1]network 192.168.30.0
[LWS1-rip-1]network 192.168.40.0
[LWS1-rip-1]network 192.168.70.0
[LWS1-rip-1]quit
[LWS1]quit
```

### ８、S２

```sh
<Huawei>sys
Enter system view, return user view with Ctrl+Z.
[Huawei]un in en
Info: Information center is disabled.
[Huawei]sys LWS2
[LWS2]int g0/0/2
[LWS2-GigabitEthernet0/0/2]un sh
Info: Interface GigabitEthernet0/0/2 is not shutdown.
[LWS2-GigabitEthernet0/0/2]port link-t t
[LWS2-GigabitEthernet0/0/2]port t allow vlan all
[LWS2-GigabitEthernet0/0/2]int g0/0/3
[LWS2-GigabitEthernet0/0/3]un sh
Info: Interface GigabitEthernet0/0/3 is not shutdown.
[LWS2-GigabitEthernet0/0/3]port link-t t
[LWS2-GigabitEthernet0/0/3]port t allow vlan all
[LWS2-GigabitEthernet0/0/3]int g0/0/4
[LWS2-GigabitEthernet0/0/4]un sh
Info: Interface GigabitEthernet0/0/4 is not shutdown.
[LWS2-GigabitEthernet0/0/4]port link-t t
[LWS2-GigabitEthernet0/0/4]port t allow vlan all
[LWS2-GigabitEthernet0/0/4]quit

[LWS2]vlan 10
[LWS2-vlan10]vlan 20
[LWS2-vlan20]vlan 30
[LWS2-vlan30]vlan 40
[LWS2-vlan40]quit

[LWS2]vlan 80
[LWS2-vlan80]quit
[LWS2]int g0/0/1
[LWS2-GigabitEthernet0/0/1]un sh
Info: Interface GigabitEthernet0/0/1 is not shutdown.
[LWS2-GigabitEthernet0/0/1]port link-t a
[LWS2-GigabitEthernet0/0/1]port de vlan 80
[LWS2-GigabitEthernet0/0/1]quit
[LWS2]int vlan 80
[LWS2-Vlanif80]ip add 192.168.80.254 24
[LWS2-Vlanif80]quit

[LWS2]int vlan 10
[LWS2-Vlanif10]ip add 192.168.10.254 255.255.255.0
[LWS2-Vlanif10]vrrp vrid 10 vi 192.168.10.1
[LWS2-Vlanif10]int vlan 20
[LWS2-Vlanif20]ip add 192.168.20.254 255.255.255.0
[LWS2-Vlanif20]vrrp vrid 20 vi 192.168.20.1
[LWS2-Vlanif20]int vlan 30
[LWS2-Vlanif30]ip add 192.168.30.254 255.255.255.0
[LWS2-Vlanif30]vrrp vrid 30 vi 192.168.30.1
[LWS2-Vlanif30]vrrp vrid 30 prio 120
[LWS2-Vlanif30]int vlan 40
[LWS2-Vlanif40]ip add 192.168.40.254 24
[LWS2-Vlanif40]vrrp vrid 40 vi 192.168.40.1
[LWS2-Vlanif40]vrrp vrid 40 prio 120
[LWS2-Vlanif40]quit
[LWS2]stp mode stp
Info: This operation may take a few seconds. Please wait for a moment...done.
[LWS2]stp prio 4096


[LWS2]rip 1
[LWS2-rip-1]net 192.168.10.0
[LWS2-rip-1]net 192.168.20.0
[LWS2-rip-1]net 192.168.30.0
[LWS2-rip-1]net 192.168.40.0
[LWS2-rip-1]net 192.168.80.0
[LWS2-rip-1]quit
```

### ９、S３

```sh
<Huawei>sys 
Enter system view, return user view with Ctrl+Z.
[Huawei]un in en
Info: Information center is disabled.
[Huawei]sys LWS3
[LWS3]vlan 50
[LWS3-vlan50]vlan 60
[LWS3-vlan60]vlan 90
[LWS3-vlan90]quit
[LWS3]int g0/0/2
[LWS3-GigabitEthernet0/0/2]un sh
Info: Interface GigabitEthernet0/0/2 is not shutdown.
[LWS3-GigabitEthernet0/0/2]port link-t t
[LWS3-GigabitEthernet0/0/2]port t allow vlan all
[LWS3-GigabitEthernet0/0/2]int g0/0/1
[LWS3-GigabitEthernet0/0/1]un sh
Info: Interface GigabitEthernet0/0/1 is not shutdown.
[LWS3-GigabitEthernet0/0/1]port link-t a
[LWS3-GigabitEthernet0/0/1]port de vlan 90
[LWS3-GigabitEthernet0/0/1]quit
[LWS3]int vlan 50
[LWS3-Vlanif50]ip add 192.168.50.1 24
[LWS3-Vlanif50]int vlan 60
[LWS3-Vlanif60]ip add 192.168.60.1 24
[LWS3-Vlanif60]int vlan 90
[LWS3-Vlanif90]ip add 192.168.90.1 24
[LWS3-Vlanif90]quit

[LWS3]dhcp en
[LWS3]ip pool vlan50
Info:It's successful to create an IP address pool.
[LWS3-ip-pool-vlan50]gateway-list 192.168.50.1
[LWS3-ip-pool-vlan50]net 192.168.50.0 mask 255.255.255.0
[LWS3-ip-pool-vlan50]quit
[LWS3]ip pool vlan60
Info:It's successful to create an IP address pool.
[LWS3-ip-pool-vlan60]gateway-list 192.168.60.1
[LWS3-ip-pool-vlan60]net 192.168.60.0 mask 255.255.255.0
[LWS3-ip-pool-vlan60]quit
[LWS3]int vlan 10
[LWS3-VLANIF10]dhcp select global

[LWS3]rip 1
[LWS3-rip-1]net 192.168.50.0
[LWS3-rip-1]net 192.168.60.0
[LWS3-rip-1]net 192.168.90.0
[LWS3-rip-1]quit
```

### １０、Ｒ１

```sh
<Huawei>sys
Enter system view, return user view with Ctrl+Z.
[Huawei]un in en
Info: Information center is disabled.
[Huawei]sys LWR1
[LWR1]int e0/0/0
[LWR1-Ethernet0/0/0]ip add 192.168.70.50 24
[LWR1-Ethernet0/0/0]int e0/0/1
[LWR1-Ethernet0/0/1]ip add 192.168.80.50 24
[LWR1-Ethernet0/0/1]int g0/0/0
[LWR1-GigabitEthernet0/0/0]ip add 192.168.100.50 24
[LWR1-GigabitEthernet0/0/0]quit

[LWR1]rip 1
[LWR1-rip-1]net 192.168.70.0
[LWR1-rip-1]net 192.168.80.0
[LWR1-rip-1]net 192.168.100.0
[LWR1-rip-1]quit
```

### １１、Ｒ２

```sh
<Huawei>sys
Enter system view, return user view with Ctrl+Z.
[Huawei]un in en
Info: Information center is disabled.
[Huawei]int e0/0/0
[Huawei-Ethernet0/0/0]ip add 192.168.100.51 24
[Huawei-Ethernet0/0/0]int e0/0/1
[Huawei-Ethernet0/0/1]ip add 192.168.110.51 24
[Huawei-Ethernet0/0/1]quit

[Huawei]rip 1
[Huawei-rip-1]net 192.168.100.0
[Huawei-rip-1]net 192.168.110.0
[Huawei-rip-1]quit
```

### １２、Ｒ３

```sh
<Huawei>sys
Enter system view, return user view with Ctrl+Z.
[Huawei]un in en
Info: Information center is disabled.
[Huawei]sys LWR3
[LWR3]int e0/0/0
[LWR3-Ethernet0/0/0]ip add 192.168.110.50 24
[LWR3-Ethernet0/0/0]int e0/0/1
[LWR3-Ethernet0/0/1]ip add 192.168.90.50 24
[LWR3-Ethernet0/0/1]quit

[LWR3]rip 1
[LWR3-rip-1]net 192.168.90.0
[LWR3-rip-1]net 192.168.110.0
[LWR3-rip-1]quit
```

## 三、测试

> PC互ping

![](https://cdn.wallleap.cn/img/pic/web-HCL6/pic4.png)

> S4或S5

```sh
dis stp brief
```

![](https://cdn.wallleap.cn/img/pic/web-HCL6/pic5.png)

> S1或S2

```sh
dis vrrp brief
```

接着`shutdown`S1的上层端口

![](https://cdn.wallleap.cn/img/pic/web-HCL6/pic6.png)

Master变为backup
