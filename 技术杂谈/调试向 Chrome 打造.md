---
title: 调试向 Chrome 打造
date: 2020-03-25 10:33
updated: 2020-03-25 10:33
cover: //cdn.wallleap.cn/img/pic/cover/202302GRCVVo.jpg
category: 技术杂谈
tags:
  - web
  - 前端
description: 调试向 Chrome 打造
---

创建一个单独调试用的 Chrome 快捷方式

## 1、问题起源

* 由于自己日常使用的 Chrome 安装了太多插件，调试的时候受插件的影响，很难进行识别，因此需要一个单独用于开发调试的 Chrome
* Chrome 默认安装到 C 盘，移动到其他盘之后，再进行安装打开的仍是同一个浏览器

## 2、解决方法

主要就是利用 Chrome 的多用户会生成一个独立的、相互隔离的浏览器

### 方法一、自己指定存放数据路径(推荐)

1、进入 Chrome 所在目录(可以通过默认的快捷方式右击-属性-打开文件所在位置)，接着右击 Chrome，选择创建快捷方式

![创建快捷方式](https://cdn.wallleap.cn/img/pic/illustration/image-20200716091222532.png)

2、对创建的图标进行命名，右键属性

![属性](https://cdn.wallleap.cn/img/pic/illustration/image-20200716091419216.png)

3、目标字段：添加 `--user-data-dir` 参数，设置一个目标存放数据，笔者设置的是 `D:\ChromeData\WebChrome`

![修改目标](https://cdn.wallleap.cn/img/pic/illustration/image-20200716091648127.png)

4、确定（可以换一个图标再点确定！）

### 方法二、直接生成新用户快捷方式

 打开谷歌浏览器，点击如下的图标

![点击图标](https://cdn.wallleap.cn/img/pic/illustration/image-20200716092020261.png)

点击添加

![点击添加](https://cdn.wallleap.cn/img/pic/illustration/image-20200716092116598.png)

输入任意用户名，默认勾选添加快捷方式，点击添加

![](https://cdn.wallleap.cn/img/pic/illustration/image-20200716092240575.png)

之后就可以使用独立的 Chrome 了

![](https://cdn.wallleap.cn/img/pic/illustration/image-20200716092343187.png)

而且，你可以在开发工具中指定 Chrome 路径为你创建的快捷方式的路径，之后默认就会以该浏览器打开网页了

![IDE 指定 Chromepath](https://cdn.wallleap.cn/img/pic/illustration/image-20200716092823125.png)

### 方法三、直接创建新用户

Edge 日用，Chrome 专门作为调试的工具

* 默认的调试常规的前端项目
* React、Vue 调试中专门安装各自的调试插件

![](https://cdn.wallleap.cn/img/pic/illustration/202305261440805.png)

参考文档：

* [Chrome双开(同一个版本配置两个独立的浏览器,附图)](https://blog.csdn.net/lpw_cn/article/details/105574710)
* [启动多个独立谷歌浏览器](https://blog.csdn.net/QiaoRui_/article/details/86512063)
