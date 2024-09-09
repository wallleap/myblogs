---
title: HCNA 学习之虚拟局域网 VLAN
date: 2019-09-14 18:06
updated: 2019-09-14 18:06
cover: //cdn.wallleap.cn/img/pic/cover/202302QIAwJ8.jpg
category: 技术杂谈
tags:
  - 网络
  - HCNA
description: HCNA 学习之虚拟局域网 VLAN
---

虚拟局域网

## VLAN基础配置

现在我们先了解一下什么是 VLAN，VLAN 是用来干什么的

在此之前我们先讲下**广播域**和**冲突域**

**广播域**（broadcast domain）就是说如果站点发出一个广播信号后能接收到这个信号的范围。通常来说一个局域网就是一个广播域。（路由器隔离广播域）
**冲突域**（collision domain），所有直接连接在一起的，而且必须竞争以太网总线的节点都可以认为是处在同一个冲突域中，说白了就是一次只有一个设备发送信息，其他的只能等待。交换机或 hub 可以隔离冲突域。

### VLAN是什么

> **VLAN**（Virtual Local Area Network）的中文名为”虚拟局域网”。
>
> 虚拟局域网（VLAN）是一组逻辑上的设备和用户，这些设备和用户并不受物理位置的限制，可以根据功能、部门及应用等因素将它们组织起来，相互之间的通信就好像它们在同一个网段中一样，由此得名虚拟局域网。
>
> VLAN 是一种比较新的技术，工作在 OSI 参考模型的第 2 层和第 3 层，一个 VLAN 就是一个广播域，VLAN 之间的通信是通过第3层的路由器来完成的。
>
> 与传统的局域网技术相比较，VLAN 技术更加灵活，它具有以下优点：
>
> - 网络设备的移动、添加和修改的管理开销减少；
> - 可以控制广播活动；
> - 可提高网络的安全性。
>
> 在计算机网络中，一个二层网络可以被划分为多个不同的广播域，一个广播域对应了一个特定的用户组，默认情况下这些不同的广播域是相互隔离的。不同的广播域之间想要通信，需要通过一个或多个路由器。这样的一个广播域就称为 VLAN。

### VLAN是用来干什么的

交换机能够有效地隔绝冲突域，但是这个网络中的设备还是处于一个广播域，所有的设备之间都可以相互通信。

但是，有时我们并不希望所有设备都处于一个广播域，因此，人们使用 VLAN 技术将一个物理的 LAN 在逻辑上划分成多个广播域（**使用 VLAN 隔离广播域**）

一个 VLAN 中的设备之间能够之间通信，但不同 VLAN 内的设备之间不能直接互通。

不同的 VLAN 使用不同的 VLAN ID 区分，VLAN ID 的范围是 `0~4095`，可配置的值为 `1~4094`，0 和 4095 为保留值。

### 划分依据

1、按端口划分 VLAN

> 许多 VLAN 厂商都利用交换机的端口来划分 VLAN 成员。
>
> 被设定的端口都在同一个广播域中。例如，一个交换机的 1，2，3，4，5 端口被定义为虚拟网 AAA，同一交换机的 6，7，8 端口组成虚拟网 BBB。这样做允许各端口之间的通讯，并允许共享型网络的升级。但是，这种划分模式将虚拟网限制在了一台交换机上。
>
> 第二代端口VLAN技术允许跨越多个交换机的多个不同端口划分 VLAN，不同交换机上的若干个端口可以组成同一个虚拟网。
>
> 以交换机端口来划分网络成员，其配置过程简单明了。因此，从目前来看，这种根据端口来划分 VLAN 的方式仍然是最常用的一种方式。

2、按 MAC 地址划分 VLAN

