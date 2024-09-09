---
title: PS 学习案例之蒙版
date: 2021-03-04 22:16
updated: 2021-03-04 22:16
cover: //cdn.wallleap.cn/img/pic/cover/2023023IfpRe.jpg
category: 设计相关
tags:
  - 设计
  - PS
description: PS 学习案例之蒙版
---

了解 PS 中常见的蒙版类型和操作

## 一、简介

PS 中的蒙版可以分为**图层蒙版**、**矢量蒙版**、**剪切蒙版**、**快速蒙版**四类。

- 蒙版可以理解为浮在图层上面的一块**玻璃**，它本身不包含图像数据，只是对图层的部分起到遮挡的作用，当我们对图层进行操作时，被挡的数据是不会受到影响的(这样可以不需要直接在原图层上修改，达到保护图片的作用)

- 蒙版是将不同**灰度色值**转化为不同的**透明度值**，并作用到它所在的图层，让图层不同地方透明度发生相应的变化。纯黑色表示完全透明，纯白色表示完全不透明。

- PS 可以直接新建的有两种，一种是白蒙版，另一种是黑蒙版(反向蒙版)，添加蒙版之后一般用颜色相反的画笔进行涂抹，并且画笔的不透明度一般设置在 20%-25%，画笔笔尖采用柔笔

- 白蒙版直接新建蒙版，黑蒙版 <kbd>Alt</kbd> + 创建蒙版：

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210309152659135.png)

## 二、案例

### 1、剪切蒙版

步骤1、将形状图层放下面

步骤2、将需要剪贴的图层放上面(主体物在上方——第一视觉看到的)

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304111427253.png)

步骤3、按住 <kbd>Alt</kbd> + 点击两个图层的中间即可创建剪贴蒙版(以后也可以用这个方式把图层样式、图层放到某个图层里/下)

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304111829545.png)

### 2、图层蒙版案例

#### (1) 鸡身鸭蹼

