---
title: HCL 的安装和使用
date: 2019-09-09 21:34
updated: 2019-09-09 21:34
cover: //cdn.wallleap.cn/img/pic/cover/202302nAUrrn.jpg
category: 技术杂谈
tags:
  - 网络
  - 华三
description: HCL 的安装和使用
---

安装和简单的使用

## HCL的安装

下载下面的文件

`链接:https://pan.baidu.com/s/13kzRjgJqHXOsvRK54Waz1w  密码:mqh3`

双击 HCL_V2.1.1_Setup.exe 开始安装，安装过程中注意不要勾选 VBox，单独安装 VBox

安装完成之后双击 VirtualBox-4.2.4-81684-Win.exe，没什么注意事项，一直下一步，点允许即可

## HCL 使用

右击 HCL，选择属性

![1](https://cdn.wallleap.cn/img/pic/web-HCL0/pic1.png)

点击兼容性，按图修改

![2](https://cdn.wallleap.cn/img/pic/web-HCL0/pic2.png)

点击更改高 DPI 设置，勾选如图复选框

![3](https://cdn.wallleap.cn/img/pic/web-HCL0/pic3.png)

之后双击打开即可

选择两个 PC 测试，VMbox 会相应生成设备

![4](https://cdn.wallleap.cn/img/pic/web-HCL0/pic4.png)

点击启动按钮

![5](https://cdn.wallleap.cn/img/pic/web-HCL0/pic5.png)

稍等一会右击 vPC，点击配置，输入相关参数，点击启用，这时接口状态显示为 ADM

![6](https://cdn.wallleap.cn/img/pic/web-HCL0/pic6.png)

勾选接口管理下方的启用选项

![7](https://cdn.wallleap.cn/img/pic/web-HCL0/pic7.png)

将两个都配置好，接口状态变为 UP

![8](https://cdn.wallleap.cn/img/pic/web-HCL0/pic8.png)

![9](https://cdn.wallleap.cn/img/pic/web-HCL0/pic9.png)

双击 PC，进入命令行，ping 对方 IP，能 ping 通，软件安装和使用都不会有问题了

![10](https://cdn.wallleap.cn/img/pic/web-HCL0/pic10.png)
