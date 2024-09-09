---
title: 使用 Markdown Here 对微信公众号文章进行排版
date: 2020-03-27 22:36
updated: 2020-03-27 22:36
cover: //cdn.wallleap.cn/img/pic/cover/202302FRH4Wo.jpg
category: 技术杂谈
tags:
  - Markdown
  - 微信
description: 使用 Markdown Here 对微信公众号文章进行排版
---

今天讲下微信公众号图文排版

## 0、图文基本排版

具体的大家可以自己去搜索一下，我在这推荐一个知乎里的问题，回答挺多的：

如何排版微信公众平台的文章？<https://www.zhihu.com/question/23640203>

下面的是截取自这些回答里的一些

![](https://cdn.wallleap.cn/img/pic/test/wechat.png)

![](https://cdn.wallleap.cn/img/pic/test/WeChat2.png)

![](https://cdn.wallleap.cn/img/pic/test/WeChat3.png)

---

当然啦，今天主要不是要讲这个

而是要讲【如何利用 Markdown Here 来进行图文排版】

## 1、安装 Markdown Here 插件

首先我们前往 Markdown Here 官网：

<https://markdown-here.com/>

两个链接随意点一个

![](https://cdn.wallleap.cn/img/pic/test/WeChat4.png)

支持这些浏览器

![](https://cdn.wallleap.cn/img/pic/test/WeChat5.png)

可以直接点击上面五个中对应浏览器前往应用商店下载，也可以点击最后一个去 GitHub 下载

![](https://cdn.wallleap.cn/img/pic/test/WeChat7.png)

我使用的是 Chrome，因此点击下方这个压缩包下载

![](https://cdn.wallleap.cn/img/pic/test/WeChat8.png)

下载完成之后，解压该压缩包，注意选择解压到 Chrome 或者自己新建一个文件夹，把解压出来的三个文件夹和一个 JSON 文件剪切进去

接着打开 Chrome，进入扩展程序页面，开启开发者模式，加载已解压的压缩程序

![](https://cdn.wallleap.cn/img/pic/test/WeChat9.png)

但是还是推荐到谷歌商店下载

若你想访问谷歌，可以使用这个插件

<https://github.com/haotian-wang/google-access-helper>

## 2、修改 CSS 渲染

在标签栏的下方找到 Markdown Here 的图标

右击它，点击选项

![](https://cdn.wallleap.cn/img/pic/test/WeChat10.png)

之后你会来到这个页面

![](https://cdn.wallleap.cn/img/pic/test/WeChat11.png)

我们暂时需要修改的只有基本渲染 CSS

而且修改的也不是所有的内容

### 修改所有的字体

```css
/* This is the overall wrapper, it should be treated as the `body` section. */
.markdown-here-wrapper {
  font-size: 14px;
  color: #595959;
  padding: 16px;
}
```

注释中说这个相当于 body，而我们的内容基本上都放在这里面，因此可以修改大部分统一的样式

这里将字体修改为 14 像素

字体颜色设置为 `#595959`，也就是稍微灰一点

向内缩进 16 像素

### 预格式文本及代码

```css
pre, code {
  font-size: 0.85em;
  font-family: Consolas, Inconsolata, Courier, monospace;
  color:#fff;
}

code {
  margin: 0 0.15em;
  padding: 0 0.3em;
  white-space: pre-wrap;
  border: 1px solid #EAEAEA;
  background-color: black;
  border-radius: 3px;
  display: inline; /* added to fix Yahoo block display of inline code */
}

pre {
  font-size: 1em;
  line-height: 1.2em;
}

pre code {
  white-space: pre;
  overflow: auto; /* fixes issue #70: Firefox/Thunderbird: Code blocks with horizontal scroll would have bad background colour */
  border-radius: 3px;
  border: 1px solid #CCC;
  padding: 0.5em 0.7em;
  display: block !important; /* added to counteract the Yahoo-specific `code` rule; without this, code blocks in Blogger are broken */
}

/* In edit mode, Wordpress uses a `* { font: ...;} rule+style that makes highlighted
code look non-monospace. This rule will override it. */
.markdown-here-wrapper[data-md-url*="wordpress."] code span {
  font: inherit;
}

/* Wordpress adds a grey background to `pre` elements that doesn't go well with
our syntax highlighting. */
.markdown-here-wrapper[data-md-url*="wordpress."] pre {
  background-color: transparent;
}
```

### 段落

```css
/* This spacing has been tweaked to closely match Gmail+Chrome "paragraph" (two line breaks) spacing.
Note that we only use a top margin and not a bottom margin -- this prevents the
"blank line" look at the top of the email (issue #243).
*/
p {
  /* !important is needed here because Hotmail/Outlook.com uses !important to
     kill the margin in <p>. We need this to win. */
  margin: 0 0 1.2em 0 !important;
}
```

每个段落在下方加外边距 1.2 个文字大小，即 `1.2*14px`

### 表格、引用、列表等

```css
table, pre, dl, blockquote, q, ul, ol {
  margin: 1.2em 0;
}

ul, ol {
  padding-left: 2em;
}

li {
  margin: 0.5em 0;
}

/* Space paragraphs in a list the same as the list itself. */
li p {
  /* Needs !important to override rule above. */
  margin: 0.5em 0 !important;
}

/* Smaller spacing for sub-lists */
ul ul, ul ol, ol ul, ol ol {
  margin: 0;
  padding-left: 1em;
}

/* Use Roman numerals for sub-ordered-lists. (Like Github.) */
ol ol, ul ol {
  list-style-type: lower-roman;
}

/* Use letters for sub-sub-ordered lists. (Like Github.) */
ul ul ol, ul ol ol, ol ul ol, ol ol ol {
  list-style-type: lower-alpha;
}

dl {
  padding: 0;
}

dl dt {
  font-size: 1em;
  font-weight: bold;
  font-style: italic;
}

dl dd {
  margin: 0 0 1em;
  padding: 0 1em;
}

blockquote, q {
  border-left: 4px solid #42b983;
  border-right: 4px solid #42b983;
  padding: 0 1em;
  background-color: #ecf8f2;
  color: #888;
  quotes: none;
}

/*
blockquote::before, q::before {
  content: none;
}

blockquote::after,  q::after{
  position: relative;
    content: '\f10e' !important;
    font-size: 1rem;
    float: right;
    top: -1rem;
    margin-right: -10px;
    color: red;
    font-family: FontAwesome;
}  // emmmm，本来想加引号的，但是不支持
*/


table {
  padding: 0;
  border-collapse: collapse;
  border-spacing: 0;
  font-size: 1em;
  font: inherit;
  border: 0;
}

tbody {
  margin: 0;
  padding: 0;
  border: 0;
}

table tr {
  border: 0;
  border-top: 1px solid #CCC;
  background-color: white;
  margin: 0;
  padding: 0;
}

table tr:nth-child(2n) {
  background-color: #F8F8F8;
}

table tr th, table tr td {
  font-size: 1em;
  border: 1px solid #CCC;
  margin: 0;
  padding: 0.5em 1em;
}

table tr th {
 font-weight: bold;
  color: white;
  background-color: #009688;
}
```

### 标题

```css
h1, h2, h3, h4, h5, h6 {
  text-align: center;
  padding: 0;
  font-weight: bold;
  color: #000;
  margin-bottom: 50px;
}

h1 {
  margin:0 auto;
  width: 500px;
  line-height:36px;
  font-size: 18px;
  border: 2px solid #57d9ff;
  background-color: #CCFFFF;
  border-radius: 8px; 
}

h2 {
  font-size: 16px;
  border-bottom: 5px solid #a9d3d6;
}

h3 {
  width: 30%;
  position: relative;  
  left:33%;  
  font-size: 15px;
  border-bottom: 2px solid #FFFF66;
  box-shadow: 10px 10px 5px #888888;
}

h4 {
  font-size: 1.2em;
  display: inline-block;
  color: #333333;
}

h5 {
  font-size: 1em;
}

h6 {
  font-size: 14px;
  color: #FFCC99;
  margin-bottom: 10px;
}
```

一级标题应该不会在文中用到，主要是二级标题和三级标题

三级标题可以稍微改宽一点

六级标题我用来写最低下的"历史文章"四个字了

### 链接

```css
/*
a {
  color: #7cc7ff; 
}
a:hover{
  color: orange;
}
*/
a{
  display: block;
  margin: 0 auto;
  text-align: center;
  font-size: 14px;
  color: #fff;
  width: 300px;
  line-height: 20px;
  background-color: #FFCCCC;
  box-shadow: 1px 1px 5px #888888;
  border-radius: 10px;
}
a:hover {
  color: red;
} 
```

由于微信不让插入其他的链接，只能插已经发布的图文，因此直接改成了历史文章链接样式了

### 图片

```css
img {
  display: block;
  margin: 0 auto;
  height:auto;
  max-width:100%;
  border-radius:5px;
  padding:2px;
  border:2px solid #f3f3f3;
  box-shadow: 0px 0px 10px #888888;
}
```

### 其他

```css
/* 这个是分隔符 */
hr {
  width:30%;
  height:1px;
  border:2px;
  background:#efefef;
  margin:20px auto;
}
/* 这是强调的 */
strong {
  font-weight: bold;
  color: #990033;
}
```

如果你想把其他的也给设置好自己的样式，可以把所有的标签都写一遍，然后F12查看标签，接着给该标签设置样式就行啦

## 3、使用演示

### 标题

一级标题，比如说你想把文章的标题再写一遍

```markdown
# 使用Markdown Here给微信公众号图文排版
```

# ![](https://cdn.wallleap.cn/img/pic/test/image-20200327223934241.png)

二级标题，用于设置文章下的大标题

```markdown
## 我是二级标题
```

![](https://cdn.wallleap.cn/img/pic/test/image-20200327224005387.png)

三级标题，大标题下的子标题

```markdown
### 我是三级标题
```

![](https://cdn.wallleap.cn/img/pic/test/image-20200327224028548.png)

如果觉得两层标题不够还可以把四级标题设置好样式

### 表格

```markdown
| 表头1 | 表头二  | 表头三 |
| ----- | :--: | -----: |
| AAA   | 111  |  一一一 |
| BBB   | 222  |  二二二 |
| CCC   | 333  |  三三三 |
```

![](https://cdn.wallleap.cn/img/pic/test/image-20200327224056078.png)

### 引用

```markdown
> 用大于号
> 这是引用的内容
```

![](https://cdn.wallleap.cn/img/pic/test/image-20200327224130129.png)

### 列表

```markdown
- 无序列表
- 无序列表   可以使用- + *

1.有序列表
2.有序列表
```

- 无序列表
- 无序列表

1.有序列表
2.有序列表

### 图片

```markdown
![](图片链接)
```

### 分隔符

```markdown
---
+++
***
```

---

只写了一个

### 强调

```markdown
**这是强调的内容**
```

你知道吗**这是强调的内容**，哈哈

### 代码

````markdown
`单行代码`

​```代码语言
代码块
```
````

### 历史文章

​`###### 历史文章`

`[](文章链接)`

![](https://cdn.wallleap.cn/img/pic/test/WeChat12.png)
