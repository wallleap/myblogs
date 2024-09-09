---
title: 安装华为模拟器 eNSP
date: 2019-09-10 01:34
updated: 2019-09-10 01:34
cover: //cdn.wallleap.cn/img/pic/cover/202302QIAwJ8.jpg
category: 技术杂谈
tags:
  - 网络
  - HCNA
description: 安装华为模拟器 eNSP
---

win10 安装 eNSP

## 1、根据自己电脑系统选择适合版本下载

本来 eNSP 在华为官网是可以下载的，但因为安全问题，现只提供给客户下载

因此我将在下面放出下载链接

由于 win10 和 eNSP 之间存在兼容性问题，因此需要重点注意，而 win7 则没有这种顾虑：

- Win7：随便哪个版本，只需要在安装的时候注意防火墙即可
- Win10：这个就有严格的版本要求了

按照网上的以及我自己的测试，eNSP 500 + vBox 5.1.26 是没有问题的

- Win10
- eNSP V100R002C00B500 Setup
- VirtualBox-5.1.26-117224-Win

eNSP分享：

链接：https://pan.baidu.com/s/1_zmQKGPe04BeUx5Xh8qQCQ  提取码：bili

这里面有三个版本的，按需求下载

不知道应该下载哪个版本的直接下最新版 eNSP V100R003C00SPC100，看里面的安装指南(先安装好 VMBox\WareShark 等软件)

## 2、win10 安装注意事项

首先安装 eNSP，前面的只有一个按钮选项，点击就行

到这步，点击“我愿意接受此协议”，接着点“下一步”

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423335.webp)

安装位置的话，直接修改成磁盘根目录/eNSP

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423336.webp)

在到这里需要注意下，取消勾选“安装 VirtualBox 5.0.16”前的复选框，接着点击“下一步”

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423337.webp)

接着按提示安装完 eNSP、WinPcap、Wirehark 即可

基本上这些都可以默认的，直接点下一步、next、Install、Finish 即可

注意，安装完成之后不要立即打开 eNSP，也就是在这一步取消复选框再点完成

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423339.webp)

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423340.webp)

接下来就可以安装 VBox 了

好吧，在安装 VBox 之前，部分电脑还需要进入 BIOS 开启虚拟化功能

给一个参考链接，https://jingyan.baidu.com/article/574c52195b675c6c8d9dc138.html

如果和这个不同自行百度

开启虚拟化后，进入系统，双击 VBox 安装包进行安装

同理，更改下目录，当然，这里用默认的目录也可以

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423341.webp)

如果安装过程中弹窗，请点击“是”

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423342.webp)

第一次安装，可能会弹出下面这个界面，咱点击“安装”

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423343.webp)

到这个界面，VBox 也安装完成了

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423344.webp)

## 3、其他设置

### 防火墙

我们使用 eNSP 中的设备需要在防火墙中运行 eNSP 相关服务访问

当然，我们可以直接关掉系统的防火墙，毕竟我们会安装安全防护软件，这里推荐使用火绒

首先进入控制面板

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423345.webp)

按照下图，点击进入这个位置

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423346.webp)

点击左边的“高级设置”

再点击“属性”，把这三项都设置为关闭

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423347.webp)

看到这个就是关闭成功了

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423348.webp)

### 注册设备

现在我们进入 VBox，这里没有设备，我们需要进入 eNSP 设置

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423349.webp)

进入 eNSP，点击左上角，新建一个空白的拓扑

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423350.webp)

再点击右上方的菜单-工具-注册设备

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423351.webp)

勾选三个复选框，点击注册

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423352.webp)

好吧，弄完之后 VBox 还是看不到设备

我们在拓扑上添加上设备测试一下，路由器选择 AR3260(基本上这个能用其他的都 OK 了)，交换机选择 S3700

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423353.webp)

启动一下所有的设备，没有弹出错误，等待一会变成绿色，点进设备，没有 `######`

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423354.webp)

![](https://cdn.wallleap.cn/img/pic/illustration/202308071423355.webp)

一般这样就 OK 了

## 补充

按照上面的肯定就不会有错了，但是，出现的一般错误还是要说下的

### 显示“错误代码40”

这个可以直接点击解决方案，按照那上面的一个个解决

### 一直输出 `#` 号

就是系统防火墙的问题，关掉就行
