---
title: PS 学习案例之草莓小屋
date: 2021-03-10 14:16
updated: 2021-03-10 14:16
cover: //cdn.wallleap.cn/img/pic/cover/2023023IfpRe.jpg
category: 设计相关
tags:
  - 设计
  - PS
description: PS 学习案例之草莓小屋
---

利用 PS 制作一个简单的合成效果

## 一、前言

利用 PS 中各种基本工具制作一个草莓小屋效果

## 二、抠图

先将窗口排列设为双联垂直，方便观察操作

![更改排列](https://cdn.wallleap.cn/img/pic/illustration/image-20210308100932542.png)

所有抠出来的图都转换为**智能对象**进行放大缩小

### 1、草莓

将草莓拖入 PS，<kbd>Ctrl</kbd> + <kbd>J</kbd> 复制图层

使用快速选择工具选出草莓(或者使用魔棒工具选择白色区域，把连续前的勾去掉，再反选)

选择好之后 <kbd>Ctrl</kbd> + <kbd>J</kbd> 复制到新图层

添加一个黑色图层到底下发现有白边

![抠出来的草莓有白边](https://cdn.wallleap.cn/img/pic/illustration/image-20210309171835211.png)

按住 <kbd>Ctrl</kbd>，单击抠出来的草莓图层缩略图，选择-修改-收缩，收缩 1-2 像素

![去掉白边](https://cdn.wallleap.cn/img/pic/illustration/image-20210309172217248.png)

接着 <kbd>Ctrl</kbd> + <kbd>J</kbd> 复制到新图层，把收缩前的图层删除或隐藏查看效果，鼠标右击这个图层，点击转换为智能对象

![转换为智能对象](https://cdn.wallleap.cn/img/pic/illustration/image-20210309172514976.png)

使用的时候直接把这个图层拖入到另一个图片中即可

### 2、门窗、台阶

门窗、台阶使用钢笔工具抠图

将图片拖入PS，<kbd>Ctrl</kbd> + <kbd>J</kbd> 复制图层

选择钢笔工具，点击一个点，有弧度的点击另一个点之后，鼠标不要松，拖动鼠标，知道路径和图形相符再松开鼠标，按住 <kbd>Alt</kbd> 键点击中间蓝色的点可以把下锚点删除掉，点击 <kbd>Shift</kbd> 可以画垂直/水平线

闭合路径之后，<kbd>Ctrl</kbd> + <kbd>Enter</kbd> 载入选区，<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>i</kbd> 反选，这样便能够选择到门窗/台阶，之后 <kbd>Ctrl</kbd> + <kbd>J</kbd> 将内容复制出来，转换为智能对象

门的抠取：

![钢笔描绘门的大概形状](https://cdn.wallleap.cn/img/pic/illustration/image-20210310085532915.png)

![载入选区](https://cdn.wallleap.cn/img/pic/illustration/image-20210310085619921.png)

![反选](https://cdn.wallleap.cn/img/pic/illustration/image-20210310085643363.png)

![复制并转换为智能对象](https://cdn.wallleap.cn/img/pic/illustration/image-20210310085716614.png)

窗户的和门差不多

使用钢笔工具抠取台阶的时候，注意抠的形状问题(这里只是演示，自己抠的时候认真点)：

![钢笔描绘形状](https://cdn.wallleap.cn/img/pic/illustration/image-20210310090141528.png)

![载入选区并反选](https://cdn.wallleap.cn/img/pic/illustration/image-20210310090214207.png)

![复制图层并转换为智能对象](https://cdn.wallleap.cn/img/pic/illustration/image-20210310090244627.png)

## 三、草莓

把背景拖入到 PS 中，<kbd>Ctrl</kbd> + <kbd>J</kbd> 复制图层

### 1、位置

将抠好的草莓拖入到背景窗口中

![拖入](https://cdn.wallleap.cn/img/pic/illustration/image-20210310090624562.png)

<kbd>Ctrl</kbd> + <kbd>T</kbd> 变形，把草莓变小(按住 <kbd>Alt</kbd> + <kbd>Shift</kbd> 再拖动任意一个角可以进行中心等比缩放)，放到合适位置，感觉差不多之后回车确定

![缩放到合适大小](https://cdn.wallleap.cn/img/pic/illustration/image-20210310090930101.png)

### 2、叶子

使用快速选择工具选择叶子，复制两层方便以后使用

![复制叶子](https://cdn.wallleap.cn/img/pic/illustration/image-20210310091313315.png)

首先随便选择哪个叶子图层，<kbd>Ctrl</kbd> +点击这个图层的缩略图，载入选区，点击底部小太极图标，选择色相饱和度

![色相饱和度](https://cdn.wallleap.cn/img/pic/illustration/image-20210310091536728.png)

把鼠标移到两个图层中间，按住 <kbd>Alt</kbd> 键，这个效果只会对叶子生效

![剪切蒙版](https://cdn.wallleap.cn/img/pic/illustration/image-20210310091819455.png)

对饱和度和色相进行调节，让叶子更鲜艳一点

![色相饱和度调节](https://cdn.wallleap.cn/img/pic/illustration/image-20210310091933556.png)

### 3、色调

为了让草莓更好得融合入背景，需要对草莓进行一些处理

在草莓上面新建两个图层

![新建空白图层](https://cdn.wallleap.cn/img/pic/illustration/image-20210310092150812.png)

<kbd>Ctrl</kbd> 并点击草莓图层缩略图，选择草莓，接着在一个空白图层中用黄色画笔对草莓泛白光的边缘进行涂抹，并把图层不透明度调低，图层混合模式改为`颜色减淡`

![环境光](https://cdn.wallleap.cn/img/pic/illustration/image-20210310092508436.png)

接着到另一个空白图层用黑色画笔进行涂抹，图层样式改为变暗，适当调整不透明度

![暗部](https://cdn.wallleap.cn/img/pic/illustration/image-20210310092834767.png)

## 四、门窗

### 1、形状

把抠好的门窗拖入

<kbd>Ctrl</kbd> + <kbd>T</kbd> 进行变形，先按住 <kbd>Alt</kbd> + <kbd>Shift</kbd> 拖动任一个角进行缩小，接着右击选择水平翻转，接着右击选择斜切

![调节大小](https://cdn.wallleap.cn/img/pic/illustration/image-20210310093320041.png)

按住 <kbd>Alt</kbd>（可能是其他按键，自己尝试），水平拖动上或下的一个角，调为上宽下窄形状，适当变形

![适当调节](https://cdn.wallleap.cn/img/pic/illustration/image-20210310093816632.png)

窗户也是这样操作

![调整窗户形状](https://cdn.wallleap.cn/img/pic/illustration/image-20210310094145025.png)

### 2、图层样式

接着给门窗做一个枕状浮雕效果

点击 `fx`，选择斜面和浮雕

![斜面浮雕](https://cdn.wallleap.cn/img/pic/illustration/image-20210310094245828.png)

适当调节参数

![浮雕效果](https://cdn.wallleap.cn/img/pic/illustration/image-20210310094522403.png)

窗户也这样操作

![窗户](https://cdn.wallleap.cn/img/pic/illustration/image-20210310094549124.png)

现在把窗户上面的叶子弄出来

选中没有用过的那个叶子图层，按住 <kbd>Ctrl</kbd> 并点击图层缩略图，选择叶子，选择快速选择工具，按住 <kbd>Alt</kbd> 涂去上面的两片叶子，并且收缩2像素，<kbd>Ctrl</kbd> + <kbd>J</kbd> 复制图层，转换为智能对象，把它缩小并放到窗户上，对它进行色相饱和度调节

![调节叶子](https://cdn.wallleap.cn/img/pic/illustration/image-20210310095622580.png)

## 五、台阶

将抠好的台阶拖入，对它进行缩放，给它一个色彩平衡，让台阶变黄一点

![台阶](https://cdn.wallleap.cn/img/pic/illustration/image-20210310100005666.png)

## 六、兔子

直接把兔子拖到合适的位置缩小即可

![兔子](https://cdn.wallleap.cn/img/pic/illustration/image-20210310100113269.png)

## 七、阴影

绘制一个椭圆形，滤镜-模糊-高斯模糊，调整透明度，把图层拖到背景图层上面，效果就完成了

![加阴影](https://cdn.wallleap.cn/img/pic/illustration/image-20210310100353377.png)