> 这种划分 VLAN 的方法是根据每个主机的 MAC 地址来划分，即对每个 MAC 地址的主机都配置它属于哪个组。
>
> 这种划分 VLAN 方法的最大优点就是当用户物理位置移动时，即从一个交换机换到其他的交换机时，VLAN 不用重新配置，所以，可以认为这种根据 MAC 地址的划分方法是基于用户的 VLAN，这种方法的缺点是初始化时，所有的用户都必须进行配置，如果有几百个甚至上千个用户的话，配置是非常累的。
>
> 而且这种划分的方法也导致了交换机执行效率的降低，因为在每一个交换机的端口都可能存在很多个 VLAN 组的成员，这样就无法限制广播包了。另外，对于使用笔记本电脑的用户来说，他们的网卡可能经常更换，这样，VLAN 就必须不停地配置。

3、按网络层划分

> 这种划分 VLAN 的方法是根据每个主机的网络层地址或协议类型（如果支持多协议）划分的，虽然这种划分方法是根据网络地址，比如 IP 地址，但它不是路由，与网络层的路由毫无关系。
>
> 这种方法的优点是用户的物理位置改变了，不需要重新配置所属的 VLAN，而且可以根据协议类型来划分 VLAN，这对网络管理者来说很重要，还有，这种方法不需要附加的帧标签来识别 VLAN，这样可以减少网络的通信量。
>
> 这种方法的缺点是效率低，因为检查每一个数据包的网络层地址是需要消耗处理时间的（相对于前面两种方法），一般的交换机芯片都可以自动检查网络上数据包的以太网帧头，但要让芯片能检查IP帧头，需要更高的技术，同时也更费时。当然，这与各个厂商的实现方法有关。

4、按 IP 组播划分

> IP组播实际上也是一种 VLAN 的定义，即认为一个组播组就是一个 VLAN，这种划分的方法将 VLAN 扩大到了广域网，因此这种方法具有更大的灵活性，而且也很容易通过路由器进行扩展，当然这种方法不适合局域网，主要是效率不高。

5、基于规则的 VLAN

> 也称为基于策略的 VLAN。这是最灵活的 VLAN 划分方法，具有自动配置的能力，能够把相关的用户连成一体，在逻辑划分上称为“关系网络”。网络管理员只需在网管软件中确定划分 VLAN 的规则（或属性），那么当一个站点加入网络中时，将会被“感知”，并被自动地包含进正确的VLAN 中。同时，对站点的移动和改变也可自动识别和跟踪。
>
> 采用这种方法，整个网络可以非常方便地通过路由器扩展网络规模。有的产品还支持一个端口上的主机分别属于不同的 VLAN，这在交换机与共享式Hub共存的环境中显得尤为重要。自动配置 VLAN 时，交换机中软件自动检查进入交换机端口的广播信息的IP源地址，然后软件自动将这个端口分配给一个由 IP 子网映射成的 VLAN。

6、按用户定义、非用户授权划分

> 基于用户定义、非用户授权来划分 VLAN，是指为了适应特别的 VLAN 网络，根据具体的网络用户的特别要求来定义和设计 VLAN，而且可以让非 VLAN 群体用户访问 VLAN，但是需要提供用户密码，在得到 VLAN 管理的认证后才可以加入一个 VLAN。
>
> 以上划分 VLAN 的方式中，基于端口的 VLAN 端口方式建立在物理层上；MAC 方式建立在数据链路层上；网络层和 IP 广播方式建立在第三层上。

### 基本配置

1、创建 VLAN

```sh
[s1]vlan 10                  # 在系统视图创建vlan
[s1-vlan10]description VLAN10   # 命名
[s1-vlan10]vlan 20      # 可以在这个视图接着创建vlan
# 创建多个vlan
[s1]vlan batch 30 40
```

2、查看 VLAN 信息

```sh
[s1]display vlan
```

3、查看配置好的 VLAN 的简要信息

```sh
[s1]display vlan summary
```

4、查看VLAN和接口配置情况

```sh
[s1]display port vlan
```

## VLAN 技术原理

交换机用 VLAN 标签来区分不同 VLAN 的以太网帧

