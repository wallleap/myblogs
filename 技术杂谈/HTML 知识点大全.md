---
title: HTML 知识点大全
date: 2020-04-02 08:33
updated: 2020-04-02 08:33
cover: //cdn.wallleap.cn/img/pic/cover/202302VruszT.jpg
category: 技术杂谈
tags:
  - web
  - 前端
description: HTML 知识点大全
---

HTML 搭建网页的结构，相当于人体骨架

## 一、HTML 简介

### 1、HTML

全称为超文本标记语言（Hypetext Markup Language）

- 其中<font color=orange>超文本</font>是相对纯文本来说的，HTML 除了纯文本内容（文字、字符）还可以包括超链接、图片、音频、视频

- 负责网页三要素中的结构

- 使用<font color=orange>标签(记)</font>的形式来标识网页中的不同组成部分`<标签名>`

  - 开始标签 `<h1>`，结束标签 `</h1>`

- 超文本标识——超链接、图片等

### 2、网页标准格式

一个简单的网页可以只有文本内容，也就是内容只写入纯文本，文件名后缀为 `.html` 或 `.htm`，浏览器将会把文本内容自动加到 `body` 标签中，基本内容如下

- `<html></html>` 根标签，有且只有一个，网页内容写到里面

- html 两个子标签：

  - `<head></head>` 设置网页头部信息 不会在网页中直接显示 给浏览器看 解析网页
  - `<body></body>` 网页主体 页面中可见部分写在这
  - `head` 子标签：
    - `<title></title>` 网页标题 将在浏览器标签栏显示
    - `<meta >` 元信息

标签关系 —— 父标签、子标签、兄弟标签、祖先标签、后代标签

```html
<html>
   <head>
      <title></title>
   </head>
   <body>
     文本内容在这
   </body>
</html>
```

### 3、发展

- 1993年6月：HTML第一个版本发布
- 1995年11月：HTML2.0
- 1997年1月：HTML3.2(W3C推荐)
- 1999年12月：HTML4.01(W3C推荐)
- 2000年底：XHTML1.0(W3C推荐)
- 2014年10月：HTML5(W3C推荐)

html xml xhtml html5

## 二、HTML 5 标准

（1）Doctype 使用版本

> `<!DOCTYPE>` 声明必须是 HTML 文档的第一行，位于 `<html>` 标签之前。
>
> `<!DOCTYPE>` 声明不是 HTML 标签；它是指示 web 浏览器关于页面使用哪个 HTML 版本进行编写的指令。
>
> 在 HTML 4.01 中，`<!DOCTYPE>` 声明引用 DTD，因为 HTML 4.01 基于 SGML。DTD 规定了标记语言的规则，这样浏览器才能正确地呈现内容。
>
> HTML5 不基于 SGML，所以不需要引用 DTD。
>
> **提示：**请始终向 HTML 文档添加 `<!DOCTYPE>` 声明，这样浏览器才能获知文档类型。

HTML 4

- 过渡版
  
  ```HTML
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
  "http://www.w3.org/TR/html4/loose.dtd">
  ```

- 严格版
  
  ```html
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
  "http://www.w3.org/TR/html4/strict.dtd">
  ```

- 框架版
  
  ```html
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
  "http://www.w3.org/TR/html4/frameset.dtd">
  ```

XHTML

```HTML
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```

HTML5

html4.01 和 xhtml 的文档声明这么麻烦，还好我们只要使用 HTML 5 就 OK 了

```html
<!DOCTYPE html>
```

不写文档声明，有些浏览器会进入**怪异模式**（解析网页时出现异常）

（2）一个最基本的 HTML 5 页面

```html
<!DOCTYPE html>
<html lang="en"> <!-- en英文、zh中文 -->
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>网页标题</title>
</head>
<body>
  <h1>网页正文</h1>
</body>
</html>
```

- Doctype 文档声明，必须放在 html 标签前面，且之前不能放置内容，即使是注释
- html、head、body、title 根标签、头部标签、主体标签、网页标题，html 中的 lang 属性规定元素内容的语言，当然，这个属性其他标签也有
- meta 元素可提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词，这里charset设定的字符集为 UTF-8，viewport 主要针对移动端

## 三、语法规范

- HTML 中不区分大小写，一般使用小写

- 注释不能嵌套

- 标签必须结构完整，要么成对出现，要么自结束标签(浏览器尽最大努力正确解析页面，修正不符合语法规范的内容，但是有些情况会修正错)

- HTML 标签可以嵌套，但是不能交叉嵌套

- 属性必须有值，且值必须加引号(单引号、双引号都可以)

## 四、概念

### 1、标记

又称标签，标签注重的是语义化，即什么标签做什么事（比如一个标题那么就用 `h$` 包裹）

### 2、元素

一个完整的标签（包含标签括起来的内容）

### 3、标签分类

（1）根据是否有结束标签

- 单标签：又称自结束标签，例如 `<img src='../img/1.png' >`，推荐在后面的 `>` 之前不加上 `/`（如果在 xml 中，必须加上 `/`）
- 双标签：具有开始标签和结束标签，内容写在开始标签和结束标签之间，例如 `<h1>一级标题</h1>`

（2）根据内容是否可替换

- 替换，例如图片标签中没有内容，但是它会被 `src` 中图片替换
- 非替换，常规的文本相关的标签，标签中是什么内容就显示什么内容

（3）根据元素中是否有内容

- 有内容：有结束标签，内容放在开始标签和结束标签中
- 空元素：没有闭合的标签，例如后面讲的 link、hr、br、img 等标签

（4）根据显示模式（这个需要掌握，一般说 HTML 标签，就按这个分）

- 行内元素：`b、big、i、small、tt、abbr、acronym、cite、code、dfn、em、kbd、strong、samp、var、a、bbdo、br、img、map、object、q、script、span、sub、sup、button、input、label、select、textarea`——只占据它对应标签的边框所包含的空间
- 块级元素：`address、article、aside、audio、blockquote、canvas、dd、div、dl、fieldset、figcaption、figure、footer、form、h1-6、header、hgroup、hr、noscript、ol、output、p、pre、section、table、tfoot、ul、video`——独占一行
- 行内块元素：`input、td`

这个是常用的分类（然而 MDN 中并没有分行块元素），CSS 中还会再提到

