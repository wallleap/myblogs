---
title: web 入门基础知识
date: 2020-03-24 10:33
updated: 2020-03-24 10:33
cover: //cdn.wallleap.cn/img/pic/cover/2023029majaI.jpg
category: 技术杂谈
tags:
  - web
  - 前端
description: web 入门基础知识
---

总结一下前端学习之前需要了解的内容

## 1、 软件开发架构

* C/S架构：客户端/服务器——用户需要下载安装客户端软件使用，服务器负责处理软件的业务逻辑、同时更新、不能跨平台、通信采用自有协议(相对安全)，客户端功能强大，可以减轻服务器端压力，但是客户端维护开发成本高(胖客户端)

* ✪ B/S架构：浏览器/服务器端——本质上也是C/S，使用浏览器作为软件的客户端，通过浏览器访问网页的形式来使用软件、软件不需要安装(使用浏览器访问指定的网址)、客户端不需要更新、可跨平台使用、通信采用通用的HTTP协议(相对不安全)，客户端维护成本低，可跨平台，但服务器负担重，缺点是客户端功能较简单，用户体验不如C/S(瘦客户端)

## 2、软件开发流程

1. 网页设计师根据需求设计网页(PS)
2. 前端工程师将设计做成静态网页(HTML+CSS)
3. 后台工程师将静态网页修改为动态网页(JSP\PHP\Python\ASP) 提供接口  JS Nodejs

