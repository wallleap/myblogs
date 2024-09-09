---
title: mac 使用 Hexo 和 GitHub 搭建博客之发布文章
date: 2019-08-25 08:46
updated: 2019-08-25 08:46
cover: //cdn.wallleap.cn/img/pic/cover/202302tJDFmU.jpg
category: 技术杂谈
tags:
  - 博客
  - Hexo
description: mac 使用 Hexo 和 GitHub 搭建博客之发布文章
---

修改文章模板并编写好文章，调试之后进行提交

## 0.准备工作

### 修改文章模板

上一个文章有提到过修改 `scaffolds/post.md` 达到修改博文模板的作用

```sh
--- 
title: {{ title }}   #文章标题，可以和文件名不同
date: {{ date }}  #发布时间
categories:      #分类
    - category
    - subcategory
tags:                #标签
    - tag1
    - tag2
---
```

### ~~文中图片放置~~放弃这用方法

前面博客中还提到过插入图片的，这里总结一下

- 下面这个要填写你使用 github.io 访问博客的地址

```sh
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://wallleap.github.io
```

- 这个需要改成true

```sh
post_asset_folder: true
```

- ~~安装插件~~

```sh
npm install hexo-assert-folder --save
```

但是这个插件的内容需要修改【不然可能会出Bug】

打开 `/node_modules/hexo-asset-image/index.js`，将内容更换为下面的代码  

```sh
'use strict';
var cheerio = require('cheerio');

// http://stackoverflow.com/questions/14480345/how-to-get-the-nth-occurrence-in-a-string
function getPosition(str, m, i) {
return str.split(m, i).join(m).length;
}

var version = String(hexo.version).split('.');
hexo.extend.filter.register('after_post_render', function(data){
var config = hexo.config;
if(config.post_asset_folder){
var link = data.permalink;
if(version.length > 0 && Number(version[0]) == 3)
var beginPos = getPosition(link, '/', 1) + 1;
else
var beginPos = getPosition(link, '/', 3) + 1;
// In hexo 3.1.1, the permalink of "about" page is like ".../about/index.html".
var endPos = link.lastIndexOf('/') + 1;
link = link.substring(beginPos, endPos);

var toprocess = ['excerpt', 'more', 'content'];
for(var i = 0; i < toprocess.length; i++){
var key = toprocess[i];

var $ = cheerio.load(data[key], {
ignoreWhitespace: false,
xmlMode: false,
lowerCaseTags: false,
decodeEntities: false
});

$('img').each(function(){
if ($(this).attr('src')){
// For windows style path, we replace '\' to '/'.
var src = $(this).attr('src').replace('\\', '/');
if(!/http[s]*.*|\/\/.*/.test(src) &&
!/^\s*\//.test(src)) {
// For "about" page, the first part of "src" can't be removed.
// In addition, to support multi-level local directory.
var linkArray = link.split('/').filter(function(elem){
return elem != '';
});
var srcArray = src.split('/').filter(function(elem){
return elem != '' && elem != '.';
});
if(srcArray.length > 1)
srcArray.shift();
src = srcArray.join('/');
$(this).attr('src', config.root + link + src);
console.info&&console.info("update link as:-->"+config.root + link + src);
}
}else{
console.info&&console.info("no src attr, skipped...");
console.info&&console.info($(this));
}
});
data[key] = $.html();
}
}
});
```

当然啦，这是以前不成熟的用法，这样做图片全都放到博客的站点目录了，会使访问速度更慢

### 文中图片之搭建自己的图床

这里我们使用的是 GitHub 仓库 + jsDelivr 的 cdn 加速服务

主要就是 GitHub 仓库放置你的 js、img、css 等文件，然后通过 jsDelivr 的域名进行访问

就比如你新建了一个 cdn 仓库(可以不以这个命名)

接着把这个仓库克隆 `git clone git@github.com:用户名/cdn.git` 下来，创建三个目录，分别是

- js
- img
- css

分别放置的是 js 文件、图片、css 文件，每次放置好文件后

使用命令上传

```sh
git add . && git commit -m "update" && git push -f
```

接着使用链接引用即可

```sh
// load any GitHub release, commit, or branch

// note: we recommend using npm for projects that support it

https://cdn.jsdelivr.net/gh/user/repo@version/file


// load jQuery v3.2.1

https://cdn.jsdelivr.net/gh/jquery/jquery@3.2.1/dist/jquery.min.js


// use a version range instead of a specific version

https://cdn.jsdelivr.net/gh/jquery/jquery@3.2/dist/jquery.min.js

https://cdn.jsdelivr.net/gh/jquery/jquery@3/dist/jquery.min.js


// omit the version completely to get the latest one

// you should NOT use this in production

https://cdn.jsdelivr.net/gh/jquery/jquery/dist/jquery.min.js


// add ".min" to any JS/CSS file to get a minified version

// if one doesn't exist, we'll generate it for you

https://cdn.jsdelivr.net/gh/jquery/jquery@3.2.1/src/core.min.js


// add / at the end to get a directory listing

https://cdn.jsdelivr.net/gh/jquery/jquery/
```

就比如我们要引用 cdn 仓库下 img 目录下的 picture.png

我们就可以使用链接 `https://cdn.jsdelivr.net/gh/用户名/cdn@latest/img/picture.png`

## 1.新建文章 md 文件

在终端输入 `hexo new "文章英文名"`

*比如* `hexo new "first-blog"`，将会在 `source/_posts` 下生成一个 `文章名.md` 文件，如 `first-blog.md`，同时生成一个同名文件夹 `first-blog` ，~~写文章的时候可以将图片放到该文件夹中~~。

## 2.修改文章内容

手动进入目录 `source/_posts`，打开刚刚新建的 md 文件，这里可以选择使用不同的编辑器，或者在一些网站上（比如 CSDN）写好了再复制进来。

打开文件，你可以看到 *例* 

```sh
--- 
title: first-blog
date: 2019-08-29
categories: 
    - 
    - 
tags:
    - 
    - 
---
```

现在需要修改内容了

````sh
---
title: 我的第一篇博文      #文章标题
date:2019-08-29           
categories:         #如果开启了多级分类，则可以按下面这样写，分类显示二级分类，文章在博客下的心得分类中
    - 博客         #-前面tab，后面一个空格
    - 心得
tags:                  #可以这样写，会显示blog,博客,心得三个标签     
    - blog
    - 博客
    - 心得
---

下面写文章内容，markdown 语法，自己搜一下。比如  

## 二级标题

注意空格和回车

> 引用或强调

```C++
std::cout << "hello" << endl;
```
````

## 3.发布文章

`hexo clean`、`hexo g`
`hexo s`，打开网页测试，没错误就可以输入下面的命令了
`hexo d`