![pic48](https://cdn.wallleap.cn/img/pic/test/hcna-pic48.png)

帧格式

![pic49](https://cdn.wallleap.cn/img/pic/test/hcna-pic49.png)

### 单交换机 VLAN 标签操作

- 在进入交换机端口是，附加缺省 VLAN 标签
- 出交换机端口时，去掉 VLAN 标签

![pic50](https://cdn.wallleap.cn/img/pic/test/hcna-pic50.png)

### Access 链路类型端口

Access 接口是交换机上用来连接用户主机的接口。

当 Access 接口从主机收到一个不带 VLAN 标签的数据帧时，会给该数据帧加上与 PVID 一致的 VLAN 标签。

当 Access 接口要发送一个带 VLAN 标签的数据帧给主机时，首先检查该数据帧的 VLAN ID 是否与自己的 PVID 相同，若相同，则去掉 VLAN 标签后发送该数据帧给主机；若不相同，直接丢弃该数据帧。

一般在与客户机相连的接口上配置。

![pic51](https://cdn.wallleap.cn/img/pic/test/hcna-pic51.png)

### 跨交换机 VLAN 标签

带有 VLAN 标签的以太网帧在交换机间传递

![pic52](https://cdn.wallleap.cn/img/pic/test/hcna-pic52.png)

### Trunk 链路类型端口

为了使 VLAN 的数据帧能够跨跃多台交换机传递，交换机之间互联的链路需要设置为干道链路（Trunk Link）
允许多个 VLAN 通过，可以接收和发送多个 VLAN 的数据帧，缺省 VLAN 的以太网帧不带标签。

当 Trunk 端口收到数据帧时，如果该帧不包含 802.1Q 的 VLAN 标签，将打上该 Trunk 端口的 PVID；如果该帧包含 802.1Q 的 VLAN 标签，则不改变。
当 Trunk 端口发送数据帧时，当所发送帧的 VLAN ID 与端口的 PVID 不同时，检查是否允许该 VLAN 通过，若允许的话直接转发，不允许就直接丢弃；当该帧的 VLAN ID 与端口的 PVID 相同时，则剥离 VLAN 标签后转发。

一般用于交换机与交换机之间连接的接口。

![pic53](https://cdn.wallleap.cn/img/pic/test/hcna-pic53.png)

### Hybrid 链路类型端口

允许多个 VLAN 通过，可以接收和发送多个 VLAN 的数据帧。
Hybrid 端口和 Trunk 端口的不同之处在于：

- Hybrid 端口允许多个 VLAN 的以太网帧不带标签
- Trunk 端口只允许缺省 VLAN 的以太网帧不带标签

![pic54](https://cdn.wallleap.cn/img/pic/test/hcna-pic54.png)

### 接口配置

---

#### 配置 access 口

```sh
[s1]int g0/0/2       # 进入与PC相连的接口
[s1-g0/0/2]port link-type access  # 配置接口类型为Access
[s1-g0/0/2]port default vlan 10     # 配置接口的默认VLAN并加入VLAN10 默认情况下，所有接口的默认VLAN ID为1
```

---

#### 配置 Trunk 口

```sh
[s1]int g0/0/1       # 进入与另一交换机相连的接口
[s1-g0/0/1]port link-type trunk  # 配置接口类型为Trunk
[s1-g0/0/1]port trunk allow-pass vlan 10 20     # 允许VLAN10、20通过
[s1-g0/0/1]port trunk allow-pass vlan all     # 允许所有VLAN通过(1~4094)
```

---

#### 配置 Hybrid

```sh
# 与主机相连
[s1-g0/0/2]undo port default vlan #恢复接口默认VLAN
[s1-g0/0/2]port link-type hybrid  #设置接口类型为Hybrid
[s1-g0/0/2]port hybrid untagged vlan 20  #转发VLAN20帧时剥离tag
[s1-g0/0/2]port hybrid pvid vlan 20  #默认VLAN ID
# 与switch相连
[s1-g0/0/1]port trunk allow-pass vlan 1
[s1-g0/0/1]port link-type hybrid
[s1-g0/0/1]port hybrid tagged vlan 10 20   #接收带有VLAN10、20标签的帧
```

## VLAN 间路由

由于 VLAN 隔离了二层广播域，也间接的隔离了各个 VLAN 之间的其他二层流量交换，这样导致属于不同 VLAN 之间的用户不能进行二层的通信，但是如果我们想让 VLAN10 和 VLAN20 之间能够通信怎么办呢

——经过三层的路由转发能将报文从一个 VLAN 转发到另外一个 VLAN。

### 路由器物理接口

这个讲还是得讲的，但是一般不用，所以只给个拓扑图，不配置

![pic56](https://cdn.wallleap.cn/img/pic/test/hcna-pic56.png)

随着交换机 VLAN 的数量增加，需要路由器的接口也随之增加。而路由器的端口数量有限且某些端口也并不是一直工作状态，导致成本高且某些端口使用率低，造成浪费。

### 单臂路由

和上面的相比，只是将物理接口转换成了虚拟子接口，节省了路由器端口

![pic57](https://cdn.wallleap.cn/img/pic/test/hcna-pic57.png)
配置：

S1、S2（下面两交换机）与 PC 相连的接口配置为 Access 接口，并且 S1 的 E0/0/1 及 E0/0/3 都是 VLAN10，S2 的 E0/0/1 为 VLAN20、E0/0/3 为 VLAN30；
S1、S2、S3 与交换机/路由器相连的接口配置为 Trunk 口，并且允许所有 VLAN 通过
剩下的重头戏：配置 R1

```sh
# 进入子接口1并且配置好IP
[R1]int g0/0/0.1
[R1-GigabitEthernet0/0/0.1]ip add 192.168.1.254 24
# 配置子接口封装
[R1-GigabitEthernet0/0/0.1]dot1q termination vid 10
Mar  7 2020 00:05:38-08:00 R1 %%01IFNET/4/LINK_STATE(l)[0]:The line protocol IP
on the interface GigabitEthernet0/0/0.1 has entered the UP state.
# 开启子接口的ARP广播功能
[R1-GigabitEthernet0/0/0.1]arp broadcast enable
```

其他两个接口也这样配置

![pic58](https://cdn.wallleap.cn/img/pic/test/hcna-pic58.png)

配置完成之后，可以使用命令  `display ip interface brief` 查看接口状态

![pic59](https://cdn.wallleap.cn/img/pic/test/hcna-pic59.png)

使用命令  `display ip routing-table` 查看路由表

之后使用 ping IP 测试连通性即可

### 利用三层交换机

三层交换机带有路由功能，VLANIF 接口可以配置 IP 地址，借助 VLANIF 接口，三层交换机就能实现路由转发功能

![pic60](https://cdn.wallleap.cn/img/pic/test/hcna-pic60.png)

设置好 PC 的网络参数，IP、掩码已给出，网关为 192.168.*.254

**接着配置交换机 SW**

创建 VLAN 并配置接口

```sh
[SW]vlan 10
[SW-vlan10]vlan 20
[SW-vlan20]int g0/0/1
[SW-GigabitEthernet0/0/1]port link-type access
[SW-GigabitEthernet0/0/1]port defaut vlan 10
[SW-GigabitEthernet0/0/1]int g0/0/2
[SW-GigabitEthernet0/0/2]port link-type access
[SW-GigabitEthernet0/0/2]port defaut vlan 20
[SW-GigabitEthernet0/0/2]int g0/0/3
[SW-GigabitEthernet0/0/3]port link-type access
[SW-GigabitEthernet0/0/3]port defaut vlan 10
```

配置 VLANIF

```sh
[SW]int VLANif 10
[SW-Vlanif10]ip add 192.168.1.254 24
[SW-Vlanif10]int VLANif 20
[SW-Vlanif20]ip add 192.168.1.254 24
```

这样就配置成功了

查看接口状态

![pic61](https://cdn.wallleap.cn/img/pic/test/hcna-pic61.png)

PC 测试

![pic62](https://cdn.wallleap.cn/img/pic/test/hcna-pic62.png)

VLAN 的就到这里了，拜拜~
