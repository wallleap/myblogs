---
title: 信息杂乱，终究还是需要 RSS
date: 2024-03-19 20:28
updated: 2024-03-19 20:28
cover: //cdn.wallleap.cn/img/pic/cover/rss.jpg
category: 生活随笔
tags:
  - RSS
  - 阅读
description: 信息杂乱，终究还是需要 RSS
---

之前还是很排斥 RSS 的，因为从没有真正去用过它，每次都只是随便添加一两个订阅就完事。但是最近通勤的时候没事做，想看看一些资讯、博客文章。

通过最近的翻阅、查看，发现公众号、微博、掘金等有很多杂乱的信息，都是自己不太想看的，但标题起得“很有韵味”，点进去之后就马上又退出，浪费时间。

这个时候就想到了 RSS 订阅的好处了，但现在支持 RSS 的站点挺少的。

刚巧几年前用过 RSSHub，它可以对不支持的站点生成 RSS，然后兴致冲冲打开官网 <https://rsshub.app/>，发现直接访问不了，翻一下之后发现它提供了更多的公共实例可使用。

## 部署 RSSHub

担心其他的实例可能会失效，因此决定自己通过 Docker 部署一个。

直接运行命令：

```sh
docker run --name rsshub -p 12000:1200 -v /www/wwwroot/rsshub.wallleap.cn:/app/data -d diygod/rsshub
```

执行完成之后开放一下 `12000` 端口，通过 `IP:12000` 能够正常访问。

接着使用 Nginx 进行反向代理 `proxy_pass http://127.0.0.1:12000;`，配置一下域名解析和 SSL，就能够通过域名 <https://rsshub.wallleap.cn> 访问啦。

## 生成一个订阅源

具体的链接拼接可以前往 <https://docs.rsshub.app/zh/guide/>

现在以我的 GitHub 博客仓库 Issue 为例

找到 GitHub Issue 相关的，查看例子和路由

![image-20240319210219528](https://cdn.wallleap.cn/img/pic/illustration/202403192102654.png)

`:` 开头的需要进行替换，`?` 结尾的可省略，我的仓库是 `wallleap/myblogs`

所以直接替换上去，拼接上自己的域名就是 <https://rsshub.wallleap.cn/github/issue/wallleap/myblogs>

接着按照这种方式拼接更多需要的订阅源

## 在手机上添加订阅源

我应当不会在电脑上去看这个，所以直接介绍手机上的操作

使用的 APP 为 [Feeder: Android RSS reader app](https://github.com/spacecowboy/Feeder)

![](https://cdn.wallleap.cn/img/pic/illustration/202403192125996.png)

进入应用后点击右上角三个点，添加订阅，输入订阅地址，点击搜索，出现结果后点击

![](https://cdn.wallleap.cn/img/pic/illustration/202403192131857.png)

填写标题、标签，启用新内容通知，点击确认

进入订阅页面后下滑刷新，之后就能获取到订阅内容了

## 订阅源

### 资讯类

- 中国日报・时政：`http://feedmaker.kindle4rss.com/feeds/china.chinadaily.xml`
- 中国日报・资讯：`https://plink.anyfeeder.com/chinadaily/world`
- 人民网-国际新闻：`https://plink.anyfeeder.com/people/world`
- 联合早报：`https://plink.anyfeeder.com/zaobao/realtime/china`
- 联合早报・国际：`https://plink.anyfeeder.com/zaobao/realtime/world`
- 澎湃新闻：`https://plink.anyfeeder.com/weixin/thepapernews`
- 纽约时报中文：`https://cn.nytimes.com/rss.html`
- BBC News：`https://rss.app/feeds/DkgMdvgltCDIbX6d.xml`

### 博客

- 阮一峰：`https://www.ruanyifeng.com/blog/atom.xml`
- 张鑫旭：`https://www.zhangxinxu.com/wordpress/feed/`
- Antfu：`https://antfu.me/feed.xml`

### 技术类（论坛/平台）

- V2ex：`https://v2ex.com/index.xml`
- Hacker news：`https://hackernewsrss.com/feed.xml`
- 掘金・前端：`https://rsshub.app/juejin/category/frontend`
- 人人都是产品经理日榜热门：`https://webfollow.cc/channel/plink.anyfeeder.com/woshipm/popular`

- 知乎每日精选：`http://www.zhihu.com/rss`
- 知乎日报：`http://feeds.feedburner.com/zhihu-daily`

### 阅读

- 十点读书：`https://plink.anyfeeder.com/weixin/duhaoshu`
- 观止-每日一文：`https://plink.anyfeeder.com/meiriyiwen`

### B 站

待拼接：`https://rsshub.app/bilibili/user/dynamic/:uid`
