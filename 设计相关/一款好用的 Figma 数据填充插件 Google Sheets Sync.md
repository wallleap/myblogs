---
title: 一款好用的 Figma 数据填充插件 Google Sheets Sync
date: 2022-01-06 17:16
updated: 2022-01-06 17:16
cover: //cdn.wallleap.cn/img/post/cover2.jpg
category: 设计相关
tags:
  - 设计
  - UI
description: 一款好用的 Figma 数据填充插件 Google Sheets Sync
---

本文是关于一个 Figma 数据填充插件使用教程

## 一、前言

最近使用 [Figma](https://www.figma.com/)，发现它是真的好用啊。UI 组件化，修改主组件可以统一修改衍生的组件，变体组件（组件集）的使用能很方便切换样式…… [Figma 社区](https://www.figma.com/community/explore)提供了很多插件、使用教程、案例等。这次分享的是插件 [Google Sheets Sync](https://www.figma.com/community/plugin/735770583268406934/Google-Sheets-Sync)，插件的[官方文档](https://docs.sheetssync.app/)在这，条理挺清晰的。

> What can this plugin do?
> - Change the content in your Text layers
> - Download and set image backgrounds from URLs
> - Swap out Components for specific instances (including Variants)
> - Change colours of your layers
> - Plus lots more...

这个插件可以：填充文本、图片(通过图片链接下载填充)、属性值、颜色等，可以让某图层显示或者隐藏，甚至直接填充组件/组件集

~~唯一的缺点是需要科学上网~~

这个缺点已经解决了，现在支持本地导入表格

## 二、基本使用

### 1、谷歌表格写入数据

科学上网之后注册/登录谷歌账号，进入[表格创建页](https://docs.google.com/spreadsheets/u/0/)，点击添加空白表格

![创建表格](https://cdn.wallleap.cn/img/pic/illustration/202305280031934.png)

接下来可以直接复制别人的数据，我是复制的UP主[草帽sMao](https://space.bilibili.com/108104104)[这个视频](https://www.bilibili.com/video/BV1Qt4y1e7J1)简介里的：

> <https://docs.google.com/spreadsheets/d/1t23BAon8spOILyH49A_htAPDAJ03Hfw5ZUgiqHdOkU0/edit?usp=sharing>

或者使用[后羿采集器](https://www.houyicaiji.com/)进行数据的采集

表格主要格式是：

第一行为标题，下面的是数据，每列不要有空格

![红框内的是标题](https://cdn.wallleap.cn/img/pic/illustration/202305280031935.png)

### 2、获取谷歌表格分享链接

点击右上角的共享

![共享](https://cdn.wallleap.cn/img/pic/illustration/202305280031936.png)

链接默认是受限的，我们需要点击更改权限

![更改权限](https://cdn.wallleap.cn/img/pic/illustration/202305280031937.png)

之后点击复制链接即可

![复制链接](https://cdn.wallleap.cn/img/pic/illustration/202305280031938.png)

### 3、安装Google Sheets Sync插件

点击链接[https://www.figma.com/community/plugin/735770583268406934/Google-Sheets-Sync](https://www.figma.com/community/plugin/735770583268406934/Google-Sheets-Sync)，点击安装

![点击安装](https://cdn.wallleap.cn/img/pic/illustration/202305280031939.png)

如下显示安装成功，再次点击可以卸载

![安装成功](https://cdn.wallleap.cn/img/pic/illustration/202305280031940.png)

### 4、使用 Google Sheets Sync 插件

我们先使用最简单的**文本填充**功能和**图片填充**

新建设计文件，按照下方格式绘制，并且创建组件

![创建组件](https://cdn.wallleap.cn/img/pic/illustration/202305280031941.png)

这里需要填充的图层重命名为`#标题栏中一项名字`（这样的是按顺序的）、`#标题.x`（这样是随机的）

![标题](https://cdn.wallleap.cn/img/pic/illustration/202305280031942.png)

按 Alt +鼠标拖动复制出一个，接着按快捷键 `Ctrl+D` 复制其他的

可以选中需要填充的，右击-plugins-Google Sheets Sync

![调用插件](https://cdn.wallleap.cn/img/pic/illustration/202305280031943.png)

将刚刚获取到的链接粘贴到第一个文本框，下面可以选择

- 当前选中的

- 当前页面

- 整个设计文件

我们选择选中的就行

![选项](https://cdn.wallleap.cn/img/pic/illustration/202305280031944.png)

之后点击 Fetch & Sync 即可

![获取同步](https://cdn.wallleap.cn/img/pic/illustration/202305280031945.png)

稍等一会之后就能填充好数据了

![数据填充成功](https://cdn.wallleap.cn/img/pic/illustration/202305280031946.png)

以后更新可以直接点击右边的 Re-sync……了

![更新](https://cdn.wallleap.cn/img/pic/illustration/202305280031947.png)

基本使用就是这样：

1. 获取表格分享链接，注意权限问题

2. 命名图层，以 `#` 号开头(还有进阶操作)

3. 运行插件，输入分享链接获取并同步

4. 修改数据或者图层名字之后可以直接再次同步

## 三、进阶操作

### 1、组件、组件集填充

首先准备一些组件

![组件和组件集](https://cdn.wallleap.cn/img/pic/illustration/202305280031948.png)

Alt +拖动任一组件进行复制

![生成组件](https://cdn.wallleap.cn/img/pic/illustration/202305280031949.png)

修改表格数据，组件填入组件名，组件集则填入响应的文本

![重命名画框](https://cdn.wallleap.cn/img/pic/illustration/202305280031950.png)

选中这些组件/组件集，Ctrl+R 重命名为 `#Component`

![批量重命名](https://cdn.wallleap.cn/img/pic/illustration/202305280031951.png)

重新同步一下表格数据

![重新同步](https://cdn.wallleap.cn/img/pic/illustration/202305280031952.png)

同步完成（仅作展示）

![同步完成](https://cdn.wallleap.cn/img/pic/illustration/202305280031953.png)

### 2、属性样式填充

使用方式是`#属性值`，如果前面有了填充的名字的话，使用空格分割`#文本 空格 #属性值` ，eg：`#mail.x #color`

> 注意：
>
> 如果您的图层是 `Text Layer`（文字）或 `Component Instance layer`（里面包含文字），那么您需要在 Google Sheets 中的 Value 前面加上`/`以便插件知道您指定的是特殊数据类型（而不是内容或组件名称）—— 对于所有其他图层类型，您无需执行此操作。

#### （1）图层显示

表格中数据值为 `show` 或者 `hide`，如果是文本的话，值为 `/show` 或 `hide`

示例：

表格中添加一列 `display` 或 `show`，值随机填充为 `/show` 或 `/hide`

![添加列](https://cdn.wallleap.cn/img/pic/illustration/202305280031954.png)

在之前的界面中添加一个圆与文字，表示在线状态，并且修改这个 Frame 名字为 `#show.x`

![显示](https://cdn.wallleap.cn/img/pic/illustration/202305280031955.png)

同步一下表格，可以看到有些有显示，部分没有显示

![同步后](https://cdn.wallleap.cn/img/pic/illustration/202305280031956.png)

#### （2）填充颜色

可以改变图层的颜色，表格中值只能是以 `#` 开头的16进制的Hex颜色值，如果图层为文字，需要加上 `/`

![填充颜色](https://cdn.wallleap.cn/img/pic/illustration/202305280031957.png)

像上图这种文字颜色和头像框颜色修改的，都是可以实现的（头像边框最方便的实现方式是加描边，但是这个插件只能是填充颜色）

在表格中添加 `gender_color` 列，数据使用公式 `If(gender_cn列中的相同行格="男", "/#2aa1f7", "/#f4bfcf")`，当 `gender_cn` 列中的值为男时，填充蓝色，否则填充粉色（值使用 `/` 是因为需要填充的有文字）

![添加颜色列](https://cdn.wallleap.cn/img/pic/illustration/202305280031958.png)

在头像下面新建一个圆形，命名为 `#gender_color`，性别后的文字图层重命名为 `#gender_cn #gender_color`（但是由于头像、名字用了随机值的方式，性别和头像、名字会匹配不上）

![重命名](https://cdn.wallleap.cn/img/pic/illustration/202305280031959.png)

这样就 OK 了

#### （3）图层不透明度

如果值以 `%` 结尾，则获取到时会修改图层不透明度

现在我们修改头像后面那个圆图层的不透明度，在 `1%` - `99%` 之间取随机值

在表格中添加一列 `opacity`，使用公式 `=RANDBETWEEN(1,99)%` 填充

![不透明度](https://cdn.wallleap.cn/img/pic/illustration/202305280031960.png)

注意需要修改格式-数字-百分比

![数字格式](https://cdn.wallleap.cn/img/pic/illustration/202305280031961.png)

接着在更多样式里把小数点后两位去除

在图层名后加上 `opacity.x`

![图层名](https://cdn.wallleap.cn/img/pic/illustration/202305280031964.png)

更新一下即可

#### （4）尺寸大小

值的格式为`数字+以下三个字母之一`

- `s`：设定图层的宽高为前面的数字

- 比如 `32s` 是同时设置宽高为 32px

- `w`：设定图层的宽度为数字

- `43w` 代表将图层的宽设置为 43px

- `h`：设定图层的高度为数字

- `54h`表示将图层的搞设置为 54px

在表格中填入数据

- 数字的公式：`RANDBETWEEN(111,999)`，随机生成三位数字

- 后面的三列分别填充 `s`、`w`、`h`

- 三列需要使用的分别命名为 `size_s`、`size_w`、`size_h`，公式是`=数字列&字母列`

![表格数据](https://cdn.wallleap.cn/img/pic/illustration/202305280031965.png)

Figma中绘制如下形状，红蓝矩形大小大于 1000px，蓝色中的小画框名字为 `#size_s.x`，红色中的小画框命名为 `#size_w.x #size_h.x`

![矩形](https://cdn.wallleap.cn/img/pic/illustration/202305280031966.png)

同步一下

![大小随机](https://cdn.wallleap.cn/img/pic/illustration/202305280031967.png)

#### （5）位置

- 相对位置

- `数字x`：该图层相对于父元素向右偏移数字 px

- `数字y`：该图层相对于父元素向下偏移数字 px

- 绝对位置

- `数字xx`：该图层在页面中 x 轴的位置为数字 px

- `数字yy`：该图层在页面中 y 轴的位置为数字 px

和上面方式相同，拼接出位置的数据

![位置](https://cdn.wallleap.cn/img/pic/illustration/202305280031968.png)

画框中，将红蓝色中的小矩形固定一下长宽，并且放置到红蓝画框的左上角，命名如下

![命名](https://cdn.wallleap.cn/img/pic/illustration/202305280031969.png)

我们先在插件中 Fetch 一下数据，可以看到都是 312

![Fetch](https://cdn.wallleap.cn/img/pic/illustration/202305280031970.png)

接着同步一下，使用矩形量一下

![同步](https://cdn.wallleap.cn/img/pic/illustration/202305280031971.png)

可以发现，蓝色下的是相对于页面原点的偏移，不是相对于父元素蓝色画框；而红色下的矩形是相对于父元素红色画框原点的偏移

#### （8）角度

表格中的值以 `°` 结尾的话，会以该数值进行图层旋转

#### （7）文本相关

- 字体大小

  - `font-size:数值`，例如 `font-size:12`

- 文本对齐

  - 水平

    - `text-align:left`

    - `text-align:right`

    - `text-align:center`

    - `text-align:justified`

  - 垂直

    - `text-align-vertical:top`

    - `text-align-vertical:center`

    - `text-align-vertical:bottom`

- 行高

  - auto：`line-height:auto`

  - 数值：`line-height:30`

  - 百分比：`line-height:150%`

- 间距

  - 数值：`letter-spacing:12`

  - 百分比：`letter-spacing:200%`

### 3、调用表格中其他工作表

所有能包裹的（page、Frame、Group）的图层名加上`空格//空格工作表名`，eg：`Page1 // Data2`

![工作表](https://cdn.wallleap.cn/img/pic/illustration/202305280031972.png)