![](https://cdn.wallleap.cn/img/pic/illustration/image-20200705094201933.png)

## 3、技术

* 前端：HTML(结构)、CSS(表现)、**JavaScript**(行为)——(W3C 标准)
  
  由浏览器负责解释执行，分别描述页面的结构、控制页面内中元素的样式、响应用户操作

* 后端：ASP、PHP、JSP、NodeJS 等

  由服务器负责执行

静态网页和动态网页

* 静态网页：由前端技术实现（扩展名：`.htm` 或 `.html`）
* 动态网页：由前端和后台（服务器端）技术共同实现（扩展名：`.asp` 或 `.php` 或 `.jsp`）

## 4、工具

* 浏览器：Firefox、Chrome、IE

* 编辑器：Sublime Text、VS code

* 调试工具：FireBug

* 图片工具：PhotoShop

* IDE（集成开发工具）：DW、WebStorm、Hbuilder

* IE6浏览器兼容测试：ietester

## 5、万维网联盟(W3C)

万维网联盟(W3C)：World Wid Web Consortium 定义网页相关标准(HTML、CSS、DOM、HTTP、XML等)

WHATWG：网页超文本应用技术工作小组 推动网络 HTML5 标准

## 6、文档

W3School离线手册

CSS

Unicode

正则表达式

MDN

……

## 7、其他

### (1)HTTP

> HTTP(Hyper Text Transfer Protocol，超文本传输协议)是一个简单的请求-响应协议，它通常运行在TCP之上。它指定了客户端可能发送给服务器什么样的消息以及得到什么样的响应。请求和响应消息的头以ASCII码形式给出；而消息内容则具有一个类似MIME的格式。
>
> HTTP是基于客户/服务器模式，且面向连接的。典型的HTTP事务处理有如下的过程：
>
> （1）客户与服务器建立连接；
>
> （2）客户向服务器提出请求；
>
> （3）服务器接受请求，并根据请求返回相应的文件作为应答；
>
> （4）客户与服务器关闭连接。

状态码

| 消息                    | 描述                                                         |
| ----------------------- | ------------------------------------------------------------ |
| 100 Continue            | 服务器仅接收到部分请求，但是一旦服务器并没有拒绝该请求，客户端应该继续发送其余的请求。 |
| 101 Switching Protocols | 服务器转换协议：服务器将遵从客户的请求转换到另外一种协议。   |

| 消息                              | 描述                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| **200** OK                        | 请求成功（其后是对GET和POST请求的应答文档。）                |
| 201 Created                       | 请求被创建完成，同时新的资源被创建。                         |
| 202 Accepted                      | 供处理的请求已被接受，但是处理未完成。                       |
| 203 Non-authoritative Information | 文档已经正常地返回，但一些应答头可能不正确，因为使用的是文档的拷贝。 |
| 204 No Content                    | 没有新文档。浏览器应该继续显示原来的文档。如果用户定期地刷新页面，而Servlet可以确定用户文档足够新，这个状态代码是很有用的。 |
| 205 Reset Content                 | 没有新文档。但浏览器应该重置它所显示的内容。用来强制浏览器清除表单输入内容。 |
| 206 Partial Content               | 客户发送了一个带有Range头的GET请求，服务器完成了它。         |

| 消息                   | 描述                                                         |
| ---------------------- | ------------------------------------------------------------ |
| 300 Multiple Choices   | 多重选择。链接列表。用户可以选择某链接到达目的地。最多允许五个地址。 |
| 301 Moved Permanently  | 所请求的页面已经转移至新的url。                              |
| 302 Found              | 所请求的页面已经临时转移至新的url。                          |
| 303 See Other          | 所请求的页面可在别的url下被找到。                            |
| 304 Not Modified       | 未按预期修改文档。客户端有缓冲的文档并发出了一个条件性的请求（一般是提供If-Modified-Since头表示客户只想比指定日期更新的文档）。服务器告诉客户，原来缓冲的文档还可以继续使用。 |
| 305 Use Proxy          | 客户请求的文档应该通过Location头所指明的代理服务器提取。     |
| 306 *Unused*           | 此代码被用于前一版本。目前已不再使用，但是代码依然被保留。   |
| 307 Temporary Redirect | 被请求的页面已经临时移至新的url。                            |

| 消息                                | 描述                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| 400 Bad Request                     | 服务器未能理解请求。                                         |
| 401 Unauthorized                    | 被请求的页面需要用户名和密码。                               |
| 401.1                               | 登录失败。                                                   |
| 401.2                               | 服务器配置导致登录失败。                                     |
| 401.3                               | 由于 ACL 对资源的限制而未获得授权。                          |
| 401.4                               | 筛选器授权失败。                                             |
| 401.5                               | ISAPI/CGI 应用程序授权失败。                                 |
| 401.7                               | 访问被 Web 服务器上的 URL 授权策略拒绝。这个错误代码为 IIS 6.0 所专用。 |
| 402 Payment Required                | 此代码尚无法使用。                                           |
| 403 Forbidden                       | 对被请求页面的访问被禁止。                                   |
| 403.1                               | 执行访问被禁止。                                             |
| 403.2                               | 读访问被禁止。                                               |
| 403.3                               | 写访问被禁止。                                               |
| 403.4                               | 要求 SSL。                                                   |
| 403.5                               | 要求 SSL 128。                                               |
| 403.6                               | IP 地址被拒绝。                                              |
| 403.7                               | 要求客户端证书。                                             |
| 403.8                               | 站点访问被拒绝。                                             |
| 403.9                               | 用户数过多。                                                 |
| 403.10                              | 配置无效。                                                   |
| 403.11                              | 密码更改。                                                   |
| 403.12                              | 拒绝访问映射表。                                             |
| 403.13                              | 客户端证书被吊销。                                           |
| 403.14                              | 拒绝目录列表。                                               |
| 403.15                              | 超出客户端访问许可。                                         |
| 403.16                              | 客户端证书不受信任或无效。                                   |
| 403.17                              | 客户端证书已过期或尚未生效。                                 |
| 403.18                              | 在当前的应用程序池中不能执行所请求的 URL。这个错误代码为 IIS 6.0 所专用。 |
| 403.19                              | 不能为这个应用程序池中的客户端执行 CGI。这个错误代码为 IIS 6.0 所专用。 |
| 403.20                              | Passport 登录失败。这个错误代码为 IIS 6.0 所专用。           |
| 404 Not Found                       | 服务器无法找到被请求的页面。                                 |
| 404.0                               | （无）–没有找到文件或目录。                                  |
| 404.1                               | 无法在所请求的端口上访问 Web 站点。                          |
| 404.2                               | Web 服务扩展锁定策略阻止本请求。                             |
| 404.3                               | MIME 映射策略阻止本请求。                                    |
| 405 Method Not Allowed              | 请求中指定的方法不被允许。                                   |
| 406 Not Acceptable                  | 服务器生成的响应无法被客户端所接受。                         |
| 407 Proxy Authentication Required   | 用户必须首先使用代理服务器进行验证，这样请求才会被处理。     |
| 408 Request Timeout                 | 请求超出了服务器的等待时间。                                 |
| 409 Conflict                        | 由于冲突，请求无法被完成。                                   |
| 410 Gone                            | 被请求的页面不可用。                                         |
| 411 Length Required                 | "Content-Length" 未被定义。如果无此内容，服务器不会接受请求。 |
| 412 Precondition Failed             | 请求中的前提条件被服务器评估为失败。                         |
| 413 Request Entity Too Large        | 由于所请求的实体的太大，服务器不会接受请求。                 |
| 414 Request-url Too Long            | 由于url太长，服务器不会接受请求。当post请求被转换为带有很长的查询信息的get请求时，就会发生这种情况。 |
| 415 Unsupported Media Type          | 由于媒介类型不被支持，服务器不会接受请求。                   |
| 416 Requested Range Not Satisfiable | 服务器不能满足客户在请求中指定的Range头。                    |
| 417 Expectation Failed              | 执行失败。                                                   |
| 423                                 | 锁定的错误。                                                 |

| 消息                           | 描述                                                  |
| ------------------------------ | ----------------------------------------------------- |
| 500 Internal Server Error      | 请求未完成。服务器遇到不可预知的情况。                |
| 500.12                         | 应用程序正忙于在 Web 服务器上重新启动。               |
| 500.13                         | Web 服务器太忙。                                      |
| 500.15                         | 不允许直接请求 Global.asa。                           |
| 500.16                         | UNC 授权凭据不正确。这个错误代码为 IIS 6.0 所专用。   |
| 500.18                         | URL 授权存储不能打开。这个错误代码为 IIS 6.0 所专用。 |
| 500.100                        | 内部 ASP 错误。                                       |
| 501 Not Implemented            | 请求未完成。服务器不支持所请求的功能。                |
| 502 Bad Gateway                | 请求未完成。服务器从上游服务器收到一个无效的响应。    |
| 502.1                          | CGI 应用程序超时。　·                                 |
| 502.2                          | CGI 应用程序出错。                                    |
| 503 Service Unavailable        | 请求未完成。服务器临时过载或宕机。                    |
| 504 Gateway Timeout            | 网关超时。                                            |
| 505 HTTP Version Not Supported | 服务器不支持请求中指明的HTTP协议版本。                |

### (2)IP 地址与 ARP

IP 地址（Internet Protocol Address）是指互联网协议地址，又译为网际协议地址。IP 地址是[IP 协议](https://baike.baidu.com/item/IP协议)提供的一种统一的地址格式，它为互联网上的每一个网络和每一台主机分配一个逻辑地址，以此来屏蔽物理地址的差异。

* 公有地址（Public address）由 Inter NIC（Internet Network Information Center 因特网信息中心）负责。这些 IP 地址分配给注册并向 Inter NIC 提出申请的组织机构。通过它直接访问因特网。

* 私有地址（Private address）属于非注册地址，专门为组织机构内部使用。

以下列出留用的内部私有地址

|      | 私有地址段                   |
| ---- | ---------------------------- |
| A类  | 10.0.0.0--10.255.255.255     |
| B类  | 172.16.0.0--172.31.255.255   |
| C类  | 192.168.0.0--192.168.255.255 |

地址解析协议，即 ARP（Address Resolution Protocol），是根据[IP 地址](https://baike.baidu.com/item/IP地址)获取[物理地址](https://baike.baidu.com/item/物理地址/2129)的一个[TCP/IP 协议](https://baike.baidu.com/item/TCP%2FIP协议)。

### (3)URL 与 DNS

在 WWW 上，每一信息资源都有统一的且在网上唯一的地址，该地址就叫 URL（Uniform Resource Locator,统一资源定位符），它是 WWW 的统一资源定位标志，就是指网络地址。

也可认为由4部分组成：协议、主机、端口、路径

URL的一般语法格式为：`protocol :// hostname[:port] / path / [;parameters][?query]#fragment`

例如：`https://loacalhost:3000/test`

`ftp://192.168.10.100/`

域名系统（服务）协议（DNS）是一种分布式网络目录服务，主要用于域名与 IP 地址的相互转换。

### (4)浏览器

* 发展历程

1992年，托尼哟翰逊(Tony Johnson)发布了 Midas，它允许用户浏览 UNIX 和 VMS 网页上的文档。

1993年，NCSA 发布了 Mosaic 浏览器。

1994年，网景公司(Netscape)发布了 Navigator 浏览器。

1995年，IE浏览器(Internet Explorer)的发布掀起了“浏览器之战”。

1996年，网景公司的 Navigator 浏览器所占有的浏览器市场份额达 86%。微软公司开始将 IE 浏览器整合到 OS (操作系统)中。

1996年9月，Opera 浏览器面世。

1998年，网景公司启动其开源产品，开始推出 Mozilla。这一年的下半年，网景公司被 AOL(美国在线服务公司)收购。

2002年，Firefox(火狐)浏览器面世。

2003年，苹果公司发布 Safari 浏览器。

2004年，IE 浏览器所占有的市场份额达到了历史顶峰-92%。自此以后，其市场份额开始下滑。

2006年6月，Firefox 3 的发布创下了吉尼斯世界纪录——一天有800万人下载。

2006年10月，专为 Windows XP、Windows Server 2003 和 Windows Vista 而设计的 IE 7 面世。

2008年，谷歌公司发布 Chrome 浏览器。

2009年，专为 Windows 7、Windows Server 2003 与 2008、Windows Vista 和 WindowsXP 设计的 IE 8 面世。同年，Firefox 3.5 面世。它是第一款支持多点触控的浏览器。

2010年，谷歌公司发布了 Chrome 5.0 浏览器。它是第一款稳定支持三个平台的浏览器，还是第一款有书签同步功能(bookmark synchronization)的浏览器。

2011年，微软发布 IE 9，IE 9 采用了新的 JavaScript 引擎 Chakra，使网页加载速度更快，同时利用显卡 GPU 加速文字和图形的渲染，使 CPU 的负担大大减轻。另外，IE 9开始支持 HTML5 和 CSS3。

2012年，Windows 8 正式上市后，IE 10 问世。

2013年，随着 Windows 8.1 的正式发布，IE 11 问世。IE 11 在IE 10 的基础上再次扩大对 HTML5 和 CSS3 的支持，如支持 HTML5 拖放、HTML5 全屏、CSS 边框图、视频码率控制、视频字幕隐藏、媒体加密、WebGL 等，使得 IE 11 全面支持 HTML5 新特性。

* 浏览器的种类很多，但是主流的内核只有四种，各种不同的浏览器，就是在主流内核的基础上，添加不同的功能构成 。

1、Trident 内核

代表产品为 Internet Explorer，又称其为 IE 内核。Trident（又称为 MSHTML），是微软开发的一种排版引擎。使用 Trident 渲染引擎的浏览器有：IE、傲游、世界之窗浏览器、Avant、腾讯 TT、Netscape 8、NetCaptor、Sleipnir、GOSURF、GreenBrowser 和 KKman等  。

2、Gecko 内核

代表作品为 Mozilla Firefox。Gecko 是一套开放源代码的、以 C++ 编写的网页排版引擎，是最流行的排版引擎之一，仅次于 Trident。使用它的最著名浏览器有 Firefox、Netscape6至9  。

3、WebKit 内核

代表作品有 Safari、Chrome。WebKit 是一个开源项目，包含了来自 KDE 项目和苹果公司的一些组件，主要用于 macOS 系统，它的特点在于源码结构清晰、渲染速度极快。缺点是对网页代码的兼容性不高，导致一些编写不标准的网页无法正常显示。

4、Presto 内核

代表作品 Opera。Presto 是由 Opera Software 开发的浏览器排版引擎，供 Opera 7.0 及以上使用。它取代了日版Opera 4至6版本使用的 Elektra 排版引擎，包括加入动态功能，例如网页或其部分可随着DOM及Script语法的事件而重新排版  。

* 主流的浏览器分为 IE、Chrome、Firefox、Safari 等几大类，它们具有以下特点：

1、IE 浏览器。IE 浏览器是微软推出的 Windows 系统自带的浏览器，它的内核是由微软独立开发的，简称 IE 内核，该浏览器只支持 Windows 平台。国内大部分的浏览器，都是在IE内核基础上提供了一些插件，如360浏览器、搜狗浏览器等。

2、Chrome 浏览器。Chrome 浏览器由 Google 在开源项目的基础上进行独立开发的一款浏览器，市场占有率第一，而且它提供了很多方便开发者使用的插件，因此该浏览器也是本书开发的主要浏览器。Chrome 浏览器不仅支持 Windows 平台，还支持 Linux、Mac 系统，同时它也提供了移动端的应用（如 Android 和 iOS 平台）。

3、Firefox 浏览器。Firefox 浏览器是开源组织提供的一款开源的浏览器，它开源了浏览器的源码，同时也提供了很多插件，方便了用户的使用，支持 Windows 平台、Linux 平台和 Mac 平台 。

4、Safari 浏览器。Safari 浏览器主要是 Apple 公司为 Mac 系统量身打造的一款浏览器，主要应用在 Mac 和 iOS 系统中 。

5、欧朋（Opera）浏览器。

* 移动端浏览器

1、内置浏览器

手机操作系统厂商开发

2、可下载浏览器

独立于操作系统，QQ 浏览器、UC 浏览器

3、webview

独立程序，留给原生应用的一个操作系统浏览接口

4、代理浏览器

在服务端完成渲染，返回一个压缩页面

5、混合浏览器

代理浏览器、完备浏览器(在浏览器上渲染页面)结合——省流模式

## 其他文章

[web入门基础知识](https://www.jianshu.com/p/43dc210968a2)

[浏览器简介](https://www.cnblogs.com/superjishere/p/11628235.html)

[What really happens when you navigate to a URL](http://igoro.com/archive/what-really-happens-when-you-navigate-to-a-url/)

[HTTP必知必会](https://www.cnblogs.com/starstone/p/4890409.html) [Vscode 小白使用介绍](https://www.cnblogs.com/tu-0718/p/10935910.html)

[前端vscode常用快捷键总结](https://www.cnblogs.com/web-shu/p/11958885.html)

[Vscode前端开发插件大全](https://segmentfault.com/a/1190000020361775)

[VsCode中使用Emmet神器快速编写HTML代码](https://www.cnblogs.com/summit7ca/p/6944215.html)
