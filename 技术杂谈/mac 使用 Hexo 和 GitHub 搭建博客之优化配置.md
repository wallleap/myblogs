---
title: mac 使用 Hexo 和 GitHub 搭建博客之优化配置
date: 2019-08-24 20:21
updated: 2019-08-24 20:21
cover: //cdn.wallleap.cn/img/pic/cover/202302tJDFmU.jpg
category: 技术杂谈
tags:
  - 博客
  - Hexo
description: mac 使用 Hexo 和 GitHub 搭建博客之优化配置
---

优化博客根目录和主题下配置文件

## 一、修改 `_config.yml`

搭建博客的时候顺便改了下基本的配置，现在来看下这些配置修改

`~/blog/_config.yml`

这个是全局的配置文件，[上一个博客](../mac 使用 Hexo 和 GitHub 搭建博客之开始搭建/index.html)已经讲的很清楚了，这里不再赘述

由于需要用主题 3-hexo 高亮代码，将这里的高亮渲染关闭

```sh
highlight:
    enable: false
```

`~/blog/themes/3-hexo/_config.yml`

这个是主题的配置文件，仅给出需要修改的地方

你的头像 url

需要到 `～/blog/themes/3-hexo/source/img` 下把 avatar.jpg 替换为自己头像

```md
avatar: /img/avatar.jpg
favicon: /img/avatar.jpg
```

博客根目录，如果没有错误不需要修改，如果部署后样式丢失，一般就是这里错了，可能需要改成 `/仓库名`

```sh
blog_path: /
```

链接图标，将链接全部改为自己的即可

 ```sh
csdn: https://me.csdn.net/qq_36949103
```

多作者模式，按需求填写

```sh
author:
    on: false
    authors:
        author1: luwang
        author2: wallleap
```

分类文章数、多级分类 按需启用 

```sh
category:
    num: true # 分类显示文章数
    sub: true # 开启多级分类
```

文末声明  改为自己的

```sh
article_txt: 
```

打赏功能  需要到 `～/blog/themes/3-hexo/source/img` 下把 weixin.jpg 和 alipay.jpg 替换为自己微信和支付宝收款码

```sh
reward: true
```

其他的都有说明，自己看着修改就行

评论系统启用方式：[完美替代多说-gitment](https://yelog.org/2017/06/26/gitment/)

## 二、优化页面

### 1、主页 `~/blog/themes/3-hexo/indexs.md`

由于是 md 文件，因此可以按照正常的 Markdown 语法进行修改

### 2、发布页模板 `~/blog/scaffolds/post.md`

为了以后写博文方便，可以按照习惯修改模板，我的模板如下：

```sh
---
title: {{ title }}
date: {{ date }}
tags: 
    - tag1
    - tag2
categories: 
    - category1
    - category2
---
```

标签改为多标签，分类为二级分类

### 3、其他页面

```sh
hexo new page "about"
```

还有 category 等都可以添加

about 页还需要修改主题 `_config.yml`：

![](https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/pic/mac-blog2/pic1.jpg)

## 三、域名解析

### 1、域名解析

进入到购买域名的控制台，找到域名服务或解析服务

![](https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/pic/mac-blog2/pic2.jpg)

点击自己域名后的解析设置

![](https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/pic/mac-blog2/pic3.jpg)

点击添加记录

![](https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/pic/mac-blog2/pic4.jpg)

按照下图填写，注意记录值填 `自己的用户名.github.io`

![](https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/pic/mac-blog2/pic5.jpg)

也可以再添加主机记录用 www 的，这样输入 www 也能访问

![](https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/pic/mac-blog2/pic6.jpg)

### 2、添加文件

做完了解析工作还是不行的，需要在仓库加上 CNAME 文件，文件中只需要填写域名，比如我的：

![](https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/pic/mac-blog2/pic7.jpg)

由于仓库中上传时会自动删除，因此放到 `~/blog/source/` 下

## 四、评论系统

上面主题配置中有提到过，但对于一个博客而言，评论部分是不可或缺的，因此将其单独说明。

由于本人只用过 `gitment` 和 `gitalk`，而个人感觉 `gitalk` 更好用一点，因此这里介绍 `gitalk` 使用，上面有 `gitment` 的教程链接

首先打开主题配置文件(`~/blog/themes/3-hexo/_config.yml`)，找到评论设置，将 `comment` 字段的 `on` 设为 `true`，`type` 设为 `gitalk`。找到 `gitalk` 字段，添加 `on:true`,其他的评论系统字段添加 `on:false`.接着打开链接 [https://github.com/settings/applications/new](https://github.com/settings/applications/new)，登录 GitHub 账户

![](https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/pic/mac-blog2/pic8.jpg)

注意 callbalk URL 一定要是自己域名的地址，接着点击绿色按钮，把 Client ID 和 Client Secret 复制到主题配置文件的 gitalk 字段相应位置，接着 githubID 和 adminUser 填自己的用户名即可，repo 填博客的仓库(即`用户名.github.io`)

![](https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/pic/mac-blog2/pic9.jpg)

## 五、博客美化

### 1、了解hexo博客layout

### 2、修改layout中各布局代码

### 3、css美化

### 4、其他小部件
