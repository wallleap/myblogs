---
title: mac 使用 Hexo 和 GitHub 搭建博客之开始搭建
date: 2019-08-24 20:14
updated: 2019-08-24 20:14
cover: //cdn.wallleap.cn/img/pic/cover/202302tJDFmU.jpg
category: 技术杂谈
tags:
  - 博客
  - Hexo
description: mac 使用 Hexo 和 GitHub 搭建博客之开始搭建
---

利用 hexo 搭建博客并上传到 GitHub，利用 GitHub Pages 访问

## 一、安装

### （一）git 安装及 GitHub 注册

1、安装 git

命令安装 git 需要先安装好 homebrew 和 XCode(可以先在 APP Store 下载)：

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
# 如果不需要完整版 XCode 也可以只安装 Command Line Tools
xcode-select --install
```

安装git：

```shell
brew install git
```

2、注册 GitHub 帐号

进入 [GitHub官网](https://github.com)，Sign up 页面输入相关信息，没有错误之后点击 <font color="green">Sign up for GitHub</font>，注册账号

![2-1](https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/pic/mac-blog1/github1.png)

接着点击右上角头像，点击 Your repositories

![2-2](https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/pic/mac-blog1/github2.png)

到达仓库(repositories)界面，点击 <font color="green">New</font>

![2-3](https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/pic/mac-blog1/github3.png)

如图 2-4，前面是用户名，仓库名设置为 `用户名.github.io`，点击 <font color="green">Create repository</font>，创建仓库

![2-4](https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/pic/mac-blog1/github4.jpg)

接着进入图 2-5 界面，左边的暂时不用管，直接点击头像

![2-5](https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/pic/mac-blog1/github5.jpg)

点击 Settings

![2-6](https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/pic/mac-blog1/github6.jpg)

点击左侧导航栏中 SSH and GPG keys

![2-7](https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/pic/mac-blog1/github7.jpg)

接着打开 iTerm2 或者终端输入以下命令

```sh
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱地址"
ssh-keygen -t rsa -C "你的邮箱地址"   #需要回车4次左右
cat ~/.ssh/id_rsa.pub
```

将文件中的 key 复制下来

回到网页，单击 <font color="green">New SSH key</font>

![2-8](https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/pic/mac-blog1/github8.jpg)

`Title` 随意填，将刚复制的 key 粘贴到 `Key` 的文本框中，点击 <font color="green">Add SSH key</font>

3、测试

输入命令 `ssh -T git@github.com`，显示如下字样，说明连接成功

![3](https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/pic/mac-blog1/github9.png)

### （二）安装 node.js

在上一步基础上可以直接使用 homebrew 下载安装 node.js，输入命令：

```sh
brew install node
```

### （三）安装 Hexo

安装好 git 和 node.js 之后就可以使用 npm 安装 Hexo 了

```sh
npm install -g hexo-cli
```

如果报的不是关键性错误，可以跳过不管，直接下一步

## 二、Hexo 初始化及本地测试

### 1、初始化 Hexo

创建一个目录用来作为你的 blog 目录，例如 blog；并在该目录中进行 Hexo 的初始化：

```sh
hexo init blog
cd ~/blog
npm install
```

### 2、本地测试

先安装 hexo server

```sh
sudo npm install hexo-server 
```

然后生成静态页面并打开 hexo 本地服务

```sh
hexo generate   # 或 hexo g
hexo server
```

按命令行提示，打开 <http://localhost:4000> 即可测试代码了。 

## 三、配置

### 1、关联 GitHub 账户

进入 blog 目录，编辑该目录下 `_config.yml` 文件

```sh
cd ~/blog
vi _config.yml
```

修改最下方的 `deploy` 字段：

```sh
deploy:
  type: git
  repo: git@github.com:y/用户名.用户名github.io.git   #将你刚刚创建的仓库地址复制过来
  branch: master
