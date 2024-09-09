---
title: mac 使用 Hexo 和 GitHub 搭建博客之博客维护
date: 2019-08-25 09:30
updated: 2019-08-25 09:30
cover: //cdn.wallleap.cn/img/pic/cover/202302tJDFmU.jpg
category: 技术杂谈
tags:
  - 博客
  - Hexo
description: mac 使用 Hexo 和 GitHub 搭建博客之博客维护
---

我们搭建好了博客，做好了美化，剩下的肯定就是默默的写文章啦，毕竟只有精品的文章才能更好地吸引流量啊

but 写好了文章，万一因电脑故障等原因博客根目录直接删除了咋办呢

博客文章还好，毕竟已经上传了，直接导下来转换一下就 OK 了，但是自己美化的和其他配置咋办

so 我们要做好备份

## 备份

首先在博客根目录 `git init` 创建 git 仓库，接着在 GitHub（或其他托管平台、自建远程仓库等）创建仓库并和本地仓库建立联系。

但是这个还是比较麻烦对吧

我们可以在 GitHub 上创建一个私有仓库，比如 MyBlog，接着执行

```shell
git clone 仓库地址
```

把仓库克隆下来，这样直接就绑定了，不需要再进行其他配置

接下来我们要做的就是把以前的博客根目录下除了 `.git` 的其他文件和目录都复制过来

需要备份的时候就直接运行

```shell
git add . && git commit -m "update" && git push -f
```

就 OK 啦

## 设置命令别名

通过 alias，触发一些命令的集合

在 `~/.bashrc` 或 `~/.zshrc` 文件中添加

```shell
alias hs='hexo clean && hexo g && hexo s'
alias hd='hexo clean && hexo g && hexo d && git add . && git commit -m "update" && git push -f'
```

需要在本地调试时直接运行 `hs` 即可

部署和备份运行 `hd`

## 添加站点统计代码

一般使用[百度统计](https://tongji.baidu.com/web/welcome/login)

## 站点 SEO 收录

首先每篇文章一定要写好标题、关键词、描述

谷歌和必应一般会自动收录，也可以自己到管理平台上添加

百度则需要自己到搜索资源平台添加

链接为 <https://ziyuan.baidu.com/dashboard/index>

首先添加自己的站点，找到添加网页关键词，点击

添入自己的信息

添加站点成功之后，点击侧边栏的快速收录/普通收录

有多种选择，我们就用主动推送和 sitemap

## 部署到个人服务器

建议使用宝塔面板，简单快捷

## 部署到国内服务器后的域名备案

可以使用阿里云的备案小助手或者腾讯云的备案小程序，都很方便

## 开放一定时间之后添加广告

可以接入百度联盟、谷歌广告、360 广告等

链接分别为：

- <https://union.baidu.com/>
- <https://www.google.cn/adsense/start/>
- <https://e.360.cn/>

直接注册即可，审核通过之后就可以添加广告了
