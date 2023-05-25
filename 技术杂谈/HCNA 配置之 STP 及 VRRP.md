---
title: HCNA 配置之 STP 及 VRRP
date: 2019-09-18 16:13
updated: 2019-09-18 16:13
cover: //cdn.wallleap.cn/img/pic/cover/202302QIAwJ8.jpg
category: 技术杂谈
tags:
  - 网络
  - HCNA
description: HCNA 配置之 STP 及 VRRP
---

生成树协议和网关单点故障解决

## 一、实验目的

1、VRRP
2、STP
3、能用 DHCP 自动获取 IP
4、能相互 ping 通

## 二、配置

> 拓扑如下

![](https://cdn.wallleap.cn/img/pic/web-HCL5/pic1.png)

### 四个PC

![](https://cdn.wallleap.cn/img/pic/web-HCL5/pic2.png)

### S3：

```sh
<Huawei>sys 
Enter system view, return user view with Ctrl+Z.
[Huawei]sys LWS3
```

> 去除提示信息

```sh
[LWS3]undo info-center enable 
Info: Information center is disabled.
```

> 创建VLAN

```sh
[LWS3]vlan 10
[LWS3-vlan10]vlan 20
[LWS3-vlan20]quit
```

> 接口配置

```sh
[LWS3]int e0/0/3
[LWS3-Ethernet0/0/3]un sh
Info: Interface Ethernet0/0/3 is not shutdown.
[LWS3-Ethernet0/0/3]port link-type access
[LWS3-Ethernet0/0/3]port default vlan 10
[LWS3-Ethernet0/0/3]quit
[LWS3]int e0/0/4
[LWS3-Ethernet0/0/4]un sh
Info: Interface Ethernet0/0/4 is not shutdown.
[LWS3-Ethernet0/0/4]port link-ty a
[LWS3-Ethernet0/0/4]port de vlan 20
[LWS3-Ethernet0/0/4]quit
[LWS3]int e0/0/1
[LWS3-Ethernet0/0/1]un sh
Info: Interface Ethernet0/0/1 is not shutdown.
[LWS3-Ethernet0/0/1]port link-ty t
[LWS3-Ethernet0/0/1]port t allow-pass vlan all
[LWS3-Ethernet0/0/1]quit
[LWS3]int e0/0/2
[LWS3-Ethernet0/0/2]un sh
Info: Interface Ethernet0/0/2 is not shutdown.
[LWS3-Ethernet0/0/2]port link-ty t
[LWS3-Ethernet0/0/2]port t allow vlan all
[LWS3-Ethernet0/0/2]quit
```

> 开启stp

```sh
[LWS3]stp mode stp
Info: This operation may take a few seconds. Please wait for a moment...done.
```

> 保存配置

```sh
<LWS3>save
The current configuration will be written to the device.
Are you sure to continue?[Y/N]y
Now saving the current configuration to the slot 0.
Save the configuration successfully.
```

### S4：

```sh
<Huawei>sys
Enter system view, return user view with Ctrl+Z.
[Huawei]sys LWS4
[LWS4]un in en
Info: Information center is disabled.
[LWS4]vlan 30
[LWS4-vlan30]vlan 40
[LWS4-vlan40]quit
[LWS4-Ethernet0/0/3]un sh
Info: Interface Ethernet0/0/3 is not shutdown.
[LWS4-Ethernet0/0/3]port link-t a
[LWS4-Ethernet0/0/3]port de vlan 30
[LWS4-Ethernet0/0/3]quit
[LWS4]int e0/0/4
[LWS4-Ethernet0/0/4]un sh
Info: Interface Ethernet0/0/4 is not shutdown.
[LWS4-Ethernet0/0/4]port link-t a
[LWS4-Ethernet0/0/4]port de vlan 40
[LWS4-Ethernet0/0/4]quit
[LWS4]int e0/0/1
[LWS4-Ethernet0/0/1]un sh
Info: Interface Ethernet0/0/1 is not shutdown.
[LWS4-Ethernet0/0/1]port link-t t
[LWS4-Ethernet0/0/1]port t allow vlan all
[LWS4-Ethernet0/0/1]quit
[LWS4]int e0/0/2
[LWS4-Ethernet0/0/2]un sh
Info: Interface Ethernet0/0/2 is not shutdown.
[LWS4-Ethernet0/0/2]port link-t t
[LWS4-Ethernet0/0/2]port t allow vlan all
[LWS4-Ethernet0/0/2]quit
[LWS4]stp mode stp
Info: This operation may take a few seconds. Please wait for a moment...done.
```

### S1：

```sh
<Huawei>sys
Enter system view, return user view with Ctrl+Z.
[Huawei]sys LWS1
```

> 去除提示信息

```sh
[LWS1]un in en
Info: Information center is disabled.
```

> 创建vlan

```sh
[LWS1]vlan 10
[LWS1-vlan10]vlan 20
[LWS1-vlan20]vlan 30
[LWS1-vlan30]vlan 40
```

> 设置接口

```sh
[LWS1]int g0/0/1
[LWS1-GigabitEthernet0/0/1]un sh
Info: Interface GigabitEthernet0/0/1 is not shutdown.
[LWS1-GigabitEthernet0/0/1]port link-t t
[LWS1-GigabitEthernet0/0/1]port t allow vlan all
[LWS1-GigabitEthernet0/0/1]quit
[LWS1]int g0/0/2
[LWS1-GigabitEthernet0/0/2]un sh
Info: Interface GigabitEthernet0/0/2 is not shutdown.
[LWS1-GigabitEthernet0/0/2]port link-t t
[LWS1-GigabitEthernet0/0/2]port t allow vlan all
[LWS1-GigabitEthernet0/0/2]quit
[LWS1]int g0/0/3
[LWS1-GigabitEthernet0/0/3]un sh
Info: Interface GigabitEthernet0/0/3 is not shutdown.
[LWS1-GigabitEthernet0/0/3]port link-t t
[LWS1-GigabitEthernet0/0/3]port t allow vlan all
[LWS1-GigabitEthernet0/0/3]quit
```

> 配置STP

```sh
[LWS1]stp mode stp
Info: This operation may take a few seconds. Please wait for a moment...done.
[LWS1]stp priority 0
```

> 配置vlan地址（网关），vrrp

```sh
[LWS1]int vlanif10
[LWS1-Vlanif10]ip add 192.168.10.1 255.255.255.0　　　
[LWS1-Vlanif10]vrrp vrid 10 virtual-ip 192.168.10.254
[LWS1-Vlanif10]vrrp vrid 10 prio 120
[LWS1-Vlanif10]int vlanif20
[LWS1-Vlanif20]ip add 192.168.20.1 255.255.255.0
[LWS1-Vlanif20]vrrp vrid 20 virtual-ip 192.168.20.254
[LWS1-Vlanif20]vrrp vrid 20 prio 120
[LWS1-Vlanif20]int vlanif30
[LWS1-Vlanif30]ip add 192.168.30.1 255.255.255.0
[LWS1-Vlanif30]vrrp vrid 30 virtual-ip 192.168.30.254
[LWS1-Vlanif30]int vlanif40
[LWS1-Vlanif40]ip add 192.168.40.1 255.255.255.0
[LWS1-Vlanif40]vrrp vrid 40 virtual-ip 192.168.40.254
[LWS1-Vlanif40]quit
```

> 配置DHCP

```sh
[LWS1]dhcp en
Info: The operation may take a few seconds. Please wait for a moment.done.
[LWS1]ip pool vlan10
Info:It's successful to create an IP address pool.
[LWS1-ip-pool-vlan10]gateway-list 192.168.10.254
[LWS1-ip-pool-vlan10]network 192.168.10.0 mask 255.255.255.0
[LWS1-ip-pool-vlan10]quit
[LWS1]ip pool vlan20
Info:It's successful to create an IP address pool.
[LWS1-ip-pool-vlan20]gateway-list 192.168.20.254
[LWS1-ip-pool-vlan20]network 192.168.20.0 mask 255.255.255.0
[LWS1-ip-pool-vlan20]excluded-ip-address 192.168.20.1 192.168.20.127
[LWS1-ip-pool-vlan20]quit
[LWS1]ip pool vlan30
Info:It's successful to create an IP address pool.
[LWS1-ip-pool-vlan30]gateway-list 192.168.30.254
[LWS1-ip-pool-vlan30]network 192.168.30.0 mask 255.255.255.0
[LWS1-ip-pool-vlan30]excluded-ip-address 192.168.30.1 192.168.30.127
[LWS1-ip-pool-vlan30]quit
[LWS1]ip pool vlan40
Info:It's successful to create an IP address pool.
[LWS1-ip-pool-vlan40]gateway-list 192.168.40.254
[LWS1-ip-pool-vlan40]network 192.168.40.0 mask 255.255.255.0
[LWS1-ip-pool-vlan40]excluded-ip-address 192.168.40.1 192.168.40.127
[LWS1-ip-pool-vlan40]quit
[LWS1]int vlan 10
[LWS1-Vlanif10]dhcp select global
[LWS1-Vlanif10]int vlan 20
[LWS1-Vlanif20]dhcp select global
[LWS1-Vlanif20]int vlan 30
[LWS1-Vlanif30]dhcp select global
[LWS1-Vlanif30]int vlan 40
[LWS1-Vlanif40]dhcp select global
[LWS1-Vlanif40]quit
```

### S2：

```sh
<Huawei>sys
Enter system view, return user view with Ctrl+Z.
[Huawei]sys LWS2
[LWS2]un in en
Info: Information center is disabled.
[LWS2]vlan 10
[LWS2-vlan10]vlan 20
[LWS2-vlan20]vlan 30
[LWS2-vlan30]vlan 40
[LWS2-vlan40]quit
[LWS2]int g0/0/1
[LWS2-GigabitEthernet0/0/1]un sh
Info: Interface GigabitEthernet0/0/1 is not shutdown.
[LWS2-GigabitEthernet0/0/1]port link-t t
[LWS2-GigabitEthernet0/0/1]port t allow vlan all
[LWS2-GigabitEthernet0/0/1]quit
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
[LWS2-GigabitEthernet0/0/3]quit

[LWS2]stp mode stp
Info: This operation may take a few seconds. Please wait for a moment...done.
[LWS2]stp prio 4096

[LWS2]int vlanif10
[LWS2-Vlanif10]ip add 192.168.10.2 24　　
[LWS2-Vlanif10]vrrp vrid 10 virtual-ip 192.168.10.254
[LWS2-Vlanif10]int vlanif20
[LWS2-Vlanif20]ip add 192.168.20.2 24
[LWS2-Vlanif20]vrrp vrid 20 virtual-ip 192.168.20.254
[LWS2-Vlanif20]int vlanif30
[LWS2-Vlanif30]ip add 192.168.30.2 24
[LWS2-Vlanif30]vrrp vrid 30 virtual-ip 192.168.30.254
[LWS2-Vlanif30]vrrp vrid 30 prio 120
[LWS2-Vlanif30]int vlanif40
[LWS2-Vlanif40]ip add 192.168.40.2 24
[LWS2-Vlanif40]vrrp vrid 30 virtual-ip 192.168.40.254
[LWS2-Vlanif40]un vrrp vrid 30 virtual-ip 192.168.40.254
[LWS2-Vlanif40]vrrp vrid 40 virtual-ip 192.168.40.254
[LWS2-Vlanif40]vrrp vrid 40 prio 120
[LWS2-Vlanif40]quit

[LWS2]dhcp en
Info: The operation may take a few seconds. Please wait for a moment.done.
[LWS2]i pool vlan10
Info:It's successful to create an IP address pool.
[LWS2-ip-pool-vlan10]gateway-list 192.168.10.254
[LWS2-ip-pool-vlan10]network 192.168.10.0 mask 255.255.255.0
[LWS2-ip-pool-vlan10]ex 192.168.10.128 192.168.10.253
[LWS2-ip-pool-vlan10]quit
[LWS2]i pool vlan20
Info:It's successful to create an IP address pool.
[LWS2-ip-pool-vlan20]gateway-list 192.168.20.254
[LWS2-ip-pool-vlan20]network 192.168.20.0 mask 255.255.255.0
[LWS2-ip-pool-vlan20]ex 192.168.20.128 192.168.20.253
[LWS2-ip-pool-vlan20]quit
[LWS2]i pool vlan30
Info:It's successful to create an IP address pool.
[LWS2-ip-pool-vlan30]gateway-list 192.168.30.254
[LWS2-ip-pool-vlan30]network 192.168.30.0 mask 255.255.255.0
[LWS2-ip-pool-vlan30]ex 192.168.30.128 192.168.30.253
[LWS2-ip-pool-vlan30]quit
[LWS2]i pool vlan40
Info:It's successful to create an IP address pool.
[LWS2-ip-pool-vlan40]gateway-list 192.168.40.254
[LWS2-ip-pool-vlan40]network 192.168.40.0 mask 255.255.255.0
[LWS2-ip-pool-vlan40]ex 192.168.40.128 192.168.40.253
[LWS2-ip-pool-vlan40]quit
[LWS2]
[LWS2]int vlan 10
[LWS2-Vlanif10]dhcp select global
[LWS2-Vlanif10]int vlan 20
[LWS2-Vlanif20]dhcp select global
[LWS2-Vlanif20]int vlan 30
[LWS2-Vlanif30]dhcp select global
[LWS2-Vlanif30]int vlan 40
[LWS2-Vlanif40]dhcp select global
[LWS2-Vlanif40]quit
```

## 三、测试

> PC：

Ipconfig查看IP然后Ping另一台PC

![](https://cdn.wallleap.cn/img/pic/web-HCL5/pic3.png)

![](https://cdn.wallleap.cn/img/pic/web-HCL5/pic4.png)

![](https://cdn.wallleap.cn/img/pic/web-HCL5/pic5.png)

> S3或S4

`dis stp brief`

![](https://cdn.wallleap.cn/img/pic/web-HCL5/pic6.png)

> S1或S2

`dis vrrp brief`

![](https://cdn.wallleap.cn/img/pic/web-HCL5/pic7.png)

![](https://cdn.wallleap.cn/img/pic/web-HCL5/pic8.png)