```

接下来安装 hexo 的 git 部署，在命令行中执行：

```sh
npm install hexo-deployer-git --save
```

最后，将生成静态页面并部署到 GitHub 的仓库中，执行：

```sh
hexo generate
hexo deploy
```

或者

```sh
hexo d -g
```

### 2、基本配置

详情见[配置](https://hexo.io/zh-cn/docs/configuration)

以下是基本的配置

```sh
# Hexo Configuration
## Docs: https://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/
# Site  ##页面信息
title: Who's Blog  ##标题，即浏览器标签栏显示的内容
subtitle: Why so serious?  ##副标题
description:        ##描述，简介
author:        ##作者
language: zh-CN  ##语言
timezone: Asia/Shanghai  ##时区

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://用户名.github.io              ## 有些人说这里填域名，可是后面需要用到图片的相关插件，这里填写这个即可
root: /   ## 这里如果你就是在 用户名.github.io 仓库则不用管，如果是 blog 仓库则需要改成 /blog
permalink: :year/:month/:day/:title/
permalink_defaults:

# Directory  ##文件目录，可不改
source_dir: source
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang
skip_render:
# Writing  ##静态页面生成属性，可不改
new_post_name: :year-:month-:day-:title.md # File name of new posts
default_layout: post
titlecase: false # Transform title into titlecase
external_link: true # Open external links in new tab
filename_case: 0
render_drafts: false
post_asset_folder: true   # 后面图片插入需要用到的
relative_link: false
future: true
highlight: 
enable: true 
line_number: true 
auto_detect: false 
tab_replace:

# Category & Tag ##标签，可不改
default_category: uncategorized
category_map:
tag_map:
# Date / Time format  ##时间格式，可不改
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss

# Pagination ##每页显示文章数，按需改
## Set per_page to 0 to disable pagination
per_page: 10
pagination_dir: page
# Extensions ##主题设置
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: 3-hexo  ## 主题使用 3-hexo

# Deployment  ##git部署关联
## Docs: https://hexo.io/docs/deployment.html
deploy: 
type: git 
repo: github: https://github.com/用户名/用户名.github.io.git
branch: master
```

### 3、主题配置

#### 主题下载

到 [Hexo 的主题库](https://hexo.io/themes/)中挑选一个主题，比如 3-hexo，首先找到[主题的仓库地址](https://yelog.org/2017/03/07/3-hexo/)，将文件克隆到 `themes` 目录下：

```sh
git clone https://github.com/yelog/hexo-theme-3-hexo.git themes/3-hexo
```

#### 安装插件

安装 Less，主题使用 Less 作为 CSS 预处理工具：

```sh
npm install hexo-renderer-less --save
```

安装 feed，用于生成 RSS：

```sh
npm install hexo-generator-feed --save
```

安装 json-content，用于生成静态站点数据，提供搜索功能的数据源：

```sh
npm install hexo-generator-json-content --save
```

安装字数统计(由于主题使用这个插件，必须安装，否则会报错)

```sh
npm i --save hexo-wordcount
```

安装搜索插件

```sh
npm install hexo-generator-search --save
```

安装图片插件

```sh
npm install hexo-assert-folder --save
```

#### 新建页面

```sh
hexo new page tags    #开启标签页
hexo new page about。    #开启“关于”页
hexo new page categories #分类
hexo new page 404     #404
```

分别修改各个页面的源数据：

`blog/source/tags/index.md`

```sh
---
title: tags
date: 2019-08-24 14:56:43
layout: tags
noDate: true
comments: false
---
```

`blog/source/about/index.md`

```sh
---
title: about
date: 2019-08-24 19:27:02
---
```

`blog/source/categories/index.md`

```sh
---
title: categories
date: 2019-08-24 20:21:00
---
```

`blog/source/404/index.md`

```sh
---
title: 404
permalink: /404
date: 2019-08-24 17:56:50
---
---
## 页面未找到！
```

#### 修改 hexo 配置文件 `_config.yml` 中的主题标签

```sh
theme: 3-hexo
highlight:
  enable: false #关闭hexo渲染高亮，使用主题代码块高亮
```

#### 修改主题配置文件 `blog/themes/3-hexo/_config.yml`

[https://yelog.org/2017/03/07/3-hexo/](https://yelog.org/2017/03/07/3-hexo/)

在 hexo 根目录 source 下添加 avatar.jpg 文件，作为头像

## 四、测试后上传

### 1、测试

```sh
hexo g
hexo server
```

访问 <http://localhost:4000/>，没有问题就可以部署上传了

### 2、部署上传

```sh
hexo d -g
```

### 3、访问网页

在浏览器输入地址：`http://用户名.github.io` 即可访问
