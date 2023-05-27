---
title: Hexo 主题 Sakura 美化
date: 2020-03-08 21:09
updated: 2020-03-08 21:09
cover: //cdn.wallleap.cn/img/pic/cover/202302O55cFw.jpg
category: 技术杂谈
tags:
  - 博客
  - Hexo
description: Hexo 主题 Sakura 美化
---

文章很长，做好心里准备……

接上次的文章

[闲着也是闲着，不如搭个免费的博客玩玩](https://mp.weixin.qq.com/s/ngKKulHlt9LghOWRlYPccg)

## 0、前言

做 Hexo 的美化工作，主要是：

- 修改布局文件(HTML 模板 ejs 文件)，添加功能
- 做好 CSS

还是得对 HTML(结构)、CSS(表现)、Javascript(行为)有一定的了解

### 目录和文件分析

现在我们来分析一下 `themes/Sakura` 目录结构和文件

![](https://cdn.wallleap.cn/img/pic/test/theme-sakura-pic1.jpg)

首先分析下目录，主要包括以下几个

```md
- languages    这个文件夹中存放的是语言文件，主要是博客中的一些字符以简体中文、繁体中文、英文显示的定义
- layout   这个是布局文件夹，所有的博客页面HTML和JavaScript以ejs模板存放在这
  - _partial   这里的和下面的都是公共的页面，可以引入到HTML的任意位置
  - _widget
    - Search  这里存放的是页内搜索的ejs文件
- source  这个文件夹和博客根目录下的source文件夹是一样的，但是为了存放主题相关的文件
  - css   这里存放css文件
  - fonts   字体文件
  - images   图片
  - js   js文件
```

### 代码插入位置

再接着就是需要知道我们插入的文件和代码应该放到哪里

一般来说我们的 js、css 代码一般以文件形式存放到 js、css 文件夹中，接着再引入 HTML 代码中，引入位置一般在 `<head></head>` 标签中，当然啦 css、js 位置也不是固定的，你也可以直接放到 HTML 页面结构的中央和结尾，也就是 `<body></body>` 之间或者 `</body>` 之后、`</head>` 之前（推荐 CSS 文件和依赖 JS 放到 `</head>` 前、其他 JS 文件放到 `</body>` 前）

具体参考：HTML 中引入 js、css 的三种方式——行内样式、页面中样式、外部文件导入

就对应我们现在要修改的文件中的 `_partial` 目录下 `head.ejs` ——这个 `<html><head></head>` 就在这个文件中

`footer.ejs` 是底部元素，一般个人、企业版权写在这里，因为一般大部分文件都会引入，因此 js 代码也可以写在这

`layout.ejs` 这个也是所有页面需要引入的，因为 `</body></html>` 标签在这里

要是想将功能单独添加到某个页面，那你就找到那个 `ejs` 文件放到里面就醒了

---

好了，下面就正式开始添加功能和修改样式了

## 1、博客原有功能修改

博客原有功能修改主要指的是博客根目录配置文件和主题配置文件的修改

因为大部分的都已经在上次的博客搭建文章中写了

就不多说了吧

### 不讲了的

主要包括各种页面结构的修改：

- 首页轮播图
- 站点图标、头像、赞赏等图片的链接修改
- 个人化的站点标题、副标题、描述、关键词等
- 导航栏的修改、添加、删除等

![](https://cdn.wallleap.cn/img/pic/test/theme-sakura-pic2.jpg)

- 通知的修改
- startdash 的图片、链接修改
- 社交链接的修改等

这上面这些应该都是不需要再讲了的

### 导航栏中的关于

主要是关于>我？这个的修改

这个要修改的文件在 `Sakura/source/js` 目录下，名字为 `botui.js`

主要修改 content 后面双引号里的内容，自行修改为自己的就行

```javascript
function bot_ui_ini() {
    var botui = new BotUI("hello-mashiro")
    botui.message.add({
        delay: 800,
        content: "Hi, there👋"
    }).then(function () {
        botui.message.add({
            delay: 1100,
            content: "这里是 Mashiro"
        }).then(function () {
            botui.message.add({
                delay: 1100,
                content: "一个可爱的蓝孩子~"
            }).then(function () {
                botui.action.button({
                    delay: 1600,
                    action: [{
                        text: "然后呢？ 😃",
                        value: "sure"
                    }, {
                        text: "少废话！ 🙄",
                        value: "skip"
                    }]
                }).then(function (a) {
                    "sure" == a.value && sure();
                    "skip" == a.value && end()
                })
            })
        })
    });
    var sure = function () {
            botui.message.add({
                delay: 600,
                content: "😘"
            }).then(function () {
                secondpart()
            })
        },
        end = function () {
            botui.message.add({
                delay: 600,
                content: "![...](https://view.moezx.cc/images/2018/05/06/a1c4cd0452528b572af37952489372b6.md.jpg)"
            })
        },
        secondpart = function () {
            botui.message.add({
                delay: 1500,
                content: "目前就读于上海财经大学"
            }).then(function () {
                botui.message.add({
                    delay: 1500,
                    content: "向往技术却误入商科，但后来喜欢上了经济学…"
                }).then(function () {
                    botui.message.add({
                        delay: 1200,
                        content: "因为数据分析也需要Coder嘛"
                    }).then(function () {
                        botui.message.add({
                            delay: 1500,
                            content: "主攻 R 语言和 Python，略懂 STATA，偶尔也折腾 HTML/CSS/JavaScript/PHP"
                        }).then(function () {
                            botui.message.add({
                                delay: 1500,
                                content: "研究的方向，是经济/金融方向的数据分析（data science）以及机器学习（machine learning）"
                            }).then(function () {
                                botui.message.add({
                                    delay: 1800,
                                    content: "喜欢画画，希望有一天能够被称为画师"
                                }).then(function () {
                                    botui.action.button({
                                        delay: 1100,
                                        action: [{
                                            text: "为什么叫Mashiro呢？ 🤔",
                                            value: "why-mashiro"
                                        }]
                                    }).then(function (a) {
                                        thirdpart()
                                    })
                                })
                            })
                        })
                    })
                })
            })
        },
        thirdpart = function () {
            botui.message.add({
                delay: 1E3,
                content: "Mashiro以及站名都来自一部动画，因为和主角有一样的爱好~ 如果有兴趣可以找找首页上的视频~"
            }).then(function () {
                botui.action.button({
                    delay: 1500,
                    action: [{
                        text: "为什么是白猫呢？ 🤔",
                        value: "why-cat"
                    }]
                }).then(function (a) {
                    fourthpart()
                })
            })
        },
        fourthpart = function () {
            botui.message.add({
                delay: 1E3,
                content: "因为对GitHub有种执念… "
            }).then(function () {
                botui.message.add({
                    delay: 1100,
                    content: "而且我真的是猫控！"
                }).then(function () {
                    botui.action.button({
                        delay: 1500,
                        action: [{
                            text: "域名有什么含意吗？(ง •_•)ง",
                            value: "why-domain"
                        }]
                    }).then(function (a) {
                        fifthpart()
                    })
                })
            })
        },
        fifthpart = function () {
            botui.message.add({
                delay: 1E3,
                content: "emmmm，看备案信息你就知道了=.= 本来想要zheng.xin的，但50万真买不起。。"
            }).then(function () {
                botui.message.add({
                    delay: 1600,
                    content: "那么，仔细看看我的博客吧？ ^_^"
                })
            })
        } 
}
```

### 导航栏中的客户端

这个可以使用 Fusion App 把你自己的博客封装成 APP

然后放到蓝奏云上，生成二维码放上来

### 导航栏中的 RSS

根目录下的配置文件中已经有了

```yml
#RSS
feed:
  type: atom
  path: atom.xml
  limit: 20
  hub:
  content:
  content_limit: 140
  content_limit_delim: ' '
  order_by: -date
```

这些代码

因此我们只需要安装好插件就行了

```shell
npm install hexo-generator-feed
```

当然啦，如果本来就能显示内容，那么就不需要安装了

### 每个页面中的顶部图片

就比如关于>主题这个页面

我们进入根目录下，再进入 source 目录找到 theme-sakura，进入该目录点击 index.md，修改 photos 后面的内容，改为你想要的图片链接

```markdown
---
title: theme-sakura
comments: false
date: 2019-01-04 22:53:25
keywords: Hexo 主题 Sakura 🌸
description:
photos: https://static.2heng.xin/wp-content/uploads//2018/05/sakura2.jpeg
---
Hexo主题Sakura修改自WordPress主题[Sakura](https://github.com/mashirozx/Sakura/)，感谢原作者[Mashiro](https://2heng.xin/)
```

### 文章上面和首页文章列表的图片

也是修改的你新建的文章中的 photos 后面的图片链接

这些都是这个主题支持的内容，在上篇文章中写过的文章模板

```md
---
title: 文章标题
author: 作者名
avatar: 作者头像链接
authorLink: hojun.cn  #作者的域名
authorAbout: 一个好奇的人  #关于
authorDesc: 一个好奇的人  #作者描述
categories: 分类
date: 2018-12-12 22:16:01 #时间，这个一般都自动创建
comments: true  # 是否需要留言
tags:        # 下面可以写多个标签
 - web
 - 悦读
keywords: Sakura   # 文章关键词
description: hexo-sakura主题使用教程   #文章描述
photos: https://static.2heng.xin/wp-content/uploads//2019/02/wallhaven-672007-1-1024x576.png
---
```

### 清单下的番组

这个是在 source 下 bangumi 下的 index.md 中修改的

```md
---
layout: bangumi
title: bangumi
comments: false
date: 2019-02-10 21:32:48
keywords:
description:
bangumis:
  - img: https://lain.bgm.tv/pic/cover/l/0e/1e/218971_2y351.jpg # 番的图片
    title: 朝花夕誓——于离别之朝束起约定之花  # 番的中文标题
    status: 已追完  # 追番状态
    progress: 100   # 追番进度
    jp: さよならの朝に約束の花をかざろう   # 日文标题
    time: 2018-02-24 SUN.  # 这个是出版的时间
    desc: 这里是你追的番的描述
---
```

### 清单下的歌单和左下角悬浮歌单

主要是修改你的 id，歌单 id 的获取方式：

进入[网易云网页版](https://music.163.com/)登录账号，选择一个歌单打开

浏览器的链接将会显示 id，就最后一个字段，把那些数字复制到下面就行

`https://music.163.com/?from=infinity#/playlist?id=2162711186`

清单下的歌单文件是 `source/music/index.md`

```md
---
title: music
date: 2018-12-20 23:14:28
keywords: 喜欢的音乐
description: 
comments: false
photos: https://cdn.jsdelivr.net/gh/honjun/cdn@1.4/img/banner/music.jpg
---
{% raw %}
<meting-js
  server="netease"
  type="playlist"
  id="2731690811"
  mutex="true">
</meting-js>

<meting-js
  server="netease"
  type="playlist"
  id="419239189"
  mutex="true">
</meting-js>
{% endraw %}
```

悬浮音乐的代码在主题配置文件中

```md
aplayer: 
  id: 2660651585
  server: netease
  type: playlist
  fixed: true
  autoplay: false
  loop: all
  order: random
  preload: auto
  volume: 0.7
  mutex: true
```

### 友链添加

友链修改文件在 `source/links/index.md`

```md
---
layout: links
title: links
date: 2018-12-19 23:11:06
keywords: 友人帐
description: 
comments: true
photos: https://cdn.jsdelivr.net/gh/honjun/cdn@1.4/img/banner/links.jpg
links:
  - group: 个人项目
    desc: 充分说明这家伙是条咸鱼 < (￣︶￣)>
    items:
    - url: https://shino.cc/fgvf
      img: https://cloud.moezx.cc/Picture/svg/landscape/fields.svg
      name: Google
      desc: Google 镜像
    - url: https://shino.cc/fgvf
      img: https://cloud.moezx.cc/Picture/svg/landscape/fields.svg
      name: Google
      desc: Google 镜像
  - group: 小伙伴们
    desc: 欢迎交换友链 ꉂ(ˊᗜˋ)
    items:  ## 友链添加主要是在这里
    - url: https://shino.cc/fgvf # 他的链接
      img: https://cloud.moezx.cc/Picture/svg/landscape/fields.svg # 他的头像
      name: Google # 他的博客名
      desc: Google 镜像 # 博客描述
    - url: https://shino.cc/fgvf
      img: https://cloud.moezx.cc/Picture/svg/landscape/fields.svg
      name: Google
      desc: Google 镜像
---
```

不需要修改 `layout` 目录下文件的应该就这些了

接下来就直接按点添加功能和美化了

## 2、添加标题恶搞

默认的是离开时候还是现实自己的文字标题

添加之后离开和回到这个页面时显示

![](https://cdn.wallleap.cn/img/pic/test/theme-sakura-pic3.jpg)

> 挺多的 js 都直接集合到我的 cdn 中了，大部分都是网上到处搜查的

为了达到上述效果,我们可以在 `head.ejs` 或者 `footer.ejs` 中加入代码

```ejs
<script src="https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/js/hititle.js"></script>
```

例如加入到 `head.ejs` 的该位置

![](https://cdn.wallleap.cnme-sakura-pic4.jpg)

加入之后刷新就能生效了

## 3、添加鼠标单击特效

单击特效有很多种，这里给出三个吧

现在我们把这个代码放到 `layout.ejs` 的 `</body>` 标签前

```ejs
<!-- 点击出现社会主义彩色文字 -->
<script src="https://cdn.jsdelivr.net/gh/wallleap/cdn/js/shehuizhuyi.js"></script>
<!-- 点击出现爱心 -->
<script src="https://cdn.jsdelivr.net/gh/wallleap/cdn/js/love.js"></script>
<!-- 点击出现彩色气球爆炸效果 -->
<canvas class="fireworks" style="position: fixed;left: 0;top: 0;z-index: 1; pointer-events: none;" ></canvas> 
<script type="text/javascript" src="//cdn.bootcss.com/animejs/2.2.0/anime.min.js"></script> 
<script src="https://cdn.jsdelivr.net/gh/wallleap/cdn/js/clickBom.js"></script>
```

可以分别添加一种，也可以多种混合，但是三种一起使用感觉效果不太好

下面是前两者结合的效果：

![](https://cdn.wallleap.cn/img/pic/test/theme-sakura-pic5.gif)

最后一种：

![](https://cdn.wallleap.cn/img/pic/test/theme-sakura-pic6.gif)

## 4、鼠标滑过的特效

这个有很多个，这里展示一个

把代码插入到 `layout.ejs` 中

```ejs
<script src="https://cdn.jsdelivr.net/gh/wallleap/cdn/js/xuehua.js"></script>
```

效果如下：

![](https://cdn.wallleap.cn/img/pic/test/theme-sakura-pic7.gif)

## 5、背景显示飘动的彩带

在需要的页面添加，我们还是在所有页面都加上，layout.ejs中加入代码

```ejs
<script src="https://cdn.jsdelivr.net/gh/wallleap/cdn/js/piao.js"></script>
```

![](https://cdn.wallleap.cn/img/pic/test/theme-sakura-pic8.gif)

## 6、背景添加动态线条，随鼠标动

仍是 `layout.ejs` 中

```ejs
<script src="https://cdn.jsdelivr.net/gh/wallleap/cdn/js/canvas-nest.min.js"></script>
```

![](https://cdn.wallleap.cn/img/pic/test/theme-sakura-pic9.gif)

## 7、樱花飘落或雪花飘落

仍是 `layout.ejs` 中

樱花飘落：

```ejs
<script src="https://cdn.jsdelivr.net/gh/wallleap/cdn/js/sakura.js"></script>
```

雪花飘落：

```ejs
<script src="https://cdn.jsdelivr.net/gh/wallleap/cdn/js/xuehuapiaoluo.js"></script>
// 或者
<script src="https://cdn.jsdelivr.net/gh/wallleap/cdn/js/snow.js"></script>
```

选择一个就行了

## 8、禁用一些按键

为了阻止某些使用 F12、Ctrl+Alt+I 调用开发者选项的用户

还有禁用了鼠标右键，可以开启禁用鼠标左键拖动选择文字

```ejs
<script src="https://cdn.jsdelivr.net/gh/wallleap/cdn/js/noSomeKey.js"></script>
```

## 9、添加画板娘

这次不用插件来添加，直接引入js代码

```ejs
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/font-awesome/css/font-awesome.min.css"> <!-- 这条在sakura中已有，可不添加 -->
<script src="https://cdn.jsdelivr.net/gh/stevenjoezhang/live2d-widget@latest/autoload.js"></script>
```

仓库链接在这：[live2d-widget](https://github.com/stevenjoezhang/live2d-widget)

## 10、添加前往 GitHub 的彩带

前往 [GitHub Ribbons](https://github.blog/2008-12-19-github-ribbons/)

挑选样式之后，复制相应的代码，粘贴到合适的地方

## 11、加入预加载

Sakura 主题集成了图片懒加载，可是页面放到 GitHub 加载还是很慢，matery 主题就加入了预加载，从那里得到灵感，因此我们加入预加载

还是在 `layout.ejs` 中添加

```ejs
<script src="//instant.page/3.0.0" type="module" defer integrity="sha384-OeDn4XE77tdHo8pGtE1apMPmAipjoxUQ++eeJa6EtJCfHlvijigWiJpD7VDPWXV1"></script>
```

官网在这：[预加载](https://instant.page/)

## 12、添加计数

主要使用的是不蒜子和 LeanCloud

LeanCloud 我使用起来并不理想，因此不讲，想要了解自己去官网看

不蒜子的：

```ejs
<script src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
```

再进入不蒜子官网查看访问量 pv、用户访问量 uv使用

## 13、添加一言 API、诗词

[今日诗词](https://www.jinrishici.com/#)提供了诗词的 API

我们将这个诗词放到以前的描述那里，社交图标的上方

![](https://cdn.wallleap.cn/img/pic/test/theme-sakura-pic10.jpg)

修改 `headertop.ejs`，找到下面的代码

```html
<div class="header-info">  <!-- 找到这个位置 -->
        <!-- <p><%= theme.description %></p> -->  把这句注释掉
        <p id="jinrishici-sentence">正在加载今日诗词....</p>
        <script src="https://sdk.jinrishici.com/v2/browser/jinrishici.js" charset="utf-8"></script>
        <!-- 添加上面的两句 -->
        <div class="top-social_v2"> 
```

一言 API 的可以前往这个网址查看使用：

[一言开发者中心](https://developer.hitokoto.cn/sentence/)

正好通知也没有啥用，把他换掉

进入 `index.ejs`，查找 `<%= theme.notice%>`，将其替换为下面的

```ejs
      <span id="hitokoto" style="margin-left:5px;"> :D 获取中...</span>
      <p align="right" id="afrom"></p>
      <script src="https://cdn.jsdelivr.net/npm/bluebird@3/js/browser/bluebird.min.js"></script>
      <script src="https://cdn.jsdelivr.net/npm/whatwg-fetch@2.0.3/fetch.min.js"></script>
      <script>
        fetch('https://v1.hitokoto.cn/?c=h')
          .then(function (res){
            return res.json();
          })
          .then(function (data) {
            var hitokoto = document.getElementById('hitokoto');
            var afrom = document.getElementById('afrom');
            hitokoto.innerText = data.hitokoto;
            afrom.innerText =  '——【' + data.from + ' ' + data.from_who + '】';
          })
          .catch(function (err) {
            console.error(err);
          })
      </script>
```

## 14、添加底部的网站运行时间

在 `footer.ejs` 选择合适位置添加代码

```html
<span id="timeDate">载入天数...</span><span id="times">载入时分秒...</span>
<script>
  var now = new Date(); 
  function createtime() { 
    var grt= new Date("03/08/2020 16:44:00");//此处修改你的建站时间或者网站上线时间 
    now.setTime(now.getTime()+250); 
    days = (now - grt ) / 1000 / 60 / 60 / 24; dnum = Math.floor(days); 
    hours = (now - grt ) / 1000 / 60 / 60 - (24 * dnum); hnum = Math.floor(hours); 
    if(String(hnum).length ==1 ){hnum = "0" + hnum;} minutes = (now - grt ) / 1000 /60 - (24 * 60 * dnum) - (60 * hnum); 
    mnum = Math.floor(minutes); if(String(mnum).length ==1 ){mnum = "0" + mnum;} 
    seconds = (now - grt ) / 1000 - (24 * 60 * 60 * dnum) - (60 * 60 * hnum) - (60 * mnum); 
    snum = Math.round(seconds); if(String(snum).length ==1 ){snum = "0" + snum;} 
    document.getElementById("timeDate").innerHTML = "本站已安全运行 "+dnum+" 天 "; 
    document.getElementById("times").innerHTML = hnum + " 小时 " + mnum + " 分 " + snum + " 秒"; 
  } 
  setInterval("createtime()",250);
</script>
```

## 15、添加底部动态滚动文字

```ejs
<div id="binft"></div>
  <script>
    var binft = function (r) {
      function t() {
        return b[Math.floor(Math.random() * b.length)]
      }  
      function e() {
        return String.fromCharCode(94 * Math.random() + 33)
      }
      function n(r) {
        for (var n = document.createDocumentFragment(), i = 0; r > i; i++) {
          var l = document.createElement("span");
          l.textContent = e(), l.style.color = t(), n.appendChild(l)
        }
        return n
      }
      function i() {
        var t = o[c.skillI];
        c.step ? c.step-- : (c.step = g, c.prefixP < l.length ? (c.prefixP >= 0 && (c.text += l[c.prefixP]), c.prefixP++) : "forward" === c.direction ? c.skillP < t.length ? (c.text += t[c.skillP], c.skillP++) : c.delay ? c.delay-- : (c.direction = "backward", c.delay = a) : c.skillP > 0 ? (c.text = c.text.slice(0, -1), c.skillP--) : (c.skillI = (c.skillI + 1) % o.length, c.direction = "forward")), r.textContent = c.text, r.appendChild(n(c.prefixP < l.length ? Math.min(s, s + c.prefixP) : Math.min(s, t.length - c.skillP))), setTimeout(i, d)
      }
      var l = "",
      o = ["青青陵上柏，磊磊涧中石。", "人生天地间，忽如远行客。","斗酒相娱乐，聊厚不为薄。", "驱车策驽马，游戏宛与洛。","洛中何郁郁，冠带自相索。","长衢罗夹巷，王侯多第宅。","两宫遥相望，双阙百余尺。","极宴娱心意，戚戚何所迫？"].map(function (r) {
      return r + ""
      }),
      a = 2,
      g = 1,
      s = 5,
      d = 75,
      b = ["rgb(110,64,170)", "rgb(150,61,179)", "rgb(191,60,175)", "rgb(228,65,157)", "rgb(254,75,131)", "rgb(255,94,99)", "rgb(255,120,71)", "rgb(251,150,51)", "rgb(226,183,47)", "rgb(198,214,60)", "rgb(175,240,91)", "rgb(127,246,88)", "rgb(82,246,103)", "rgb(48,239,130)", "rgb(29,223,163)", "rgb(26,199,194)", "rgb(35,171,216)", "rgb(54,140,225)", "rgb(76,110,219)", "rgb(96,84,200)"],
      c = {
        text: "",
        prefixP: -s,
        skillI: 0,
        skillP: 0,
        direction: "forward",
        delay: a,
        step: g
      };
      i()
      };
      binft(document.getElementById('binft'));
  </script>
```

## 16、加入天气插件

前往

[中国天气](https://cj.weather.com.cn/plugin/pc)

这个网址查看详情

可以选用小视图，添加到 `link.ejs` 中

![](https://cdn.wallleap.cn/img/pic/test/theme-sakura-pic11.jpg)

## 17、顶部加载条

这个 sakura 有，但是想记录一下

head 中加入

```html
<script src="//cdn.bootcss.com/pace/1.0.2/pace.min.js"></script>
<link href="//cdn.bootcss.com/pace/1.0.2/themes/pink/pace-theme-flash.css" rel="stylesheet">
<style>
  .pace .pace-progress {
  background: #1E92FB; /*进度条颜色*/
  height: 3px;
  }
  .pace .pace-progress-inner {
  box-shadow: 0 0 10px #1E92FB, 0 0 5px     #1E92FB; /*阴影颜色*/
  }
  .pace .pace-activity {
  border-top-color: #1E92FB;    /*上边框颜色*/
  border-left-color: #1E92FB;    /*左边框颜色*/
  }
</style>
```

## 18、修改鼠标样式

在 `style.css` 中添加，sakura 已有，可不管，当然啦，也可以去找一下其他好看的图标

```css
// 鼠标样式
  * {
      cursor: url("https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/cursor/normal.cur"),auto!important
  }
  :active {
      cursor: url("https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/img/cursor/No_Disponible.cur"),auto!important
  }
```

## 19、评论系统

sakura 自带的系统为 valine，我们可以自行替换成其他的

就比如来必力，前往

[来必力官网](https://www.livere.com/)

注册登录后，点击菜单栏的【安装】，出现这个界面，直接点击【现在安装】

![](<https://cdn.wallleap.cn>

前往管理页，点击左边的【代码管理】

你将会看到这样的代码

![](https://cdn.wallleap.cnpg)

data-uid 后面的双引号中的内容剪切出来

然后到主题配置文件下修改，找到最下面的 valine

将 valine 改成 false，添加最后两行

```yml
# Valine
valine: false
v_appId: Cu2IPPUW8BnkmwzFa8WrS9VC-gzGzoHsz
v_appKey: kgcNfaHXq91mfCaAIcbjGChl
# livere
livere: true
  data_uid: 刚刚复制的uid
```

接着把下面的代码复制到 comment.ejs 中

```html
<% if (theme.livere && post.comments) { %>
<!-- 来必力City版安装代码 -->
<div id="lv-container" data-id="city" data-uid="<%= theme.livere.data_uid %>">
<script type="text/javascript">
   (function(d, s) {
       var j, e = d.getElementsByTagName(s)[0];

       if (typeof LivereTower === 'function') { return; }

       j = d.createElement(s);
       j.src = 'https://cdn-city.livere.com/js/embed.dist.js';
       j.async = true;

       e.parentNode.insertBefore(j, e);
   })(document, 'script');
</script>
<noscript>为正常使用来必力评论功能请激活JavaScript</noscript>
</div>
<!-- City版安装代码已完成 -->
<% } %>
```

## 20、在线联系

DaoVoice 在线联系

前往网站

[DaoVoice](https://www.daovoice.io/)

可以使用GitHub或者微信登录，也可以前往

[这里注册](http://dashboard.daovoice.io/get-started?invite_code=da070d64)

邀请码填：`da070d64`

![](https://cdn.wallleap.cnpg)

进入之后点击应用设置，再点击安装到网站

再将第一个代码复制到 `</head>` 之前，将下面两个复制到 `layout.ejs`

## 21、添加优美的标签页

这个标签页和分类页提取自 matery，不得不说 matery 真的很漂亮

![](https://cdn.wallleap.cnme-sakura-pic15.jpg)

首先我们要创建几个文件，文件所在目录如下

```
- layout
  tags.ejs
  - _widget
    tag-cloud.ejs
    tag-wordcloud.ejs
```

也就是 `tags.ejs` 放在 layout 根目录下，下面两个文件放在 layout 子目录 `_widget` 下

修改 `tags.ejs`

```ejs
<%- partial('_partial/header') %>
<main class="content">
    <%- partial('_widget/tag-cloud') %>
    <%- partial('_widget/tag-wordcloud') %>
</main>
```

修改 `_widget/tag-cloud.ejs`

```ejs
<%
var colorArr = ['#F9EBEA', '#F5EEF8', '#D5F5E3', '#E8F8F5', '#FEF9E7',
    '#F8F9F9', '#82E0AA', '#D7BDE2', '#A3E4D7', '#85C1E9', '#F8C471', '#F9E79F', '#FFF'];
var colorCount = colorArr.length;
var hashCode = function (str) {
    if (!str && str.length === 0) {
        return 0;
    }

    var hash = 0;
    for (var i = 0, len = str.length; i < len; i++) {
        hash = ((hash << 5) - hash) + str.charCodeAt(i);
        hash |= 0;
    }
    return hash;
};
var i = 0;
var isTag = is_tag();
%>

<div id="tags" class="container chip-container">
    <div class="card">
        <div class="card-content">
            <div class="tag-title center-align">
                <i class="fa fa-tags"></i>&nbsp;&nbsp;文章标签
            </div>
            <div class="tag-chips">
                <% site.tags.map(function(tag) { %>
                <%
                    i++;
                    var color = i >= colorCount ? colorArr[Math.abs(hashCode(tag.name) % colorCount)]
                            : colorArr[i - 1];
                %>
                <a href="<%- url_for(tag.path) %>" title="<%- tag.name %>: <%- tag.length %>">
                    <span class="chip center-align waves-effect waves-light
                            <% if (isTag && tag.name == page.tag) { %> chip-active <% } else { %> chip-default <% } %>"
                            data-tagname="<%- tag.name %>" style="background-color: <%- color %>;"><%- tag.name %>
                        <span class="tag-length"><%- tag.length %></span>
                    </span>
                </a>
                <% }); %>
            </div>
        </div>
    </div>
</div>
```

修改 `_widget/tag-wordcloud.ejs`

```ejs
<link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/gh/wallleap/cdn/css/jqcloud.css">
<style type="text/css">
    #tag-wordcloud {
        width: 100%;
        height: 300px;
    }
</style>

<div class="container" data-aos="fade-up">
    <div class="card">
        <div id="tag-wordcloud" class="card-content"></div>
    </div>
</div>
<script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.4.4/jquery.min.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/wallleap/cdn/js/jqcloud-1.0.4.js"></script>
<script type="text/javascript">
    <%
    let tagWordArr = [];
    site.tags.map(function(tag) {
        tagWordArr.push({'text': tag.name, 'weight': tag.length, 'link': tag.permalink});
    });

    let tagWords = JSON.stringify(tagWordArr);
    %>

    $('#tag-wordcloud').jQCloud(<%- tagWords %>, {
        autoResize: true
    });
</script>
```

将这段代码复制到 style.css 末尾

```css
.chip-container {
    margin-top: 60px;
}

.chip-container .tag-title {
    margin-bottom: 10px;
    color: #3C4858;
    font-size: 1.75rem;
    font-weight: 400;
}

.chip-container .tag-chips {
    margin: 1rem auto 0.5rem;
    max-width: 850px;
    text-align: center;
}

.chip-container .tags-posts {
    margin-top: 20px;
}

.chip-container .chip-default {
    color: #34495e;
}

.chip-container .chip-active {
    color: #FFF !important;
    background: linear-gradient(to bottom right, #FF5E3A 0%, #FF2A68 100%) !important;
    box-shadow: 2px 5px 10px #aaa !important;
}

.chip-container .chip {
    margin: 10px 10px;
    padding: 19px 14px;
    display: inline-flex;
    line-height: 0;
    font-size: 1rem;
    font-weight: 500;
    border-radius: 5px;
    cursor: pointer;
    box-shadow: 0 3px 5px rgba(0, 0, 0, .12);
}

.chip-container .chip:hover {
    color: #fff;
    background: linear-gradient(to right, #4cbf30 0%, #0f9d58 100%) !important;
}

.chip .tag-length {
    margin-left: 5px;
    margin-right: -2px;
    font-size: 0.5rem;
}

.chip-default .tag-length {
    color: #e91e63;
    margin-top: 1px;
}

.chip-active .tag-length {
    color: #fff;
}

.tag-title.center-align{
    margin-top: 100px;
    text-align : center;
}
```

使用命令`hexo new page "tags"`，修改博客根目录下 `source/tags/index.md`

```md
---
title: tags
date: 2020-03-09 13:50:05
layout: tags
---
```

在 <http://localhost:4000/tags> 查看页面

## 22、添加优美的分类页

![](https://cdn.wallleap.cn/img/pic/test/theme-sakura-pic16.jpg)

接着创建几个文件，文件所在目录如下

```
- layout
  categories.ejs
  - _widget
    category-cloud.ejs
    category-radar.ejs
```

也就是 `categories.ejs` 放在 layout 根目录下，下面两个文件放在 layout 子目录 `_widget` 下

添加代码

`categories.ejs`

```ejs
<%- partial('_partial/header') %>
<main class="content">

    <%- partial('_widget/category-cloud') %>

    <% if (site.categories && site.categories.length > 0) { %>
    <%- partial('_widget/category-radar') %>
    <% } %>

</main>
```

`category-cloud.ejs`

```ejs
<%
var colorArr = ['#F9EBEA', '#F5EEF8', '#D5F5E3', '#E8F8F5', '#FEF9E7',
    '#F8F9F9', '#82E0AA', '#D7BDE2', '#A3E4D7', '#85C1E9', '#F8C471', '#F9E79F', '#FFF'];
var colorCount = colorArr.length;
var hashCode = function (str) {
    if (!str && str.length === 0) {
        return 0;
    }

    var hash = 0;
    for (var i = 0, len = str.length; i < len; i++) {
        hash = ((hash << 5) - hash) + str.charCodeAt(i);
        hash |= 0;
    }
    return hash;
};
var i = 0;
var isCategory = is_category();
%>

<div id="category-cloud" class="container chip-container">
    <div class="card">
        <div class="card-content">
            <div class="tag-title center-align">
                <i class="fa fa-bookmark"></i>&nbsp;&nbsp;文章分类
            </div>
            <div class="tag-chips">
                <% if (site.categories && site.categories.length > 0) { %>
                <% site.categories.map(function(category) { %>
                <%
                    i++;
                    var color = i >= colorCount ? colorArr[Math.abs(hashCode(category.name) % colorCount)]
                            : colorArr[i - 1];
                %>
                <a href="<%- url_for(category.path) %>" title="<%- category.name %>: <%- category.length %>">
                    <span class="chip center-align waves-effect waves-light
                            <% if (isCategory && category.name == page.category) { %> chip-active <% } else { %> chip-default <% } %>"
                            style="background-color: <%- color %>;"><%- category.name %>
                        <span class="tag-length"><%- category.length %></span>
                    </span>
                </a>
                <% }); %>
                <% } else { %>
                <%= __('categoryEmptyTip') %>
                <% } %>
            </div>
        </div>
    </div>
</div>
```

`category-radar.ejs`

```ejs
<style type="text/css">
    #category-radar {
        margin-top: 50px;
        width: 100%;
        height: 360px;
    }
</style>

<div class="container" data-aos="fade-up">
    <div class="card">
        <div id="category-radar" class="card-content"></div>
    </div>
</div>

<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/wallleap/cdn/js/echarts.min.js"></script>
<script type="text/javascript">
    let radarChart = echarts.init(document.getElementById('category-radar'));

    <%
        var categories = site.categories;

        // Find the maximum and average values of the post categories.
        var radarValueArr = [];
        categories.some(function(category) {
            radarValueArr.push(category.length);
        });

        var max = Math.max.apply(null, radarValueArr) + Math.min.apply(null, radarValueArr);

        // Calculate the data needed for the radar chart.
        var indicatorArr = [];
        categories.map(function(category) {
            indicatorArr.push({'name': category.name, 'max': max});
        });

        var indicatorData = JSON.stringify(indicatorArr);
        var radarValueData = JSON.stringify(radarValueArr);
    %>

    let option = {
        title: {
            left: 'center',
            text: '文章分类雷达图',
            textStyle: {
                fontWeight: 500,
                fontSize: 22
            }
        },
        tooltip: {},
        radar: {
            name: {
                textStyle: {
                    color: '#3C4858'
                }
            },
            indicator: <%- indicatorData %>,
            nameGap: 5,
            center: ['50%','55%'],
            radius: '66%'
        },
        series: [{
            type: 'radar',
            color: ['#3ecf8e'],
            itemStyle: {normal: {areaStyle: {type: 'default'}}},
            data : [
                {
                    value : <%- radarValueData %>,
                    name : '文章分类数量'
                }
            ]
        }]
    };

    radarChart.setOption(option);
</script>
```

接着用命令 `hexo new page "categories"` 创建分类页

修改博客根目录下 `source/categories/index.md`

```md
---
title: categories
date: 2020-03-09 13:50:05
layout: categories
---
```

<http://localhost:4000/categories>

查看

接着就是把这两个页面放到导航栏上面去

修改主题配置文件，将这两行代码放到留言板之前

```yml
 标签: {path: /tags/, fa: fa-tag }
  分类: {path: /categories/, fa: fa-bookmark }
```

## 23、已经集成的一些插件

emoji 表情：

[hexo-filter-github-emojis](https://github.com/crimx/hexo-filter-github-emojis)

正常插件安装版画板娘：

[hexo-helper-live2d](https://github.com/EYHN/hexo-helper-live2d)

图片懒加载(sakura 已经有了，但不是这种方式)：

[hexo-lazyload-image](https://www.npmjs.com/package/hexo-lazyload-image)

[hexo-lazyload-image-enhance](https://github.com/barretlee/hexo-lazyload-image-enhance)

字数统计(好像没装)：

[hexo-wordcount](https://github.com/willin/hexo-wordcount)

fancybox：

[*hexo*-tag-*fancybox*_img](https://github.com/honjun/hexo-tag-fancybox_img)

bilibili：

[hexo-tag-bili](https://github.com/honjun/hexo-tag-bili)

## 24、文章末尾版权信息添加

首先我们在 `_partial` 目录下新建文件 `article_copyright.ejs`

```ejs
<div class="my_post_copyright">
  <script src="//cdn.bootcss.com/clipboard.js/1.5.10/clipboard.min.js"></script>
  
  <!-- JS库 sweetalert 可修改路径 -->
  <script src="https://cdn.bootcss.com/jquery/2.0.0/jquery.min.js"></script>
  <script src="https://unpkg.com/sweetalert/dist/sweetalert.min.js"></script>
  <p><span>本文标题:</span><%= post.title %></p>
  <p><span>文章字数:</span><span class="post-count"><%=wordcount(post.content) %></span></p>
  <p><span>文章作者:</span><a  title="<%=config.author%>"><%=config.author%></a></p>
  <p><span>发布时间:</span><%= post.date.format("YYYY-MM-DD, HH:mm:ss") %></p>
  <p><span>最后更新:</span><%= post.updated.format("YYYY-MM-DD, HH:mm:ss") %></p>
  <p><span>原始链接:</span></span><a class="post-url" href="<%- url_for(post.path) %>" title="<%= post.title %>"><%= post.permalink %></a>
    <span class="copy-path"  title="点击复制文章链接"><i class="fa fa-clipboard" data-clipboard-text="{{ page.permalink }}"  aria-label="复制成功！"></i></span>
  </p>
  <p><span>许可协议:</span><i class="fa fa-creative-commons"></i> <a rel="license" href="https://creativecommons.org/licenses/by-nc-nd/4.0/" target="_blank" title="Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)">署名-非商业性使用-禁止演绎 4.0 国际</a> 转载请保留原文链接及作者。</p>  
</div>
<script> 
    var clipboard = new Clipboard('.fa-clipboard');
    $(".fa-clipboard").click(function(){
      clipboard.on('success', function(){
        swal({   
          title: "",   
          text: '复制成功',
          icon: "success", 
          showConfirmButton: true
          });
 });
    });  
</script>
```

需要文章字数的，一定要先安装字数统计插件，上面列出了，不用就把那行注释掉

接着将下面的代码

```ejs
        <% if (post.copyright) { %>
          <%- partial('../_partial/article_copyright') %>
        <% } %>
```

复制到 `common-article.ejs` 的这个位置

![](https://cdn.wallleap.cn/img/pic/test/theme-sakura-pic17.jpg)

将 CSS 代码复制到 style.css 中

```css
.my_post_copyright {
  width: 85%;
  max-width: 45em;
  margin: 2.8em auto 0;
  padding: 0.5em 1.0em;
  border: 1px solid #d3d3d3;
  font-size: 0.93rem;
  line-height: 1.6em;
  word-break: break-all;
  background: rgba(255,255,255,0.4);
}
.my_post_copyright p{margin:0;}
.my_post_copyright span {
  display: inline-block;
  width: 5.2em;
  color: #b5b5b5;
  font-weight: bold;
}
.my_post_copyright .raw {
  margin-left: 1em;
  width: 5em;
}
.my_post_copyright a {
  color: #808080;
  border-bottom:0;
}
.my_post_copyright a:hover {
  color: #a3d2a3;
  text-decoration: underline;
}
.my_post_copyright:hover .fa-clipboard {
  color: #000;
}
.my_post_copyright .post-url:hover {
  font-weight: normal;
}
.my_post_copyright .copy-path {
  margin-left: 1em;
  width: 1em;
  +mobile(){display:none;}
}
.my_post_copyright .copy-path:hover {
  color: #808080;
  cursor: pointer;
}
```

## 25、添加404页面

在博客根目录的 source 目录下新建 404.html

随便找个模板，在开头加入代码

```md
---
layout: false
---
```

例如

```html
---
layout: false
---
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=0, minimum-scale=1.0, maximum-scale=1.0">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black">
<meta name="format-detection" content="telephone=no">
<title>404</title>
<style>html, body{height:95%;}body{background: #0f3854;background: -webkit-radial-gradient(center ellipse, #0a2e38 0%, #000000 70%);background: radial-gradient(ellipse at center, #0a2e38 0%, #000000 70%);background-size: 100%;}p{margin:0;padding:0;}#clock{font-family: 'Share Tech Mono', monospace;color: #ffffff;text-align: center;position: absolute;left: 50%;top: 50%;-webkit-transform: translate(-50%, -50%);transform: translate(-50%, -50%);color: #daf6ff;text-shadow: 0 0 20px #0aafe6, 0 0 20px rgba(10, 175, 230, 0);}#clock .time{letter-spacing: 0.05em;font-size: 60px;padding: 5px 0;}#clock .date{letter-spacing:0.1em;font-size:15px;}#clock .text{letter-spacing: 0.1em;font-size:12px;padding:20px 0 0;}</style>
<script type="text/javascript">
!function(e,t){"object"==typeof exports&&"undefined"!=typeof module?module.exports=t():"function"==typeof define&&define.amd?define(t):e.Vue=t()}(this,function(){"use strict";function e(e){return void 0===e||null===e}function t(e){return void 0!==e&&null!==e}function n(e){return!0===e}function r(e){return!1===e}function i(e){return"string"==typeof e||"number"==typeof e}function o(e){return null!==e&&"object"==typeof e}function a(e){return"[object Object]"===Ti.call(e)}function s(e){return"[object RegExp]"===Ti.call(e)}function c(e){return null==e?"":"object"==typeof e?JSON.stringify(e,null,2):String(e)}function u(e){var t=parseFloat(e);return isNaN(t)?e:t}function l(e,t){for(var n=Object.create(null),r=e.split(","),i=0;i<r.length;i++)n[r[i]]=!0;return t?function(e){return n[e.toLowerCase()]}:function(e){return n[e]}}function f(e,t){if(e.length){var n=e.indexOf(t);if(n>-1)return e.splice(n,1)}}function p(e,t){return ji.call(e,t)}function d(e){var t=Object.create(null);return function(n){return t[n]||(t[n]=e(n))}}function v(e,t){function n(n){var r=arguments.length;return r?r>1?e.apply(t,arguments):e.call(t,n):e.call(t)}return n._length=e.length,n}function h(e,t){t=t||0;for(var n=e.length-t,r=new Array(n);n--;)r[n]=e[n+t];return r}function m(e,t){for(var n in t)e[n]=t[n];return e}function g(e){for(var t={},n=0;n<e.length;n++)e[n]&&m(t,e[n]);return t}function y(){}function _(e,t){var n=o(e),r=o(t);if(!n||!r)return!n&&!r&&String(e)===String(t);try{return JSON.stringify(e)===JSON.stringify(t)}catch(n){return e===t}}function b(e,t){for(var n=0;n<e.length;n++)if(_(e[n],t))return n;return-1}function $(e){var t=!1;return function(){t||(t=!0,e.apply(this,arguments))}}function C(e){var t=(e+"").charCodeAt(0);return 36===t||95===t}function x(e,t,n,r){Object.defineProperty(e,t,{value:n,enumerable:!!r,writable:!0,configurable:!0})}function w(e){if(!zi.test(e)){var t=e.split(".");return function(e){for(var n=0;n<t.length;n++){if(!e)return;e=e[t[n]]}return e}}}function k(e,t,n){if(Ui.errorHandler)Ui.errorHandler.call(null,e,t,n);else{if(!qi||"undefined"==typeof console)throw e;console.error(e)}}function A(e){return"function"==typeof e&&/native code/.test(e.toString())}function O(e){lo.target&&fo.push(lo.target),lo.target=e}function S(){lo.target=fo.pop()}function T(e,t){e.__proto__=t}function E(e,t,n){for(var r=0,i=n.length;r<i;r++){var o=n[r];x(e,o,t[o])}}function j(e,t){if(o(e)){var n;return p(e,"__ob__")&&e.__ob__ instanceof go?n=e.__ob__:mo.shouldConvert&&!oo()&&(Array.isArray(e)||a(e))&&Object.isExtensible(e)&&!e._isVue&&(n=new go(e)),t&&n&&n.vmCount++,n}}function N(e,t,n,r){var i=new lo,o=Object.getOwnPropertyDescriptor(e,t);if(!o||!1!==o.configurable){var a=o&&o.get,s=o&&o.set,c=j(n);Object.defineProperty(e,t,{enumerable:!0,configurable:!0,get:function(){var t=a?a.call(e):n;return lo.target&&(i.depend(),c&&c.dep.depend(),Array.isArray(t)&&D(t)),t},set:function(t){var r=a?a.call(e):n;t===r||t!==t&&r!==r||(s?s.call(e,t):n=t,c=j(t),i.notify())}})}}function L(e,t,n){if(Array.isArray(e)&&"number"==typeof t)return e.length=Math.max(e.length,t),e.splice(t,1,n),n;if(p(e,t))return e[t]=n,n;var r=e.__ob__;return e._isVue||r&&r.vmCount?n:r?(N(r.value,t,n),r.dep.notify(),n):(e[t]=n,n)}function I(e,t){if(Array.isArray(e)&&"number"==typeof t)return void e.splice(t,1);var n=e.__ob__;e._isVue||n&&n.vmCount||p(e,t)&&(delete e[t],n&&n.dep.notify())}function D(e){for(var t=void 0,n=0,r=e.length;n<r;n++)t=e[n],t&&t.__ob__&&t.__ob__.dep.depend(),Array.isArray(t)&&D(t)}function M(e,t){if(!t)return e;for(var n,r,i,o=Object.keys(t),s=0;s<o.length;s++)n=o[s],r=e[n],i=t[n],p(e,n)?a(r)&&a(i)&&M(r,i):L(e,n,i);return e}function P(e,t){return t?e?e.concat(t):Array.isArray(t)?t:[t]:e}function R(e,t){var n=Object.create(e||null);return t?m(n,t):n}function F(e){var t=e.props;if(t){var n,r,i,o={};if(Array.isArray(t))for(n=t.length;n--;)"string"==typeof(r=t[n])&&(i=Li(r),o[i]={type:null});else if(a(t))for(var s in t)r=t[s],i=Li(s),o[i]=a(r)?r:{type:r};e.props=o}}function B(e){var t=e.directives;if(t)for(var n in t){var r=t[n];"function"==typeof r&&(t[n]={bind:r,update:r})}}function H(e,t,n){function r(r){var i=yo[r]||_o;c[r]=i(e[r],t[r],n,r)}"function"==typeof t&&(t=t.options),F(t),B(t);var i=t.extends;if(i&&(e=H(e,i,n)),t.mixins)for(var o=0,a=t.mixins.length;o<a;o++)e=H(e,t.mixins[o],n);var s,c={};for(s in e)r(s);for(s in t)p(e,s)||r(s);return c}function U(e,t,n,r){if("string"==typeof n){var i=e[t];if(p(i,n))return i[n];var o=Li(n);if(p(i,o))return i[o];var a=Ii(o);if(p(i,a))return i[a];var s=i[n]||i[o]||i[a];return s}}function V(e,t,n,r){var i=t[e],o=!p(n,e),a=n[e];if(K(Boolean,i.type)&&(o&&!p(i,"default")?a=!1:K(String,i.type)||""!==a&&a!==Mi(e)||(a=!0)),void 0===a){a=z(r,i,e);var s=mo.shouldConvert;mo.shouldConvert=!0,j(a),mo.shouldConvert=s}return a}function z(e,t,n){if(p(t,"default")){var r=t.default;return e&&e.$options.propsData&&void 0===e.$options.propsData[n]&&void 0!==e._props[n]?e._props[n]:"function"==typeof r&&"Function"!==J(t.type)?r.call(e):r}}function J(e){var t=e&&e.toString().match(/^\s*function (\w+)/);return t?t[1]:""}function K(e,t){if(!Array.isArray(t))return J(t)===J(e);for(var n=0,r=t.length;n<r;n++)if(J(t[n])===J(e))return!0;return!1}function q(e){return new bo(void 0,void 0,void 0,String(e))}function W(e){var t=new bo(e.tag,e.data,e.children,e.text,e.elm,e.context,e.componentOptions);return t.ns=e.ns,t.isStatic=e.isStatic,t.key=e.key,t.isComment=e.isComment,t.isCloned=!0,t}function Z(e){for(var t=e.length,n=new Array(t),r=0;r<t;r++)n[r]=W(e[r]);return n}function G(e){function t(){var e=arguments,n=t.fns;if(!Array.isArray(n))return n.apply(null,arguments);for(var r=0;r<n.length;r++)n[r].apply(null,e)}return t.fns=e,t}function Y(t,n,r,i,o){var a,s,c,u;for(a in t)s=t[a],c=n[a],u=wo(a),e(s)||(e(c)?(e(s.fns)&&(s=t[a]=G(s)),r(u.name,s,u.once,u.capture,u.passive)):s!==c&&(c.fns=s,t[a]=c));for(a in n)e(t[a])&&(u=wo(a),i(u.name,n[a],u.capture))}function Q(r,i,o){function a(){o.apply(this,arguments),f(s.fns,a)}var s,c=r[i];e(c)?s=G([a]):t(c.fns)&&n(c.merged)?(s=c,s.fns.push(a)):s=G([c,a]),s.merged=!0,r[i]=s}function X(n,r,i){var o=r.options.props;if(!e(o)){var a={},s=n.attrs,c=n.props;if(t(s)||t(c))for(var u in o){var l=Mi(u);ee(a,c,u,l,!0)||ee(a,s,u,l,!1)}return a}}function ee(e,n,r,i,o){if(t(n)){if(p(n,r))return e[r]=n[r],o||delete n[r],!0;if(p(n,i))return e[r]=n[i],o||delete n[i],!0}return!1}function te(e){for(var t=0;t<e.length;t++)if(Array.isArray(e[t]))return Array.prototype.concat.apply([],e);return e}function ne(e){return i(e)?[q(e)]:Array.isArray(e)?ie(e):void 0}function re(e){return t(e)&&t(e.text)&&r(e.isComment)}function ie(r,o){var a,s,c,u=[];for(a=0;a<r.length;a++)s=r[a],e(s)||"boolean"==typeof s||(c=u[u.length-1],Array.isArray(s)?u.push.apply(u,ie(s,(o||"")+"_"+a)):i(s)?re(c)?c.text+=String(s):""!==s&&u.push(q(s)):re(s)&&re(c)?u[u.length-1]=q(c.text+s.text):(n(r._isVList)&&t(s.tag)&&e(s.key)&&t(o)&&(s.key="__vlist"+o+"_"+a+"__"),u.push(s)));return u}function oe(e,t){return o(e)?t.extend(e):e}function ae(r,i,a){if(n(r.error)&&t(r.errorComp))return r.errorComp;if(t(r.resolved))return r.resolved;if(n(r.loading)&&t(r.loadingComp))return r.loadingComp;if(!t(r.contexts)){var s=r.contexts=[a],c=!0,u=function(){for(var e=0,t=s.length;e<t;e++)s[e].$forceUpdate()},l=$(function(e){r.resolved=oe(e,i),c||u()}),f=$(function(e){t(r.errorComp)&&(r.error=!0,u())}),p=r(l,f);return o(p)&&("function"==typeof p.then?e(r.resolved)&&p.then(l,f):t(p.component)&&"function"==typeof p.component.then&&(p.component.then(l,f),t(p.error)&&(r.errorComp=oe(p.error,i)),t(p.loading)&&(r.loadingComp=oe(p.loading,i),0===p.delay?r.loading=!0:setTimeout(function(){e(r.resolved)&&e(r.error)&&(r.loading=!0,u())},p.delay||200)),t(p.timeout)&&setTimeout(function(){e(r.resolved)&&f(null)},p.timeout))),c=!1,r.loading?r.loadingComp:r.resolved}r.contexts.push(a)}function se(e){if(Array.isArray(e))for(var n=0;n<e.length;n++){var r=e[n];if(t(r)&&t(r.componentOptions))return r}}function ce(e){e._events=Object.create(null),e._hasHookEvent=!1;var t=e.$options._parentListeners;t&&fe(e,t)}function ue(e,t,n){n?Co.$once(e,t):Co.$on(e,t)}function le(e,t){Co.$off(e,t)}function fe(e,t,n){Co=e,Y(t,n||{},ue,le,e)}function pe(e,t){var n={};if(!e)return n;for(var r=[],i=0,o=e.length;i<o;i++){var a=e[i];if(a.context!==t&&a.functionalContext!==t||!a.data||null==a.data.slot)r.push(a);else{var s=a.data.slot,c=n[s]||(n[s]=[]);"template"===a.tag?c.push.apply(c,a.children):c.push(a)}}return r.every(de)||(n.default=r),n}function de(e){return e.isComment||" "===e.text}function ve(e,t){t=t||{};for(var n=0;n<e.length;n++)Array.isArray(e[n])?ve(e[n],t):t[e[n].key]=e[n].fn;return t}function he(e){var t=e.$options,n=t.parent;if(n&&!t.abstract){for(;n.$options.abstract&&n.$parent;)n=n.$parent;n.$children.push(e)}e.$parent=n,e.$root=n?n.$root:e,e.$children=[],e.$refs={},e._watcher=null,e._inactive=null,e._directInactive=!1,e._isMounted=!1,e._isDestroyed=!1,e._isBeingDestroyed=!1}function me(e,t,n){e.$el=t,e.$options.render||(e.$options.render=xo),$e(e,"beforeMount");var r;return r=function(){e._update(e._render(),n)},e._watcher=new Lo(e,r,y),n=!1,null==e.$vnode&&(e._isMounted=!0,$e(e,"mounted")),e}function ge(e,t,n,r,i){var o=!!(i||e.$options._renderChildren||r.data.scopedSlots||e.$scopedSlots!==Vi);if(e.$options._parentVnode=r,e.$vnode=r,e._vnode&&(e._vnode.parent=r),e.$options._renderChildren=i,t&&e.$options.props){mo.shouldConvert=!1;for(var a=e._props,s=e.$options._propKeys||[],c=0;c<s.length;c++){var u=s[c];a[u]=V(u,e.$options.props,t,e)}mo.shouldConvert=!0,e.$options.propsData=t}if(n){var l=e.$options._parentListeners;e.$options._parentListeners=n,fe(e,n,l)}o&&(e.$slots=pe(i,r.context),e.$forceUpdate())}function ye(e){for(;e&&(e=e.$parent);)if(e._inactive)return!0;return!1}function _e(e,t){if(t){if(e._directInactive=!1,ye(e))return}else if(e._directInactive)return;if(e._inactive||null===e._inactive){e._inactive=!1;for(var n=0;n<e.$children.length;n++)_e(e.$children[n]);$e(e,"activated")}}function be(e,t){if(!(t&&(e._directInactive=!0,ye(e))||e._inactive)){e._inactive=!0;for(var n=0;n<e.$children.length;n++)be(e.$children[n]);$e(e,"deactivated")}}function $e(e,t){var n=e.$options[t];if(n)for(var r=0,i=n.length;r<i;r++)try{n[r].call(e)}catch(n){k(n,e,t+" hook")}e._hasHookEvent&&e.$emit("hook:"+t)}function Ce(){jo=Ao.length=Oo.length=0,So={},To=Eo=!1}function xe(){Eo=!0;var e,t;for(Ao.sort(function(e,t){return e.id-t.id}),jo=0;jo<Ao.length;jo++)e=Ao[jo],t=e.id,So[t]=null,e.run();var n=Oo.slice(),r=Ao.slice();Ce(),Ae(n),we(r),ao&&Ui.devtools&&ao.emit("flush")}function we(e){for(var t=e.length;t--;){var n=e[t],r=n.vm;r._watcher===n&&r._isMounted&&$e(r,"updated")}}function ke(e){e._inactive=!1,Oo.push(e)}function Ae(e){for(var t=0;t<e.length;t++)e[t]._inactive=!0,_e(e[t],!0)}function Oe(e){var t=e.id;if(null==So[t]){if(So[t]=!0,Eo){for(var n=Ao.length-1;n>jo&&Ao[n].id>e.id;)n--;Ao.splice(n+1,0,e)}else Ao.push(e);To||(To=!0,co(xe))}}function Se(e){Io.clear(),Te(e,Io)}function Te(e,t){var n,r,i=Array.isArray(e);if((i||o(e))&&Object.isExtensible(e)){if(e.__ob__){var a=e.__ob__.dep.id;if(t.has(a))return;t.add(a)}if(i)for(n=e.length;n--;)Te(e[n],t);else for(r=Object.keys(e),n=r.length;n--;)Te(e[r[n]],t)}}function Ee(e,t,n){Do.get=function(){return this[t][n]},Do.set=function(e){this[t][n]=e},Object.defineProperty(e,n,Do)}function je(e){e._watchers=[];var t=e.$options;t.props&&Ne(e,t.props),t.methods&&Re(e,t.methods),t.data?Le(e):j(e._data={},!0),t.computed&&De(e,t.computed),t.watch&&Fe(e,t.watch)}function Ne(e,t){var n=e.$options.propsData||{},r=e._props={},i=e.$options._propKeys=[],o=!e.$parent;mo.shouldConvert=o;for(var a in t)!function(o){i.push(o);var a=V(o,t,n,e);N(r,o,a),o in e||Ee(e,"_props",o)}(a);mo.shouldConvert=!0}function Le(e){var t=e.$options.data;t=e._data="function"==typeof t?Ie(t,e):t||{},a(t)||(t={});for(var n=Object.keys(t),r=e.$options.props,i=n.length;i--;)r&&p(r,n[i])||C(n[i])||Ee(e,"_data",n[i]);j(t,!0)}function Ie(e,t){try{return e.call(t)}catch(e){return k(e,t,"data()"),{}}}function De(e,t){var n=e._computedWatchers=Object.create(null);for(var r in t){var i=t[r],o="function"==typeof i?i:i.get;n[r]=new Lo(e,o,y,Mo),r in e||Me(e,r,i)}}function Me(e,t,n){"function"==typeof n?(Do.get=Pe(t),Do.set=y):(Do.get=n.get?!1!==n.cache?Pe(t):n.get:y,Do.set=n.set?n.set:y),Object.defineProperty(e,t,Do)}function Pe(e){return function(){var t=this._computedWatchers&&this._computedWatchers[e];if(t)return t.dirty&&t.evaluate(),lo.target&&t.depend(),t.value}}function Re(e,t){e.$options.props;for(var n in t)e[n]=null==t[n]?y:v(t[n],e)}function Fe(e,t){for(var n in t){var r=t[n];if(Array.isArray(r))for(var i=0;i<r.length;i++)Be(e,n,r[i]);else Be(e,n,r)}}function Be(e,t,n){var r;a(n)&&(r=n,n=n.handler),"string"==typeof n&&(n=e[n]),e.$watch(t,n,r)}function He(e){var t=e.$options.provide;t&&(e._provided="function"==typeof t?t.call(e):t)}function Ue(e){var t=Ve(e.$options.inject,e);t&&Object.keys(t).forEach(function(n){N(e,n,t[n])})}function Ve(e,t){if(e){for(var n=Array.isArray(e),r=Object.create(null),i=n?e:so?Reflect.ownKeys(e):Object.keys(e),o=0;o<i.length;o++)for(var a=i[o],s=n?a:e[a],c=t;c;){if(c._provided&&s in c._provided){r[a]=c._provided[s];break}c=c.$parent}return r}}function ze(e,n,r,i,o){var a={},s=e.options.props;if(t(s))for(var c in s)a[c]=V(c,s,n||{});else t(r.attrs)&&Je(a,r.attrs),t(r.props)&&Je(a,r.props);var u=Object.create(i),l=function(e,t,n,r){return Ye(u,e,t,n,r,!0)},f=e.options.render.call(null,l,{data:r,props:a,children:o,parent:i,listeners:r.on||{},injections:Ve(e.options.inject,i),slots:function(){return pe(o,i)}});return f instanceof bo&&(f.functionalContext=i,f.functionalOptions=e.options,r.slot&&((f.data||(f.data={})).slot=r.slot)),f}function Je(e,t){for(var n in t)e[Li(n)]=t[n]}function Ke(r,i,a,s,c){if(!e(r)){var u=a.$options._base;if(o(r)&&(r=u.extend(r)),"function"==typeof r&&(!e(r.cid)||void 0!==(r=ae(r,u,a)))){ft(r),i=i||{},t(i.model)&&Ge(r.options,i);var l=X(i,r,c);if(n(r.options.functional))return ze(r,l,i,a,s);var f=i.on;i.on=i.nativeOn,n(r.options.abstract)&&(i={}),We(i);var p=r.options.name||c;return new bo("vue-component-"+r.cid+(p?"-"+p:""),i,void 0,void 0,void 0,a,{Ctor:r,propsData:l,listeners:f,tag:c,children:s})}}}function qe(e,n,r,i){var o=e.componentOptions,a={_isComponent:!0,parent:n,propsData:o.propsData,_componentTag:o.tag,_parentVnode:e,_parentListeners:o.listeners,_renderChildren:o.children,_parentElm:r||null,_refElm:i||null},s=e.data.inlineTemplate;return t(s)&&(a.render=s.render,a.staticRenderFns=s.staticRenderFns),new o.Ctor(a)}function We(e){e.hook||(e.hook={});for(var t=0;t<Ro.length;t++){var n=Ro[t],r=e.hook[n],i=Po[n];e.hook[n]=r?Ze(i,r):i}}function Ze(e,t){return function(n,r,i,o){e(n,r,i,o),t(n,r,i,o)}}function Ge(e,n){var r=e.model&&e.model.prop||"value",i=e.model&&e.model.event||"input";(n.props||(n.props={}))[r]=n.model.value;var o=n.on||(n.on={});t(o[i])?o[i]=[n.model.callback].concat(o[i]):o[i]=n.model.callback}function Ye(e,t,r,o,a,s){return(Array.isArray(r)||i(r))&&(a=o,o=r,r=void 0),n(s)&&(a=Bo),Qe(e,t,r,o,a)}function Qe(e,n,r,i,o){if(t(r)&&t(r.__ob__))return xo();if(!n)return xo();Array.isArray(i)&&"function"==typeof i[0]&&(r=r||{},r.scopedSlots={default:i[0]},i.length=0),o===Bo?i=ne(i):o===Fo&&(i=te(i));var a,s;if("string"==typeof n){var c;s=Ui.getTagNamespace(n),a=Ui.isReservedTag(n)?new bo(Ui.parsePlatformTagName(n),r,i,void 0,void 0,e):t(c=U(e.$options,"components",n))?Ke(c,r,e,i,n):new bo(n,r,i,void 0,void 0,e)}else a=Ke(n,r,e,i);return t(a)?(s&&Xe(a,s),a):xo()}function Xe(n,r){if(n.ns=r,"foreignObject"!==n.tag&&t(n.children))for(var i=0,o=n.children.length;i<o;i++){var a=n.children[i];t(a.tag)&&e(a.ns)&&Xe(a,r)}}function et(e,n){var r,i,a,s,c;if(Array.isArray(e)||"string"==typeof e)for(r=new Array(e.length),i=0,a=e.length;i<a;i++)r[i]=n(e[i],i);else if("number"==typeof e)for(r=new Array(e),i=0;i<e;i++)r[i]=n(i+1,i);else if(o(e))for(s=Object.keys(e),r=new Array(s.length),i=0,a=s.length;i<a;i++)c=s[i],r[i]=n(e[c],c,i);return t(r)&&(r._isVList=!0),r}function tt(e,t,n,r){var i=this.$scopedSlots[e];if(i)return n=n||{},r&&m(n,r),i(n)||t;var o=this.$slots[e];return o||t}function nt(e){return U(this.$options,"filters",e,!0)||Ri}function rt(e,t,n){var r=Ui.keyCodes[t]||n;return Array.isArray(r)?-1===r.indexOf(e):r!==e}function it(e,t,n,r){if(n)if(o(n)){Array.isArray(n)&&(n=g(n));var i;for(var a in n){if("class"===a||"style"===a)i=e;else{var s=e.attrs&&e.attrs.type;i=r||Ui.mustUseProp(t,s,a)?e.domProps||(e.domProps={}):e.attrs||(e.attrs={})}a in i||(i[a]=n[a])}}else;return e}function ot(e,t){var n=this._staticTrees[e];return n&&!t?Array.isArray(n)?Z(n):W(n):(n=this._staticTrees[e]=this.$options.staticRenderFns[e].call(this._renderProxy),st(n,"__static__"+e,!1),n)}function at(e,t,n){return st(e,"__once__"+t+(n?"_"+n:""),!0),e}function st(e,t,n){if(Array.isArray(e))for(var r=0;r<e.length;r++)e[r]&&"string"!=typeof e[r]&&ct(e[r],t+"_"+r,n);else ct(e,t,n)}function ct(e,t,n){e.isStatic=!0,e.key=t,e.isOnce=n}function ut(e){e._vnode=null,e._staticTrees=null;var t=e.$vnode=e.$options._parentVnode,n=t&&t.context;e.$slots=pe(e.$options._renderChildren,n),e.$scopedSlots=Vi,e._c=function(t,n,r,i){return Ye(e,t,n,r,i,!1)},e.$createElement=function(t,n,r,i){return Ye(e,t,n,r,i,!0)}}function lt(e,t){var n=e.$options=Object.create(e.constructor.options);n.parent=t.parent,n.propsData=t.propsData,n._parentVnode=t._parentVnode,n._parentListeners=t._parentListeners,n._renderChildren=t._renderChildren,n._componentTag=t._componentTag,n._parentElm=t._parentElm,n._refElm=t._refElm,t.render&&(n.render=t.render,n.staticRenderFns=t.staticRenderFns)}function ft(e){var t=e.options;if(e.super){var n=ft(e.super);if(n!==e.superOptions){e.superOptions=n;var r=pt(e);r&&m(e.extendOptions,r),t=e.options=H(n,e.extendOptions),t.name&&(t.components[t.name]=e)}}return t}function pt(e){var t,n=e.options,r=e.extendOptions,i=e.sealedOptions;for(var o in n)n[o]!==i[o]&&(t||(t={}),t[o]=dt(n[o],r[o],i[o]));return t}function dt(e,t,n){if(Array.isArray(e)){var r=[];n=Array.isArray(n)?n:[n],t=Array.isArray(t)?t:[t];for(var i=0;i<e.length;i++)(t.indexOf(e[i])>=0||n.indexOf(e[i])<0)&&r.push(e[i]);return r}return e}function vt(e){this._init(e)}function ht(e){e.use=function(e){if(e.installed)return this;var t=h(arguments,1);return t.unshift(this),"function"==typeof e.install?e.install.apply(e,t):"function"==typeof e&&e.apply(null,t),e.installed=!0,this}}function mt(e){e.mixin=function(e){return this.options=H(this.options,e),this}}function gt(e){e.cid=0;var t=1;e.extend=function(e){e=e||{};var n=this,r=n.cid,i=e._Ctor||(e._Ctor={});if(i[r])return i[r];var o=e.name||n.options.name,a=function(e){this._init(e)};return a.prototype=Object.create(n.prototype),a.prototype.constructor=a,a.cid=t++,a.options=H(n.options,e),a.super=n,a.options.props&&yt(a),a.options.computed&&_t(a),a.extend=n.extend,a.mixin=n.mixin,a.use=n.use,Bi.forEach(function(e){a[e]=n[e]}),o&&(a.options.components[o]=a),a.superOptions=n.options,a.extendOptions=e,a.sealedOptions=m({},a.options),i[r]=a,a}}function yt(e){var t=e.options.props;for(var n in t)Ee(e.prototype,"_props",n)}function _t(e){var t=e.options.computed;for(var n in t)Me(e.prototype,n,t[n])}function bt(e){Bi.forEach(function(t){e[t]=function(e,n){return n?("component"===t&&a(n)&&(n.name=n.name||e,n=this.options._base.extend(n)),"directive"===t&&"function"==typeof n&&(n={bind:n,update:n}),this.options[t+"s"][e]=n,n):this.options[t+"s"][e]}})}function $t(e){return e&&(e.Ctor.options.name||e.tag)}function Ct(e,t){return"string"==typeof e?e.split(",").indexOf(t)>-1:!!s(e)&&e.test(t)}function xt(e,t,n){for(var r in e){var i=e[r];if(i){var o=$t(i.componentOptions);o&&!n(o)&&(i!==t&&wt(i),e[r]=null)}}}function wt(e){e&&e.componentInstance.$destroy()}function kt(e){for(var n=e.data,r=e,i=e;t(i.componentInstance);)i=i.componentInstance._vnode,i.data&&(n=At(i.data,n));for(;t(r=r.parent);)r.data&&(n=At(n,r.data));return Ot(n)}function At(e,n){return{staticClass:St(e.staticClass,n.staticClass),class:t(e.class)?[e.class,n.class]:n.class}}function Ot(e){var n=e.class,r=e.staticClass;return t(r)||t(n)?St(r,Tt(n)):""}function St(e,t){return e?t?e+" "+t:e:t||""}function Tt(n){if(e(n))return"";if("string"==typeof n)return n;var r="";if(Array.isArray(n)){for(var i,a=0,s=n.length;a<s;a++)t(n[a])&&t(i=Tt(n[a]))&&""!==i&&(r+=i+" ");return r.slice(0,-1)}if(o(n)){for(var c in n)n[c]&&(r+=c+" ");return r.slice(0,-1)}return r}function Et(e){return fa(e)?"svg":"math"===e?"math":void 0}function jt(e){if(!qi)return!0;if(da(e))return!1;if(e=e.toLowerCase(),null!=va[e])return va[e];var t=document.createElement(e);return e.indexOf("-")>-1?va[e]=t.constructor===window.HTMLUnknownElement||t.constructor===window.HTMLElement:va[e]=/HTMLUnknownElement/.test(t.toString())}function Nt(e){if("string"==typeof e){var t=document.querySelector(e);return t||document.createElement("div")}return e}function Lt(e,t){var n=document.createElement(e);return"select"!==e?n:(t.data&&t.data.attrs&&void 0!==t.data.attrs.multiple&&n.setAttribute("multiple","multiple"),n)}function It(e,t){return document.createElementNS(ua[e],t)}function Dt(e){return document.createTextNode(e)}function Mt(e){return document.createComment(e)}function Pt(e,t,n){e.insertBefore(t,n)}function Rt(e,t){e.removeChild(t)}function Ft(e,t){e.appendChild(t)}function Bt(e){return e.parentNode}function Ht(e){return e.nextSibling}function Ut(e){return e.tagName}function Vt(e,t){e.textContent=t}function zt(e,t,n){e.setAttribute(t,n)}function Jt(e,t){var n=e.data.ref;if(n){var r=e.context,i=e.componentInstance||e.elm,o=r.$refs;t?Array.isArray(o[n])?f(o[n],i):o[n]===i&&(o[n]=void 0):e.data.refInFor?Array.isArray(o[n])&&o[n].indexOf(i)<0?o[n].push(i):o[n]=[i]:o[n]=i}}function Kt(e,n){return e.key===n.key&&e.tag===n.tag&&e.isComment===n.isComment&&t(e.data)===t(n.data)&&qt(e,n)}function qt(e,n){if("input"!==e.tag)return!0;var r;return(t(r=e.data)&&t(r=r.attrs)&&r.type)===(t(r=n.data)&&t(r=r.attrs)&&r.type)}function Wt(e,n,r){var i,o,a={};for(i=n;i<=r;++i)o=e[i].key,t(o)&&(a[o]=i);return a}function Zt(e,t){(e.data.directives||t.data.directives)&&Gt(e,t)}function Gt(e,t){var n,r,i,o=e===ga,a=t===ga,s=Yt(e.data.directives,e.context),c=Yt(t.data.directives,t.context),u=[],l=[];for(n in c)r=s[n],i=c[n],r?(i.oldValue=r.value,Xt(i,"update",t,e),i.def&&i.def.componentUpdated&&l.push(i)):(Xt(i,"bind",t,e),i.def&&i.def.inserted&&u.push(i));if(u.length){var f=function(){for(var n=0;n<u.length;n++)Xt(u[n],"inserted",t,e)};o?Q(t.data.hook||(t.data.hook={}),"insert",f):f()}if(l.length&&Q(t.data.hook||(t.data.hook={}),"postpatch",function(){for(var n=0;n<l.length;n++)Xt(l[n],"componentUpdated",t,e)}),!o)for(n in s)c[n]||Xt(s[n],"unbind",e,e,a)}function Yt(e,t){var n=Object.create(null);if(!e)return n;var r,i;for(r=0;r<e.length;r++)i=e[r],i.modifiers||(i.modifiers=ba),n[Qt(i)]=i,i.def=U(t.$options,"directives",i.name,!0);return n}function Qt(e){return e.rawName||e.name+"."+Object.keys(e.modifiers||{}).join(".")}function Xt(e,t,n,r,i){var o=e.def&&e.def[t];if(o)try{o(n.elm,e,n,r,i)}catch(r){k(r,n.context,"directive "+e.name+" "+t+" hook")}}function en(n,r){if(!e(n.data.attrs)||!e(r.data.attrs)){var i,o,a=r.elm,s=n.data.attrs||{},c=r.data.attrs||{};t(c.__ob__)&&(c=r.data.attrs=m({},c));for(i in c)o=c[i],s[i]!==o&&tn(a,i,o);Gi&&c.value!==s.value&&tn(a,"value",c.value);for(i in s)e(c[i])&&(aa(i)?a.removeAttributeNS(oa,sa(i)):ra(i)||a.removeAttribute(i))}}function tn(e,t,n){ia(t)?ca(n)?e.removeAttribute(t):e.setAttribute(t,t):ra(t)?e.setAttribute(t,ca(n)||"false"===n?"false":"true"):aa(t)?ca(n)?e.removeAttributeNS(oa,sa(t)):e.setAttributeNS(oa,t,n):ca(n)?e.removeAttribute(t):e.setAttribute(t,n)}function nn(n,r){var i=r.elm,o=r.data,a=n.data;if(!(e(o.staticClass)&&e(o.class)&&(e(a)||e(a.staticClass)&&e(a.class)))){var s=kt(r),c=i._transitionClasses;t(c)&&(s=St(s,Tt(c))),s!==i._prevClass&&(i.setAttribute("class",s),i._prevClass=s)}}function rn(e){function t(){(a||(a=[])).push(e.slice(v,i).trim()),v=i+1}var n,r,i,o,a,s=!1,c=!1,u=!1,l=!1,f=0,p=0,d=0,v=0;for(i=0;i<e.length;i++)if(r=n,n=e.charCodeAt(i),s)39===n&&92!==r&&(s=!1);else if(c)34===n&&92!==r&&(c=!1);else if(u)96===n&&92!==r&&(u=!1);else if(l)47===n&&92!==r&&(l=!1);else if(124!==n||124===e.charCodeAt(i+1)||124===e.charCodeAt(i-1)||f||p||d){switch(n){case 34:c=!0;break;case 39:s=!0;break;case 96:u=!0;break;case 40:d++;break;case 41:d--;break;case 91:p++;break;case 93:p--;break;case 123:f++;break;case 125:f--}if(47===n){for(var h=i-1,m=void 0;h>=0&&" "===(m=e.charAt(h));h--);m&&wa.test(m)||(l=!0)}}else void 0===o?(v=i+1,o=e.slice(0,i).trim()):t();if(void 0===o?o=e.slice(0,i).trim():0!==v&&t(),a)for(i=0;i<a.length;i++)o=on(o,a[i]);return o}function on(e,t){var n=t.indexOf("(");return n<0?'_f("'+t+'")('+e+")":'_f("'+t.slice(0,n)+'")('+e+","+t.slice(n+1)}function an(e){console.error("[Vue compiler]: "+e)}function sn(e,t){return e?e.map(function(e){return e[t]}).filter(function(e){return e}):[]}function cn(e,t,n){(e.props||(e.props=[])).push({name:t,value:n})}function un(e,t,n){(e.attrs||(e.attrs=[])).push({name:t,value:n})}function ln(e,t,n,r,i,o){(e.directives||(e.directives=[])).push({name:t,rawName:n,value:r,arg:i,modifiers:o})}function fn(e,t,n,r,i,o){r&&r.capture&&(delete r.capture,t="!"+t),r&&r.once&&(delete r.once,t="~"+t),r&&r.passive&&(delete r.passive,t="&"+t);var a;r&&r.native?(delete r.native,a=e.nativeEvents||(e.nativeEvents={})):a=e.events||(e.events={});var s={value:n,modifiers:r},c=a[t];Array.isArray(c)?i?c.unshift(s):c.push(s):a[t]=c?i?[s,c]:[c,s]:s}function pn(e,t,n){var r=dn(e,":"+t)||dn(e,"v-bind:"+t);if(null!=r)return rn(r);if(!1!==n){var i=dn(e,t);if(null!=i)return JSON.stringify(i)}}function dn(e,t){var n;if(null!=(n=e.attrsMap[t]))for(var r=e.attrsList,i=0,o=r.length;i<o;i++)if(r[i].name===t){r.splice(i,1);break}return n}function vn(e,t,n){var r=n||{},i=r.number,o=r.trim,a="$$v";o&&(a="(typeof $$v === 'string'? $$v.trim(): $$v)"),i&&(a="_n("+a+")");var s=hn(t,a);e.model={value:"("+t+")",expression:'"'+t+'"',callback:"function ($$v) {"+s+"}"}}function hn(e,t){var n=mn(e);return null===n.idx?e+"="+t:"var $$exp = "+n.exp+", $$idx = "+n.idx+";if (!Array.isArray($$exp)){"+e+"="+t+"}else{$$exp.splice($$idx, 1, "+t+")}"}function mn(e){if(Ko=e,Jo=Ko.length,Wo=Zo=Go=0,e.indexOf("[")<0||e.lastIndexOf("]")<Jo-1)return{exp:e,idx:null};for(;!yn();)qo=gn(),_n(qo)?$n(qo):91===qo&&bn(qo);return{exp:e.substring(0,Zo),idx:e.substring(Zo+1,Go)}}function gn(){return Ko.charCodeAt(++Wo)}function yn(){return Wo>=Jo}function _n(e){return 34===e||39===e}function bn(e){var t=1;for(Zo=Wo;!yn();)if(e=gn(),_n(e))$n(e);else if(91===e&&t++,93===e&&t--,0===t){Go=Wo;break}}function $n(e){for(var t=e;!yn()&&(e=gn())!==t;);}function Cn(e,t,n){Yo=n;var r=t.value,i=t.modifiers,o=e.tag,a=e.attrsMap.type;if("select"===o)kn(e,r,i);else if("input"===o&&"checkbox"===a)xn(e,r,i);else if("input"===o&&"radio"===a)wn(e,r,i);else if("input"===o||"textarea"===o)An(e,r,i);else if(!Ui.isReservedTag(o))return vn(e,r,i),!1;return!0}function xn(e,t,n){var r=n&&n.number,i=pn(e,"value")||"null",o=pn(e,"true-value")||"true",a=pn(e,"false-value")||"false";cn(e,"checked","Array.isArray("+t+")?_i("+t+","+i+")>-1"+("true"===o?":("+t+")":":_q("+t+","+o+")")),fn(e,Aa,"var $$a="+t+",$$el=$event.target,$$c=$$el.checked?("+o+"):("+a+");if(Array.isArray($$a)){var $$v="+(r?"_n("+i+")":i)+",$$i=_i($$a,$$v);if($$c){$$i<0&&("+t+"=$$a.concat($$v))}else{$$i>-1&&("+t+"=$$a.slice(0,$$i).concat($$a.slice($$i+1)))}}else{"+hn(t,"$$c")+"}",null,!0)}function wn(e,t,n){var r=n&&n.number,i=pn(e,"value")||"null";i=r?"_n("+i+")":i,cn(e,"checked","_q("+t+","+i+")"),fn(e,Aa,hn(t,i),null,!0)}function kn(e,t,n){var r=n&&n.number,i='Array.prototype.filter.call($event.target.options,function(o){return o.selected}).map(function(o){var val = "_value" in o ? o._value : o.value;return '+(r?"_n(val)":"val")+"})",o="var $$selectedVal = "+i+";";o=o+" "+hn(t,"$event.target.multiple ? $$selectedVal : $$selectedVal[0]"),fn(e,"change",o,null,!0)}function An(e,t,n){var r=e.attrsMap.type,i=n||{},o=i.lazy,a=i.number,s=i.trim,c=!o&&"range"!==r,u=o?"change":"range"===r?ka:"input",l="$event.target.value";s&&(l="$event.target.value.trim()"),a&&(l="_n("+l+")");var f=hn(t,l);c&&(f="if($event.target.composing)return;"+f),cn(e,"value","("+t+")"),fn(e,u,f,null,!0),(s||a||"number"===r)&&fn(e,"blur","$forceUpdate()")}function On(e){var n;t(e[ka])&&(n=Zi?"change":"input",e[n]=[].concat(e[ka],e[n]||[]),delete e[ka]),t(e[Aa])&&(n=eo?"click":"change",e[n]=[].concat(e[Aa],e[n]||[]),delete e[Aa])}function Sn(e,t,n,r,i){if(n){var o=t,a=Qo;t=function(n){null!==(1===arguments.length?o(n):o.apply(null,arguments))&&Tn(e,t,r,a)}}Qo.addEventListener(e,t,to?{capture:r,passive:i}:r)}function Tn(e,t,n,r){(r||Qo).removeEventListener(e,t,n)}function En(t,n){if(!e(t.data.on)||!e(n.data.on)){var r=n.data.on||{},i=t.data.on||{};Qo=n.elm,On(r),Y(r,i,Sn,Tn,n.context)}}function jn(n,r){if(!e(n.data.domProps)||!e(r.data.domProps)){var i,o,a=r.elm,s=n.data.domProps||{},c=r.data.domProps||{};t(c.__ob__)&&(c=r.data.domProps=m({},c));for(i in s)e(c[i])&&(a[i]="");for(i in c)if(o=c[i],"textContent"!==i&&"innerHTML"!==i||(r.children&&(r.children.length=0),o!==s[i]))if("value"===i){a._value=o;var u=e(o)?"":String(o);Nn(a,r,u)&&(a.value=u)}else a[i]=o}}function Nn(e,t,n){return!e.composing&&("option"===t.tag||Ln(e,n)||In(e,n))}function Ln(e,t){return document.activeElement!==e&&e.value!==t}function In(e,n){var r=e.value,i=e._vModifiers;return t(i)&&i.number||"number"===e.type?u(r)!==u(n):t(i)&&i.trim?r.trim()!==n.trim():r!==n}function Dn(e){var t=Mn(e.style);return e.staticStyle?m(e.staticStyle,t):t}function Mn(e){return Array.isArray(e)?g(e):"string"==typeof e?Ta(e):e}function Pn(e,t){var n,r={};if(t)for(var i=e;i.componentInstance;)i=i.componentInstance._vnode,i.data&&(n=Dn(i.data))&&m(r,n);(n=Dn(e.data))&&m(r,n);for(var o=e;o=o.parent;)o.data&&(n=Dn(o.data))&&m(r,n);return r}function Rn(n,r){var i=r.data,o=n.data;if(!(e(i.staticStyle)&&e(i.style)&&e(o.staticStyle)&&e(o.style))){var a,s,c=r.elm,u=o.staticStyle,l=o.normalizedStyle||o.style||{},f=u||l,p=Mn(r.data.style)||{};r.data.normalizedStyle=t(p.__ob__)?m({},p):p;var d=Pn(r,!0);for(s in f)e(d[s])&&Na(c,s,"");for(s in d)(a=d[s])!==f[s]&&Na(c,s,null==a?"":a)}}function Fn(e,t){if(t&&(t=t.trim()))if(e.classList)t.indexOf(" ")>-1?t.split(/\s+/).forEach(function(t){return e.classList.add(t)}):e.classList.add(t);else{var n=" "+(e.getAttribute("class")||"")+" ";n.indexOf(" "+t+" ")<0&&e.setAttribute("class",(n+t).trim())}}function Bn(e,t){if(t&&(t=t.trim()))if(e.classList)t.indexOf(" ")>-1?t.split(/\s+/).forEach(function(t){return e.classList.remove(t)}):e.classList.remove(t);else{for(var n=" "+(e.getAttribute("class")||"")+" ",r=" "+t+" ";n.indexOf(r)>=0;)n=n.replace(r," ");e.setAttribute("class",n.trim())}}function Hn(e){if(e){if("object"==typeof e){var t={};return!1!==e.css&&m(t,Ma(e.name||"v")),m(t,e),t}return"string"==typeof e?Ma(e):void 0}}function Un(e){za(function(){za(e)})}function Vn(e,t){(e._transitionClasses||(e._transitionClasses=[])).push(t),Fn(e,t)}function zn(e,t){e._transitionClasses&&f(e._transitionClasses,t),Bn(e,t)}function Jn(e,t,n){var r=Kn(e,t),i=r.type,o=r.timeout,a=r.propCount;if(!i)return n();var s=i===Ra?Ha:Va,c=0,u=function(){e.removeEventListener(s,l),n()},l=function(t){t.target===e&&++c>=a&&u()};setTimeout(function(){c<a&&u()},o+1),e.addEventListener(s,l)}function Kn(e,t){var n,r=window.getComputedStyle(e),i=r[Ba+"Delay"].split(", "),o=r[Ba+"Duration"].split(", "),a=qn(i,o),s=r[Ua+"Delay"].split(", "),c=r[Ua+"Duration"].split(", "),u=qn(s,c),l=0,f=0;return t===Ra?a>0&&(n=Ra,l=a,f=o.length):t===Fa?u>0&&(n=Fa,l=u,f=c.length):(l=Math.max(a,u),n=l>0?a>u?Ra:Fa:null,f=n?n===Ra?o.length:c.length:0),{type:n,timeout:l,propCount:f,hasTransform:n===Ra&&Ja.test(r[Ba+"Property"])}}function qn(e,t){for(;e.length<t.length;)e=e.concat(e);return Math.max.apply(null,t.map(function(t,n){return Wn(t)+Wn(e[n])}))}function Wn(e){return 1e3*Number(e.slice(0,-1))}
function Zn(n,r){var i=n.elm;t(i._leaveCb)&&(i._leaveCb.cancelled=!0,i._leaveCb());var a=Hn(n.data.transition);if(!e(a)&&!t(i._enterCb)&&1===i.nodeType){for(var s=a.css,c=a.type,l=a.enterClass,f=a.enterToClass,p=a.enterActiveClass,d=a.appearClass,v=a.appearToClass,h=a.appearActiveClass,m=a.beforeEnter,g=a.enter,y=a.afterEnter,_=a.enterCancelled,b=a.beforeAppear,C=a.appear,x=a.afterAppear,w=a.appearCancelled,k=a.duration,A=ko,O=ko.$vnode;O&&O.parent;)O=O.parent,A=O.context;var S=!A._isMounted||!n.isRootInsert;if(!S||C||""===C){var T=S&&d?d:l,E=S&&h?h:p,j=S&&v?v:f,N=S?b||m:m,L=S&&"function"==typeof C?C:g,I=S?x||y:y,D=S?w||_:_,M=u(o(k)?k.enter:k),P=!1!==s&&!Gi,R=Qn(L),F=i._enterCb=$(function(){P&&(zn(i,j),zn(i,E)),F.cancelled?(P&&zn(i,T),D&&D(i)):I&&I(i),i._enterCb=null});n.data.show||Q(n.data.hook||(n.data.hook={}),"insert",function(){var e=i.parentNode,t=e&&e._pending&&e._pending[n.key];t&&t.tag===n.tag&&t.elm._leaveCb&&t.elm._leaveCb(),L&&L(i,F)}),N&&N(i),P&&(Vn(i,T),Vn(i,E),Un(function(){Vn(i,j),zn(i,T),F.cancelled||R||(Yn(M)?setTimeout(F,M):Jn(i,c,F))})),n.data.show&&(r&&r(),L&&L(i,F)),P||R||F()}}}function Gn(n,r){function i(){w.cancelled||(n.data.show||((a.parentNode._pending||(a.parentNode._pending={}))[n.key]=n),v&&v(a),b&&(Vn(a,f),Vn(a,d),Un(function(){Vn(a,p),zn(a,f),w.cancelled||C||(Yn(x)?setTimeout(w,x):Jn(a,l,w))})),h&&h(a,w),b||C||w())}var a=n.elm;t(a._enterCb)&&(a._enterCb.cancelled=!0,a._enterCb());var s=Hn(n.data.transition);if(e(s))return r();if(!t(a._leaveCb)&&1===a.nodeType){var c=s.css,l=s.type,f=s.leaveClass,p=s.leaveToClass,d=s.leaveActiveClass,v=s.beforeLeave,h=s.leave,m=s.afterLeave,g=s.leaveCancelled,y=s.delayLeave,_=s.duration,b=!1!==c&&!Gi,C=Qn(h),x=u(o(_)?_.leave:_),w=a._leaveCb=$(function(){a.parentNode&&a.parentNode._pending&&(a.parentNode._pending[n.key]=null),b&&(zn(a,p),zn(a,d)),w.cancelled?(b&&zn(a,f),g&&g(a)):(r(),m&&m(a)),a._leaveCb=null});y?y(i):i()}}function Yn(e){return"number"==typeof e&&!isNaN(e)}function Qn(n){if(e(n))return!1;var r=n.fns;return t(r)?Qn(Array.isArray(r)?r[0]:r):(n._length||n.length)>1}function Xn(e,t){!0!==t.data.show&&Zn(t)}function er(e,t,n){var r=t.value,i=e.multiple;if(!i||Array.isArray(r)){for(var o,a,s=0,c=e.options.length;s<c;s++)if(a=e.options[s],i)o=b(r,nr(a))>-1,a.selected!==o&&(a.selected=o);else if(_(nr(a),r))return void(e.selectedIndex!==s&&(e.selectedIndex=s));i||(e.selectedIndex=-1)}}function tr(e,t){for(var n=0,r=t.length;n<r;n++)if(_(nr(t[n]),e))return!1;return!0}function nr(e){return"_value"in e?e._value:e.value}function rr(e){e.target.composing=!0}function ir(e){e.target.composing&&(e.target.composing=!1,or(e.target,"input"))}function or(e,t){var n=document.createEvent("HTMLEvents");n.initEvent(t,!0,!0),e.dispatchEvent(n)}function ar(e){return!e.componentInstance||e.data&&e.data.transition?e:ar(e.componentInstance._vnode)}function sr(e){var t=e&&e.componentOptions;return t&&t.Ctor.options.abstract?sr(se(t.children)):e}function cr(e){var t={},n=e.$options;for(var r in n.propsData)t[r]=e[r];var i=n._parentListeners;for(var o in i)t[Li(o)]=i[o];return t}function ur(e,t){if(/\d-keep-alive$/.test(t.tag))return e("keep-alive",{props:t.componentOptions.propsData})}function lr(e){for(;e=e.parent;)if(e.data.transition)return!0}function fr(e,t){return t.key===e.key&&t.tag===e.tag}function pr(e){e.elm._moveCb&&e.elm._moveCb(),e.elm._enterCb&&e.elm._enterCb()}function dr(e){e.data.newPos=e.elm.getBoundingClientRect()}function vr(e){var t=e.data.pos,n=e.data.newPos,r=t.left-n.left,i=t.top-n.top;if(r||i){e.data.moved=!0;var o=e.elm.style;o.transform=o.WebkitTransform="translate("+r+"px,"+i+"px)",o.transitionDuration="0s"}}function hr(e){return is=is||document.createElement("div"),is.innerHTML=e,is.textContent}function mr(e,t){var n=t?zs:Vs;return e.replace(n,function(e){return Us[e]})}function gr(e,t){function n(t){l+=t,e=e.substring(t)}function r(e,n,r){var i,s;if(null==n&&(n=l),null==r&&(r=l),e&&(s=e.toLowerCase()),e)for(i=a.length-1;i>=0&&a[i].lowerCasedTag!==s;i--);else i=0;if(i>=0){for(var c=a.length-1;c>=i;c--)t.end&&t.end(a[c].tag,n,r);a.length=i,o=i&&a[i-1].tag}else"br"===s?t.start&&t.start(e,[],!0,n,r):"p"===s&&(t.start&&t.start(e,[],!1,n,r),t.end&&t.end(e,n,r))}for(var i,o,a=[],s=t.expectHTML,c=t.isUnaryTag||Pi,u=t.canBeLeftOpenTag||Pi,l=0;e;){if(i=e,o&&Bs(o)){var f=o.toLowerCase(),p=Hs[f]||(Hs[f]=new RegExp("([\\s\\S]*?)(</"+f+"[^>]*>)","i")),d=0,v=e.replace(p,function(e,n,r){return d=r.length,Bs(f)||"noscript"===f||(n=n.replace(/<!--([\s\S]*?)-->/g,"$1").replace(/<!\[CDATA\[([\s\S]*?)]]>/g,"$1")),t.chars&&t.chars(n),""});l+=e.length-v.length,e=v,r(f,l-d,l)}else{var h=e.indexOf("<");if(0===h){if(_s.test(e)){var m=e.indexOf("--\x3e");if(m>=0){n(m+3);continue}}if(bs.test(e)){var g=e.indexOf("]>");if(g>=0){n(g+2);continue}}var y=e.match(ys);if(y){n(y[0].length);continue}var _=e.match(gs);if(_){var b=l;n(_[0].length),r(_[1],b,l);continue}var $=function(){var t=e.match(hs);if(t){var r={tagName:t[1],attrs:[],start:l};n(t[0].length);for(var i,o;!(i=e.match(ms))&&(o=e.match(ps));)n(o[0].length),r.attrs.push(o);if(i)return r.unarySlash=i[1],n(i[0].length),r.end=l,r}}();if($){!function(e){var n=e.tagName,i=e.unarySlash;s&&("p"===o&&cs(n)&&r(o),u(n)&&o===n&&r(n));for(var l=c(n)||"html"===n&&"head"===o||!!i,f=e.attrs.length,p=new Array(f),d=0;d<f;d++){var v=e.attrs[d];$s&&-1===v[0].indexOf('""')&&(""===v[3]&&delete v[3],""===v[4]&&delete v[4],""===v[5]&&delete v[5]);var h=v[3]||v[4]||v[5]||"";p[d]={name:v[1],value:mr(h,t.shouldDecodeNewlines)}}l||(a.push({tag:n,lowerCasedTag:n.toLowerCase(),attrs:p}),o=n),t.start&&t.start(n,p,l,e.start,e.end)}($);continue}}var C=void 0,x=void 0,w=void 0;if(h>=0){for(x=e.slice(h);!(gs.test(x)||hs.test(x)||_s.test(x)||bs.test(x)||(w=x.indexOf("<",1))<0);)h+=w,x=e.slice(h);C=e.substring(0,h),n(h)}h<0&&(C=e,e=""),t.chars&&C&&t.chars(C)}if(e===i){t.chars&&t.chars(e);break}}r()}function yr(e,t){var n=t?qs(t):Js;if(n.test(e)){for(var r,i,o=[],a=n.lastIndex=0;r=n.exec(e);){i=r.index,i>a&&o.push(JSON.stringify(e.slice(a,i)));var s=rn(r[1].trim());o.push("_s("+s+")"),a=i+r[0].length}return a<e.length&&o.push(JSON.stringify(e.slice(a))),o.join("+")}}function _r(e,t){function n(e){e.pre&&(s=!1),Os(e.tag)&&(c=!1)}Cs=t.warn||an,Ts=t.getTagNamespace||Pi,Ss=t.mustUseProp||Pi,Os=t.isPreTag||Pi,ks=sn(t.modules,"preTransformNode"),ws=sn(t.modules,"transformNode"),As=sn(t.modules,"postTransformNode"),xs=t.delimiters;var r,i,o=[],a=!1!==t.preserveWhitespace,s=!1,c=!1;return gr(e,{warn:Cs,expectHTML:t.expectHTML,isUnaryTag:t.isUnaryTag,canBeLeftOpenTag:t.canBeLeftOpenTag,shouldDecodeNewlines:t.shouldDecodeNewlines,start:function(e,a,u){var l=i&&i.ns||Ts(e);Zi&&"svg"===l&&(a=Rr(a));var f={type:1,tag:e,attrsList:a,attrsMap:Dr(a),parent:i,children:[]};l&&(f.ns=l),Pr(f)&&!oo()&&(f.forbidden=!0);for(var p=0;p<ks.length;p++)ks[p](f,t);if(s||(br(f),f.pre&&(s=!0)),Os(f.tag)&&(c=!0),s)$r(f);else{wr(f),kr(f),Tr(f),Cr(f),f.plain=!f.key&&!a.length,xr(f),Er(f),jr(f);for(var d=0;d<ws.length;d++)ws[d](f,t);Nr(f)}if(r?o.length||r.if&&(f.elseif||f.else)&&Sr(r,{exp:f.elseif,block:f}):r=f,i&&!f.forbidden)if(f.elseif||f.else)Ar(f,i);else if(f.slotScope){i.plain=!1;var v=f.slotTarget||'"default"';(i.scopedSlots||(i.scopedSlots={}))[v]=f}else i.children.push(f),f.parent=i;u?n(f):(i=f,o.push(f));for(var h=0;h<As.length;h++)As[h](f,t)},end:function(){var e=o[o.length-1],t=e.children[e.children.length-1];t&&3===t.type&&" "===t.text&&!c&&e.children.pop(),o.length-=1,i=o[o.length-1],n(e)},chars:function(e){if(i&&(!Zi||"textarea"!==i.tag||i.attrsMap.placeholder!==e)){var t=i.children;if(e=c||e.trim()?Mr(i)?e:tc(e):a&&t.length?" ":""){var n;!s&&" "!==e&&(n=yr(e,xs))?t.push({type:2,expression:n,text:e}):" "===e&&t.length&&" "===t[t.length-1].text||t.push({type:3,text:e})}}}}),r}function br(e){null!=dn(e,"v-pre")&&(e.pre=!0)}function $r(e){var t=e.attrsList.length;if(t)for(var n=e.attrs=new Array(t),r=0;r<t;r++)n[r]={name:e.attrsList[r].name,value:JSON.stringify(e.attrsList[r].value)};else e.pre||(e.plain=!0)}function Cr(e){var t=pn(e,"key");t&&(e.key=t)}function xr(e){var t=pn(e,"ref");t&&(e.ref=t,e.refInFor=Lr(e))}function wr(e){var t;if(t=dn(e,"v-for")){var n=t.match(Gs);if(!n)return;e.for=n[2].trim();var r=n[1].trim(),i=r.match(Ys);i?(e.alias=i[1].trim(),e.iterator1=i[2].trim(),i[3]&&(e.iterator2=i[3].trim())):e.alias=r}}function kr(e){var t=dn(e,"v-if");if(t)e.if=t,Sr(e,{exp:t,block:e});else{null!=dn(e,"v-else")&&(e.else=!0);var n=dn(e,"v-else-if");n&&(e.elseif=n)}}function Ar(e,t){var n=Or(t.children);n&&n.if&&Sr(n,{exp:e.elseif,block:e})}function Or(e){for(var t=e.length;t--;){if(1===e[t].type)return e[t];e.pop()}}function Sr(e,t){e.ifConditions||(e.ifConditions=[]),e.ifConditions.push(t)}function Tr(e){null!=dn(e,"v-once")&&(e.once=!0)}function Er(e){if("slot"===e.tag)e.slotName=pn(e,"name");else{var t=pn(e,"slot");t&&(e.slotTarget='""'===t?'"default"':t),"template"===e.tag&&(e.slotScope=dn(e,"scope"))}}function jr(e){var t;(t=pn(e,"is"))&&(e.component=t),null!=dn(e,"inline-template")&&(e.inlineTemplate=!0)}function Nr(e){var t,n,r,i,o,a,s,c=e.attrsList;for(t=0,n=c.length;t<n;t++)if(r=i=c[t].name,o=c[t].value,Zs.test(r))if(e.hasBindings=!0,a=Ir(r),a&&(r=r.replace(ec,"")),Xs.test(r))r=r.replace(Xs,""),o=rn(o),s=!1,a&&(a.prop&&(s=!0,"innerHtml"===(r=Li(r))&&(r="innerHTML")),a.camel&&(r=Li(r)),a.sync&&fn(e,"update:"+Li(r),hn(o,"$event"))),s||Ss(e.tag,e.attrsMap.type,r)?cn(e,r,o):un(e,r,o);else if(Ws.test(r))r=r.replace(Ws,""),fn(e,r,o,a,!1,Cs);else{r=r.replace(Zs,"");var u=r.match(Qs),l=u&&u[1];l&&(r=r.slice(0,-(l.length+1))),ln(e,r,i,o,l,a)}else un(e,r,JSON.stringify(o))}function Lr(e){for(var t=e;t;){if(void 0!==t.for)return!0;t=t.parent}return!1}function Ir(e){var t=e.match(ec);if(t){var n={};return t.forEach(function(e){n[e.slice(1)]=!0}),n}}function Dr(e){for(var t={},n=0,r=e.length;n<r;n++)t[e[n].name]=e[n].value;return t}function Mr(e){return"script"===e.tag||"style"===e.tag}function Pr(e){return"style"===e.tag||"script"===e.tag&&(!e.attrsMap.type||"text/javascript"===e.attrsMap.type)}function Rr(e){for(var t=[],n=0;n<e.length;n++){var r=e[n];nc.test(r.name)||(r.name=r.name.replace(rc,""),t.push(r))}return t}function Fr(e,t){e&&(Es=ic(t.staticKeys||""),js=t.isReservedTag||Pi,Hr(e),Ur(e,!1))}function Br(e){return l("type,tag,attrsList,attrsMap,plain,parent,children,attrs"+(e?","+e:""))}function Hr(e){if(e.static=zr(e),1===e.type){if(!js(e.tag)&&"slot"!==e.tag&&null==e.attrsMap["inline-template"])return;for(var t=0,n=e.children.length;t<n;t++){var r=e.children[t];Hr(r),r.static||(e.static=!1)}}}function Ur(e,t){if(1===e.type){if((e.static||e.once)&&(e.staticInFor=t),e.static&&e.children.length&&(1!==e.children.length||3!==e.children[0].type))return void(e.staticRoot=!0);if(e.staticRoot=!1,e.children)for(var n=0,r=e.children.length;n<r;n++)Ur(e.children[n],t||!!e.for);e.ifConditions&&Vr(e.ifConditions,t)}}function Vr(e,t){for(var n=1,r=e.length;n<r;n++)Ur(e[n].block,t)}function zr(e){return 2!==e.type&&(3===e.type||!(!e.pre&&(e.hasBindings||e.if||e.for||Ei(e.tag)||!js(e.tag)||Jr(e)||!Object.keys(e).every(Es))))}function Jr(e){for(;e.parent;){if(e=e.parent,"template"!==e.tag)return!1;if(e.for)return!0}return!1}function Kr(e,t,n){var r=t?"nativeOn:{":"on:{";for(var i in e){var o=e[i];r+='"'+i+'":'+qr(i,o)+","}return r.slice(0,-1)+"}"}function qr(e,t){if(!t)return"function(){}";if(Array.isArray(t))return"["+t.map(function(t){return qr(e,t)}).join(",")+"]";var n=ac.test(t.value),r=oc.test(t.value);if(t.modifiers){var i="",o="",a=[];for(var s in t.modifiers)uc[s]?(o+=uc[s],sc[s]&&a.push(s)):a.push(s);a.length&&(i+=Wr(a)),o&&(i+=o);return"function($event){"+i+(n?t.value+"($event)":r?"("+t.value+")($event)":t.value)+"}"}return n||r?t.value:"function($event){"+t.value+"}"}function Wr(e){return"if(!('button' in $event)&&"+e.map(Zr).join("&&")+")return null;"}function Zr(e){var t=parseInt(e,10);if(t)return"$event.keyCode!=="+t;var n=sc[e];return"_k($event.keyCode,"+JSON.stringify(e)+(n?","+JSON.stringify(n):"")+")"}function Gr(e,t){e.wrapData=function(n){return"_b("+n+",'"+e.tag+"',"+t.value+(t.modifiers&&t.modifiers.prop?",true":"")+")"}}function Yr(e,t){var n=Ps,r=Ps=[],i=Rs;Rs=0,Fs=t,Ns=t.warn||an,Ls=sn(t.modules,"transformCode"),Is=sn(t.modules,"genData"),Ds=t.directives||{},Ms=t.isReservedTag||Pi;var o=e?Qr(e):'_c("div")';return Ps=n,Rs=i,{render:"with(this){return "+o+"}",staticRenderFns:r}}function Qr(e){if(e.staticRoot&&!e.staticProcessed)return Xr(e);if(e.once&&!e.onceProcessed)return ei(e);if(e.for&&!e.forProcessed)return ri(e);if(e.if&&!e.ifProcessed)return ti(e);if("template"!==e.tag||e.slotTarget){if("slot"===e.tag)return mi(e);var t;if(e.component)t=gi(e.component,e);else{var n=e.plain?void 0:ii(e),r=e.inlineTemplate?null:li(e,!0);t="_c('"+e.tag+"'"+(n?","+n:"")+(r?","+r:"")+")"}for(var i=0;i<Ls.length;i++)t=Ls[i](e,t);return t}return li(e)||"void 0"}function Xr(e){return e.staticProcessed=!0,Ps.push("with(this){return "+Qr(e)+"}"),"_m("+(Ps.length-1)+(e.staticInFor?",true":"")+")"}function ei(e){if(e.onceProcessed=!0,e.if&&!e.ifProcessed)return ti(e);if(e.staticInFor){for(var t="",n=e.parent;n;){if(n.for){t=n.key;break}n=n.parent}return t?"_o("+Qr(e)+","+Rs+++(t?","+t:"")+")":Qr(e)}return Xr(e)}function ti(e){return e.ifProcessed=!0,ni(e.ifConditions.slice())}function ni(e){function t(e){return e.once?ei(e):Qr(e)}if(!e.length)return"_e()";var n=e.shift();return n.exp?"("+n.exp+")?"+t(n.block)+":"+ni(e):""+t(n.block)}function ri(e){var t=e.for,n=e.alias,r=e.iterator1?","+e.iterator1:"",i=e.iterator2?","+e.iterator2:"";return e.forProcessed=!0,"_l(("+t+"),function("+n+r+i+"){return "+Qr(e)+"})"}function ii(e){var t="{",n=oi(e);n&&(t+=n+","),e.key&&(t+="key:"+e.key+","),e.ref&&(t+="ref:"+e.ref+","),e.refInFor&&(t+="refInFor:true,"),e.pre&&(t+="pre:true,"),e.component&&(t+='tag:"'+e.tag+'",');for(var r=0;r<Is.length;r++)t+=Is[r](e);if(e.attrs&&(t+="attrs:{"+yi(e.attrs)+"},"),e.props&&(t+="domProps:{"+yi(e.props)+"},"),e.events&&(t+=Kr(e.events,!1,Ns)+","),e.nativeEvents&&(t+=Kr(e.nativeEvents,!0,Ns)+","),e.slotTarget&&(t+="slot:"+e.slotTarget+","),e.scopedSlots&&(t+=si(e.scopedSlots)+","),e.model&&(t+="model:{value:"+e.model.value+",callback:"+e.model.callback+",expression:"+e.model.expression+"},"),e.inlineTemplate){var i=ai(e);i&&(t+=i+",")}return t=t.replace(/,$/,"")+"}",e.wrapData&&(t=e.wrapData(t)),t}function oi(e){var t=e.directives;if(t){var n,r,i,o,a="directives:[",s=!1;for(n=0,r=t.length;n<r;n++){i=t[n],o=!0;var c=Ds[i.name]||lc[i.name];c&&(o=!!c(e,i,Ns)),o&&(s=!0,a+='{name:"'+i.name+'",rawName:"'+i.rawName+'"'+(i.value?",value:("+i.value+"),expression:"+JSON.stringify(i.value):"")+(i.arg?',arg:"'+i.arg+'"':"")+(i.modifiers?",modifiers:"+JSON.stringify(i.modifiers):"")+"},")}return s?a.slice(0,-1)+"]":void 0}}function ai(e){var t=e.children[0];if(1===t.type){var n=Yr(t,Fs);return"inlineTemplate:{render:function(){"+n.render+"},staticRenderFns:["+n.staticRenderFns.map(function(e){return"function(){"+e+"}"}).join(",")+"]}"}}function si(e){return"scopedSlots:_u(["+Object.keys(e).map(function(t){return ci(t,e[t])}).join(",")+"])"}function ci(e,t){return t.for&&!t.forProcessed?ui(e,t):"{key:"+e+",fn:function("+String(t.attrsMap.scope)+"){return "+("template"===t.tag?li(t)||"void 0":Qr(t))+"}}"}function ui(e,t){var n=t.for,r=t.alias,i=t.iterator1?","+t.iterator1:"",o=t.iterator2?","+t.iterator2:"";return t.forProcessed=!0,"_l(("+n+"),function("+r+i+o+"){return "+ci(e,t)+"})"}function li(e,t){var n=e.children;if(n.length){var r=n[0];if(1===n.length&&r.for&&"template"!==r.tag&&"slot"!==r.tag)return Qr(r);var i=t?fi(n):0;return"["+n.map(vi).join(",")+"]"+(i?","+i:"")}}function fi(e){for(var t=0,n=0;n<e.length;n++){var r=e[n];if(1===r.type){if(pi(r)||r.ifConditions&&r.ifConditions.some(function(e){return pi(e.block)})){t=2;break}(di(r)||r.ifConditions&&r.ifConditions.some(function(e){return di(e.block)}))&&(t=1)}}return t}function pi(e){return void 0!==e.for||"template"===e.tag||"slot"===e.tag}function di(e){return!Ms(e.tag)}function vi(e){return 1===e.type?Qr(e):hi(e)}function hi(e){return"_v("+(2===e.type?e.expression:_i(JSON.stringify(e.text)))+")"}function mi(e){var t=e.slotName||'"default"',n=li(e),r="_t("+t+(n?","+n:""),i=e.attrs&&"{"+e.attrs.map(function(e){return Li(e.name)+":"+e.value}).join(",")+"}",o=e.attrsMap["v-bind"];return!i&&!o||n||(r+=",null"),i&&(r+=","+i),o&&(r+=(i?"":",null")+","+o),r+")"}function gi(e,t){var n=t.inlineTemplate?null:li(t,!0);return"_c("+e+","+ii(t)+(n?","+n:"")+")"}function yi(e){for(var t="",n=0;n<e.length;n++){var r=e[n];t+='"'+r.name+'":'+_i(r.value)+","}return t.slice(0,-1)}function _i(e){return e.replace(/\u2028/g,"\\u2028").replace(/\u2029/g,"\\u2029")}function bi(e,t){var n=_r(e.trim(),t);Fr(n,t);var r=Yr(n,t);return{ast:n,render:r.render,staticRenderFns:r.staticRenderFns}}function $i(e,t){try{return new Function(e)}catch(n){return t.push({err:n,code:e}),y}}function Ci(e,t){var n=(t.warn,dn(e,"class"));n&&(e.staticClass=JSON.stringify(n));var r=pn(e,"class",!1);r&&(e.classBinding=r)}function xi(e){var t="";return e.staticClass&&(t+="staticClass:"+e.staticClass+","),e.classBinding&&(t+="class:"+e.classBinding+","),t}function wi(e,t){var n=(t.warn,dn(e,"style"));n&&(e.staticStyle=JSON.stringify(Ta(n)));var r=pn(e,"style",!1);r&&(e.styleBinding=r)}function ki(e){var t="";return e.staticStyle&&(t+="staticStyle:"+e.staticStyle+","),e.styleBinding&&(t+="style:("+e.styleBinding+"),"),t}function Ai(e,t){t.value&&cn(e,"textContent","_s("+t.value+")")}function Oi(e,t){t.value&&cn(e,"innerHTML","_s("+t.value+")")}function Si(e){if(e.outerHTML)return e.outerHTML;var t=document.createElement("div");return t.appendChild(e.cloneNode(!0)),t.innerHTML}var Ti=Object.prototype.toString,Ei=l("slot,component",!0),ji=Object.prototype.hasOwnProperty,Ni=/-(\w)/g,Li=d(function(e){return e.replace(Ni,function(e,t){return t?t.toUpperCase():""})}),Ii=d(function(e){return e.charAt(0).toUpperCase()+e.slice(1)}),Di=/([^-])([A-Z])/g,Mi=d(function(e){return e.replace(Di,"$1-$2").replace(Di,"$1-$2").toLowerCase()}),Pi=function(){return!1},Ri=function(e){return e},Fi="data-server-rendered",Bi=["component","directive","filter"],Hi=["beforeCreate","created","beforeMount","mounted","beforeUpdate","updated","beforeDestroy","destroyed","activated","deactivated"],Ui={optionMergeStrategies:Object.create(null),silent:!1,productionTip:!1,devtools:!1,performance:!1,errorHandler:null,ignoredElements:[],keyCodes:Object.create(null),isReservedTag:Pi,isReservedAttr:Pi,isUnknownElement:Pi,getTagNamespace:y,parsePlatformTagName:Ri,mustUseProp:Pi,_lifecycleHooks:Hi},Vi=Object.freeze({}),zi=/[^\w.$]/,Ji=y,Ki="__proto__"in{},qi="undefined"!=typeof window,Wi=qi&&window.navigator.userAgent.toLowerCase(),Zi=Wi&&/msie|trident/.test(Wi),Gi=Wi&&Wi.indexOf("msie 9.0")>0,Yi=Wi&&Wi.indexOf("edge/")>0,Qi=Wi&&Wi.indexOf("android")>0,Xi=Wi&&/iphone|ipad|ipod|ios/.test(Wi),eo=Wi&&/chrome\/\d+/.test(Wi)&&!Yi,to=!1;if(qi)try{var no={};Object.defineProperty(no,"passive",{get:function(){to=!0}}),window.addEventListener("test-passive",null,no)}catch(e){}var ro,io,oo=function(){return void 0===ro&&(ro=!qi&&"undefined"!=typeof global&&"server"===global.process.env.VUE_ENV),ro},ao=qi&&window.__VUE_DEVTOOLS_GLOBAL_HOOK__,so="undefined"!=typeof Symbol&&A(Symbol)&&"undefined"!=typeof Reflect&&A(Reflect.ownKeys),co=function(){function e(){r=!1;var e=n.slice(0);n.length=0;for(var t=0;t<e.length;t++)e[t]()}var t,n=[],r=!1;if("undefined"!=typeof Promise&&A(Promise)){var i=Promise.resolve(),o=function(e){console.error(e)};t=function(){i.then(e).catch(o),Xi&&setTimeout(y)}}else if("undefined"==typeof MutationObserver||!A(MutationObserver)&&"[object MutationObserverConstructor]"!==MutationObserver.toString())t=function(){setTimeout(e,0)};else{var a=1,s=new MutationObserver(e),c=document.createTextNode(String(a));s.observe(c,{characterData:!0}),t=function(){a=(a+1)%2,c.data=String(a)}}return function(e,i){var o;if(n.push(function(){if(e)try{e.call(i)}catch(e){k(e,i,"nextTick")}else o&&o(i)}),r||(r=!0,t()),!e&&"undefined"!=typeof Promise)return new Promise(function(e,t){o=e})}}();io="undefined"!=typeof Set&&A(Set)?Set:function(){function e(){this.set=Object.create(null)}return e.prototype.has=function(e){return!0===this.set[e]},e.prototype.add=function(e){this.set[e]=!0},e.prototype.clear=function(){this.set=Object.create(null)},e}();var uo=0,lo=function(){this.id=uo++,this.subs=[]};lo.prototype.addSub=function(e){this.subs.push(e)},lo.prototype.removeSub=function(e){f(this.subs,e)},lo.prototype.depend=function(){lo.target&&lo.target.addDep(this)},lo.prototype.notify=function(){for(var e=this.subs.slice(),t=0,n=e.length;t<n;t++)e[t].update()},lo.target=null;var fo=[],po=Array.prototype,vo=Object.create(po);["push","pop","shift","unshift","splice","sort","reverse"].forEach(function(e){var t=po[e];x(vo,e,function(){for(var n=arguments,r=arguments.length,i=new Array(r);r--;)i[r]=n[r];var o,a=t.apply(this,i),s=this.__ob__;switch(e){case"push":case"unshift":o=i;break;case"splice":o=i.slice(2)}return o&&s.observeArray(o),s.dep.notify(),a})});var ho=Object.getOwnPropertyNames(vo),mo={shouldConvert:!0,isSettingProps:!1},go=function(e){if(this.value=e,this.dep=new lo,this.vmCount=0,x(e,"__ob__",this),Array.isArray(e)){(Ki?T:E)(e,vo,ho),this.observeArray(e)}else this.walk(e)};go.prototype.walk=function(e){for(var t=Object.keys(e),n=0;n<t.length;n++)N(e,t[n],e[t[n]])},go.prototype.observeArray=function(e){for(var t=0,n=e.length;t<n;t++)j(e[t])};var yo=Ui.optionMergeStrategies;yo.data=function(e,t,n){return n?e||t?function(){var r="function"==typeof t?t.call(n):t,i="function"==typeof e?e.call(n):void 0;return r?M(r,i):i}:void 0:t?"function"!=typeof t?e:e?function(){return M(t.call(this),e.call(this))}:t:e},Hi.forEach(function(e){yo[e]=P}),Bi.forEach(function(e){yo[e+"s"]=R}),yo.watch=function(e,t){if(!t)return Object.create(e||null);if(!e)return t;var n={};m(n,e);for(var r in t){var i=n[r],o=t[r];i&&!Array.isArray(i)&&(i=[i]),n[r]=i?i.concat(o):[o]}return n},yo.props=yo.methods=yo.computed=function(e,t){if(!t)return Object.create(e||null);if(!e)return t;var n=Object.create(null);return m(n,e),m(n,t),n};var _o=function(e,t){return void 0===t?e:t},bo=function(e,t,n,r,i,o,a){this.tag=e,this.data=t,this.children=n,this.text=r,this.elm=i,this.ns=void 0,this.context=o,this.functionalContext=void 0,this.key=t&&t.key,this.componentOptions=a,this.componentInstance=void 0,this.parent=void 0,this.raw=!1,this.isStatic=!1,this.isRootInsert=!0,this.isComment=!1,this.isCloned=!1,this.isOnce=!1},$o={child:{}};$o.child.get=function(){return this.componentInstance},Object.defineProperties(bo.prototype,$o);var Co,xo=function(){var e=new bo;return e.text="",e.isComment=!0,e},wo=d(function(e){var t="&"===e.charAt(0);e=t?e.slice(1):e;var n="~"===e.charAt(0);e=n?e.slice(1):e;var r="!"===e.charAt(0);return e=r?e.slice(1):e,{name:e,once:n,capture:r,passive:t}}),ko=null,Ao=[],Oo=[],So={},To=!1,Eo=!1,jo=0,No=0,Lo=function(e,t,n,r){this.vm=e,e._watchers.push(this),r?(this.deep=!!r.deep,this.user=!!r.user,this.lazy=!!r.lazy,this.sync=!!r.sync):this.deep=this.user=this.lazy=this.sync=!1,this.cb=n,this.id=++No,this.active=!0,this.dirty=this.lazy,this.deps=[],this.newDeps=[],this.depIds=new io,this.newDepIds=new io,this.expression="","function"==typeof t?this.getter=t:(this.getter=w(t),this.getter||(this.getter=function(){})),this.value=this.lazy?void 0:this.get()};Lo.prototype.get=function(){O(this);var e,t=this.vm;if(this.user)try{e=this.getter.call(t,t)}catch(e){k(e,t,'getter for watcher "'+this.expression+'"')}else e=this.getter.call(t,t);return this.deep&&Se(e),S(),this.cleanupDeps(),e},Lo.prototype.addDep=function(e){var t=e.id;this.newDepIds.has(t)||(this.newDepIds.add(t),this.newDeps.push(e),this.depIds.has(t)||e.addSub(this))},Lo.prototype.cleanupDeps=function(){for(var e=this,t=this.deps.length;t--;){var n=e.deps[t];e.newDepIds.has(n.id)||n.removeSub(e)}var r=this.depIds;this.depIds=this.newDepIds,this.newDepIds=r,this.newDepIds.clear(),r=this.deps,this.deps=this.newDeps,this.newDeps=r,this.newDeps.length=0},Lo.prototype.update=function(){this.lazy?this.dirty=!0:this.sync?this.run():Oe(this)},Lo.prototype.run=function(){if(this.active){var e=this.get();if(e!==this.value||o(e)||this.deep){var t=this.value;if(this.value=e,this.user)try{this.cb.call(this.vm,e,t)}catch(e){k(e,this.vm,'callback for watcher "'+this.expression+'"')}else this.cb.call(this.vm,e,t)}}},Lo.prototype.evaluate=function(){this.value=this.get(),this.dirty=!1},Lo.prototype.depend=function(){for(var e=this,t=this.deps.length;t--;)e.deps[t].depend()},Lo.prototype.teardown=function(){var e=this;if(this.active){this.vm._isBeingDestroyed||f(this.vm._watchers,this);for(var t=this.deps.length;t--;)e.deps[t].removeSub(e);this.active=!1}};var Io=new io,Do={enumerable:!0,configurable:!0,get:y,set:y},Mo={lazy:!0},Po={init:function(e,t,n,r){if(!e.componentInstance||e.componentInstance._isDestroyed){(e.componentInstance=qe(e,ko,n,r)).$mount(t?e.elm:void 0,t)}else if(e.data.keepAlive){var i=e;Po.prepatch(i,i)}},prepatch:function(e,t){var n=t.componentOptions;ge(t.componentInstance=e.componentInstance,n.propsData,n.listeners,t,n.children)},insert:function(e){var t=e.context,n=e.componentInstance;n._isMounted||(n._isMounted=!0,$e(n,"mounted")),e.data.keepAlive&&(t._isMounted?ke(n):_e(n,!0))},destroy:function(e){var t=e.componentInstance;t._isDestroyed||(e.data.keepAlive?be(t,!0):t.$destroy())}},Ro=Object.keys(Po),Fo=1,Bo=2,Ho=0;!function(e){e.prototype._init=function(e){var t=this;t._uid=Ho++,t._isVue=!0,e&&e._isComponent?lt(t,e):t.$options=H(ft(t.constructor),e||{},t),t._renderProxy=t,t._self=t,he(t),ce(t),ut(t),$e(t,"beforeCreate"),Ue(t),je(t),He(t),$e(t,"created"),t.$options.el&&t.$mount(t.$options.el)}}(vt),function(e){var t={};t.get=function(){return this._data};var n={};n.get=function(){return this._props},Object.defineProperty(e.prototype,"$data",t),Object.defineProperty(e.prototype,"$props",n),e.prototype.$set=L,e.prototype.$delete=I,e.prototype.$watch=function(e,t,n){var r=this;n=n||{},n.user=!0;var i=new Lo(r,e,t,n);return n.immediate&&t.call(r,i.value),function(){i.teardown()}}}(vt),function(e){var t=/^hook:/;e.prototype.$on=function(e,n){var r=this,i=this;if(Array.isArray(e))for(var o=0,a=e.length;o<a;o++)r.$on(e[o],n);else(i._events[e]||(i._events[e]=[])).push(n),t.test(e)&&(i._hasHookEvent=!0);return i},e.prototype.$once=function(e,t){function n(){r.$off(e,n),t.apply(r,arguments)}var r=this;return n.fn=t,r.$on(e,n),r},e.prototype.$off=function(e,t){var n=this,r=this;if(!arguments.length)return r._events=Object.create(null),r;if(Array.isArray(e)){for(var i=0,o=e.length;i<o;i++)n.$off(e[i],t);return r}var a=r._events[e];if(!a)return r;if(1===arguments.length)return r._events[e]=null,r;for(var s,c=a.length;c--;)if((s=a[c])===t||s.fn===t){a.splice(c,1);break}return r},e.prototype.$emit=function(e){var t=this,n=t._events[e];if(n){n=n.length>1?h(n):n;for(var r=h(arguments,1),i=0,o=n.length;i<o;i++)n[i].apply(t,r)}return t}}(vt),function(e){e.prototype._update=function(e,t){var n=this;n._isMounted&&$e(n,"beforeUpdate");var r=n.$el,i=n._vnode,o=ko;ko=n,n._vnode=e,n.$el=i?n.__patch__(i,e):n.__patch__(n.$el,e,t,!1,n.$options._parentElm,n.$options._refElm),ko=o,r&&(r.__vue__=null),n.$el&&(n.$el.__vue__=n),n.$vnode&&n.$parent&&n.$vnode===n.$parent._vnode&&(n.$parent.$el=n.$el)},e.prototype.$forceUpdate=function(){var e=this;e._watcher&&e._watcher.update()},e.prototype.$destroy=function(){var e=this;if(!e._isBeingDestroyed){$e(e,"beforeDestroy"),e._isBeingDestroyed=!0;var t=e.$parent;!t||t._isBeingDestroyed||e.$options.abstract||f(t.$children,e),e._watcher&&e._watcher.teardown();for(var n=e._watchers.length;n--;)e._watchers[n].teardown();e._data.__ob__&&e._data.__ob__.vmCount--,e._isDestroyed=!0,e.__patch__(e._vnode,null),$e(e,"destroyed"),e.$off(),e.$el&&(e.$el.__vue__=null),e.$options._parentElm=e.$options._refElm=null}}}(vt),function(e){e.prototype.$nextTick=function(e){return co(e,this)},e.prototype._render=function(){var e=this,t=e.$options,n=t.render,r=t.staticRenderFns,i=t._parentVnode;if(e._isMounted)for(var o in e.$slots)e.$slots[o]=Z(e.$slots[o]);e.$scopedSlots=i&&i.data.scopedSlots||Vi,r&&!e._staticTrees&&(e._staticTrees=[]),e.$vnode=i;var a;try{a=n.call(e._renderProxy,e.$createElement)}catch(t){k(t,e,"render function"),a=e._vnode}return a instanceof bo||(a=xo()),a.parent=i,a},e.prototype._o=at,e.prototype._n=u,e.prototype._s=c,e.prototype._l=et,e.prototype._t=tt,e.prototype._q=_,e.prototype._i=b,e.prototype._m=ot,e.prototype._f=nt,e.prototype._k=rt,e.prototype._b=it,e.prototype._v=q,e.prototype._e=xo,e.prototype._u=ve}(vt);var Uo=[String,RegExp],Vo={name:"keep-alive",abstract:!0,props:{include:Uo,exclude:Uo},created:function(){this.cache=Object.create(null)},destroyed:function(){var e=this;for(var t in e.cache)wt(e.cache[t])},watch:{include:function(e){xt(this.cache,this._vnode,function(t){return Ct(e,t)})},exclude:function(e){xt(this.cache,this._vnode,function(t){return!Ct(e,t)})}},render:function(){var e=se(this.$slots.default),t=e&&e.componentOptions;if(t){var n=$t(t);if(n&&(this.include&&!Ct(this.include,n)||this.exclude&&Ct(this.exclude,n)))return e;var r=null==e.key?t.Ctor.cid+(t.tag?"::"+t.tag:""):e.key;this.cache[r]?e.componentInstance=this.cache[r].componentInstance:this.cache[r]=e,e.data.keepAlive=!0}return e}},zo={KeepAlive:Vo};!function(e){var t={};t.get=function(){return Ui},Object.defineProperty(e,"config",t),e.util={warn:Ji,extend:m,mergeOptions:H,defineReactive:N},e.set=L,e.delete=I,e.nextTick=co,e.options=Object.create(null),Bi.forEach(function(t){e.options[t+"s"]=Object.create(null)}),e.options._base=e,m(e.options.components,zo),ht(e),mt(e),gt(e),bt(e)}(vt),Object.defineProperty(vt.prototype,"$isServer",{get:oo}),Object.defineProperty(vt.prototype,"$ssrContext",{get:function(){return this.$vnode.ssrContext}}),vt.version="2.3.4";var Jo,Ko,qo,Wo,Zo,Go,Yo,Qo,Xo,ea=l("style,class"),ta=l("input,textarea,option,select"),na=function(e,t,n){return"value"===n&&ta(e)&&"button"!==t||"selected"===n&&"option"===e||"checked"===n&&"input"===e||"muted"===n&&"video"===e},ra=l("contenteditable,draggable,spellcheck"),ia=l("allowfullscreen,async,autofocus,autoplay,checked,compact,controls,declare,default,defaultchecked,defaultmuted,defaultselected,defer,disabled,enabled,formnovalidate,hidden,indeterminate,inert,ismap,itemscope,loop,multiple,muted,nohref,noresize,noshade,novalidate,nowrap,open,pauseonexit,readonly,required,reversed,scoped,seamless,selected,sortable,translate,truespeed,typemustmatch,visible"),oa="http://www.w3.org/1999/xlink",aa=function(e){return":"===e.charAt(5)&&"xlink"===e.slice(0,5)},sa=function(e){return aa(e)?e.slice(6,e.length):""},ca=function(e){return null==e||!1===e},ua={svg:"http://www.w3.org/2000/svg",math:"http://www.w3.org/1998/Math/MathML"},la=l("html,body,base,head,link,meta,style,title,address,article,aside,footer,header,h1,h2,h3,h4,h5,h6,hgroup,nav,section,div,dd,dl,dt,figcaption,figure,hr,img,li,main,ol,p,pre,ul,a,b,abbr,bdi,bdo,br,cite,code,data,dfn,em,i,kbd,mark,q,rp,rt,rtc,ruby,s,samp,small,span,strong,sub,sup,time,u,var,wbr,area,audio,map,track,video,embed,object,param,source,canvas,script,noscript,del,ins,caption,col,colgroup,table,thead,tbody,td,th,tr,button,datalist,fieldset,form,input,label,legend,meter,optgroup,option,output,progress,select,textarea,details,dialog,menu,menuitem,summary,content,element,shadow,template"),fa=l("svg,animate,circle,clippath,cursor,defs,desc,ellipse,filter,font-face,foreignObject,g,glyph,image,line,marker,mask,missing-glyph,path,pattern,polygon,polyline,rect,switch,symbol,text,textpath,tspan,use,view",!0),pa=function(e){return"pre"===e},da=function(e){return la(e)||fa(e)},va=Object.create(null),ha=Object.freeze({createElement:Lt,createElementNS:It,createTextNode:Dt,createComment:Mt,insertBefore:Pt,removeChild:Rt,appendChild:Ft,parentNode:Bt,nextSibling:Ht,tagName:Ut,setTextContent:Vt,setAttribute:zt}),ma={create:function(e,t){Jt(t)},update:function(e,t){
e.data.ref!==t.data.ref&&(Jt(e,!0),Jt(t))},destroy:function(e){Jt(e,!0)}},ga=new bo("",{},[]),ya=["create","activate","update","remove","destroy"],_a={create:Zt,update:Zt,destroy:function(e){Zt(e,ga)}},ba=Object.create(null),$a=[ma,_a],Ca={create:en,update:en},xa={create:nn,update:nn},wa=/[\w).+\-_$\]]/,ka="__r",Aa="__c",Oa={create:En,update:En},Sa={create:jn,update:jn},Ta=d(function(e){var t={},n=/;(?![^(]*\))/g,r=/:(.+)/;return e.split(n).forEach(function(e){if(e){var n=e.split(r);n.length>1&&(t[n[0].trim()]=n[1].trim())}}),t}),Ea=/^--/,ja=/\s*!important$/,Na=function(e,t,n){if(Ea.test(t))e.style.setProperty(t,n);else if(ja.test(n))e.style.setProperty(t,n.replace(ja,""),"important");else{var r=Ia(t);if(Array.isArray(n))for(var i=0,o=n.length;i<o;i++)e.style[r]=n[i];else e.style[r]=n}},La=["Webkit","Moz","ms"],Ia=d(function(e){if(Xo=Xo||document.createElement("div"),"filter"!==(e=Li(e))&&e in Xo.style)return e;for(var t=e.charAt(0).toUpperCase()+e.slice(1),n=0;n<La.length;n++){var r=La[n]+t;if(r in Xo.style)return r}}),Da={create:Rn,update:Rn},Ma=d(function(e){return{enterClass:e+"-enter",enterToClass:e+"-enter-to",enterActiveClass:e+"-enter-active",leaveClass:e+"-leave",leaveToClass:e+"-leave-to",leaveActiveClass:e+"-leave-active"}}),Pa=qi&&!Gi,Ra="transition",Fa="animation",Ba="transition",Ha="transitionend",Ua="animation",Va="animationend";Pa&&(void 0===window.ontransitionend&&void 0!==window.onwebkittransitionend&&(Ba="WebkitTransition",Ha="webkitTransitionEnd"),void 0===window.onanimationend&&void 0!==window.onwebkitanimationend&&(Ua="WebkitAnimation",Va="webkitAnimationEnd"));var za=qi&&window.requestAnimationFrame?window.requestAnimationFrame.bind(window):setTimeout,Ja=/\b(transform|all)(,|$)/,Ka=qi?{create:Xn,activate:Xn,remove:function(e,t){!0!==e.data.show?Gn(e,t):t()}}:{},qa=[Ca,xa,Oa,Sa,Da,Ka],Wa=qa.concat($a),Za=function(r){function o(e){return new bo(E.tagName(e).toLowerCase(),{},[],void 0,e)}function a(e,t){function n(){0==--n.listeners&&s(e)}return n.listeners=t,n}function s(e){var n=E.parentNode(e);t(n)&&E.removeChild(n,e)}function c(e,r,i,o,a){if(e.isRootInsert=!a,!u(e,r,i,o)){var s=e.data,c=e.children,l=e.tag;t(l)?(e.elm=e.ns?E.createElementNS(e.ns,l):E.createElement(l,e),g(e),v(e,c,r),t(s)&&m(e,r),d(i,e.elm,o)):n(e.isComment)?(e.elm=E.createComment(e.text),d(i,e.elm,o)):(e.elm=E.createTextNode(e.text),d(i,e.elm,o))}}function u(e,r,i,o){var a=e.data;if(t(a)){var s=t(e.componentInstance)&&a.keepAlive;if(t(a=a.hook)&&t(a=a.init)&&a(e,!1,i,o),t(e.componentInstance))return f(e,r),n(s)&&p(e,r,i,o),!0}}function f(e,n){t(e.data.pendingInsert)&&(n.push.apply(n,e.data.pendingInsert),e.data.pendingInsert=null),e.elm=e.componentInstance.$el,h(e)?(m(e,n),g(e)):(Jt(e),n.push(e))}function p(e,n,r,i){for(var o,a=e;a.componentInstance;)if(a=a.componentInstance._vnode,t(o=a.data)&&t(o=o.transition)){for(o=0;o<S.activate.length;++o)S.activate[o](ga,a);n.push(a);break}d(r,e.elm,i)}function d(e,n,r){t(e)&&(t(r)?r.parentNode===e&&E.insertBefore(e,n,r):E.appendChild(e,n))}function v(e,t,n){if(Array.isArray(t))for(var r=0;r<t.length;++r)c(t[r],n,e.elm,null,!0);else i(e.text)&&E.appendChild(e.elm,E.createTextNode(e.text))}function h(e){for(;e.componentInstance;)e=e.componentInstance._vnode;return t(e.tag)}function m(e,n){for(var r=0;r<S.create.length;++r)S.create[r](ga,e);A=e.data.hook,t(A)&&(t(A.create)&&A.create(ga,e),t(A.insert)&&n.push(e))}function g(e){for(var n,r=e;r;)t(n=r.context)&&t(n=n.$options._scopeId)&&E.setAttribute(e.elm,n,""),r=r.parent;t(n=ko)&&n!==e.context&&t(n=n.$options._scopeId)&&E.setAttribute(e.elm,n,"")}function y(e,t,n,r,i,o){for(;r<=i;++r)c(n[r],o,e,t)}function _(e){var n,r,i=e.data;if(t(i))for(t(n=i.hook)&&t(n=n.destroy)&&n(e),n=0;n<S.destroy.length;++n)S.destroy[n](e);if(t(n=e.children))for(r=0;r<e.children.length;++r)_(e.children[r])}function b(e,n,r,i){for(;r<=i;++r){var o=n[r];t(o)&&(t(o.tag)?($(o),_(o)):s(o.elm))}}function $(e,n){if(t(n)||t(e.data)){var r,i=S.remove.length+1;for(t(n)?n.listeners+=i:n=a(e.elm,i),t(r=e.componentInstance)&&t(r=r._vnode)&&t(r.data)&&$(r,n),r=0;r<S.remove.length;++r)S.remove[r](e,n);t(r=e.data.hook)&&t(r=r.remove)?r(e,n):n()}else s(e.elm)}function C(n,r,i,o,a){for(var s,u,l,f,p=0,d=0,v=r.length-1,h=r[0],m=r[v],g=i.length-1,_=i[0],$=i[g],C=!a;p<=v&&d<=g;)e(h)?h=r[++p]:e(m)?m=r[--v]:Kt(h,_)?(x(h,_,o),h=r[++p],_=i[++d]):Kt(m,$)?(x(m,$,o),m=r[--v],$=i[--g]):Kt(h,$)?(x(h,$,o),C&&E.insertBefore(n,h.elm,E.nextSibling(m.elm)),h=r[++p],$=i[--g]):Kt(m,_)?(x(m,_,o),C&&E.insertBefore(n,m.elm,h.elm),m=r[--v],_=i[++d]):(e(s)&&(s=Wt(r,p,v)),u=t(_.key)?s[_.key]:null,e(u)?(c(_,o,n,h.elm),_=i[++d]):(l=r[u],Kt(l,_)?(x(l,_,o),r[u]=void 0,C&&E.insertBefore(n,_.elm,h.elm),_=i[++d]):(c(_,o,n,h.elm),_=i[++d])));p>v?(f=e(i[g+1])?null:i[g+1].elm,y(n,f,i,d,g,o)):d>g&&b(n,r,p,v)}function x(r,i,o,a){if(r!==i){if(n(i.isStatic)&&n(r.isStatic)&&i.key===r.key&&(n(i.isCloned)||n(i.isOnce)))return i.elm=r.elm,void(i.componentInstance=r.componentInstance);var s,c=i.data;t(c)&&t(s=c.hook)&&t(s=s.prepatch)&&s(r,i);var u=i.elm=r.elm,l=r.children,f=i.children;if(t(c)&&h(i)){for(s=0;s<S.update.length;++s)S.update[s](r,i);t(s=c.hook)&&t(s=s.update)&&s(r,i)}e(i.text)?t(l)&&t(f)?l!==f&&C(u,l,f,o,a):t(f)?(t(r.text)&&E.setTextContent(u,""),y(u,null,f,0,f.length-1,o)):t(l)?b(u,l,0,l.length-1):t(r.text)&&E.setTextContent(u,""):r.text!==i.text&&E.setTextContent(u,i.text),t(c)&&t(s=c.hook)&&t(s=s.postpatch)&&s(r,i)}}function w(e,r,i){if(n(i)&&t(e.parent))e.parent.data.pendingInsert=r;else for(var o=0;o<r.length;++o)r[o].data.hook.insert(r[o])}function k(e,n,r){n.elm=e;var i=n.tag,o=n.data,a=n.children;if(t(o)&&(t(A=o.hook)&&t(A=A.init)&&A(n,!0),t(A=n.componentInstance)))return f(n,r),!0;if(t(i)){if(t(a))if(e.hasChildNodes()){for(var s=!0,c=e.firstChild,u=0;u<a.length;u++){if(!c||!k(c,a[u],r)){s=!1;break}c=c.nextSibling}if(!s||c)return!1}else v(n,a,r);if(t(o))for(var l in o)if(!j(l)){m(n,r);break}}else e.data!==n.text&&(e.data=n.text);return!0}var A,O,S={},T=r.modules,E=r.nodeOps;for(A=0;A<ya.length;++A)for(S[ya[A]]=[],O=0;O<T.length;++O)t(T[O][ya[A]])&&S[ya[A]].push(T[O][ya[A]]);var j=l("attrs,style,class,staticClass,staticStyle,key");return function(r,i,a,s,u,l){if(e(i))return void(t(r)&&_(r));var f=!1,p=[];if(e(r))f=!0,c(i,p,u,l);else{var d=t(r.nodeType);if(!d&&Kt(r,i))x(r,i,p,s);else{if(d){if(1===r.nodeType&&r.hasAttribute(Fi)&&(r.removeAttribute(Fi),a=!0),n(a)&&k(r,i,p))return w(i,p,!0),r;r=o(r)}var v=r.elm,m=E.parentNode(v);if(c(i,p,v._leaveCb?null:m,E.nextSibling(v)),t(i.parent)){for(var g=i.parent;g;)g.elm=i.elm,g=g.parent;if(h(i))for(var y=0;y<S.create.length;++y)S.create[y](ga,i.parent)}t(m)?b(m,[r],0,0):t(r.tag)&&_(r)}}return w(i,p,f),i.elm}}({nodeOps:ha,modules:Wa});Gi&&document.addEventListener("selectionchange",function(){var e=document.activeElement;e&&e.vmodel&&or(e,"input")});var Ga={inserted:function(e,t,n){if("select"===n.tag){var r=function(){er(e,t,n.context)};r(),(Zi||Yi)&&setTimeout(r,0)}else"textarea"!==n.tag&&"text"!==e.type&&"password"!==e.type||(e._vModifiers=t.modifiers,t.modifiers.lazy||(e.addEventListener("change",ir),Qi||(e.addEventListener("compositionstart",rr),e.addEventListener("compositionend",ir)),Gi&&(e.vmodel=!0)))},componentUpdated:function(e,t,n){if("select"===n.tag){er(e,t,n.context);(e.multiple?t.value.some(function(t){return tr(t,e.options)}):t.value!==t.oldValue&&tr(t.value,e.options))&&or(e,"change")}}},Ya={bind:function(e,t,n){var r=t.value;n=ar(n);var i=n.data&&n.data.transition,o=e.__vOriginalDisplay="none"===e.style.display?"":e.style.display;r&&i&&!Gi?(n.data.show=!0,Zn(n,function(){e.style.display=o})):e.style.display=r?o:"none"},update:function(e,t,n){var r=t.value;r!==t.oldValue&&(n=ar(n),n.data&&n.data.transition&&!Gi?(n.data.show=!0,r?Zn(n,function(){e.style.display=e.__vOriginalDisplay}):Gn(n,function(){e.style.display="none"})):e.style.display=r?e.__vOriginalDisplay:"none")},unbind:function(e,t,n,r,i){i||(e.style.display=e.__vOriginalDisplay)}},Qa={model:Ga,show:Ya},Xa={name:String,appear:Boolean,css:Boolean,mode:String,type:String,enterClass:String,leaveClass:String,enterToClass:String,leaveToClass:String,enterActiveClass:String,leaveActiveClass:String,appearClass:String,appearActiveClass:String,appearToClass:String,duration:[Number,String,Object]},es={name:"transition",props:Xa,abstract:!0,render:function(e){var t=this,n=this.$slots.default;if(n&&(n=n.filter(function(e){return e.tag}),n.length)){var r=this.mode,o=n[0];if(lr(this.$vnode))return o;var a=sr(o);if(!a)return o;if(this._leaving)return ur(e,o);var s="__transition-"+this._uid+"-";a.key=null==a.key?s+a.tag:i(a.key)?0===String(a.key).indexOf(s)?a.key:s+a.key:a.key;var c=(a.data||(a.data={})).transition=cr(this),u=this._vnode,l=sr(u);if(a.data.directives&&a.data.directives.some(function(e){return"show"===e.name})&&(a.data.show=!0),l&&l.data&&!fr(a,l)){var f=l&&(l.data.transition=m({},c));if("out-in"===r)return this._leaving=!0,Q(f,"afterLeave",function(){t._leaving=!1,t.$forceUpdate()}),ur(e,o);if("in-out"===r){var p,d=function(){p()};Q(c,"afterEnter",d),Q(c,"enterCancelled",d),Q(f,"delayLeave",function(e){p=e})}}return o}}},ts=m({tag:String,moveClass:String},Xa);delete ts.mode;var ns={props:ts,render:function(e){for(var t=this.tag||this.$vnode.data.tag||"span",n=Object.create(null),r=this.prevChildren=this.children,i=this.$slots.default||[],o=this.children=[],a=cr(this),s=0;s<i.length;s++){var c=i[s];c.tag&&null!=c.key&&0!==String(c.key).indexOf("__vlist")&&(o.push(c),n[c.key]=c,(c.data||(c.data={})).transition=a)}if(r){for(var u=[],l=[],f=0;f<r.length;f++){var p=r[f];p.data.transition=a,p.data.pos=p.elm.getBoundingClientRect(),n[p.key]?u.push(p):l.push(p)}this.kept=e(t,null,u),this.removed=l}return e(t,null,o)},beforeUpdate:function(){this.__patch__(this._vnode,this.kept,!1,!0),this._vnode=this.kept},updated:function(){var e=this.prevChildren,t=this.moveClass||(this.name||"v")+"-move";if(e.length&&this.hasMove(e[0].elm,t)){e.forEach(pr),e.forEach(dr),e.forEach(vr);var n=document.body;n.offsetHeight;e.forEach(function(e){if(e.data.moved){var n=e.elm,r=n.style;Vn(n,t),r.transform=r.WebkitTransform=r.transitionDuration="",n.addEventListener(Ha,n._moveCb=function e(r){r&&!/transform$/.test(r.propertyName)||(n.removeEventListener(Ha,e),n._moveCb=null,zn(n,t))})}})}},methods:{hasMove:function(e,t){if(!Pa)return!1;if(null!=this._hasMove)return this._hasMove;var n=e.cloneNode();e._transitionClasses&&e._transitionClasses.forEach(function(e){Bn(n,e)}),Fn(n,t),n.style.display="none",this.$el.appendChild(n);var r=Kn(n);return this.$el.removeChild(n),this._hasMove=r.hasTransform}}},rs={Transition:es,TransitionGroup:ns};vt.config.mustUseProp=na,vt.config.isReservedTag=da,vt.config.isReservedAttr=ea,vt.config.getTagNamespace=Et,vt.config.isUnknownElement=jt,m(vt.options.directives,Qa),m(vt.options.components,rs),vt.prototype.__patch__=qi?Za:y,vt.prototype.$mount=function(e,t){return e=e&&qi?Nt(e):void 0,me(this,e,t)},setTimeout(function(){Ui.devtools&&ao&&ao.emit("init",vt)},0);var is,os=!!qi&&function(e,t){var n=document.createElement("div");return n.innerHTML='<div a="'+e+'">',n.innerHTML.indexOf(t)>0}("\n","&#10;"),as=l("area,base,br,col,embed,frame,hr,img,input,isindex,keygen,link,meta,param,source,track,wbr"),ss=l("colgroup,dd,dt,li,options,p,td,tfoot,th,thead,tr,source"),cs=l("address,article,aside,base,blockquote,body,caption,col,colgroup,dd,details,dialog,div,dl,dt,fieldset,figcaption,figure,footer,form,h1,h2,h3,h4,h5,h6,head,header,hgroup,hr,html,legend,li,menuitem,meta,optgroup,option,param,rp,rt,source,style,summary,tbody,td,tfoot,th,thead,title,tr,track"),us=/([^\s"'<>\/=]+)/,ls=/(?:=)/,fs=[/"([^"]*)"+/.source,/'([^']*)'+/.source,/([^\s"'=<>`]+)/.source],ps=new RegExp("^\\s*"+us.source+"(?:\\s*("+ls.source+")\\s*(?:"+fs.join("|")+"))?"),ds="[a-zA-Z_][\\w\\-\\.]*",vs="((?:"+ds+"\\:)?"+ds+")",hs=new RegExp("^<"+vs),ms=/^\s*(\/?)>/,gs=new RegExp("^<\\/"+vs+"[^>]*>"),ys=/^<!DOCTYPE [^>]+>/i,_s=/^<!--/,bs=/^<!\[/,$s=!1;"x".replace(/x(.)?/g,function(e,t){$s=""===t});var Cs,xs,ws,ks,As,Os,Ss,Ts,Es,js,Ns,Ls,Is,Ds,Ms,Ps,Rs,Fs,Bs=l("script,style,textarea",!0),Hs={},Us={"&lt;":"<","&gt;":">","&quot;":'"',"&amp;":"&","&#10;":"\n"},Vs=/&(?:lt|gt|quot|amp);/g,zs=/&(?:lt|gt|quot|amp|#10);/g,Js=/\{\{((?:.|\n)+?)\}\}/g,Ks=/[-.*+?^${}()|[\]\/\\]/g,qs=d(function(e){var t=e[0].replace(Ks,"\\$&"),n=e[1].replace(Ks,"\\$&");return new RegExp(t+"((?:.|\\n)+?)"+n,"g")}),Ws=/^@|^v-on:/,Zs=/^v-|^@|^:/,Gs=/(.*?)\s+(?:in|of)\s+(.*)/,Ys=/\((\{[^}]*\}|[^,]*),([^,]*)(?:,([^,]*))?\)/,Qs=/:(.*)$/,Xs=/^:|^v-bind:/,ec=/\.[^.]+/g,tc=d(hr),nc=/^xmlns:NS\d+/,rc=/^NS\d+:/,ic=d(Br),oc=/^\s*([\w$_]+|\([^)]*?\))\s*=>|^function\s*\(/,ac=/^\s*[A-Za-z_$][\w$]*(?:\.[A-Za-z_$][\w$]*|\['.*?']|\[".*?"]|\[\d+]|\[[A-Za-z_$][\w$]*])*\s*$/,sc={esc:27,tab:9,enter:13,space:32,up:38,left:37,right:39,down:40,delete:[8,46]},cc=function(e){return"if("+e+")return null;"},uc={stop:"$event.stopPropagation();",prevent:"$event.preventDefault();",self:cc("$event.target !== $event.currentTarget"),ctrl:cc("!$event.ctrlKey"),shift:cc("!$event.shiftKey"),alt:cc("!$event.altKey"),meta:cc("!$event.metaKey"),left:cc("'button' in $event && $event.button !== 0"),middle:cc("'button' in $event && $event.button !== 1"),right:cc("'button' in $event && $event.button !== 2")},lc={bind:Gr,cloak:y},fc={staticKeys:["staticClass"],transformNode:Ci,genData:xi},pc={staticKeys:["staticStyle"],transformNode:wi,genData:ki},dc=[fc,pc],vc={model:Cn,text:Ai,html:Oi},hc={expectHTML:!0,modules:dc,directives:vc,isPreTag:pa,isUnaryTag:as,mustUseProp:na,canBeLeftOpenTag:ss,isReservedTag:da,getTagNamespace:Et,staticKeys:function(e){return e.reduce(function(e,t){return e.concat(t.staticKeys||[])},[]).join(",")}(dc)},mc=function(e){function t(t,n){var r=Object.create(e),i=[],o=[];if(r.warn=function(e,t){(t?o:i).push(e)},n){n.modules&&(r.modules=(e.modules||[]).concat(n.modules)),n.directives&&(r.directives=m(Object.create(e.directives),n.directives));for(var a in n)"modules"!==a&&"directives"!==a&&(r[a]=n[a])}var s=bi(t,r);return s.errors=i,s.tips=o,s}function n(e,n,i){n=n||{};var o=n.delimiters?String(n.delimiters)+e:e;if(r[o])return r[o];var a=t(e,n),s={},c=[];s.render=$i(a.render,c);var u=a.staticRenderFns.length;s.staticRenderFns=new Array(u);for(var l=0;l<u;l++)s.staticRenderFns[l]=$i(a.staticRenderFns[l],c);return r[o]=s}var r=Object.create(null);return{compile:t,compileToFunctions:n}}(hc),gc=mc.compileToFunctions,yc=d(function(e){var t=Nt(e);return t&&t.innerHTML}),_c=vt.prototype.$mount;return vt.prototype.$mount=function(e,t){if((e=e&&Nt(e))===document.body||e===document.documentElement)return this;var n=this.$options;if(!n.render){var r=n.template;if(r)if("string"==typeof r)"#"===r.charAt(0)&&(r=yc(r));else{if(!r.nodeType)return this;r=r.innerHTML}else e&&(r=Si(e));if(r){var i=gc(r,{shouldDecodeNewlines:os,delimiters:n.delimiters},this),o=i.render,a=i.staticRenderFns;n.render=o,n.staticRenderFns=a}}return _c.call(this,e,t)},vt.compile=gc,vt});
</script>
</head>
<body>
<div id="clock">
    <p class="date">...404 error page...</p>
    <p class="time">{{ time }}</p>
    <p class="text">{{ date }}</p>
</div>
<script>
var clock = new Vue({
    el: '#clock',
    data: {
        time: '',
        date: ''
    }
});
var week = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
var timerID = setInterval(updateTime, 1000);
updateTime();
function updateTime() {
    var cd = new Date();
    clock.time = zeroPadding(cd.getHours(), 2) + ':' + zeroPadding(cd.getMinutes(), 2) + ':' + zeroPadding(cd.getSeconds(), 2);
    clock.date = zeroPadding(cd.getFullYear(), 4) + '-' + zeroPadding(cd.getMonth()+1, 2) + '-' + zeroPadding(cd.getDate(), 2) + ' ' + week[cd.getDay()];
};
function zeroPadding(num, digit) {
    var zero = '';
    for(var i = 0; i < digit; i++) {
        zero += '0';
    }
    return (zero + num).slice(-digit);
}</script>
</body>
 
</html>
```

部署到 GitHub 之后，访问不存在的页面就会跳出来了

##

在博客根目录下的 source 目录下新建 CNAME 文件，如果主题 source 目录下有这个文件请删除

修改 CNAME 文件，内容为你的域名，例如我的

```
wallleap.cn
```

接着去 GitHub pages 更改域名，开启 SSL

前往阿里云的的域名解析页面添加 CANME 解析

`@ --> 用户名.github.io`

之后就可以以新的域名访问了 <https://wallleap.cn>

## 27、网站收录

主要是向各大搜索引擎提交链接

谷歌收录

[360站长平台](http://zhanzhang.so.com/sitetool/site_manage)

[百度搜索资源平台](https://ziyuan.baidu.com/linksubmit/)

百度的需要注意一下，由于 GitHub 将百度封了，因此你需要把博客双线部署到 gitlab 或 coding 才能收录

[搜狗站长平台](http://zhanzhang.sogou.com/)

## 28、网站分析

### 百度统计

前往百度统计官网

[Baidu统计](https://tongji.baidu.com/web/welcome/login)

以百度账号登录后，点击【管理】，在【网站列表】中新增网站

获取代码，将代码复制到 `</head>` 标签前，进行代码检测

以后就可以查看访问情况了

### cnzz

点击

[友盟+](https://passport.umeng.com/login?appId=cnzz)

前往，注册登录后，添加站点

根据自己喜好获取代码

粘贴到 `</body>` 前

之后就可以点击查看信息了

## 29、小技巧

### 博客备份

有一个博客备份插件

[hexo-git-backup](https://github.com/coneycode/hexo-git-backup)

能够传到 backup 分支

我们还可以把整个博客文件夹上传到 GitHub 私有仓库

### 本地预览

使用命令换个端口预览 `hexo s -p 5000`

也可以添加下列代码到博客配置文件中,使用 `hexo s` 时将会以 5000 端口运行

```yml
server:
  port: 5000
  compress: true
  header: true
```

### 快捷命令

alias 设置命令别名，将下面代码复制到 `.bashrc` 文件中

```shell
alias hs='hexo clean && hexo g && hexo s'
alias hd='hexo clean && hexo g && hexo d'
alias gp='git add . && git commit -m "update" && git push -f'
```

以后输入 `hs` 命令就可以本地预览、`hd` 部署、`gp` 上传到仓库

## 30、静态资源压缩

博客使用了图片懒加载和预加载虽然加快了一点速度，但访问还是有点慢

那么直接把 html、css、js 代码中的空格去掉，进行压缩

还有压缩一下图片，能够一定程度上缩小 public 文件夹的大小

参考这篇文章：

[Hexo博客使用gulp压缩静态资源](https://segmentfault.com/a/1190000019842178)

安装全局 `gulp`

`npm install gulp -g`

安装插件

```sh
npm install gulp-minify-css gulp-uglify gulp-htmlmin gulp-htmlclean gulp gulp-imagemin --save
# 解决【Gulp打包问题】 GulpUglifyError: unable to minify JavaScript
# 解决 gulp-uglify 压缩JavaScript 不兼容 es5 语法的问题
npm install babel-core@6.26.3 --save
npm install gulp-babel@7.0.1 --save
npm install babel-preset-es2015@6.24.1 --save
# gulp-babel 取消严格模式方法("use strict")
npm install babel-plugin-transform-remove-strict-mode --save
```

问题：如果安装 `gulp-imagemin` 错误请执行以下语句

```sh
sudo npm i gulp-imagemin --unsafe-perms
```

博客根目录创建 `gulpfile.js`

上面文章中有一句在这个版本会报错，已修改

```javascript
var gulp = require('gulp');
var minifycss = require('gulp-minify-css');
var uglify = require('gulp-uglify');
var htmlmin = require('gulp-htmlmin');
var htmlclean = require('gulp-htmlclean');
var imagemin = require('gulp-imagemin');
var babel = require('gulp-babel');

// 压缩css文件
gulp.task('minify-css', function (done) {
    return gulp.src('./public/**/*.css')
        .pipe(minifycss())
        .pipe(gulp.dest('./public'));
    done();
});

// 压缩html文件
gulp.task('minify-html', function (done) {
    return gulp.src('./public/**/*.html')
        .pipe(htmlclean())
        .pipe(htmlmin({
            removeComments: true,
            minifyJS: true,
            minifyCSS: true,
            minifyURLs: true,
        }))
        .pipe(gulp.dest('./public'));
    done();
});

// 压缩js文件
gulp.task('minify-js', function (done) {
    return gulp.src(['./public/**/*.js', '!./public/**/*.min.js'])
        .pipe(babel({
            //将ES6代码转译为可执行的JS代码
            presets: ['es2015'] // es5检查机制
        }))
        .pipe(uglify())
        .pipe(gulp.dest('./public'));
    done();
});

// 压缩 public/images 目录内图片(Version<3)
// gulp.task('minify-images', function () {
//     gulp.src('./public/images/**/*.*')
//         .pipe(imagemin({
//             optimizationLevel: 5, //类型：Number  默认：3  取值范围：0-7（优化等级）
//             progressive: true, //类型：Boolean 默认：false 无损压缩jpg图片
//             interlaced: false, //类型：Boolean 默认：false 隔行扫描gif进行渲染
//             multipass: false, //类型：Boolean 默认：false 多次优化svg直到完全优化
//         }))
//         .pipe(gulp.dest('./public/images'));
// });

// 压缩 public/images 目录内图片(Version>3)
gulp.task('minify-images', function (done) {
    gulp.src('./public/images/**/*.*')
        .pipe(imagemin([
            imagemin.gifsicle({interlaced: true}),
            // imagemin.jpegtran({progressive: true}), // 版本升级，改用下面这个
            imagemin.mozjpeg({progressive: true,}),
            imagemin.optipng({optimizationLevel: 5}),
            imagemin.svgo({
                plugins: [
                    {removeViewBox: true},
                    {cleanupIDs: false}
                ]
            })
        ]))
        .pipe(gulp.dest('./public/images'));
    done();
});

//4.0以前的写法 
//gulp.task('default', [
//  'minify-html', 'minify-css', 'minify-js', 'minify-images'
//]);
//4.0以后的写法
// 执行 gulp 命令时执行的任务
gulp.task('default', gulp.series(gulp.parallel('minify-html', 'minify-css', 'minify-js', 'minify-images')), function () {
    console.log("----------gulp Finished----------");
    // Do something after a, b, and c are finished.
});
```

根目录下创建 `.babelrc`

```
{
    'presets': ['es2015'],
    "plugins": ["transform-remove-strict-mode"]
}
```

每次生成静态文件的时候，使用命令 `hexo g && gulp` 即可，能够压缩几兆的空间

---

好的呢，这篇文章就到这里啦

这么多，可算是累死我了

再见~

参考文档：

[Hexo 博客优化之博客美化系列](https://blog.csdn.net/qq_36759224/article/details/85420403)

> 文章来源：<https://myblog.wallleap.cn/>
> 转载请不要删除这段内容
