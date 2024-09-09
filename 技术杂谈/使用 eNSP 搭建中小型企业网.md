---
title: 使用 eNSP 搭建中小型企业网
date: 2019-09-30 07:58
updated: 2019-09-30 07:58
cover: //cdn.wallleap.cn/img/pic/cover/202302hAc9mG.jpg
category: 技术杂谈
tags:
  - 网络
  - HCNA
description: 使用 eNSP 模拟搭建中小型企业网
---

局域网内的核心技术：

- 利用 VLAN 进行业务隔离；
- 通过 STP 技术来防止环路，保证冗余链路的正常通信；
- 使用 VRRP 技术来实现负载分担以及防止单点故障；
- 利用 OSPF 协议使得总部和分布的网络能够正常通信；
- 运用 ACL 和 NAT 对数据流进行控制和去外网通信。

## 实验拓扑图

![img](https://cdn.wallleap.cn/img/pic/web-HCL9/pic1.png)

实验目的：

1. 使用 VLAN 进行业务隔离，方便随时切断各部门连接
2. 使用 VLAN 间路由让各 VLAN 之间能够通信
3. PC 能够自动获取 IP
4. 外网主机能够访问服务器
5. 让任意两个 PC 能够访问外网，另外两个不能访问

## 实验配置

### (1)vlan 间路由

- **接入层交换机 LSW3**

**创建 VLAN**

```sh
[LSW3]vlan 10
[LSW3-vlan10]vlan 20
[LSW3-vlan20]quit
```

**配置与主机相连的接口为Access并绑定VLAN**

```sh
[LSW3]interface e0/0/1
[LSW3-Ethernet0/0/1]undo shutdown
Info: Interface Ethernet0/0/1 is not shutdown.
[LSW3-Ethernet0/0/1]port link-type access
[LSW3-Ethernet0/0/1]port default vlan 10
[LSW3-Ethernet0/0/1]int e0/0/2
[LSW3-Ethernet0/0/2]port link-t a
[LSW3-Ethernet0/0/2]port de vlan 20
```

**配置与交换机相连的接口为 Trunk 并允许所有 VLAN 通过**

```sh
[LSW3-Ethernet0/0/2]int e0/0/3
[LSW3-Ethernet0/0/3]port link-t t
[LSW3-Ethernet0/0/3]port t allow vlan all
[LSW3-Ethernet0/0/3]int e0/0/4
[LSW3-Ethernet0/0/4]port link-t t
[LSW3-Ethernet0/0/4]port t allow vlan all
[LSW3-Ethernet0/0/4]quit
```

- **接入层交换机 LSW4**

**与 LSW3 类似，创建 VLAN，设置接口即可**

```sh
[LSW4]vlan 30
[LSW4-vlan30]vlan 40
[LSW4-vlan40]quit
[LSW4]int e0/0/1
[LSW4-Ethernet0/0/1]port link-t a
[LSW4-Ethernet0/0/1]port de vlan 30
[LSW4-Ethernet0/0/1]int e0/0/2
[LSW4-Ethernet0/0/2]port link-t a
[LSW4-Ethernet0/0/2]port de vlan 40
[LSW4-Ethernet0/0/2]int e0/0/3
[LSW4-Ethernet0/0/3]port link-t t
[LSW4-Ethernet0/0/3]port t allow vlan all
[LSW4-Ethernet0/0/3]int e0/0/4
[LSW4-Ethernet0/0/4]port link-t t
[LSW4-Ethernet0/0/4]port t allow vlan all
[LSW4-Ethernet0/0/4]quit
```

- **核心层交换机 LSW1**

**创建 VLAN**

```sh
[LSW1]vlan 10
[LSW1-vlan10]vlan 20
[LSW1-vlan20]vlan 30
[LSW1-vlan30]vlan 40
[LSW1-vlan40]vlan 50
[LSW1-vlan50]quit
```

**与交换机相连接口设为 Trunk 并允许所有 VLAN 通过**

```sh
[LSW1]int g0/0/1
[LSW1-GigabitEthernet0/0/1]port link-t t
[LSW1-GigabitEthernet0/0/1]port t allow vlan all
[LSW1-GigabitEthernet0/0/1]int g0/0/3
[LSW1-GigabitEthernet0/0/3]port link-t t
[LSW1-GigabitEthernet0/0/3]port t allow vlan all
[LSW1-GigabitEthernet0/0/3]int g0/0/2
[LSW1-GigabitEthernet0/0/2]port link-t t
[LSW1-GigabitEthernet0/0/2]port t allow vlan all
```

**服务器接入 VLAN50，将将与服务器相连的接口设为 Access 口并绑定 VLAN50**

```sh
[LSW1-GigabitEthernet0/0/2]int g0/0/5
[LSW1-GigabitEthernet0/0/5]port link-t a
[LSW1-GigabitEthernet0/0/5]port de vlan 50
[LSW1-GigabitEthernet0/0/5]quit
```

**给连接路由器的接口绑定 VLAN60，方便配置地址**

```sh
[LSW1]vlan 60
[LSW1-vlan60]int g0/0/4
[LSW1-GigabitEthernet0/0/4]port link-t a
[LSW1-GigabitEthernet0/0/4]port de vlan 60
[LSW1-GigabitEthernet0/0/4]quit
```

**给 VLAN 分配 IP 地址（配置真实网关）**

```sh
[LSW1]int vlan 10
[LSW1-Vlanif10]ip add 192.168.10.1 24
[LSW1-Vlanif10]int vlan 20
[LSW1-Vlanif20]ip add 192.168.20.1 24
[LSW1-Vlanif20]int vlan 30
[LSW1-Vlanif30]ip add 192.168.30.1 24
[LSW1-Vlanif30]int vlan 40
[LSW1-Vlanif40]ip add 192.168.40.1 24
[LSW1-Vlanif40]int vlan 50
[LSW1-Vlanif50]ip add 192.168.50.1 24
[LSW1-Vlanif50]int vlan 60
[LSW1-Vlanif60]ip add 192.168.60.1 24
[LSW1-Vlanif60]quit
```

* **核心层交换机 LSW２**

**与 LSW１ 类似，创建 VLAN、配置好接口、设置真实网关（与 S１ 地址不同）**

```sh
[LSW2]vlan 10
[LSW2-vlan10]vlan 20
[LSW2-vlan20]vlan 30
[LSW2-vlan30]vlan 40
[LSW2-vlan40]quit
[LSW2]int g0/0/1
[LSW2-GigabitEthernet0/0/1]port link-t t
[LSW2-GigabitEthernet0/0/1]port t allow vlan all
[LSW2-GigabitEthernet0/0/1]int g0/0/2
[LSW2-GigabitEthernet0/0/2]port link-t t
[LSW2-GigabitEthernet0/0/2]port t allow vlan all
[LSW2-GigabitEthernet0/0/2]int g0/0/3
[LSW2-GigabitEthernet0/0/3]port link-t t
[LSW2-GigabitEthernet0/0/3]port t allow vlan all
[LSW2-GigabitEthernet0/0/3]quit
[LSW2]vlan 70
[LSW2-vlan70]int g0/0/4
[LSW2-GigabitEthernet0/0/4]port link-t a
[LSW2-GigabitEthernet0/0/4]port de vlan 70
[LSW2-GigabitEthernet0/0/4]quit
[LSW2]int vlan 10
[LSW2-Vlanif10]ip add 192.168.10.2 24
[LSW2-Vlanif10]int vlan 20
[LSW2-Vlanif20]ip add 192.168.20.2 24
[LSW2-Vlanif20]int vlan 30
[LSW2-Vlanif30]ip add 192.168.30.2 24
[LSW2-Vlanif30]int vlan 40
[LSW2-Vlanif40]ip add 192.168.40.2 24
[LSW2-Vlanif40]int vlan 70
[LSW2-Vlanif70]ip add 192.168.70.2 24
[LSW2-Vlanif70]quit
```

### (2)DHCP 的搭建

- **客户端开启 DHCP**

![img](https://cdn.wallleap.cn/img/pic/illustration/clip_image002-1596792968009.jpg)

- **核心交换机 LSW１ 和 LSW２ 上配置 DHCP 服务**

**开启 DHCP 服务**

```sh
[SW1]dhcp enable
Info: The operation may take a few seconds. Please wait for a moment.done.
```

**创建地址池 vlan10、vlan20、vlan30、vlan40，其中 `＄` 代表 `１`~`４`，网关使用之后配置的虚拟网关**

```sh
[LSW1]ip pool vlan＄0
Info:It's successful to create an IP address pool.
[LSW1-ip-pool-vlan$0]gateway-list 192.168.10.254
[LSW1-ip-pool-vlan$0]network 192.168.＄0.0 mask 255.255.255.0
[LSW1-ip-pool-vlan$0]quit
```

**VLAN 绑定地址池**

```sh
[LSW1]int vlan ＄0
[LSW1-Vlanif$0]dhcp select global
[LSW1-Vlanif$0]quit
```

**LSW１ 排除地址**

```sh
[LSW1-ip-pool-vlan$0]excluded-ip-address 192.168.＄0.3 192.168.＄0.127
```


**LSW２ 排除地址**

```sh
[LSW2-ip-pool-vlan$0]ex 192.168.＄0.128 192.168.＄0.253
```

### (3) STP+VRRP 的配置

* **汇聚层交换机 LSW3、LSW4 只需要开启 STP 即可**

```sh
[LSW3]stp mode stp
Info: This operation may take a few seconds. Please wait for a moment...done.
[LSW4]stp mode stp
Info: This operation may take a few seconds. Please wait for a moment...done.
```

- **核心层 LSW１ 配置**

**开启 STP**

```sh
[LSW1]stp mode stp
Info: This operation may take a few seconds. Please wait for a moment...done.
```

**设置 LSW1 为根桥**

```sh
[LSW1]stp priority 0
```

配置 VRRP，LSW1 是 VLAN10、VLAN20 的 Master，当上层接口错误时，自动降低优先级，让 LSW2 成为Master

```sh
[LSW1]int vlan 10
[LSW1-Vlanif10]vrrp vrid 10 vi 192.168.10.254
[LSW1-Vlanif10]vrrp vrid 10 prio 120
[LSW1-Vlanif10]vrrp vrid 10 track int g0/0/4 reduce 30
[LSW1-Vlanif10]int vlan 20
[LSW1-Vlanif20]vrrp vrid 20 vi 192.168.20.254
[LSW1-Vlanif20]vrrp vrid 20 prio 120
[LSW1-Vlanif20]vrrp vrid 20 track int g0/0/4 re 30
[LSW1-Vlanif20]int vlan 30
[LSW1-Vlanif30]vrrp vrid 30 vi 192.168.30.254
[LSW1-Vlanif30]int vlan 40
[LSW1-Vlanif40]vrrp vrid 40 vi 192.168.40.254
[LSW1-Vlanif40]quit
```

- **核心层 LSW２ 配置**

开启 STP，并将优先级设为 4096

```sh
[LSW2]stp mode stp
Info: This operation may take a few seconds. Please wait for a moment...done.
[LSW2]stp prio 4096
```

配置 VRRP，LSW2 是 VLAN30、VLAN40 的 Master，当上层接口错误时，自动降低优先级，让 LSW1 成为 Master

```sh
[LSW2]int vlan 10
[LSW2-Vlanif10]vrrp vrid 10 vi 192.168.10.254
[LSW2-Vlanif10]int vlan 20
[LSW2-Vlanif20]vrrp vrid 20 vi 192.168.20.254
[LSW2-Vlanif20]int vlan 30
[LSW2-Vlanif30]vrrp vrid 30 vi 192.168.30.254
[LSW2-Vlanif30]vrrp vrid 30 prio 120
[LSW2-Vlanif30]vrrp vrid 30 track int g0/0/4 re 30
[LSW2-Vlanif30]int vlan 40
[LSW2-Vlanif40]vrrp vrid 40 vi 192.168.40.254
[LSW2-Vlanif40]vrrp vrid 40 prio 120
[LSW2-Vlanif40]vrrp vrid 40 track int g0/0/4 re 30
[LSW2-Vlanif40]quit
```

### (4)OSPF 的搭建

* **LSW１ OSPF 配置**

**查看接口 IP**

```sh
[LSW1]dis ip int br

Interface                         IP Address/Mask      Physical   Protocol  
MEth0/0/1                         unassigned           down       down      
NULL0                             unassigned           up         up(s)     
Vlanif1                           unassigned           up         down      
Vlanif10                          192.168.10.1/24      up         up        
Vlanif20                          192.168.20.1/24      up         up        
Vlanif30                          192.168.30.1/24      up         up        
Vlanif40                          192.168.40.1/24      up         up        
Vlanif50                          192.168.50.1/24      up         up        
Vlanif60                          192.168.60.1/24      up         up        
```

**根据所有 IP 宣告相应网段**

```sh
[LSW1]ospf 1
[LSW1-ospf-1]area 0.0.0.0
[LSW1-ospf-1-area-0.0.0.0]net 192.168.10.0 0.0.0.255
[LSW1-ospf-1-area-0.0.0.0]net 192.168.20.0 0.0.0.255
[LSW1-ospf-1-area-0.0.0.0]net 192.168.30.0 0.0.0.255
[LSW1-ospf-1-area-0.0.0.0]net 192.168.40.0 0.0.0.255
[LSW1-ospf-1-area-0.0.0.0]net 192.168.50.0 0.0.0.255
[LSW1-ospf-1-area-0.0.0.0]net 192.168.60.0 0.0.0.255
[LSW1-ospf-1-area-0.0.0.0]quit
[LSW1-ospf-1]qu
```

- **LSW２ OSPF 配置**

**与 LSW1 类似**

```sh
[LSW2]dis ip int br
Interface                         IP Address/Mask      Physical   Protocol  
MEth0/0/1                         unassigned           down       down     
NULL0                             unassigned           up         up(s)    
Vlanif1                           unassigned           up         down      
Vlanif10                          192.168.10.2/24      up         up        
Vlanif20                          192.168.20.2/24      up         up        
Vlanif30                          192.168.30.2/24      up         up        
Vlanif40                          192.168.40.2/24      up         up        
Vlanif70                          192.168.70.2/24      up         up      

[LSW2]ospf 1
[LSW2-ospf-1]area 0.0.0.0
[LSW2-ospf-1-area-0.0.0.0]net 192.168.10.0 0.0.0.255
[LSW2-ospf-1-area-0.0.0.0]net 192.168.20.0 0.0.0.255
[LSW2-ospf-1-area-0.0.0.0]net 192.168.30.0 0.0.0.255
[LSW2-ospf-1-area-0.0.0.0]net 192.168.40.0 0.0.0.255
[LSW2-ospf-1-area-0.0.0.0]net 192.168.70.0 0.0.0.255
[LSW2-ospf-1-area-0.0.0.0]quit
[LSW2-ospf-1]quit
```

### (5)ACL+NAT

* **AR１ 上 ACL+NAT 配置**

**Easy IP：**

**配置基本 ACL 并添加规则，允许 VLAN10、VLAN30、VLAN50 访问外网，VLAN20、40 不能访问**

```sh
[AR1]acl number 2000
[AR1-acl-basic-2000]rule 0 per source 192.168.10.0 0.0.0.255
[AR1-acl-basic-2000]rule 5 per source 192.168.30.0 0.0.0.255
[AR1-acl-basic-2000]rule 10 per source 192.168.50.0 0.0.0.255
[AR1-acl-basic-2000]quit
```

**绑定规则到外网端口**

```sh
[AR1]int g0/0/2
[AR1-GigabitEthernet0/0/2]nat outbound 2000
```

**静态 NAT，将服务器内网地址转为一个专门的公有 IP**

```sh
[AR1-GigabitEthernet0/0/2]nat static global 200.200.200.10 inside 192.168.50.253
[AR1-GigabitEthernet0/0/2]quit
```

### (6)路由器 OSPF 协议的配置

- **AR１ OSPF 配置**

**配置接口 IP**

```sh
[AR1]int g0/0/0
[AR1-GigabitEthernet0/0/0]ip add 192.168.60.100 24
Sep 26 2019 09:54:53-08:00 AR1 %%01IFNET/4/LINK_STATE(l)[0]:The line protocol IP on the interface GigabitEthernet0/0/0 has entered the UP state. 
[AR1-GigabitEthernet0/0/0]int g0/0/1
[AR1-GigabitEthernet0/0/1]ip add 192.168.70.100 24
Sep 26 2019 09:55:16-08:00 AR1 %%01IFNET/4/LINK_STATE(l)[1]:The line protocol IP on the interface GigabitEthernet0/0/1 has entered the UP state.
[AR1-GigabitEthernet0/0/1]int g0/0/2
[AR1-GigabitEthernet0/0/2]ip add 200.200.200.1 24
Sep 26 2019 09:56:09-08:00 AR1 %%01IFNET/4/LINK_STATE(l)[2]:The line protocol IP on the interface GigabitEthernet0/0/2 has entered the UP state.
[AR1-GigabitEthernet0/0/2]quit
```

**查看接口地址**

```sh
[AR1]dis ip int br
Interface                         IP Address/Mask      Physical   Protocol
GigabitEthernet0/0/0              192.168.60.100/24    up         up       
GigabitEthernet0/0/1              192.168.70.100/24    up         up       
GigabitEthernet0/0/2              200.200.200.1/24     up         up        
NULL0                             unassigned           up         up(s)     
```

**宣告地址段**

```sh
[AR1]ospf 1
[AR1-ospf-1]area 0.0.0.0
[AR1-ospf-1-area-0.0.0.0]net 192.168.60.0 0.0.0.255
[AR1-ospf-1-area-0.0.0.0]net 192.168.70.0 0.0.0.255
[AR1-ospf-1-area-0.0.0.0]net 200.200.200.0 0.0.0.255
[AR1-ospf-1-area-0.0.0.0]quit
[AR1-ospf-1]quit
```

**配置到外网的默认路由，并加入到 OSPF 中**

```sh
[AR1]ip route-static 0.0.0.0 0.0.0.0 200.200.200.100
[AR1]ospf 1
[AR1-ospf-1]default-route-advertise
[AR1-ospf-1]quit
```

### (7)路由器 AR2 的配置

```sh
[AR2]int g0/0/0
[AR2-GigabitEthernet0/0/0]ip add 200.200.200.100 24
[AR2-GigabitEthernet0/0/0]int g0/0/1
[AR2-GigabitEthernet0/0/1]ip add 200.200.201.1 24
[AR2-GigabitEthernet0/0/1]quit
```

## 结果测试

### 1、内网电脑之间进行通信

![img](https://cdn.wallleap.cn/img/pic/web-HCL9/pic3.png)

PC1 能够 ping 通其他四个 VLAN 内的主机

### 2、内网主机动态获取 IP 地址

![img](https://cdn.wallleap.cn/img/pic/web-HCL9/pic2.png)

![img](https://cdn.wallleap.cn/img/pic/web-HCL9/pic4.png)

PC 配置 DHCP 能够自动获取 IP

### 3、内网主机访问外网

![img](https://cdn.wallleap.cn/img/pic/web-HCL9/pic5.png)

![img](https://cdn.wallleap.cn/img/pic/web-HCL9/pic6.png)

![img](https://cdn.wallleap.cn/img/pic/web-HCL9/pic7.png)

PC１、PC３ 和 Server1 能够 ping 通外网的主机，PC2 和 PC4 ping 通