![效果](https://cdn.wallleap.cn/img/pic/illustration/image-20210304131348101.png)

1、将鸡、鸭拖入 PS，鸡图层在上面，鸭图层在下面

![拖入素材](https://cdn.wallleap.cn/img/pic/illustration/image-20210304132101200.png)

2、把鸡图层透明度调小一点，方便看到下一个图层

![调整透明度](https://cdn.wallleap.cn/img/pic/illustration/image-20210304132205094.png)

3、移动鸭图层，让鸭的脚蹼到鸡的合适的位置（选中鸭图层，将自动选择前复选框的√去掉）

![移动](https://cdn.wallleap.cn/img/pic/illustration/image-20210304132413074.png)

4、点击鸡图层，将不透明度改为 100%，并且新建一个蒙版

![新建蒙版](https://cdn.wallleap.cn/img/pic/illustration/image-20210304132640380.png)

5、点击画笔工具，对脚的部位进行涂抹

![画笔涂抹](https://cdn.wallleap.cn/img/pic/illustration/image-20210304132600987.png)

6、涂抹完成

![完成](https://cdn.wallleap.cn/img/pic/illustration/image-20210304142035401.png)

#### (2) 人物森林（双重曝光）

1、拖入风景、人物两张图片，人物图层放在下方，风景图层放在上方

![拖入素材](https://cdn.wallleap.cn/img/pic/illustration/image-20210304113216340.png)

2、将背景图层的锁取消，点击上面的图层的眼睛，把它隐藏掉，使用快速选择工具选出人物

![建立选区](https://cdn.wallleap.cn/img/pic/illustration/image-20210304113509514.png)

3、回到风景图层，点击左边的眼睛，让该图层显示出来，点击创建蒙版按钮

![创建蒙版](https://cdn.wallleap.cn/img/pic/illustration/image-20210304113601309.png)

4、点击画笔工具，画笔笔尖形状用【柔角30】，硬度为【0%】，画笔模式为【正常】，不透明度【28%】

![画笔涂抹](https://cdn.wallleap.cn/img/pic/illustration/image-20210304113703527.png)

5、把人脸涂抹出来

![涂抹脸部](https://cdn.wallleap.cn/img/pic/illustration/image-20210304113743938.png)

#### (3) 桥和湖面（倒影）

![倒影](https://cdn.wallleap.cn/img/pic/illustration/40.jpg)

1、将两张图片拖到PS中，蓝色湖面的图层在下面，桥的图层在上面

![拖入素材](https://cdn.wallleap.cn/img/pic/illustration/image-20210309154334518.png)

2、给桥的图层添加一个蒙版

![添加蒙版](https://cdn.wallleap.cn/img/pic/illustration/image-20210309154609069.png)

3、在工具组中选择`渐变工具`

![渐变工具](https://cdn.wallleap.cn/img/pic/illustration/image-20210309154729153.png)

4、在上面设置中把渐变颜色改为【从前景色到背景色渐变】，【线性渐变】，并且把前景色调为白背景色调黑（如果正好相反，可以用快捷键 <kbd>X</kbd> 调换前背景色，或者勾选上方渐变设置中的反向，按 <kbd>D</kbd> 可以快速恢复前景色、背景色为黑白）

![调整渐变](https://cdn.wallleap.cn/img/pic/illustration/image-20210309154917995.png)

5、之后在合适的位置拉一条渐变

![拉渐变](https://cdn.wallleap.cn/img/pic/illustration/image-20210309155450740.png)

6、这样蓝色湖面就出来了，接下来就需要把倒影弄出来

![蓝色湖面](https://cdn.wallleap.cn/img/pic/illustration/image-20210309155606605.png)

7、再把桥的图片拖进来并进行垂直翻转

![复制桥图层](https://cdn.wallleap.cn/img/pic/illustration/image-20210309155827140.png)

8、把这个图层移到蒙版的下面，并且把透明度调低

![移动图层顺序](https://cdn.wallleap.cn/img/pic/illustration/image-20210309160105389.png)

9、选中移动工具，把自动选择前的勾去掉，把图片移到合适的位置

![移动](https://cdn.wallleap.cn/img/pic/illustration/image-20210309160239538.png)

### 3、利用蒙版进行人物精修

#### (1) 方法一

1、拖入图片，<kbd>Ctrl</kbd> + <kbd>J</kbd> 复制图层

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304142349456.png)

2、滤镜-模糊-**高斯模糊**，半径数值调整到图片上看不到斑点为止（调的数值决定了能够淡斑的最终程度）

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304142659034.png)

3、<kbd>Alt</kbd> + 创建蒙版创建反向(黑色)蒙版

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304142756605.png)

4、使用画笔进行涂抹（不透明度在 20%-25%）

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304142918909.png)

#### (2) 方法二

1、拖入图片，<kbd>Ctrl</kbd>+<kbd>J</kbd>复制图层

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210309160553587.png)

2、滤镜—模糊—表面模糊（根据图形设置像素数值 eg：半径20、阈值25）

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210309160651230.png)

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210309160726420.png)

3、<kbd>Ctrl</kbd>+<kbd>J</kbd>复制做好的表面模糊图层两个

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210309160746630.png)

4、给最上方图层做滤镜—模糊—高斯模糊

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210309160844076.png)

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210309160924836.png)

5、选中复制图层，按住 <kbd>Alt</kbd> 键单击蒙版，创建黑色蒙版

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210309161020192.png)

6、使用白色画笔涂抹(进行局部瑕疵擦拭)

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210309161241912.png)

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210309161122640.png)

7、涂抹完成之后

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210309161843099.png)

#### (3) 方法三(这种方法可以只用一部分步骤)

1、<kbd>Ctrl</kbd>+<kbd>J</kbd>复制图层

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304144632699.png)

2、进入通道，复制蓝色通道(这里斑在蓝色通道最明显)

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304144646875.png)

3、滤镜-其他-高反差保留，半径为8

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304144758109.png)

4、图像-计算-混合模式为强光

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304144838072.png)

5、对新的alpha1再计算一次(共计算两次)

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304144904254.png)

6、按住<kbd>Ctrl</kbd>键，点击Alpha2缩略图，给alpha2载入选区——><kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>i</kbd>反选——>删减选区（快速选择工具，按住<kbd>Alt</kbd>键把头发涂抹掉）

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304145452895.png)

7、回到RGB

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304145513614.png)

8、回到图层，点击下面太极状图标，选择曲线

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304145554066.png)

9、曲线调亮，能够消掉一点斑

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304145651532.png)

10、<kbd>Ctrl</kbd>+<kbd>g</kbd>成组

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304145726847.png)

11、对这个组创建黑色蒙版

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304145753431.png)

12、局部画笔淡斑

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304145928775.png)

13、复制背景图层2次

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304150154813.png)

14、第一个进行滤镜-模糊-表面模糊--数值为20 25，图层不透明度改为60

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304150139796.png)

15、第二个进行图像-应用图像-混合模式改为正常，通道改为红色通道，不透明度不需要太高(图中不透明度太高，颜色发生了变化)

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304150314889.png)

16、滤镜-其他-高反差保留，半径改为0.8

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304150354890.png)

17、图层混合模式改为线性光

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304150451933.png)

18、选中除背景外的所有图层，打组

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304150519053.png)

19、按两次快捷键 <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>Shift</kbd> + <kbd>e</kbd> 盖印两个图层

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304150549180.png)

20、给最上面的图层做一个滤镜-模糊-高斯模糊

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210304150649934.png)

21、给图层创建反向蒙版，用画笔淡斑

![](https://cdn.wallleap.cn/img/pic/illustration/image-20210309163720634.png)

其他两个蒙版不经常使用，这里就不做演示了

- 矢量蒙版：使用矢量工具创建矢量路径，然后创建矢量蒙版，矢量路径内的区域显示，外的区域隐藏
- 快速蒙版：使用快速选择工具选中区域，然后创建快速蒙版，选中区域显示，未选中区域隐藏
