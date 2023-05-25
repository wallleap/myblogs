---
title: 主题 aurora 使用记录
date: 2020-08-06 08:00
updated: 2020-08-06 16:00
cover: //cdn.wallleap.cn/img/pic/cover/202302MjGRMc.jpg
category: 技术杂谈
tags:
  - 主题
  - 博客
description: 记录一下基于 GitHub API 的博客主题的使用
---

使用 GitHub API 做博客接口是个非常好的想法，以后也想弄一个，先记录一下 Aurora 使用

> Aurora 是一款动漫风格博客主题，基于 Vue 开发，使用开源的 Github Api 服务。
>
> 相较于 Wordpress 和 Typecho 等博客框架，Aurora 主题最大的优势就是简单轻量与免费，全部使用现有开源免费服务，相对稳定，也不怕 Github 跑路（笑），文章发布与更新也是相当简单，不需要操作服务器与数据库，对新人来说非常友好。

## 一、初始化环境

先安装 Nodejs 和 Git 环境。

Nodejs 的版本最好使用 12 的，这个可以使用 NVM 这种的 Node 版本管理工具切换

由于 Aurora 使用 vue 开发，所以需要**安装 vue-cli**：

```bash
npm install -g @vue/cli-service-global
```

然后将主题 clone 到本地并安装依赖包：

```bash
# clone 主题
git clone git@github.com:chanshiyucx/aurora.git
 
# 进入主题目录
cd aurora

# 安装依赖包
npm install

# 本地预览
npm start
```

依赖包安装完毕，便可执行 `npm start` 本地预览效果，访问 <http://localhost:8080/>, 现在看到的是蝉时雨的博客，接下来需要我们自定义主题。

## 二、替换站点标题和图标

首先修改站点标题和图标，替换主题目录 `public/assets` 下的图标资源，然后修改 `public/index.html` 的站点标题和描述。

```html
<html lang="zh-Hans">
  <head>
    ……
    <meta name="author" content="Luwang" />   <!-- 作者，改为自己名字 -->
    <meta name="description" content="Luwang's Blog, Fighting" />  <!-- 站点描述 -->
    <meta name="keywords" content="Code, 前端, Aurora, web, 学习, blog, 博客, hackintosh, 黑苹果" />  <!-- 关键词 -->
    <link rel="apple-touch-icon" sizes="180x180" href="<%= BASE_URL %>assets/apple-touch-icon.png" />
    <link rel="icon" type="image/png" sizes="16x16" href="<%= BASE_URL %>assets/favicon-16x16.png" />
    <link rel="icon" type="image/png" sizes="32x32" href="<%= BASE_URL %>assets/favicon-32x32.png" /> <!-- 这三张在public/assets下，替换为自己的站点图标 -->
    <link rel="dns-prefetch" href="//cdn.jsdelivr.net" />
    <link rel="dns-prefetch" href="//i0.hdslb.com" />
    <link rel="dns-prefetch" href="//myblog.wallleap.cn" /> <!-- 改为自己的域名 -->
    ……
    <title>wallleap | Luwang's Blog</title> <!-- 改为自己的博客名称 -->
  </head>

```

## 三、配置主题

主题配置文件为根目录下 `src/config.js`，里面每个配置项皆有详细注释，按照注释修改即可

### 1、配置文章仓库

Aurora 使用 Github API 做后台数据托管。所以需要新建一个仓库来存放文章和一些自定义页面内容。这里新建一个仓库取名为 Blog 为例。

由于 Github API 有访问次数限制，所以需要申请 token 来解除访问限制，申请地址戳这里。将申请的 token 从中间随意拆成两部分填入配置项，拆分的目的避免代码提交的时候 GitHub 对其进行检测，导致 token 失效。

