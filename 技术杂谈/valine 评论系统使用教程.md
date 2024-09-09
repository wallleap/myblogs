---
title: valine 评论系统使用教程
date: 2020-03-30 20:32
updated: 2020-03-30 20:32
cover: //cdn.wallleap.cn/img/pic/cover/2023029eAQof.jpg
category: 技术杂谈
tags:
  - 博客
  - valine
description: valine 评论系统使用教程
---

评论系统千千万，好看兼好用的 Valine 还是 OK 的

最开始用这个评论是在使用 Sakura 主题的时候，但是那个时候没认真看教程

觉得它没有邮件提醒功能、而且有的时候还会报错，就没使用了

改用的来必力和 Gitment，Gitment 使用起来挺方便的，能够邮件提醒，而且报的错误也能解决

emmmm……一直到现在，想接着用 valine，然后搜了很多篇教程，发现 valine 还是非常好用的

手动配图：真香.gif

然后接下来就讲下怎样**添加 valine**，对其进行**美化**和添加评论功能吧

emmmm，版本 ` v1.4.0` 之后更新了很多内容，不得不说，这段时间作者真的是高产啊

![](https://cdn.wallleap.cn/img/pic/illustration/valine.png)

但是不想推翻重写，因此直接在这篇博文上修改

<font color="#bac">更新内容</font>

- [x] 去除QQ头像配置的内容，更新为新的方法
- [x] 按照官网更新配置项解释
- [x] 添加自定义表情用法
- [x] 去除评论框跟随，官方已支持
- [ ] 美化的好多不能用了

## 注册登录

前往 [LeanCloud 注册](https://leancloud.cn/dashboard/login.html#/signup)账号，如果已经有了账号，可以直接[登录](https://leancloud.cn/dashboard/login.html#/signin)

接着进入[控制台](https://leancloud.cn/dashboard/applist.html#/apps),左下角有两个按钮`快速入门`和`创建应用`，我们点击`创建应用`，随便输入一个名字，例如 `valine`，其他默认，点击`创建`

现在在控制台出现了你刚刚创建的应用，点击这个应用的右上角设置图标

进入了设置界面，点击 `valine 开发版`下面那栏里的`应用 Keys`

我们只需要里面的 `AppID` 和 `AppKey`，现在先开始下面操作，这两个等下会用到

![valine 应用 keys](https://cdn.wallleap.cn/img/pic/illustration/valine1.png)

当然啦，如果你的博客主题已经**集成**了 valine，那么将这两个值填到 `_config.yml` 的相应位置就可以了，下面的教程就可以选择性查看了

## 修改博客渲染文件

### 添加代码

现在到博客主题目录下打开 `layout` 目录，再进入 `_partial` 目录，在这个目录即 `MyBlog/themes/主题名/layout/_partial` 下新建 `comment.ejs` 文件，填入代码：

```ejs
<% if (theme.valine && post.comments) { %>
    <script src='//unpkg.com/valine/dist/Valine.min.js'></script>
    <!-- 当然啦，这个可以在<head></head>中引入 -->
    <div id="vcomments"></div>
    <script>
    new Valine({
        el: '#vcomments' ,
        appId: '<%= theme.v_appId %>',
        appKey: '<%= theme.v_appKey %>',
        avatar:'mp', 
        placeholder: 'just go go' ，
      	enableQQ: true,
      	// 设置Bilibili表情包地址
        emojiCDN: '//i0.hdslb.com/bfs/emote/', 
        // 表情title和图片映射
        emojiMaps: {
            "tv_doge": "6ea59c827c414b4a2955fe79e0f6fd3dcd515e24.png",
            "tv_亲亲": "a8111ad55953ef5e3be3327ef94eb4a39d535d06.png",
            "tv_偷笑": "bb690d4107620f1c15cff29509db529a73aee261.png",
            "tv_再见": "180129b8ea851044ce71caf55cc8ce44bd4a4fc8.png",
            "tv_冷漠": "b9cbc755c2b3ee43be07ca13de84e5b699a3f101.png",
            "tv_发怒": "34ba3cd204d5b05fec70ce08fa9fa0dd612409ff.png",
            "tv_发财": "34db290afd2963723c6eb3c4560667db7253a21a.png",
            "tv_可爱": "9e55fd9b500ac4b96613539f1ce2f9499e314ed9.png",
            "tv_吐血": "09dd16a7aa59b77baa1155d47484409624470c77.png",
            "tv_呆": "fe1179ebaa191569b0d31cecafe7a2cd1c951c9d.png",
            "tv_呕吐": "9f996894a39e282ccf5e66856af49483f81870f3.png",
            "tv_困": "241ee304e44c0af029adceb294399391e4737ef2.png",
            "tv_坏笑": "1f0b87f731a671079842116e0991c91c2c88645a.png",
            "tv_大佬": "093c1e2c490161aca397afc45573c877cdead616.png",
            "tv_大哭": "23269aeb35f99daee28dda129676f6e9ea87934f.png",
            "tv_委屈": "d04dba7b5465779e9755d2ab6f0a897b9b33bb77.png",
            "tv_害羞": "a37683fb5642fa3ddfc7f4e5525fd13e42a2bdb1.png",
            "tv_尴尬": "7cfa62dafc59798a3d3fb262d421eeeff166cfa4.png",
            "tv_微笑": "70dc5c7b56f93eb61bddba11e28fb1d18fddcd4c.png",
            "tv_思考": "90cf159733e558137ed20aa04d09964436f618a1.png",
            "tv_惊吓": "0d15c7e2ee58e935adc6a7193ee042388adc22af.png",
            // ... 更多表情
        } 
    });
    </script>
<% } %>
```

再将如下代码放到需要的位置，一般是在文章底部

```ejs
<%- partial('_partial/comment') %>
```

### 判断讲解

加入判断是为了方便开启和关闭评论，首先是主题配置文件 `_config.yml` 中,加入

```yml
valine: true   # 修改为false关闭valine评论
v_appId: 刚刚获取的appid
v_appKey: 刚刚获取的appkey
```

接着是写的文章中 `文章名.md`

```markdown
---
title: 文章名
categories: 博客
date: 2020-03-30 12:16:01
comments: true    添加上这个，如果这篇文章不需要评论改为false，默认开启
tags: hexo
---

正文
```

这里需要注意一下：以前我使用 `post.comments` 没有问题，但是现在好像不行了，如果报的是有关 `post` 的错误，可以改为 `page.comments`，或者直接去掉

### 配置项讲解

可以前往 [valine 官网](https://valine.js.org/)查看具体的使用

~~这里挑一些我们会用到的说下~~

<font color="red" size=5>更新</font> 不写出已经丢弃的配置项

除了最后一个配置项，其他都要在末尾加上英文的 `,`

```js
el: '#vcomments'
```

这个字段只要你不改 `div` 的代码就不需要修改,如果你 `div` 不想用 `id`，而是改为了 `class="valine"`，那你就需要把这里改为 `.valine`

```js
appId: '从LeanCloud的应用中得到的appId.'
appKey: '从LeanCloud的应用中得到的APP Key.'
```

上面的是基本配置

```yml
placeholder: `快来评论啊`
```

评论框占位提示符，写了之后会在评论框内出现文字

```yml
path: 'window.location.pathname'
```

当前`文章页`路径，用于区分不同的`文章页`，用这个默认值就行

> I. 请保证每个`文章页`路径的唯一性，否则可能会出现不同`文章页`下加载相同评论列表的情况。
> 
> II. 如果值为`window.location.href`，可能会出现随便加`不同参数`进入该页面，而被判断成新页面的情况。

```yml
avatar: 'mp'
```

看官网的介绍，可以配置为 QQ 头像

```yml
meta: ['nick','mail','link']
```

评论者相关属性，这里有三个：昵称、邮箱、网页链接

```yml
requiredFields: ['nick','mail']
```

设置`必填项`，默认为 `[]`，匿名显示

```yml
pageSize: '5'
```

评论列表分页，每页条数,默认为10

```ynl
lang: 'en'
```

语言，默认为中文：zh-CN

```yml
visitor: true
```

文章访问量统计,这个还是挺好用的，等下说

```yml
highlight: false
```

代码高亮，默认开启，这个不推荐关闭，去掉这个字段就行

```yml
avatarForce: false
```

每次访问强制拉取最新的评论列表头像,不推荐设置为 true，目前的评论列表头像会自动带上 Valine 的版本号

```yml
recordIP: true
```

设置为 true 之后会记录评论者 IP，默认为 false

```js
// 这里设置CDN, 默认微博表情CDN
emojiCDN: 'https://img.t.sinajs.cn/t4/appstyle/expression/ext/normal/', 
// 表情title和图片映射
emojiMaps: {
"smile":"e3/2018new_weixioa02_org.png",
"lovely":"09/2018new_keai_org.png",
// ... 更多表情
} 
```

表情设置

```js
enableQQ: true
```

启用`昵称框`自动获取`QQ昵称`和`QQ头像`, 默认关闭

## 文章阅读量

可以使用不蒜子，但是偶尔会链接不到

按照 valine 的说法：

> 如果开启了阅读量统计，Valine 会自动检测 LeanCloud 应用中是否存在 Counter 类，如果不存在会自动创建，无需手动创建~

也就是如果没使用 valine 的话还需要自己添加一个 `Counter 类`，这个是在`LeanCloud` 的`存储`中，但是我们现在配置了 valine 了就可以省事了

> Valine 会自动查找页面中 class 值为 leancloud_visitors 的元素，获取其 id 为查询条件。并将得到的值填充到其 class 的值为 leancloud-visitors-count 的子元素里：

so，我们只需要在 `comment.ejs` 的最后面加上这些即可

```ejs
<span id="/<%= page.path %>" class="leancloud_visitors" data-flag-title="Your Article Title">
    <em class="post-meta-item-text">阅读量 </em>
    <i class="leancloud-visitors-count">1000000</i>
</span>
```

如果这个 `id` 不行的话，可以改为 `page.permalink` 完整的网址试下

## ~~头像配置~~

> Valine 目前使用的是 [Gravatar](http://cn.gravatar.com/) 作为评论列表头像。
> 请自行登录或注册 Gravatar，然后修改自己的头像。
> 评论的时候，留下在 Gravatar 注册时所使用的邮箱即可。

~~valine 文档中说`感谢gravatar.cat.net提供的镜像服务`，那用 QQ 的可不可以呢~~

~~然后找到了这篇文章：~~

[Valine-实现QQ邮箱识别生成头像地址（完美解决头像问题）](https://blog.csdn.net/cungudafa/article/details/104638730/)

~~首先下载[valine.min.js](https://unpkg.com/valine@latest/dist/Valine.min.js) ，现在是1.3.10版本~~

~~放到主题的source目录的js目录下~~

~~再把刚刚上面引入的js改为~~

```ejs
<script src='//unpkg.com/valine/dist/Valine.min.js'></script>
改为
<script src='/js/Valine1.3.10.min.js'></script>
```

~~打开js文件，搜索~~

```ejs
(m.cdn+a(e.get("mail"))+m.params)+'">',
```

~~从这里往前直到 `var C=function(e,n,r)`，都替换为~~

```ejs
 var C=function(e,n,r){
	var qq_img=m.cdn+a(e.get("mail"))+m.params;//默认gravator头像接口
	 if(e.get("mail").indexOf("@qq.com") >= 0){
		var prefix = e.get("mail").replace(/@.*/, "");//前缀
		var pattern=/^\d+$/g;  //正则表达式，数字
		var result= prefix.match(pattern);//match 是匹配的意思
		if(result!==null){
			qq_img = "//q1.qlogo.cn/g?b=qq&nk="+ prefix +"&s=100";
		}
	}
	var i=u.create("div",{class:"vcard",id:e.id}),o=m.hide?"":'<img class="vimg" src="'+ (qq_img)+'">',
```

~~然后填的是QQ邮箱的话就会显示QQ头像辣~~

~~当然如果你实在很懒，可以直接使用这个已经修改好了的~~

```javascript
<script src='https://cdn.wallleap.cn/js/Valine1.3.10.min.js'></script>
```

<font color="red" size=5>注</font> 由于新版的 valine 已经加入了 QQ 头像的内容，因此教程修改为以下内容：

仍然只需要引入官方原版的 js 文件，不需要在源代码中修改了

```javascript
<script src='//unpkg.com/valine/dist/Valine.min.js'></script>
```

开启配置项中的昵称框自动获取`QQ 昵称`和`QQ 头像`功能

```js
enableQQ: true;
```

## 自定义表情

很早就想把 valine 里的表情修改为 B 站表情了，可惜没找到好用的教程，没想到作者居然加入了这个功能

使用方法：

```ejs
new Valine({
    el:'#vcomment',
    appId:'<Your_APP_ID>',
    appKey:'<Your_APP_KEY>',

    // 设置表情包地址
    emojiCDN: '//i0.hdslb.com/bfs/emote/', 
    // 表情title和图片映射
    emojiMaps: {
        "tv_doge": "6ea59c827c414b4a2955fe79e0f6fd3dcd515e24.png",
        "tv_亲亲": "a8111ad55953ef5e3be3327ef94eb4a39d535d06.png",
        "tv_偷笑": "bb690d4107620f1c15cff29509db529a73aee261.png",
        "tv_再见": "180129b8ea851044ce71caf55cc8ce44bd4a4fc8.png",
        "tv_冷漠": "b9cbc755c2b3ee43be07ca13de84e5b699a3f101.png",
        "tv_发怒": "34ba3cd204d5b05fec70ce08fa9fa0dd612409ff.png",
        "tv_发财": "34db290afd2963723c6eb3c4560667db7253a21a.png",
        "tv_可爱": "9e55fd9b500ac4b96613539f1ce2f9499e314ed9.png",
        "tv_吐血": "09dd16a7aa59b77baa1155d47484409624470c77.png",
        "tv_呆": "fe1179ebaa191569b0d31cecafe7a2cd1c951c9d.png",
        "tv_呕吐": "9f996894a39e282ccf5e66856af49483f81870f3.png",
        "tv_困": "241ee304e44c0af029adceb294399391e4737ef2.png",
        "tv_坏笑": "1f0b87f731a671079842116e0991c91c2c88645a.png",
        "tv_大佬": "093c1e2c490161aca397afc45573c877cdead616.png",
        "tv_大哭": "23269aeb35f99daee28dda129676f6e9ea87934f.png",
        "tv_委屈": "d04dba7b5465779e9755d2ab6f0a897b9b33bb77.png",
        "tv_害羞": "a37683fb5642fa3ddfc7f4e5525fd13e42a2bdb1.png",
        "tv_尴尬": "7cfa62dafc59798a3d3fb262d421eeeff166cfa4.png",
        "tv_微笑": "70dc5c7b56f93eb61bddba11e28fb1d18fddcd4c.png",
        "tv_思考": "90cf159733e558137ed20aa04d09964436f618a1.png",
        "tv_惊吓": "0d15c7e2ee58e935adc6a7193ee042388adc22af.png",
        // ... 更多表情
    } 
})
```

然后这里分享一下几个表情包：

cdn 可以填`https://cdn.wallleap.cn/tree/master/emote/xxx`

`xxx`代表里面的几个目录，每个里都提供了一个包含该目录下所有图片的 `list.txt`

```
bili B站表情包，里面有两种
cool 酷安表情包
qq   QQ表情包
tieba 百度贴吧
weibo 微博
```

我实在忘了这是在哪个地方找来的表情包了，所以暂时不声明原地址了，等找到了再加上

啊，还有一个老哥提供的，地址在下面

<https://github.com/blogimg/emotion>

## 评论框美化

默认的其实还可以，可素可以更漂亮肯定得加的

感兴趣的可以去看这篇博客 [Valine 评论框美化及功能优化](https://immmmm.com/valine-diy/)

这里我就直接搬过来啦

```css
.v .vwrap{padding: 0 0 44px;}.v .veditor{min-height:7rem;resize:none;}.v .vwrap .vedit{padding-top:0}.v .vwrap .vheader{width: 80%;bottom:0;position: absolute;background: #f7f7f7;}.v .vinput{padding:10px 15px;}.v .vwrap .vheader .vinput{border-bottom:0px}.v .vwrap .vedit .vctrl{margin-top:-44px;right:0;position:absolute;margin-right:-3px;}.v .vwrap .vcontrol{    position:absolute;right:0;bottom:0;width:20%;padding-top:0px;}.v .vwrap .vcontrol .col.col-80{width: 100%;}.v .vbtn.vsubmit{border-radius: 0;padding: 0;color: #fff;line-height: 44px;width:100%;border: none;background:#1abc9c;}.v .vwrap .vedit .vctrl span.vpreview-btn,.v .vwrap .vcontrol .col.col-20,.v .vlist .vcard .vhead .vsys{display:none;}
@media screen and (max-width: 520px){
	.v .vwrap .vheader .vinput{width: 33.33%;padding:10px 5px;}
}
```

如果你需要底部有个图片可以加上

```css
#veditor {
    background-image: url(背景图片地址);
    background-size: contain;
    background-repeat: no-repeat;
    background-position: right;
    background-color: rgba(255,255,255,0);
    resize: vertical;
}
```

`placeholder` 字段也能用上，使用今日诗词或者一言

```javascript
<script src="https://sdk.jinrishici.com/v2/browser/jinrishici.js" charset="utf-8"></script>
<script type="text/javascript">
jinrishici.load(function(result) {
	var jrsc_plac =  result.data.content + "\n「" + result.data.origin.title + "」" + result.data.origin.dynasty + " · " + result.data.origin.author
	document.getElementById("veditor").setAttribute("placeholder",jrsc_plac);
});
</script>
<style>
textarea[id='veditor']::placeholder{
    color:#b3b3b3;font-size:14px;text-align:center;line-height:6rem;
}
</style>
```

## 评论框的功能

可能需要 jQuery，先引入

```html
<script src="https://cdn.jsdelivr.net/npm/jquery/dist/jquery.min.js"></script>
```

### 前端验证

valine 自带的验证码也可以打开

主要是检查昵称和邮箱

```ejs
<script>
    document.body.addEventListener('click', function(e) {
        if (e.target.classList.contains('vsubmit')) {
            const email = document.querySelector('input[type=email]');
            const nick = document.querySelector('input[name=nick]');
            const reg = /^[A-Za-z0-9\u4e00-\u9fa5]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/;
            if (!email.value || !nick.value || !reg.test(email.value)) {
                const str = `<div class="valert text-center"><div class="vtext">请填写正确的昵称和邮箱！</div></div>`;
                const vmark = document.querySelector('.vmark');
                vmark.innerHTML = str;
                vmark.style.display = 'block';
                setTimeout(function() {
                    vmark.style.display = 'none';
                    vmark.innerHTML = '';
                }, 2500);
            }
        }
    });
</script>
```

### ~~点击回复评论框跟随~~

还是 immmmm 的

> 官方版本点击回复时都是跳回到页面上方的评论框进行回复，评论框是固定不动的。比较合理的是：点哪条的回复，评论框就显示在此条评论下方。避免页面跳上跳下。
> 相关 jQuery 代码：

```ejs
$(document).ready(function(){
	$('.vemoji-btn').text('😀');
	$("#vcomments").on('click', 'span.vat',function(){
		$(this).parent('div.vmeta').next("div.vcontent").after($("div.vwrap"));
		$('textarea#veditor').focus();
	})
})
```

## 邮件提醒

**重头戏**来了

好不容易搭了个博客，结果有人评论我们不能及时回复，这体验感多差

gitment、gitalk 都是用的 GitHub 的 issue，能够轻松地发送邮件提醒

而 valine 呢

有大佬就弄出了 valine-Admin，可以结合 LeanCloud 实现邮箱提醒功能

项目地址：[Valine-Admin](https://github.com/DesertsP/Valine-Admin)

### 云引擎设置

回到我们在 LeanCloud 创建的应用 `valine`，点击左边的第二个选项`云引擎`

点击 `web 组`下方的`设置`

在代码库的下方填上 `https://github.com/DesertsP/Valine-Admin.git`，点击方框右边的<kbd>保存</kbd>

![代码库](https://cdn.wallleap.cn/img/pic/illustration/valine2.png)

往下滑，在`自定义环境变量`这里添加如下变量

![变量](https://cdn.wallleap.cn/img/pic/illustration/valine3.png)

这些下面有解释，我们先接着往下滑，把 `Web 主机域名`启用

![Web 主机域名](https://cdn.wallleap.cn/img/pic/illustration/valine4.png)

| 变量             | 示例                                      | 说明                                                         |
| ---------------- | ----------------------------------------- | ------------------------------------------------------------ |
| **SITE_NAME**    | Deserts                                   | [必填]博客名称                                               |
| **SITE_URL**     | https://deserts.io                          | [必填]首页地址                                               |
| ***SMTP_SERVICE*** | QQ                                        | [新版支持]邮件服务提供商，支持 QQ、163、126、Gmail 以及 [更多](https://nodemailer.com/smtp/well-known/#supported-services) |
| **SMTP_USER**      | xxxxxx@qq.com                             | [必填]SMTP登录用户                                           |
| **SMTP_PASS**      | ccxxxxxxxxch                              | [必填]SMTP登录密码（QQ邮箱需要获取独立密码）                 |
| **SENDER_NAME**      | Deserts                                   | [必填]发件人                                                 |
| **SENDER_EMAIL**     | xxxxxx@qq.com                             | [必填]发件邮箱                                               |
| **ADMIN_URL**        | https://xxx.leanapp.cn/                   | [建议]Web主机二级域名，用于自动唤醒                          |
| BLOGGER_EMAIL    | xxxxx@gmail.com                           | [可选]博主通知收件地址，默认使用SENDER_EMAIL                 |
| AKISMET_KEY      | xxxxxxxxxxxx                              | [可选]Akismet Key 用于垃圾评论检测，设为MANUAL_REVIEW开启人工审核，留空不使用反垃圾 |
| MAIL_SUBJECT        | ${PARENT_NICK}，您在${SITE_NAME}上的评论收到了回复 | [可选]@通知邮件主题（标题）模板 |
| MAIL_TEMPLATE       | 见下文                                             | [可选]@通知邮件内容模板         |
| MAIL_SUBJECT_ADMIN  | ${SITE_NAME}上有新评论了                           | [可选]博主邮件通知主题模板      |
| MAIL_TEMPLATE_ADMIN | 见下文                                             | [可选]博主邮件通知内容模板      |

博客名、博客地址应该会填吧

邮件服务提供商，你使用的哪种就填哪个，比如我的是 `xxx@qq.com`，那么就填 `QQ`。

SMTP 登录用户填上你自己的邮箱

登录密码并不是真的登录密码，网易的自己搜一下`网易邮箱登录授权码`；QQ 邮箱的为独立密码

发件人填自己昵称

发件邮箱和博主收件地址都可以填刚才的邮箱

二级域名就是刚刚开启的哪个

`AKISMET_KEY`，有三种选择：不添加，不开启审核；添加后设置为 `MANUAL_REVIEW` 人工审核；设为你注册 <https://akismet.com/development/> 后获取的 key 自动审核拦截垃圾评论

### 设置邮件模板

上面还有四个变量没说，这四个就是用来设置邮件模板的，当然，你也可以用 LeanCloud 自带的

两个标题就不说了

说下`@的`和`通知博主`的内容模板

可以直接设置为项目地址中给的

也可以用 immmmm 的：

MAIL_TEMPLATE 代码，自行替换 logo 图片地址：

```html
<div style="padding:2em 10%;color:#b3b3b1;width:420px;margin:0 auto;font-size:14px";>
	<img style="display:block;width:50px;margin:0 auto" src="https://图片地址/logo.png">
	<p style="text-align:center;">Hi，<span style="color:#3eae5f"> ${PARENT_NICK} </span></p>
	<p style="font-size:13px;text-align:center;">有人回复了您在 <strong style="font-weight:bold"> ${SITE_NAME} </strong> 上的评论</p>
	<hr style="width:64px;border:0;border-bottom:1px solid #e5e5e5;margin:24px auto;">
	<div style="color:#333;overflow:hidden;">
		<p style="display:inline-block;float:left;"><span style="color:#3eae5f;font-weight:bold"> 您 </span><span>说：</span></p>
		${PARENT_COMMENT}
	</div>
	<div style="color:#333;overflow:hidden;">
		<p style="display:inline-block;float:left;"><span style="color:#3eae5f;font-weight:bold"> ${NICK} </span><span>说：</span></p>
		${COMMENT}
	</div>
	<p><a style="color:#ffffff;text-decoration:none;display:inline-block;min-height:28px;line-height:28px;padding:0 13px;outline:0;background:#3eae5f;font-size:13px;text-align:center;font-weight:400;border:0;border-radius:999em" href="${POST_URL}" target="_blank">点击查看</a></p>
	<hr style="width:64px;border:0;border-bottom:1px solid #e5e5e5;margin:24px auto;">
	<p><a style="display:block;color:#b3b3b1;text-decoration:none;text-align:center;" href="${SITE_URL}" target="_blank">${SITE_NAME}</a></p>
</div>
```

MAIL_TEMPLATE_ADMIN 通知博主邮件模板代码：

```html
<div style="line-height:24px;font-size:13px;">
    <p><span style="color:#3eae5f"> ${NICK} </span> 说：</p>
    <p >${COMMENT}</p>
    <p style="font-size:12px;line-height:12px;"><a style="color:#b3b3b1;text-decoration:none;" href="${POST_URL}" target="_blank">${POST_URL}</a></p>
</div>
```

在这里面可用的变量有：

| 模板里的变量     | 说明                            |
| -------------- | ------------------------------- |
| SITE_NAME      | 博客名称                        |
| SITE_URL       | 博客首页地址                    |
| POST_URL       | 文章地址（完整路径）            |
| *PARENT_NICK*    | 收件人昵称（被@者，父级评论人） |
| *PARENT_COMMENT* | 父级评论内容                    |
| NICK           | 新评论者昵称                    |
| COMMENT        | 新评论内容                      |

在模板中使用的话，`${变量名}`

*斜体*的两个变量表示只能在被@的模板中使用

### 开始部署

点击左边的`部署`，再点击页面中的 <kbd>Git 源码部署</kbd>

在出现的页面中`分支或版本号`下方的框中填入`master`，勾选☑️`下载最新依赖`复选框

再点击<kbd>部署</kbd>,接着等待部署完成即可

![部署](https://cdn.wallleap.cn/img/pic/illustration/valine5.png)

### 设置定时任务

到上一步已经完成了邮箱通知提醒的功能了

但是免费的 LeanCloud 有休眠政策，具体能运行几小时忘记了，但是不能全天运行

也就是说可能会漏掉一些评论的提醒

刚好 LeanCloud 有一个定时任务，可以弥补这个缺陷

不能全天24h一直运行，那么我运行一会休息一会，在运行的那个时间段里把邮件补发一下总行吧

这就是定时任务所执行的内容

点击`定时任务`，创建两个定时任务，分别填：

名称：`自动唤醒`  生产环境：`self-wake`  Cron表达式：`0 0/30 7-23 * * ?`
名称：`定时检查24小时内漏发的邮件通知`  生产环境：`resend-mails`  Cron表达式：`0 0 8 * * ?`

![](https://cdn.wallleap.cn/img/pic/illustration/valine6.png)

---

设置完成之后就 OK 啦

这样就拥有了一个完美的评论系统了

---

现在可以选择 [waline](https://waline.js.org/) 或者 [twikoo](https://twikoo.js.org/)
