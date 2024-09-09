---
title: 利用 OneManager 和 Heroku 搭建自己的网盘
date: 2020-08-16 16:42
updated: 2020-08-16 16:42
cover: //cdn.wallleap.cn/img/pic/cover/202302YRbrWm.jpg
category: 技术杂谈
tags:
  - 教程
  - 网盘
description: 利用 OneManager 和 Heroku 搭建自己的网盘
---

白嫖搭建自己的网盘并进行适度美化

## 准备

最简单的两个就不放到教程里了

- 一个 Microsoft 账号（个人、E1、E5等都行）
- 一个 GitHub 账号(自行注册)

## fork 项目

项目地址：[OneManager-php](https://github.com/qkqpttgf/OneManager-php)

登录了 GitHub 并且进入该仓库之后，点击右上角的 `Fork`，如图所示

![Fork](https://cdn.wallleap.cn/img/pic/illustration/20200816170751.png)

Forking：

![Forking](https://cdn.wallleap.cn/img/pic/illustration/20200816170802.png)

fork 成功

![Fork到自己仓库中](https://cdn.wallleap.cn/img/pic/illustration/20200816170809.png)

## 注册 Heroku 账号

如果没有 heroku 账号，[点击这里进行注册](https://signup.heroku.com/login)（有的话跳过第二步）

这里注意下：邮箱 QQ、163 的都不行，可以用 outlook 或 gmail 的

![注册](https://cdn.wallleap.cn/img/pic/illustration/20200816170817.png)

填完之后点击验证，选出符合条件的图片，点击 `VERIFY`

![验证](https://cdn.wallleap.cn/img/pic/illustration/20200816170825.png)

验证通过之后点击 `CREATE FREE ACCOUNT`

![创建帐号](https://cdn.wallleap.cn/img/pic/illustration/20200816170832.png)

之后会向你的邮箱发送一条验证邮件

![邮件](https://cdn.wallleap.cn/img/pic/illustration/20200816170840.png)

收到之后点击里面的链接即可

![点击链接](https://cdn.wallleap.cn/img/pic/illustration/20200816170846.png)

将会打开一个页面，要求输入密码和确认密码

![输入密码](https://cdn.wallleap.cn/img/pic/illustration/20200816170856.png)

输入密码和确认密码之后，点击复选框，点击底下的按钮，之后点击如下红框中的按钮

![点击按钮](https://cdn.wallleap.cn/img/pic/illustration/20200816170905.png)

## 创建应用

点击 `Create new app` 创建应用

![创建应用](https://cdn.wallleap.cn/img/pic/illustration/20200816170911.png)

输入一个可用的 app 名字，点击 `Create app`

![输入信息](https://cdn.wallleap.cn/img/pic/illustration/20200816170919.png)

点击 GitHub

![GitHub](https://cdn.wallleap.cn/img/pic/illustration/20200816170927.png)

接着点击 `Connect to GitHub`

![连接](https://cdn.wallleap.cn/img/pic/illustration/20200816170934.png)

在弹出来的框中，点击 `Authorize heroku`

![认证](https://cdn.wallleap.cn/img/pic/illustration/20200816170941.png)

按照如下图所示的操作，输入 `OneManager` → 点击 `Search` → 点击 `Connect`

![Connect](https://cdn.wallleap.cn/img/pic/illustration/20200816170949.png)

等待一会之后往下划，点击 `Deploy Branch`

![部署](https://cdn.wallleap.cn/img/pic/illustration/20200816170957.png)

部署完成之后，点击 `View`

![查看](https://cdn.wallleap.cn/img/pic/illustration/20200816171004.png)

## 安装 OneManage

在弹出来的页面中点击超链接 `点击开始安装程序`

![开始安装](https://cdn.wallleap.cn/img/pic/illustration/20200816171011.png)

点击 `新建 API Key`

![新建 API Key](https://cdn.wallleap.cn/img/pic/illustration/20200816171019.png)

往下划，找到 `API Key` 字段，点击右边的 `Reveal`，接着把框框里的 `API Key` 复制一下

![Reveal](https://cdn.wallleap.cn/img/pic/illustration/20200816171026.png)

回到刚刚的页面，将复制的 `API Key` 粘贴进去，输入密码，点击确认

![确认](https://cdn.wallleap.cn/img/pic/illustration/20200816171033.png)

出现这个界面，点击左上角的登录

![登录](https://cdn.wallleap.cn/img/pic/illustration/20200816171040.png)

输入刚刚填的密码

![输入密码](https://cdn.wallleap.cn/img/pic/illustration/20200816171047.png)

将鼠标移到`管理`上，点击`设置`

![设置](https://cdn.wallleap.cn/img/pic/illustration/20200816171052.png)

按图中说明填写/选择

![填写表单](https://cdn.wallleap.cn/img/pic/illustration/20200816171100.png)

设置成功之后，点击刷新

![刷新](https://cdn.wallleap.cn/img/pic/illustration/20200816171108.png)

将会回到这里，点击 `添加 OneDrive 盘`

![添加](https://cdn.wallleap.cn/img/pic/illustration/20200816171114.png)

随便输入两个名称，点击第一个 Redio，点击复选框，自己申请

![填写](https://cdn.wallleap.cn/img/pic/illustration/20200816171123.png)

复制上图中的 uri，即：`https://scfonedrive.github.io/`

点击这个链接：<https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade>

登录你的 Microsoft 账户(个人、商用、学校都行)

![登录](https://cdn.wallleap.cn/img/pic/illustration/20200816171131.png)

点击图中所示`新注册`添加一个应用

![注册应用](https://cdn.wallleap.cn/img/pic/illustration/20200816171138.png)

应用名称随意，勾选第三个`任何组织目录`，URI那里粘贴刚刚复制的链接，点击注册

![注册](https://cdn.wallleap.cn/img/pic/illustration/20200816171145.png)

复制应用程序 id，粘贴到 `client_id` 中

![粘贴 id](https://cdn.wallleap.cn/img/pic/illustration/20200816171202.png)

点击左侧菜单栏中的`证书和密码`——>点击`新客户端密码`——>选择`从不`——>点击添加

![添加](https://cdn.wallleap.cn/img/pic/illustration/20200816171210.png)

复制这个值，粘贴到 `client_secret` 中

![secret](https://cdn.wallleap.cn/img/pic/illustration/20200816171218.png)

输入完成之后就可以点击确定了

![点击确定](https://cdn.wallleap.cn/img/pic/illustration/20200816171226.png)

等待一会，在这个页面，点击接受

![接受](https://cdn.wallleap.cn/img/pic/illustration/20200816171232.png)

等待两个页面跳转(没截到图)

之后再到你的网盘更目录下新建两个文件：`HEAD.md`、`README.md`，使用 markdown 语法，不会的话可以下载 [Typora](https://www.typora.io/)编写

![编写说明](https://cdn.wallleap.cn/img/pic/illustration/20200816171240.png)

其中 `HEAD.md` 中的内容会在头部显示，`README.md` 文件中的内容在下面显示

![说明显示](https://cdn.wallleap.cn/img/pic/illustration/20200816171245.png)

其他文件夹下也可以这样设置

如果需要加密某个文件夹，可以在文件夹中新建 `.password` 文件（按照你前面设置的），填入密码

```md
12345678
```

之后访问该文件夹就需要输入这个密码才能进入

![访问](https://cdn.wallleap.cn/img/pic/illustration/20200816171253.png)

提供了图床功能，允许游客上传文件，需要在设置中填入图床目录（先创建好）

![图床](https://cdn.wallleap.cn/img/pic/illustration/20200816171300.png)

可以添加多个网盘

自定义整个页面（如果觉得设置页面太丑可以自己写 CSS 美化）

其他功能自己去发掘

## 阿里云服务监控

点击[云监控](https://cloudmonitor.console.aliyun.com/)，登录，点击站点监控 → 站点管理

![云监控](https://cdn.wallleap.cn/img/pic/illustration/20200816171307.png)

点击新建监控任务

![监控任务](https://cdn.wallleap.cn/img/pic/illustration/20200816171314.png)

默认协议，随便输入一个名称，输入 herokuapp 的域名，选择 30 分钟，点击相应时间取消上面的可用性，点击 info

![域名](https://cdn.wallleap.cn/img/pic/illustration/20200816171322.png)

点击确认，这样你的 Herokuapp 就不会每次访问都非常慢了(不需要唤醒了)

好了，本次教程结束