![](https://cdn.wallleap.cn/img/pic/illustration/202305230913789.png)

```javascript
// GitHub 用户名
username: 'wallleap',
// 仓库名
repository: 'blog',
// token 从中间任意位置拆开成两部分，避免 github 代码检测失效
token: ['0ad1a0539c5b96fdxxxx', 'xxxxxxxc7d1362a5746c'],
```

### 2、配置 Leancloud

Aurora 主题的文章阅读次数与 Valine 评论系统都是采用 Leancloud 存储。

注册一个 LeanCloud 账号（注意选择国际版）并新建一个应用，将应用 key 填入相应配置项。 然后创建三个 Class，Comment 用来存储游客评论、Counter 用来存储文章热度、Visitor 用来统计友链访问次数，注意新建时选择表的访问权限无限制。

![](https://cdn.wallleap.cn/img/pic/illustration/202305230913552.png)

```javascript
leancloud: {
   appId: 'APPID',
   appKey: 'APPKEY'
 }
```

### 3、配置 Gitalk

> 首先需要申请 GitHub Application，跳转地址填写你的博客域名，如果你使用 GitHub Pages 来托管你的网站，你也可以使用 <https://用户名.github.io> 域名。最后将生成的 Client ID 和 Client Secret 填入相应配置项。在开发环境调试时 Gitalk 无法展示是正常现象，发布到线上后会正常显示。

![](https://cdn.wallleap.cn/img/pic/illustration/202305230914031.png)

![](https://cdn.wallleap.cn/img/pic/illustration/202305230914674.png)

```js
gitalk: {
   clientID: '864b1c2cbc4e4aad9ed8',
   clientSecret: '6ca16373efa03347e11a96ff92e355c5cea189bb',
   repo: 'Comment', // 你的评论仓库
   owner: 'chanshiyucx', // 你的 github 账户
   admin: ['chanshiyucx'], // 你的 github 账户
   distractionFreeMode: false // 是否开始无干扰模式【背景遮罩】
}
```

### 4、页面配置

这些注释都写的很清楚，归档、分类、标签、灵感、书单、友链页基本不需要修改(如果需要的话，可以把`qoute`的内容修改下)

```
archiveOpts: {
    display: true, // 是否显示该页面
    enableComment: false, // 是否开启评论功能
    qoute: '華枝春滿 天心月圓', // 页面顶部一言
  },
```

关于页面就需要进行修改了

```javascript
   /**
   * 关于页面
   */
  aboutOpts: {
    display: true,
    enableComment: true,
    qoute: '千里之行 始于足下',
    avatar: '//cdn.wallleap.cn@latest/img/custom/avatar.jpg',   // 头像
    graduated: 'East China University of Technology (ECUT)',  // 毕业学校
    college: 'Network Engineering',  // 专业
    contact: [ // 联系方式
      {
        icon: '//cdn.jsdelivr.net/gh/chanshiyucx/yoi/blog/email.png',   // 这个是图标，可以改为自己喜欢的联系方式图标
        // link: 'http://mail.qq.com/cgi-bin/qm_share?t=qm_mailme&email=tNnR9Nfc1drH3N3NwZrX29k',
        link: 'mailto:15579576761@163.com', // 邮箱可以修改为这个
      },
      {
        icon: '//cdn.jsdelivr.net/gh/chanshiyucx/yoi/blog/github.png',
        link: 'https://github.com/wallleap',   // GitHub地址
      },
      {
        icon: '//cdn.jsdelivr.net/gh/chanshiyucx/yoi/blog/telegram.png',
        link: 'https://t.me/wallleap',   // telegram，没有可以更换为其他的，比如B站
      },
      {
        icon: '//cdn.jsdelivr.net/gh/chanshiyucx/yoi/blog/music.png',
        link: 'https://music.163.com/#/user/home?id=453867086',  // 网易云音乐
      },
      {
        icon: '//cdn.jsdelivr.net/gh/chanshiyucx/yoi/blog/rsshub.png',
        link: 'https://rsshub.app/github/issue/chanshiyucx/blog',  // 万物皆可RSS
      },
    ],
  },
```

### 5、加载动画

可以设置为自己喜欢的动态图片，但可能需要修改样式

```javascript
   /**
   * 加载动画
   */
  loadingImg: '//cdn.wallleap.cn/img/pic/illustration/loading.gif',
```

### 6、默认头图

修改链接即可，如果编写文章的时候没有设置头图，～～则会显示这个(设置了则会动态轮播)～～则会报错，默认头图只是在加载的时候会暂时代替文章封面，因此一定记得在每篇文章加上封面(后面讲)

```javascript
  /**
   * 文章默认图
   */
  defaultCover: '//cdn.wallleap.cn/img/banner/time.jpg',
```

### 7、捐赠(赛钱箱)配置

放了也不一定有人扫，扫了也不一定会付

```javascript
  /**
   * 赛钱箱
   */
  qrcode: [
    {
      name: '支付宝',
      img: '//cdn.wallleap.cn/img/custom/donate/AliPayQR.jpg', // 自己支付宝的二维码
    },
    {
      name: '微信',
      img: '//cdn.wallleap.cn/img/custom/donate/WeChatQR.jpg', // 微信收款或打赏二维码
    },
  ],
```

### 8、音乐播放器

```javascript
  /**
   * 音乐播放器,
   */
  APlayer: [
    {
      name: 'うたかたの风と蝉时雨',   // 歌曲名
      artist: 'Little Planet', // 歌手
      url: 'https://files.catbox.moe/wo7zjt.mp3', // 音乐地址
      cover: '//cdn.jsdelivr.net/gh/chanshiyucx/yoi/blog/cover1.jpg', // 图片
    },
    {
      name: '春の凑に',
      artist: 'TUMENECO',
      url: 'https://files.catbox.moe/ducy49.mp3',
      cover: '//cdn.jsdelivr.net/gh/chanshiyucx/yoi/blog/cover2.jpg',
    },
  ],
```

### 9、主题颜色

主要是两个地方：变量.scss(自行修改)和配置.js

```javascript
  /**
   * 主题配色，主要用于文章、灵感、关于等卡片配色
   * 推荐一个超棒的取色站，日本の伝統色：http://nipponcolors.com/
   */
  themeColors: [
    '#B28FCE', // 薄
    '#86C166', // 苗
    '#F596AA', // 桃
    '#F19483', // 曙
    '#F9BF45', // 玉子
    '#FAD689', // 浅黄
    '#E79460', // 洗柿
    '#2EA9DF', // 露草
    '#FB966E', // 洗朱
    '#BC9F77', // 白茶
    '#867835', // 黄海松茶
    '#B9887D', // 水がき
  ],
```

`config.js`文件就配置到这里了

## 四、友链页修改

大部分页面不需要修改，但是有些还保留了开发者的信息，需要修改为自己的，就比如友链页

要修改的文件是 `src/views/Friend/index.vue`

我们需要将下面这部分内容修改为自己的：

```vue
<div class="me">
          <span>欢迎各位大佬交换友链 (づ￣ 3￣)づ</span>
          <span>★ Bio：wallleap</span>
          <span>★ Motto：Luwang's Blog</span>
          <span>★ URL：https://myblog.wallleap.cn/</span>
          <span
            >★ Avatar：<a href="https://cdn.wallleap.cn@latest/img/custom/avatar.jpg" target="_blank"
              >点击获取</a
            ></span
          >
          <span>※ 以下友链按博主互访频率排序，并根据个人对博客内容喜好加权，博主将不定期更新排序并过滤阵亡名单。</span>
        </div>
```

## 五、定制化组件

可以对组件进行修改

比如修改Footer页脚信息 `src/components/Footer.index.vue`

```vue
<div class="site-info">
      <p>
        Blog {{ $config.title }}, Copyright &copy; 2019-2020 by Luwang
        <i class="icon icon-heart"></i> All Rights Reserved.
      </p>
      <p>
        Theme -
        <a rel="noopener noreferrer" target="_blank" href="https://github.com/chanshiyucx/aurora">Aurora</a>
        by <a  rel="noopener noreferrer" target="_blank" href="https://chanshiyu.com/">chanshiyu</a> |
        Hosted by <a>Github Pages</a> |
        {{ $config.subtitle }}
      </p>
    </div>
```

还有前面说过的 loading，如果修改了图片，但是显示太小的话，可以修改 `src/components/Loading/index.vue`，将 `width` 修改到合适的大小即可

```vue
<style lang="scss" scoped>
.loading {
  @include pc-layout {
    margin: 100px auto;
    width: 514px;
  }
  @include sp-layout {
    margin: 150px auto;
    width: 514px;
  }
}
</style>
```

## 六、本地预览并部署到GitHub

### 1、本地预览

使用命令 `npm start` 开启本地服务器，进入 <http://localhost:8000/> 预览页面，如果没有报错，预览结果与预期的相符那么就可以进行下一步了

### 2、部署

开发者提供了 deploy.sh 文件，可以一键部署(Linux、Mac)，Win 可以改写为 bat 批处理文件

因为这个修改好之后上传一次就可以了，我们也可以一步步输入命令：

1. 构建

```bash
npm run build
```

将会生成dist文件夹

2. 进入dist文件夹

```bash
cd dist
```

3. 配置自定义域名[可选]

修改 `public/CNAME` 文件，写上你自定义的域名,或者在仓库设置里修改

eg:

```
myblog.wallleap.cn
```

如果不需要(就使用 xxx.github.io)可以将这个文件删除

4. 部署到github

前提是你已经配置好了本地环境(用户名、邮箱)

```bash
git init && git add -A && git commit -m 'deploy'
```

上面这条命令不需要修改

下面这条修改好了再回车

```bash
git push -f git@github.com:用户名/用户名.github.io.git master
```

本地就彻底不需要再操作了(除非你还要修改主题文件)，剩下的到 GitHub 操作

## 七、创建页面

这里指的是菜单栏中的后面几项(提示：这几个 Issue 都需要设置为 close)

### 1、书单页面

进入 GitHub，到你的 Blog 仓库下，点击 `New Issue` 新建一个 Issue

![](https://cdn.wallleap.cn/img/pic/illustration/20200807131455.png)

点击文本框右边的 Labels 右边的齿轮图标，输入 `Book`，点击 **Create new label "Book"**，只要求名字是 Book，描述和颜色任意

![](https://cdn.wallleap.cn/img/pic/illustration/20200807132454.png)

标题为`书单`，内容按下面格式填写

![](https://cdn.wallleap.cn/img/pic/illustration/20200807132024.png)

注意第二行的空行，每一项后面也需要空一行，不会的话可以直接去 copy [蝉时雨大佬的](https://github.com/chanshiyucx/blog/issues/4)

```
## ES6 标准入门

author: 阮一峰
published: 2017-09-01
progress: 正在阅读...
rating: 5,
postTitle: ES6 标准入门
postLink: //chanshiyu.com/#/post/12
cover: //chanshiyu.com/yoi/2019/ES6-标准入门.jpg
link: //www.duokan.com/book/169714
description: 柏林已经来了命令……
```

填写完成之后，提交，之后划到最底下，点击 `Close Issue`，书单页面就 OK 了

![](https://cdn.wallleap.cn/img/pic/illustration/20200807133406.png)

### 2、灵感页

书写格式没有要求，注意标签是 `Inspiration`(自己创建哦)，Issue 状态设置为 `closed`

![](https://cdn.wallleap.cn/img/pic/illustration/20200807133740.png)

以后每写一个 Issue，只要加上标签 `Inspiration`，设为 `closed`，就能出现在灵感页

### 3、友链页

有格式要求，二级标题(即小伙伴的网站名)后需要加空行，一项写完了需要补充上空行

```
## wallleap
 
link: //myblog.wallleap.cn/
cover: //i.loli.net/2018/12/15/5c14f329b2c88.png
avatar: //i.loli.net/2018/12/15/5c14f3299c639.jpg
```

Label 为 `Friend`，issue 状态仍是 `close`

![](https://cdn.wallleap.cn/img/pic/illustration/20200807134557.png)

### 4、关于页

最好按照一个二级标题带着一堆文字(图片)的形式写，Label 为 `About`，Issue 要 close

![](https://cdn.wallleap.cn/img/pic/illustration/20200807135052.png)

页面的就到这里了

## 八、初始化评论模块

如果前面 gitalk 配置没有出错，那么这里很容易就可以开启

首先进入需要开启评论的页面，点击`使用 GitHub 登录`

![](https://cdn.wallleap.cn/img/pic/illustration/20200807140627.png)

接着在弹出来的页面中认证

![](https://cdn.wallleap.cn/img/pic/illustration/20200807140751.png)

之后确认密码，之后就可以评论了

![](https://cdn.wallleap.cn/img/pic/illustration/20200807140820.png)

## 九、写文章

### 1、文章模板

文章标题任意，内容在第一行加上：

```md
[这里随便写啥]: # 'https://raw.githubusercontent.com/chanshiyucx/yoi/master/bg/3.jpg'
```

这样就会显示文章封面了，你可以随意修改图片链接为自己的

Labels 只要不设置为上面四个页面的即可（用来标识标签，例如标签为 blog，则可设置为 **Labels: blog**），接下来会接着讲 Labels

Issue 状态不需要 close，保持 `open` 即可

### 2、文章标签和分类

之前已经说过 `Labels` 标识文章标签

而文章分类用 `Milestone` 来标识

除了在创建 Issue 的时候创建 Labels 和 Milestone，还可以先创建好，等到写文章的时候直接选用

在仓库的 Issue 页，能够看到下图所示的两个单词，任意点击一个可以进行设置

![](https://cdn.wallleap.cn/img/pic/illustration/20200807142431.png)

比如 Labels，可以点击 `New label` 新建标签，点击某标签右边的 `Edit` 对标签进行修改、`Delete` 删除

![](https://cdn.wallleap.cn/img/pic/illustration/20200807142636.png)

Milestone 页点击 `New milestone` 添加一个分类

![](https://cdn.wallleap.cn/img/pic/illustration/20200807142825.png)

格式如下：

![](https://cdn.wallleap.cn/img/pic/illustration/Aurora%25E5%2588%2586%25E7%25B1%25BB.png)

### 3、文章中的图片

为了达到最佳的图片显示效果，可以在图片链接之后加上 `?vw=宽&vh=高` 来限定图片大小

例如下面这几张：

```
![](https://cdn.jsdelivr.net/gh/chanshiyucx/yoi@latest/2019/Aurora-%E9%A3%9F%E7%94%A8%E6%8C%87%E5%8D%97/%E6%96%87%E7%AB%A0%E6%A8%A1%E6%9D%BF.png?vw=1335&vh=669)
![](https://cdn.jsdelivr.net/gh/chanshiyucx/yoi@latest/2019/Aurora-%E9%A3%9F%E7%94%A8%E6%8C%87%E5%8D%97/%E9%A1%B5%E9%9D%A2%E6%A8%A1%E6%9D%BF.png?vw=825&vh=306)
![](https://cdn.jsdelivr.net/gh/chanshiyucx/yoi@latest/2019/Aurora-%E9%A3%9F%E7%94%A8%E6%8C%87%E5%8D%97/Aurora%E5%88%86%E7%B1%BB.png?vw=880&vh=439)
```

这样子的话既可以用 GitHub 当博客，也可以调用这个 API 做一个单独的博客站点（甚至可以把博文放到仓库中同步到 GitBook，直接生成网页）