可以看下[HTML行内元素、块状元素、行内块状元素的区别](https://blog.csdn.net/yayedecsdn/article/details/100864500)标签，[HTML元素分类](https://blog.csdn.net/COCOLI_BK/article/details/85553078)特点

注意：img 和 button 标签虽然都是行内标签，但是他们自身有个特性，设置的宽高是能生效的

### 4、注释

HTML 文档中的注释使用 `<!--  -->` 包裹，写在这里面的内容浏览器能够识别，但是不会在页面中渲染显示出来

```html
<!-- 
注释内容，不会在页面中显示 好的注释习惯 简单明了
功能：
作者：
日期：
-->
```

### 5、属性

标签的属性（开始标签中添加 `属性名=”属性值”`）

例如：

```html
<p align="center" style="font-size: 14px;">文字</p>
```

- `p` 就是标签名，这是一个段落标签
- `align`、`style` 就是这个标签的属性名
- 属性名等号后的就是属性值，属性值需要用引号引起来，属性名和属性值一般成对出现（如果属性值为 BOOL 类型，有些可以省略属性值，只写属性名）
- 常见的全局属性
  - `lang` 属性
  - `title` 属性
  - `id`
  - `class`

### 6、路径

- 绝对路径：相对于根目录，`/目录`

- **相对路径**：相对于当前资源所在目录的位置

  - `../` 上层路径

  - `./` 当前路径

  - `目录/` 下层

eg：

```
- /
  - img
    - picture1.webp
  - css
    - base.css
    - index.css
  - js
    - script.js
  - html
    - blog.html
  - favicon.ico
  - index.html
```

- `index.html` 中引用 `script.js` —— `./js/script.js` 或者 `js/script.js`

- `index.html` 中引用 `favicon.ico` —— `/favicon.ico`，一般都是放在根目录，引用的时候使用绝对目录

- `blog.html` 中引用 `picture1.webp` —— `../img/picture1.webp`

### 7、进制

满几进一

- 二进制：满二进一，由 0、1 组成，例如 `11111110` 这八位表示 `2^0^ *0+2^1^ *1+2^2^+2^3^+2^4^+2^5^+2^6^+2^7^`，即十进制 254
- 八进制：满八进一，由 0~7 组成，例如 `O12` 表示十进制 10（`8^0^*2+8^1^*1`）
- 十进制：满十进一，由 0~9 组成
- 十六进制：由 `0~9、A~F` 组成，例如 `oX1e` 表示十进制 30

### 8、单位

- 1，看情况，有的是 1=100%，有的 1 指的是 1px
- % 百分比，相同百分比参照物不同，得到的结果不同
- px 像素，有物理像素、CSS 像素、设备像素
- vw/vh 1vw 等于视口宽/高度的 1%
- em 1em 为一个字体大小
- rem 根标签的字体大小

## 五、标签

### 1、根标签 `html`

一个 HTML 文档的根（顶级元素），所以它也被称为*根元素*。所有其他元素必须是此元素的后代。

通过 `lang` 属性指定整个页面的语言

```html
<html lang="en">
  ……
</html>
```

### 2、头标签 `head`

规定文档相关的配置信息（元数据），包括文档的标题，引用的文档样式和脚本等。

- `title`：网页标题

```html
<title>网页标题</title>
```

- `meta`： 设置网页元信息（meta-information），比如网页字符集、针对搜索引擎和更新频度的描述和关键词，是一个单标签：

  - 编码

    - 乱码问题原因：计算机只认识 0、1，计算机中保存的内容需要转化为二进制编码来保存，读取内容时需要转换成正确的内容----编码、解码  编码和解码采用的字符集不同

    - 常见字符集：ASCII、ISO-8859-1、GBK、GB2312（中文系统的默认编码）、UTF-8（万国码）

    - 解决：在中文系统的浏览器中，默认的都是 GB2312 编码，更改编码 Unicode，解码 head 中告诉浏览采用的编码字符集

      ```html
      <meta charset=”utf-8”/>  <!-- 编写使用的编码、字符集一致 -->
      ```

  - 重定向

      ```html
      <meta http-equiv=”refresh” content=”秒数;url=网址” />
      ```

  - 网页关键字

      ```html
      <meta name="keywords" content="关键字内容1,2,3" />
      ```

  - 网页描述

      ```html
      <meta name="description" content="描述" />
      ```

    - 搜索引擎在检索页面时，会同时检索页面中的关键字和描述，但是不会影响页面在搜索引擎中的排名

  - 与移动开发有关

      ```html
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      ```

- `link`：定义文档与外部资源的关系

    ```html
    属性 
    href -- 指定需要加载的资源的地址URI 
    media -- 媒体类型
    rel -- 指定链接类型，设定是指对象和链接目标的关系，可选值，link 还可以用 Shortcut Icon 等
    rev -- 指定链接类型 
    type -- 指定所连接文档的MIME类型，css 的 MIME 是 type/css，一般使用 type="text/css" 
    ```

  - 其中 `rel` 和 `href` 是必须要设置的

  - 引入CSS样式

    ```html
    <link rel="stylesheet" href="style.css">
    ```
  
  - 引入网页 icon 图标

    ```html
    <link rel="shortcut icon" href="/favicon.ico" type="image/x-icon">
    ```

  - 很久以前，网速非常慢，网站主要就是分享文章的，就可以标识文档开始（告知搜索引擎）、文档上一页（浏览器可以回退）、下一页（浏览器可以提前加载此页）

    ```html
    <link rel="start" type="text/html" href="http://www.dreamdu.com/xhtml/" />
    <link rel="prev" type="text/html" href="http://www.dreamdu.com/xhtml/alternate/" />
    <link rel="next" type="text/html" href="http://www.dreamdu.com/xhtml/attribute_rel/" />
    ```

  - 如果还想了解 link 标签的话，自己可以到 [html 中 link 的用法](https://www.cnblogs.com/chenkg/p/5003426.html) 去看下

- `style`：包含文档的样式信息或者文档的部分内容。默认情况下，该标签的样式信息通常是 CSS 的格式。

### 3、文档主体标签 `body`

body 元素定义文档的主体。

body 元素包含文档的所有内容（比如文本、超链接、图像、表格和列表等等）

JS DOM 中 `document.body` 属性提供了可以轻松访问文档的 body 元素的脚本。

### 4、脚本

- `noscript`：如果页面上的脚本类型不受支持或者当前在浏览器中关闭了脚本，则在 HTML` <noscript> `元素中定义脚本未被执行时的替代内容。
- `script`：HTML `<script>` 元素用于嵌入或引用可执行脚本。

## 六、常用标签

### 1、标题标签

一共有六级 h1 h2 h3 h4 h5 h6

```html
<h1>这是一级标题</h1>
```

不关心显示的大小 注重标签语义 h1 最重要，表示网页中的主要内容

对于搜索引擎来说，h1 的重要性仅次于 title

建议只使用 h1-h4

### 2、段落标签

```html
<p>这是一个段落</p>
```

表示一个段落/自然段，独占一行，两段之间有间隔

在 HTML 中，字符之间多个空格当成一个空格解析，换行也当成空格

```html
<center>需要居中的元素</center>
```

### 3、换行

```html
<br />
```

### 4、水平线(分割线)

```html
<hr />
```

### 5、容器

`div` 表示一个盒子或容器

`span` 没有特定的语义，通常用于样式的应用

### 6、文字标记

**`<b>`**：加粗

**`<strong>`**：强调

`b` 和 `strong` 的区别就在于前者是物理元素，仅表示加粗，后者是逻辑元素，表示强调的意思，`<b>` 是在 html 中的标签，而在 xhtml 中只能使用 `<strong>`，后者兼容性更好。

**`<i>`**：斜体，现在主要用于文本图标

**`<em>`**：次级强调

| 文字标记       | 语义                          |
| :------------- | :---------------------------- |
| `<blockquote>` | 长引用                        |
| `<q>`          | 短引用                        |
| `<abbr>`       | 缩写                          |
| `<address>`    | 作者联系信息                  |
| `<pre>`        | 预格式化的文本,常用于程序代码 |
| `<code>`       | 定义计算机代码文本。          |
| `<del>`        | 删除的文本                    |
| `<sub>`        | 上标                          |
| `<sup>`        | 下标                          |

### 7、超链接

a 标签可以将包含内容设置为超链接，设置了 href 属性后点击内容可跳转到相应的页面

```html
<a href="目标地址" target="_blank">链接</a>
```

常用属性：

- href:
  - url：设置为链接之后可以跳转到该页面 `<a href="https://wallleap.cn">wallleap</a>`
  - #id：设置锚点，点击可以跳转到这个 id 名处 `<h1 id="title"></h1>`，如果跳转的地方是一个超链接也可设置 name 属性，之后点击这个链接`<a href="#title">转到title</a>`，就能跳转到这个地方，也可以加到链接后：`<a href="https://a.c#title">跳转锚点</a>`
  - mailto：打开默认邮件应用发送邮件到该邮箱 `<a href="mailto:15579576761@163.com">发送邮件</a>`，也可以设置好主题、内容：`<a href="mailto:15579576761@163.com?subject=Re:wallleap.cn%20某文章&body=发送自wallleap">发送邮件</a>`（还可以有拨号等，具体的可以查看 MDN）

- target:
  - `_self`：默认，当前页面打开
  - `_blank`：设置为内联框架的名称，可以在内联框架中打开页面
  - `_top`：在当前窗口中载入整个页面

> **提示**：如果不使用 href 属性，则不可以使用如下属性：download, hreflang, media, rel, target 以及 type 属性。
>
> **提示**：被链接页面通常显示在当前浏览器窗口中，除非您规定了另一个目标（target 属性）。
>
> **提示**：请使用 CSS 来设置链接的样式。

### 8、图片标签

`<img src="路径" alt="图片描述" width="200px" height="200px" />`

alt：图片不能显示时，对图片描述；搜索引擎根据 alt 搜索图片

宽度和高度只设置一个，另一个也会等比例变化，同时指定按照值变化，自适应页面不设置宽高值

图片格式：

- JPEG(JPG) 支持颜色多，可压缩，不支持透明；

- GIF 支持颜色少，支持简单的透明，支持动态图；

- PNG 支持颜色多，支持复杂的透明；

- webp 提供了有损压缩与无损压缩（可逆压缩）的图片文件格式，

- base64：当图片很小时（一般小于8kb），或者需要先加载的图片，可以转为base64

效果不一致，使用效果好的；效果一致，使用小的。

### 9、列表标记

**1）ul、ol、li**

```html
<ol>
  <li>巴西</li>
  <li>阿根廷</li>
  <li>德国</li>
</ol>
```

1. 巴西
2. 阿根廷
3. 德国

```html
<ul>
  <li>巴西</li>
  <li>阿根廷</li>
  <li>德国</li>
</ul>
```

- 巴西
- 阿根廷
- 德国

**2）dl、dt、dd**

```html
<dl>
  <dt>计算机</dt>
  <dd>用来计算的仪器 ... ...</dd>
  <dt>显示器</dt>
  <dd>以视觉方式显示信息的装置 ... ...</dd>
</dl>
```

![](http://moretrue.cn/Public/uploads/ueditor/2/573db1f4e8657.JPG)

![](https://cdn.wallleap.cn/img/pic/illustration/20200810164728.png)

`ul`：无序列表，`li` 子元素显示为默认的黑色圆点，也可通过参数自定义列表的符号，常用于新闻列表展示

`ol`：有序列表，可以在列表前增加序号，如1，2，3，4；适用于排行榜；

`dl`：自定义列表，可以包括标题及内容，可适合用制作风箱结构；

### 9、表格标签

`table`：表格，适合于超过两行以上的数据呈现

一个表格 `<table>` 是由每行 `<tr>` 组成的，每行是由列 `<td>` 组成的。

> 所以我们要记住，一个表格是由行组成的（行是由列组成的），而不是由行和列组成的。（td 是嵌套在 tr 中的）

`<table>` 下的 `<caption>` 标签、 `<thead>` 标签、`<tbody>` 标签、`<tfoot>` 标签

- `<caption>`——表格的标题，一般是 `table` 的第一个子元素（*零个或一个*）
- `<colgroup>`——表格列组标签，用来定义表中的一组列表（*零个或多个*）
- `<thead>`——表头，表格的最上面一行（*零个或一个*）
  - `<tr>` 定义表格中的行
    - `<th>` 定义表格内的表头单元格（列），此元素内部的文本通常会呈现为粗体。
- `<tbody>`——表的主体部分（*零个或多个*）
  - `<tr>` 行
    - `<th>` 表头列（如果没有`<thead>` 就需要写上，显示在最上方；有 `<thead>` 可以 `tr*3>th+td*2` 这种形式，位于最左一列）
  - `<tr>` 行
    - `<td>` 列
- `<tfoot>`——汇总行（*零个或一个*）

注：

1、如果写了 `thead`、`tbody`、`tfoot` 这三个部分，**代码顺序书写可以随意**，浏览器显示的时候还是按照 `thead`、`tbody`、`tfoot` 的顺序依次来显示内容。如果不写 thead、tbody、tfoot，那么浏览器解析并显示表格内容的时候是从按照代码的从上到下的顺序来显示。

2、当表格非常大内容非常多的时候，如果用 `thead`、`tbody`、`tfoot` 标签的话，那么**数据可以边获取边显示**。如果不写，则必须等表格的内容全部从服务器获取完成才能显示出来。

3、`tbody` 标签是“必须的”（并不是要求一定写），即使你在代码中并没有写，在浏览器渲染之后 `tr` 和 `td` 还是会在 `tbody` 中

属性：表格中的属性差不多都是不推荐使用的（可以写样式），但由于开发的时候写属性更方便一点，因此列出来

表格 `<table>` 的属性：

- `border`：边框，单位 px。
- `style="border-collapse:collapse;"`：单元格的线和表格的边框线合并。
- `width`：宽度，单位 px。
- `height`：高度，单位 px。
- `bordercolor`：表格的边框颜色。
- `align`：**表格**的水平对齐方式，属性值可以填：`left` 、`right`、 `center`。
  - 注意：这里不是设置表格里内容的对齐方式，如果想设置内容的对齐方式，要对单元格标签 `<td>` 进行设置）
- `cellpadding`：单元格内容到边的距离，单位 px。默认情况下，文字是紧挨着左边那条线的，即默认情况下的值为 0。
  - 注意不是单元格内容到四条边的距离，而是到一条边的距离，默认是与左边那条线的距离。如果设置属性 `dir="rtl"`（在下面有讲），那就指的是内容到右边那条线的距离。
- `cellspacing`：单元格和单元格之间的距离（外边距），单位 px。默认情况下的值为0。
- `bgcolor="#99cc66"`：表格的背景颜色。
- `background="路径src/..."`：背景图片。
  - 背景图片的优先级大于背景颜色。
- `bordercolorlight`：表格的上、左边框，以及单元格的右、下边框的颜色。
- `bordercolordark`：表格的右、下边框，以及单元格的上、左的边框的颜色。
  这两个属性的目的是为了设置3D的效果。
- `dir`：公有属性，单元格内容的排列方式(direction)。 可以取值：`ltr`：从左到右（left-to-right，默认），`rtl`：从右到左（right-to-left），既然说`dir`是共有属性，如果把这个属性放在任意标签中，那表明这个标签的位置可能会从右开始排列。

行 `<tr>`属性：

- `dir`：公有属性，设置这一行单元格内容的排列方式。可以取值：`ltr`：从左到右（left-to-right，默认），`rtl`：从右到左（right-to-left）
- `bgcolor`：设置这一行的单元格的背景色。
  注：没有background属性，即：无法设置这一行的背景图片，如果非要设置，可以用css实现。
- `height`：一行的高度
- `align="center"`：一行的内容水平居中显示，取值：`left`、`center`、`right`
- `valign="center"`：一行的内容垂直居中，取值：`top`、`middle`、`bottom`

单元格(列) `td`/`th` 属性：

- `align`：内容的横向对齐方式，属性值可以填：`left`、`center`、`right`
- `valign`：内容的纵向对齐方式，属性值可以填：`top`、`middle`、`bottom`
- `width`：宽度——绝对值或者相对值(%)
- `height`：单元格的高度
- `bgcolor`：设置这个单元格的背景色
- `background`：设置这个单元格的背景图片

<font color="red">单元格合并</font>：如果要将两个单元格合并，那肯定就要删掉一个单元格。

- `colspan`：横向合并。例如 `colspan="2"` 表示当前单元格在水平方向上要占据两个单元格的位置。
- `rowspan`：纵向合并。例如 `rowspan="2"` 表示当前单元格在垂直方向上要占据两个单元格的位置。

下面用几个例子讲解表格（这些代码只是演示上面的知识，开发中千万别这样用/手动狗头）

例子1：表格由行 `tr` 组成，行由列 `td` 组成

```html
<!-- 注：table标签一定要有 -->
<table border="1"> <!-- 为了看的更清楚一点，加上border属性(开发中不推荐)——给表格加上边框 -->
  <tr>
    <td>孙悟空</td><td>未知</td><td>男</td><td>花果山</td>  <!-- 由于代码有点长，这里把td写到一行 -->
  </tr>
  <tr>
    <td>猪八戒</td><td>未知</td><td>男</td><td>高老庄</td>
  </tr>
  <tr>
    <td>沙和尚</td><td>未知</td><td>男</td><td>流沙河</td>
  </tr>
  <tr>
    <td>唐三藏</td><td>23</td><td>男</td><td>东土大唐</td>
  </tr>
  <tr>
    <td>白龙马</td><td>未知</td><td>男</td><td>鹰愁涧</td>
  </tr>
</table>
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200810160014.png)

例子2：没有加 `thead` 用 `th` 来做表头、table 部分属性

```html
<table border="1" width="400" height="200" bordercolor="skyblue" align="center" cellpadding="10px" cellspacing="5" dir="ltr">
  <tr>
    <th>姓名</th><th>年龄</th><th>性别</th><th>地点</th>
  </tr>
  <tr>
    <td>孙悟空</td><td>未知</td><td>男</td><td>花果山</td>
  </tr>
  <tr>
    <td>猪八戒</td><td>未知</td><td>男</td><td>高老庄</td>
  </tr>
  <tr>
    <td>沙和尚</td><td>未知</td><td>男</td><td>流沙河</td>
  </tr>
  <tr>
    <td>唐三藏</td><td>23</td><td>男</td><td>东土大唐</td>
  </tr>
  <tr>
    <td>白龙马</td><td>未知</td><td>男</td><td>鹰愁涧</td>
  </tr>
</table>
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200810161836.png)

例子3：有 `thead` 且 `tbody` 中不设置 `th`、table 部分属性 + tr 属性

```html
<table border="1" width="500" bordercolor="skyblue" style="border-collapse:collapse;" dir="rtl">
  <thead>
    <tr height="50" valign="bottom">
      <th>姓名</th><th>年龄</th><th>性别</th><th>地点</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>孙悟空</td><td>未知</td><td>男</td><td>花果山</td>
    </tr>
    <tr>
      <td>猪八戒</td><td>未知</td><td>男</td><td>高老庄</td>
    </tr>
    <tr>
      <td>沙和尚</td><td>未知</td><td>男</td><td>流沙河</td>
    </tr>
    <tr>
      <td>唐三藏</td><td>23</td><td>男</td><td>东土大唐</td>
    </tr>
    <tr>
      <td>白龙马</td><td>未知</td><td>男</td><td>鹰愁涧</td>
    </tr>
  </tbody>
  <tfoot>
    <tr align="center">
      <td>取经四人一马组</td><td>以前全都是仙佛来着</td><td>单身汉</td><td>前几集就凑齐了</td> <!-- 汇总行-->
    </tr>
  </tfoot>
</table>
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200810162233.png)

例子4：加上其他几个标签，有 `thead` 且 `tbody` 中设置 `th`、th/td 属性

```html
<table border="1" width="550" bordercolor="skyblue" style="border-collapse:collapse;">
  <caption>取经四人组</caption>
  <colgroup> <!-- 就是把列分组，每组可以加个类名这样的 -->
    <col style="background-color: bisque;">
    <col span="3" style="background-color: rosybrown;">
    <col span="2" style="background-color: silver;">
  </colgroup>
  <thead>
    <tr>
      <th width="100" height="50">物种</th><th>姓名</th><th>年龄</th><th>性别</th><th>地点</th>
    </tr>
  </thead>
  <tfoot>
    <tr align="center">
      <th>说明</th><td>取经四人一马组</td><td>以前全都是仙佛来着</td><td>单身汉</td><td>前几集就凑齐了</td> <!-- 汇总行-->
    </tr>
  </tfoot> <!-- 只要写了这三个，顺序无所谓，仍按照thead->tbody->tfoot -->
  <tbody>
    <tr>
      <th>猴子</th><td>孙悟空</td><td>未知</td><td>男</td><td>花果山</td>
    </tr>
    <tr>
      <th>猪头</th><td>猪八戒</td><td>未知</td><td>男</td><td>高老庄</td>
    </tr>
    <tr>
      <th>河妖？</th><td>沙和尚</td><td>未知</td><td>男</td><td>流沙河</td>
    </tr>
    <tr>
      <th>金蝉</th><td>唐三藏</td><td>23</td><td>男</td><td>东土大唐</td>
    </tr>
    <tr>
      <th>白龙</th><td>白龙马</td><td>未知</td><td>男</td><td>鹰愁涧</td>
    </tr>
  </tbody>
</table>
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200810163542.png)

例子5：单元格合并

```html
<table bgcolor="#ccc" border="1" width="550" bordercolor="red" style="border-collapse:collapse;">
  <tbody>
    <tr bgcolor="yellow">
      <th>姓名</th><th>年龄</th><th>性别</th><th>地点</th><th>前世工作地点</th>
    </tr>
    <tr>
      <td>孙悟空</td><td rowspan="3">未知</td><td rowspan="5">男</td><td>花果山</td><td bgcolor="yellowgreen" rowspan="3">天庭</td>
    </tr>
    <tr>
      <td>猪八戒</td><td>高老庄</td>
    </tr>
    <tr>
      <td>沙和尚</td><td>流沙河</td>
    </tr>
    <tr>
      <td>唐三藏</td><td>23</td><td>东土大唐</td><td>雷音寺</td>
    </tr>
    <tr>
      <td>白龙马</td><td>未知</td><td>鹰愁涧</td><td>西海</td>
    </tr>
    <tr>
      <td colspan="5" align="center">西天取经</td>
    </tr>
  </tbody>
</table>
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200810164637.png)

表格布局：还是在很久以前，表格用来做页面布局，还没学到 CSS，提下这个概念，知道有这个东东就行，现在基本也不用这个做布局了。

### 10、表单

1）表单标记

```html
<form action="表单提交的处理程序地址" method="表单提交方式(post/get)" name="表单名称"></form>
```

`form`元素将所有的表单包含起来，也相应于表单的作用域。

`get`和`post`提交方式的区别：`get`请求把表单的数据显式地放在 URL 参数中，并且对长度和数据值编码有所限制；`post` 请求把表单数据放在 HTTP 请求体中，没有长度限制。

2）文本框

```html
<input type="text" name="控件名称" value="文本框输入值" placeholder="提示信息" disabled readonly required autofocus />
```

3）密码框

```HTML
<input type="password" name="控件名称" placeholder="提示信息"/>
```

4）单选按钮：同一组单选按钮使用同一命名

```HTML
<input type="radio" name="控件名称" value="控件值1" checked />
<input type="radio" name="控件名称" value="控件值2" />
```

5）复选按钮

```html
<input type="checkbox" name="控件名称" value="控件值1" checked />
<input type="checkbox" name="控件名称" value="控件值2" checked />
<input type="checkbox" name="控件名称" value="控件值3" checked />
```

6）下拉列表

```html
<select name="控件名称" multiple="multiple" size="数值">
  <option value="控件值1" selected>选项1</option>
  <option value="控件值2">选项2</option>
</select>
```

7）多行文本框

```html
<textarea name="控件名称" cols="列数" rows="行数"></textarea>
```

8）隐藏控件

```html
<input type="hidden" name="控件名称" value="控件值" />
```

9）普通按钮

```html
<input type="button" value="按钮文字" />
<button type="button">按钮文字</button>
```

10）发送/提交按钮

```html
<input type="submit" value="按钮文字" />
<button type="submit">按钮文字</button>
```

11）重置按钮

```html
<input type="reset" value="按钮文字">
<button type="reset">按钮文字</button>
```

表单实例：

```HTML
<form action="" method="post">
  <fieldset>
    <legend>表单演示</legend>
    <p> <label for="username">姓名：</label><input type="text" name="username" id="username" placeholder="请输入姓名"
        required="required" /> </p>
    <p> <label for="pwd">密码：</label><input type="password" name="pwd" id="pwd" placeholder="请输入密码" /> </p>
    <p> 性别： <label><input type="radio" name="sex" value="1" checked="checked" />男</label> <label><input type="radio"
          name="sex" value="0" />女</label> </p>
    <p> 爱好： <label><input type="checkbox" name="basketball" value="basketball" />篮球</label> <label><input
          type="checkbox" name="football" value="football" />足球</label> </p>
    <p> <label for="bloodtype">血型：</label> <select name="bloodtype" id="bloodtype">
        <option value="A">A型</option>
        <option value="B">B型</option>
        <option value="AB">AB型</option>
        <option value="O">O型</option>
      </select> </p>
    <p> <label for="intro">介绍</label> <textarea name="intro" cols="30" rows="3" id="intro"></textarea> </p> <input
      type="submit" value="提交按钮" /> <input type="reset" value="重置按钮" /> <input type="button" value="自定义按钮" />
  </fieldset>
</form>
```

一般使用 `form` 包裹表单元素，有一个 `submit` 按钮，再给 `form` 设置 `submit` 事件，禁止默认行为，然后再做一些验证，最后再提交。

### 11、转义字符(字符实体)

```html
& 实体名字;

< `&lt;`

\> `&gt;`

空格 `&nbsp;`

版权` &copy;`
```

浏览器解析到实体时，会自动将其转换为相应字符。

| 特殊字符 |      描述      | 字符的代码 |
| :------: | :------------: | :--------: |
|          |     空格符     |  `&nbsp;`  |
|    <     |     小于号     |   `&lt;`   |
|    >     |     大于号     |   `&gt;`   |
|    &     |      和号      |  `&amp;`   |
|    ￥    |     人民币     |  `&yen;`   |
|    ©     |      版权      |  `&copy;`  |
|    ®     |    注册商标    |  `&reg;`   |
|    °     |     摄氏度     |  `&deg;`   |
|    ±     |     正负号     | `&plusmn;` |
|    ×     |      乘号      | `&times;`  |
|    ÷     |      除号      | `&divide;` |
|    ²     | 平方2（上标2） |  `&sup2`   |
|    ³     | 立方3（上标3） |  `&sup3`   |

### 12、框架网页

将浏览器窗口分解为多个小窗口，每个小窗口均可以显示各自的网页

`<frameset rows="" cols="">`：框架网页集，`rows` 为横向分隔，`cols` 为纵向分隔，值可以是具体数值也可以是百分比，注意 `frameset` 标记是和 `body` 标记同级的标记，不能将 `frameset` 标记包含在 `body` 标记中，否则将无法看到框架网页的效果。

`<frame name="" scr="" />`：指定每一个小窗口的名称和链接的网页，窗口的名称可以用于超级链接的 target 属性。

水平分隔两个窗口，每个窗口各占50%

可引入一个外部的页面

```html
<iframe src=”路径” width=”” heigh=”” name=”名称”></iframe>
```

内嵌框架 `<iframe>：可以在一个浏览器窗口种同时显式多个页面文档`

在现实开发中，不推荐使用，内联框架中的内容不会被搜索引擎所检索

## 七、HTML 5 新增标签

### 1、新增语义化标签

以前布局，我们基本用 div 来做，但是 div 对于搜索引擎来说，是没有语义的。

![](https://cdn.wallleap.cn/img/pic/illustration/20200810172732.png)

| 标签名  |      作用      |
| :-----: | :------------: |
| header  |    表示页眉    |
|   nav   |    表示导航    |
| article |      文章      |
| section |      章节      |
|  main   |  文档主要内容  |
|  aside  |     侧边栏     |
| hgroup  |   头/标题组    |
| footer  | 文档或页的页脚 |

![](https://cdn.wallleap.cn/img/pic/illustration/20200810174705.png)

```html
<header>header</header>
<nav>nav</nav>
<main>
  main
  <article>
    article
    <section>section</section>
  </article>
  <aside>aside</aside>
</main>
<footer>footer</footer>
```

兼容性解决：

- IE9：行级元素在设置宽度的时候是失效的（需要将这些标签转换为块级元素）

```css
header, nav, main, article, section, aside, footer{
  display: block;
}
```

- IE8：完全不支持语义标签(不支持HTML5)

  - 方法一：手动创建标签

    ```html
    <script>
      /* 手动创建标签：默认的标签的类型都是行级元素 */
      document.createElement("header")
      document.createElement("nav")
      document.createElement("main")
      document.createElement("article")
      document.createElement("aside")
      document.createElement("footer")
    </script>
    ```

  - 方法二：引入第三方插件 `html5shiv.min.js`

    ```html
    <script src="https://cdn.bootcdn.net/ajax/libs/html5shiv/3.7.3/html5shiv.js"></script>
    ```

### 2、列表

HTML5 中，对 ol、dl 进行了改良

- `ol`：添加了 `start`、`reversed` 属性
  - `start`：可以指定列表编号从多少开始
  - `reversed`：列表反向排序

```html
<ol start="3">
  <li>1</li>
  <li>2</li>
  <li>3</li>
</ol>
<ol start=9 reversed>
  <li>列表值1</li>
  <li>列表值2</li>
  <li>列表值3</li>
  <li>列表值4</li>
  <li>列表值5</li>
</ol>
```

- `dl`：重新定义，`dl` 标签包含多个带名字列表项；每一项包含至少一条带名字的`dt` 元素，用来表示术语；`dt` 后紧跟一个或多个 `dd` 元素，用来表示定义。在一个元素内不允许有相同名字的 `dt`元素，不允许有重复的术语。

  - 可以用于解释术语

    ```html
    <dl>
      <dt><dfn>RSS</dfn></dt>
      <dd>RSS也叫聚合RSS，是在线共享内容的一种简易方式(也叫聚合内容)……</dd>
      <dt><dfn>博客</dfn></dt>
      <dd>博客，又译为网络日志，部落格或部落阁等，是一种通常由个人管理……</dd>
    </dl>
    ```

  - 可以表示辅助信息

    ```html
    <dl>
      <dt>作者</dt>
      <dd>xxx</dd>
      <dt>出版社</dt>
      <dd>xxx出版社</dd>
      <dt>类别</dt>
      <dd>文学</dd>
    </dl>
    ```

### 3、表单

(1) 表单新增的 `type` 属性

- `email` 提供了默认的电子邮箱的完整验证，要求表单值必须包含 `@` 符号，同时必须包含服务器名称，如果不能满足验证，则会阻止当前的数据提交（submit）

    ```html
    邮箱：<input type="email">
    ```

- `tel` 并不是用来实现验证，它的本质目的是为了能够**在移动端打开数字键盘**，意味着限制了用户只能输入数字。

    ```html
    电话：<input type="tel">
    ```

- `url` 验证只能输入合法的网址，必须包含 `http://`

    ```html
    网址：<input type="url">
    ```

- `number` 只能输入数字（包含小数点），不能输入其他的字符
  - `max`：最大值，`min`：最小值，`value`：默认值

    ```html
    数量：<input type="number">
    <input type="number" value="60" min="0" max="100">
    ```

- `search` 可以提供更人性化的输入体验

    ```html
    搜索框：<input type="search">
    ```

- `range` 范围

    ```html
    范围：<input type="range" min="0" max="100" value="50">
    ```

- `color` 颜色

    ```html
    颜色：<input type="color">
    ```

- 日期时间相关

    ```html
    时间：<input type="time"> <!-- 时分秒 -->
    日期：<input type="date"> <!-- 年月日 -->
    日期时间：<input type="datetime"> <!-- 目前大多数浏览器都不支持，只有Safari -->
    日期时间：<input type="datetime-local"> <!-- 日期和时间 -->
    月份：<input type="month">
    星期：<input type="week">
    ```

(2) 表单新增的其他属性

- `placeholder` 提示文本，提示占位

- `autofocus` 自动获取焦点

- `autocomplete`：自动完成 on off

  - 必须成功提交过：提交过才会记录

  - 当前添加 `autocomplete` 的元素必须有 `name` 属性

- `required` 必须输入，如果没有输入则会阻止当前数据提交

- `pattern`：正则表达式验证

- `multiple` 可以选择多个文件，在 email 中，设置 multiple 属性之后可以输入多个邮箱地址，以逗号分隔

- `form` 指定表单 id，会随着该表单一起提交

```html
<form action="" id="myFrm">
  用户名：<input type="text" name="username" placeholder="请输入用户名" autofocus autocomplete="on">
  手机号：<input type="tel" required pattern="^(\+86)?1\d{10)$">
  文件：<input type="file" name="photo" multiple>
  邮箱：<input type="email" multiple>
  <input type="submit" value="提交">
</form>
地址：<input type="text" name="address" form="myFrm">
```

(3) 新增表单元素

- `datalist` 创建选项列表
- `option` 创建选择，属性：`value` 具体的值，`label` 提示信息，辅助值

注意：

- 需要在 `input` 中加入 `list` 属性，值为 `datalist` 的 id 名

- datalist 在不同浏览器下表现不同，很少使用
- option 可以是单标签，也可以是双标签
- 当 input 的类型为 url 时，option 的 value 必须带 http 前缀

```html
选择：<input type="text" list="selectors">
<datalist id="selectors">
  <option value="HTML" label="结构" />
  <option value="CSS" label="表现"></option>
  <option value="JavaScript" label="行为"></option>
</datalist>
网址：<input type="url" list="urls">
<datalist id="urls">
  <option value="https://www.baidu.com" label="百度" />
  <option value="http://www.sohu.com" label="搜狐"></option>
  <option value="http://www.163.com" label="网易"></option>
</datalist>
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200810190154.png)

```html
<form action="">
  用户名：<input type="text" name="username" ><br>
  密码：<input type="password" name="pwd" ><br>
  加密：<keygen></keygen><br>
  <input type="submit" value="提交">
</form>

<!-- 显示输出信息：只能显示不能修改
1、语义性更强
2、值需要你去设置，不能自动计算
-->
<output>总金额：￥100.00</output>
```

(4) 新增的表单事件

- `oninput`：监听当前指定元素内容的改变，只要**内容改变(添加内容/删除内容)**就会触发这个事件（鼠标粘贴的也能触发）

  - 对比：`onkeyup`：**键盘弹起**的时候触发，每一个键的弹起都会触发一次

- `oninvalid`：当验证不通过时触发

```html
<form action="">
  用户名：<input type="text" name="username" id="username">
  电话：<input type="tel" name="phone" pattern="^1\d{10}$" id="phone">
  <input type="submit" value="提交">
</form>
<script>
  document.getElementById('username').oninput = function(){
    console.log(this.value);
  }
  document.getElementById('phone').oninvalid = function(){
    // 设置默认的提示信息
    this.setCustomValidity('请输入合法的11位手机号')
  }
</script>
```

### 4、进度条

- `progress`
  - max：最大值
  - value：当前进度值
- `meter`度量器——衡量当前进度值 
  - high：规定的较高的值
  - low：规定的较低的值
  - max：最大值
  - min：最小值
  - value：当前度量值

```html
<progress max="100" value="50"></progress>
<meter max="100" min="0" high="80" low="40" value="10"></meter>
<meter max="100" min="0" high="80" low="40" value="50"></meter>
<meter max="100" min="0" high="80" low="40" value="90"></meter>
```

### 5、多媒体标签——音视频

`embed`：直接插入视频文件，本质调用本机上已经安装的软件，有兼容性

`flash` 插件：安装 `flash`，学习 `flash` 增加使用成本，苹果设备不支持 `flash`，后续浏览器将取消对 flash 的支持

新增：

- `audio`：音频
  - `src`: 播放的音频文件的路径
  - `controls`: 音频播放器的控制面板
  - `autoplay`: 自动播放
  - `loop`: 循环

```html
<audio src="../mp3/a.mp3" controls autoplay loop></audio>
```

- `video`：视频
  - `src`: 播放的视频文件的路径
  - `controls`: 视频播放器的控制面板
  - `autoplay`: 自动播放
  - `loop`: 循环
  - `width`: 宽度
  - `height`: 高度 设置宽高时，一般只会设置其一，使其等比缩放，如果同时设置宽度和高度，视频并不会真的调整到该大小，除非设置的刚好是等比例的
  - `poster`: 当视频还没有完全下载，或者用户还没有点击播放前的默认显示的封面，默认显示的是当前视频文件的第一幅画面

```html
<video src="../medeas/1.mp4" width="800" controls poster="../imgs/1.png" autoplay></video>
```

因为不同浏览器支持的音视频文件的格式不一样，因此需要考虑到浏览器是否支持，可以准备多个格式的视频文件，让浏览器自动选择：`source`

```html
<video controls>
  <source src="../medias/1.flv" type="video/flv">
  <source src="../medias/1.mp4" type="video/mp4">
    您的浏览器不支持视频播放，请更换浏览器！
</video>
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200810191655.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200810191742.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200810191754.png)

## 八、H5 中的 DOM 操作

### 1、获取 DOM 元素

query：查询 selector：选择器

- `document.querySelector()` 只能获取单个元素，如果获取的元素不止一个，那么只会返回满足条件的第一个元素

- `document.querySelectorAll()` 获取满足条件的所有元素——元素数组

### 2、操作类样式

`classList` 当前元素的所有样式列表——数组

- `.add` 为元素添加指定类名，一次只能添加一个
- `.remove` 为元素溢出指定名称的类样式，一次只能移除一个
- `.toggle` 切换元素的样式，如果元素之前没有指定名称的样式则添加，如果有则移除
- `.contains` 判断元素是否包含指定名称的样式，返回 true/false

```javascript
document.querySelector(‘li’).classList.add(‘red’)
document.querySelectorAll(‘li’)[1].classList.remove(‘blue’)
document.querySelectorAll(‘li’)[2].classList.toggle(‘green’)
console.log(document.querySelectorAll(‘li’)[2].classList.contains(‘green’))
console.log(document.querySelectorAll(‘li’)[2].classList.item(0))
```

以前：

```javascript
document.querySelector(‘li’).className=‘red underline’
```

### 3、自定义属性

定义：

- `data-` 开头

- `data-` 后必须至少有一个字符，多个单词使用-连接

- 建议小写、无特殊符号、非纯数字

```html
// 定义 data-单词-单词
<p data-test-a='AreYouOK'>test</p>
<script>
window.onload = function(){
  var p = document.querySelector('p')
  // 获取自定义属性值
  var value = p.dataset['testA'] // 将data-后面的单词使用camel命名法连接
  console.log(value);
}
</script>
```

## 九、常用 API

### 1、网络状态改变事件

- ononline：网络连通的时候触发这个事件

- onoffline：网络断开时触发

```javascript
// window.ononline = function () {}
window.addEventListener("online", function(){
  // 操作
  alert('网络连通了~')
})
// window.onoffline = function(){}
window.addEventListener("offline", function(){
  // 操作
  alert('网络断开了~')
})
```

### 2、全屏接口的使用

- requireFullscreen()：开启全屏显示

  - 不同浏览器需要添加不同的前缀：Chrome: webkit fireFox: moz ie: ms opera: o

- cancelFullScreen()：退出全屏显示 只能使用document来实现

- fullscreenElement：是否是全屏状态 只能使用document来实现

```html
<div>
  <img src="" alt="">
  <input type="button" id="full" value="全屏">
  <input type="button" id="cancelFull" value="退出全屏">
  <input type="button" id="isFull" value="是否全屏">
</div>
<script>
window.onload = function(){
  var div = document.querySelector('div')
  document.querySelector('#full').onclick = function(){
    if(div.requestFullscreen){
      div.requestFullscreen()
    }else if(div.webkitRequestFullscreen){
      div.webkitRequestFullscreen()
    }else if(div.mozRequestFullscreen){
      div.mozRequestFullscreen()
    }else if(div.msRequestFullscreen){
      div.msRequestFullscreen()
    }else if(div.oRequestFullscreen){
      div.oRequestFullscreen()
    }
  }
  document.querySelector('#cancelFull').onclick = function(){
    if(document.cancelFullScreen){
      document.cancelFullScreen()
    }else if(document.webkitCancelFullScreen){
      document.webkitCancelFullScreen()
    }else if(document.mozCancelFullScreen){
      document.mozCancelFullScreen()
    }else if(document.msCancelFullScreen){
      document.msCancelFullScreen()
    }else if(document.oCancelFullScreen){
      document.oCancelFullScreen()
    }
  }
  document.querySelector('#isFull').onclick = function(){
    if(document.fullscreenElement || document.webkitFullscreenElement || document.mozFullscreenElement || document.msFullscreenElement){
      alert('true')
    }else{
      alert('false')
    }
  }
}
</script>
```

### 3、文件读取 API

FileReader：读取文件内容

- readAsText()：读取文本文件（可以使用Txt打开的文件），返回文本字符串，默认编码是 UTF-8

- readAsBinaryString()：读取任意类型的文件。返回二进制字符串，这个方法不是用来读取文件展示给用户的，而是存储文件。例如：读取文件的内容，获取二进制数据，传递给后台，后台接收了数据之后，再将数据存储

- readAsDataURL()：没有返回值，参数是文件

读取文件获取一段以 data 开头的字符串，这段字符串的本质就是 DataURL。DataURL 是一种将文件（这个文件一般就是指图像或者能够嵌入到文档的文件格式）嵌入到文档的方案，将资源转换为 base64 编码的字符串形式，并且将这些内容直接存储在 url 中，优化网站的加载速度和执行效率

```html
<!-- 展示图片，src：指定路径(资源定位--url)，src请求得是外部文件，一般是服务器资源，意味着它需要向服务器发送请求，它占用服务器资源 -->
<img src="../imgs/1.jpg" alt="">
```

- abort()：中断读取

FileReader 提供一个完整的事件模型，用来捕获读取文件时的状态

- onabort：读取文件中断时触发

- onerror：读取错误时触发

- onload：文件读取成功完成时触发

- onloadend：读取完成时触发，无论成功还是失败

- onloadstart：开始读取时触发

- onprogress：读取文件过程中持续触发

```html
<!-- 实时预览图片 
及时：onchange()
预览：readAsDataURL()
-->
<form action="">
  文件；<input type="file" name="myFile" id="myFile" onchange="getFileContent();"><br>
  <input type="submit">
</form>
<img src="" alt="">
<script>
  function getFileContent(){
    var reader = new FileReader()
    var file = document.getElementById('myFile').files[0]
    reader.readAsDataURL(file)
    reader.onload = function(){
      // console.log(reader.result);
      document.querySelector('img').src = reader.result
    }
  }
</script>
```

### 4、拖拽接口

为元素添加属性：`draggable=”true”`，图片和超链接默认就能拖拽

拖拽事件：

- (被)拖拽元素
  - ondrag：拖动整个过程都会调用
  - ondragstart：当拖动开始时调用
  - ondragleave：当鼠标离开拖拽元素时调用
  - ondragend：当拖拽结束时调用

- 目标元素
  - ondragenter：当拖拽元素进入时调用
  - ondragover：当停留在目标元素上时调用
  - ondrop：当在目标元素上松开鼠标时调用 浏览器默认会阻止这个事件，我们必须在 ondragover 中阻止浏览器的默认行为
  - ondragleave：当鼠标离开目标元素时调用

```html
<style>
    .box1,.box2{
      width: 200px;
      height: 200px;
      background-color: #ddd;
      border: 1px solid red;
      float: left;
      margin-left: 30px;
    }
    #pe{
      width: 100%;
      background-color: orange;
    }
  </style>
<div class="box1">
  <p id="pe" draggable="true">拖动我啊</p>
</div>
<div class="box2"></div>
<script>
var p = document.querySelector('#pe')
var box2 = document.querySelector('.box2')
var box1 = document.querySelector('.box1')
p.ondragstart = function(){
  console.log('p ondragstart')
  
}
p.ondragend = function(){
  console.log('p ondragend')
}
p.ondragleave = function(){
  // console.log('p ondragleave')
}
p.ondrag = function(){
  // console.log('p ondrag')
}

box2.ondragenter = function(){
  console.log('box2 ondragenter')
}
box2.ondragover = function(e){
  // console.log('box2 ondragover')
  // 阻止浏览器默认行为，使ondrop事件能被触发
  e.preventDefault()
}
box2.ondrop = function(){
  // console.log('box2 ondrop')
  box2.appendChild(p)
}
box2.ondragleave = function(){
  console.log('box2 ondragleave')
}

box1.ondragover = function(e){
  // 阻止浏览器默认行为，使ondrop事件能被触发
  e.preventDefault()
}
box1.ondrop = function(){
  box1.appendChild(p)
}
</script>

<!-- 改进：利用事件捕获 -->
<div class="box1">
  <p id="pe" draggable="true">拖动我啊</p>
  <p id="p2" draggable="true">拖动我啊</p>
</div>
<div class="box2"></div>
<div class="box3"></div>
<div class="box4" draggable="true"></div>
<script>
// var obj = null // 被拖拽元素，全局变量不安全
document.ondragstart = function(e){
  /* 通过事件捕获来获取当前被拖拽的子元素 */
  // console.log(e.target);
  e.target.style.opacity = 0.5
  e.target.parentNode.style.borderWidth = '5px'
  // obj = e.target
  /*
    通过dataTransfer来实现数据的存储与获取
  * setData(format, data)
  ** 数据类型:text/html  text/uri-list
  ** 数据:一般来说是字符串值
  */
  e.dataTransfer.setData('text/html', e.target.id)
}
document.ondragend = function(e){
  e.target.style.opacity = 1
  e.target.parentNode.style.borderWidth = '1px'
}
document.ondragleave = function(e){
}
document.ondrag = function(e){
}

document.ondragenter = function(e){
  console.log(e.target);
  
}
document.ondragover = function(e){
  // 阻止浏览器默认行为，使ondrop事件能被触发
  e.preventDefault()
}
document.ondrop = function(e){
  // e.target.appendChild(obj)
  /*
   通过e.dataTransfer.setData存储的数据，只能在drop事件中获取

  */
  var id = e.dataTransfer.getData('text/html')
  console.log(id);
  e.target.appendChild(document.getElementById(id))
}
document.ondragleave = function(e){
}
</script>
```

### 5、地理定位 API

![](https://cdn.wallleap.cn/img/pic/illustration/20200810193306.png)

示例：

```html
<div class="map"></div>
<script>
var map = document.querySelector('.map')
function getLocation(){
  if(navigator.geolocation){
    navigator.geolocation.getCurrentPosition(showPosition, showError, {})
  }else{
    map.innerHTML = "Geolocation is not supported by this browser"
  }
}
function showPosition(position){
  map.innerHTML = 'Latitude:' + position.coords.latitude + "<br />Logitude:" + position.coords.longitude
}
function showError(error){
  ……
}
getLocation()
</script>
```

可以直接使用第三方地图 API，例如百度地图 API：<http://lbsyun.baidu.com/jsdemo.htm#a1_2>

### 6、通信 API

Web Sockets 是 H5 提供的在 Web 应用程序中客户端与服务器端之间进行的非 HTTP 的通信机制。

- 建立与服务器之间的通信连接

```javascript
var webSocket = new WebSocket("ws://localhost:9000/socket")
```

调用的是 WebSocket 对应，参数 url 必须以 `ws` 或 `wss` 开头

- 发送数据

```javascript
webSocket.send("data")
```

- 监听

```javascript
// 通过获取onmessage事件句柄来接收服务器传过来的数据
webSocket.onmessage = function(event){
  var data = event.data
  ...
}
// 通过获取onopen事件句柄来监听socket的打开事件
webSocket.onopen = function(event){
  // 开始通信时的处理
}
// 通过获取onclose事件句柄来监听socket的关闭事件
webSocket.onclose = function(event){
  // 通信结束时的处理
}
```

- 关闭 socket

```javascript
webSocket.close()
```

可以通过读取 `readyState` 的属性值来获取 WebSocket 对象的状态，主要有：

- CONNECTING（0），表示正在连接
- OPEN（1），表示已建立连接
- CLOSING（2），表示正在关闭连接
- CLOSED（2），表示已关闭连接

## 十、web 存储

### 1、sessionStorage 的使用

可以存储数据到本地，存储的容量 5MB 左右（每个浏览器不同）。这个数据本质是存储在当前页面的内存中；它的生命周期为关闭当前页面，关闭页面，数据会自动清除；

- `setItem(key, value)`：存储数据，以键值对方式存储

- `getItem(key)`：获取数据，通过指定名称的 key 获取对应的 value 值，如果找不到对应名称的 key，那么就会获取 null

- `removeItem(key)`：删除数据，通过指定名称 key 删除对应的值，如果 key 值错误，不会报错，也不会删除数据

- `clear()`：清空所有存储的内容

```html
<input type="text" id="username"><br>
<input type="button" value="设置数据" id="setData">
<input type="button" value="获取数据" id="getData">
<input type="button" value="删除数据" id="removeData">
<script type="text/javascript">
  document.querySelector('#setData').onclick = function(){
    var name = document.querySelector('#username').value
    // 存储数据
    window.sessionStorage.setItem("username", name)
  }
  document.querySelector('#getData').onclick = function(){
    // 获取数据
    var name = window.sessionStorage.getItem('username')
    alert(name)
  }
  document.querySelector('#removeData').onclick = function(){
    // 删除数据
    window.sessionStorage.removeItem('username')
  }
</script>
```

调试器查看

![](https://cdn.wallleap.cn/img/pic/illustration/20200810193555.png)

### 2、localStorage 的使用

存储的内容大概 20MB；不同浏览器不能共享数据，但是在同一浏览器的不同窗口中可以共享数据；永久生效，它的数据是存储在硬盘上，并不会随着页面或者浏览器的关闭而清除

- `setItem(key, value)`: 存储数据，以键值对方式存储

- `getItem(key)`: 获取数据，通过指定名称的 key 获取对应的 value 值，如果找不到对应名称的 key，那么就会获取 null

- `removeItem(key)`: 删除数据，通过指定名称 key 删除对应的值，如果 key 值错误，不会报错，也不会删除数据

- `clear()`: 清空所有存储的内容

```html
<input type="text" id="username"><br>
<input type="button" value="设置数据" id="setData">
<input type="button" value="获取数据" id="getData">
<input type="button" value="删除数据" id="removeData">
<script type="text/javascript">
  document.querySelector('#setData').onclick = function(){
    var name = document.querySelector('#username').value
    // 存储数据
    window.localStorage.setItem("username", name)
  }
  document.querySelector('#getData').onclick = function(){
    // 获取数据
    var name = window.localStorage.getItem('username')
    alert(name)
  }
  document.querySelector('#removeData').onclick = function(){
    // 删除数据
    window.localStorage.removeItem('username')
  }
</script>
```

## 十一、应用程序缓存

概念：使用 HTML5，通过创建 cache manifest 文件，可以轻松地创建 web 应用的离线版本

优势：

- 可配置需要缓存的资源

- 网络无连接应用仍可用

- 本地读取缓存资源，提升访问速度，增强用户体验

- 减少请求，缓解服务器负担

Cache Manifest 基础：

- 如需启用应用程序缓存，要在文档的 html 标签中包含 manifest 属性：

```html
<!DOCTYPE html>
<html  manifest="demo.appcache">
  ……
</html>
```

`manifest=”应用程序缓存清单文件的路径”`

- 每个指定了 manifest 的页面在用户对其访问时都会被缓存，如果未指定 manifest 属性，则页面不会被缓存(除非在 manifest 文件中直接指定了该页面)

- Manifest 文件的建议个文件扩展名为 `appcache`，这个文件的本质是一个文本文件

- 注意：manifest 文件需要配置正确的 `MIME-type`，即 `”text/cache-manifest”`，必须在 web 服务器上进行配置

`demo.appcache`：

```appcache
CACHE MANIFEST
# 注释 上面必须是当前文件的第一句

# 需要缓存的文件清单列表
CACHE:
./imgs/1.jpg
./imgs/2.jpg

# 配置每一次都需要重新从服务器获取的文件清单列表
NETWORK:
./imgs/3.jpg

# 配置如果文件无法获取则使用指定的文件进行替代
FALLBACK:
./imgs/4.jpg ./imgs/loader.gif

# /代表所有文件
```

最后，列出一下已弃用的标签

![](https://cdn.wallleap.cn/img/pic/illustration/20200810171347.png)

H5 中还有两个知识点需要单独学习的：

[Web Worker 使用教程](http://www.ruanyifeng.com/blog/2018/07/web-worker.html)

[学习 HTML5 Canvas 这一篇文章就够了](https://blog.csdn.net/u012468376/article/details/73350998)

扩展文章

[HTML 元素参考](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element)

[html中link的用法](https://www.cnblogs.com/chenkg/p/5003426.html)

[html5新标签总结](https://juejin.im/post/6844903808854654984)

[HTML5 新元素](https://www.w3school.com.cn/html/html5_new_elements.asp)
