---
title: 你必须知道的 CSS
date: 2020-04-03 20:10
updated: 2020-04-03 20:10
cover: //cdn.wallleap.cn/img/pic/cover/202302KYL2t2.jpg
category: 技术杂谈
tags:
  - web
  - 前端
description: 你必须知道的 CSS
---

CSS 控制的是网页的样式，相当于人的皮肤

## 一、CSS简介

### 1、层叠样式表(Cascading Style Sheeets)

- CSS 可以用来为网页创建样式表，通过样式表可以对网页进行装饰

- 可以将网页想象成是一层一层的结构，层次高的将会覆盖层次低的。

- CSS 可以分别为网页的各个层次设置样式

### 2、使用

- 内联样式：将 CSS 样式编写到元素的 style 属性当中

```css
<p style=”color:red;font-size:13px;”></p>
```

内联样式只对当前的元素中的内容起作用，不方便复用，结构与表现耦合，不方便后期维护，不推荐使用(可在测试样式、或 JS 控制样式时使用)

- 将 CSS 样式编写到 head 标签中的 style 标签中,通过 CSS 选择器选中指定元素，可以同时为这些元素一起设置样式，这样可以是样式进一步的复用

```css
<style type=”text/css”>
p {
  color:red;
  Font-size:13px;
}
</style>
```

将样式编写到 style 标签，可以是表现和结构进一步分离，推荐使用

- 将样式编写到外部的 css 文件中，然后通过 link 标签将外部的 css 文件引入到当前页面中，这样外部文件中的 css 样式表将会应用到当前页面中

```html
<link rel="stylesheet" type="text/css" href="style.css">
```

完全使结构和表现分离，可以让样式表在不同的页面中使用，最大限度的使样式可以进行复用，将样式统一写在样式表中，然后通过 link 标签引入，可以利用浏览器的缓存加快用户访问的速度，提高用户体验，最推荐使用

- 在 CSS 文件中引入 CSS 文件

```css
import 'var.css'
```

### 3、注释

```css
// 单行注释

/* 注释内容 */
```

注：style 中的不是 html 内容了

### 4、语法

`选择器 声明块`

- 选择器：通过选择器可以选中页面中指定的元素，并且将声明块中的样式应用到选择器对应的元素上

- 声明块：声明块紧跟在选择器的后边，使用一对 `{}` 括起来，声明块中实际上就是一组一组的名值对结构，这一组一组额名值对我们称为声明，在一个声明块中可以写多个声明，多个声明之间使用 `;` 隔开，声明的样式名和样式值之间使用 `:` 连接

例如：

```css
div{
  width: 200px;
  height: 200px;
}
```

### 5、块、内联元素

- 块元素：独占一行的元素

```html
<div>
   I’m div!
</div>
```

无论内容有多少，都会占一整行

div、p、h1、br...

div 标签没有任何语义，就是一个纯粹的块元素，并且不会为它里面的元素设置任何的默认样式，div 元素主要用来对页面进行布局的

- 内联元素(行内元素)：只占自身大小的元素，不会占用一行

```html
<span>
  I’m span.
</span>
```

a、img、iframe、span

span 没有任何的语义，span 标签用来选中文字，然后为文字设置样式

Ps:块元素主要用来做页面中的布局，内联元素主要用来选中文本设置样式

一般情况下只使用块元素去包含内联元素，而不会使用内联元素去包含块元素，a元素可以包含除它本身之外的任意元素，p元素不可以包含任何的块元素

### 6、元素之间的关系

- 父元素：直接包含子元素的元素

- 子元素：直接被父元素包含的元素

- 祖先元素：直接或间接包含后代元素的元素，父元素也是祖先元素

- 后代元素：直接或间接被祖先元素包含的元素，子元素也是后代元素

- 兄弟元素：拥有相同父元素的元素

## 二、选择器

由于选择器使用是基本的，因此就不和 CSS 3 分开讲了

### 1、元素选择器:可以选中页面中的所有指定元素

语法：`标签名{}`

```css
P{
  Color: red;
}
h1{
  Font-size:25px;
}
```

### 2、id 选择器:通过元素的 id 属性值选中唯一的一个元素

语法：`#id属性值{}`

```html
<p id=”p1”>hello</p>
<style>
  #p {
     Font-size:16px;
  }
</style>
```

### 3、类选择器:通过元素的 class 属性值选中一组元素

语法：`.class属性值{}`

```html
<p class=”p2”>111</p>
<p class=”p2”>222</p>
<style>
  .p{
    font-size:16px;
  }
</style>
```

可以同时为一个元素设置多个 class 属性值，多个值之间使用空格隔开

```html
<p class=”p2 111”>111</p>
<style>
  .111{
    font-size:20px;
  }
</style>
```

### 4、选择器分组(并集选择器)：同时选中多个选择器对应的元素

语法：`选择器1,选择器2,选择器n{}`

```css
#p1,.p2,h1{
  background-color:yellow;
}
```

### 5、通配选择器:选中页面中的所有元素

语法：`*{}`

```css
*{ 
  margin:0; 
  padding:0;
}
```

### 6、复合选择器(交集选择器):选中同时满足多个选择器的元素

语法：选择器1选择器2选择器n{}

```html
<span class="p3"></span>
<style>
  span.p3{
    background-color:yellow;
  }
</style>
```

Id 一般不使用

### 7、后代元素选择器：选中指定元素的指定后代元素

语法：`祖先元素 后代元素{}`

```html
<div>
  <p>
    <span>hello</span>
    <span>nihao</span>
  </p>
  <span>hello</span>
</div>
<style>
  div span{color:greenyellow;}
  div p span{font-size:50px;}
</style>
```

### 8、子元素选择器：选中指定父元素的指定子元素

语法：`父元素>子元素{}`

```css
div>span{background-color:red;}
```

IE6 及以下的不兼容

### 9、伪类选择器

伪类专门用来表示元素的一种的特殊的状态，例如访问过的超链接、获取焦点的文本框

当需要为处在这些特殊状态的元素设置样式时，就可以使用伪类

eg：

- 正常(未访问过的) **`a:link`**

- 访问过的 **`a:visited`** --浏览器通过历史记录来判断一个连接是否访问过。由于涉及到用户的隐私问题，故使用这个伪类只能设置字体的颜色(IE6能设置背景颜色)。

- 鼠标滑过 **`a:hover`**

- 正在点击 **`a:active`** (点击不松手)

后两个伪类其他元素也能设置(*IE6不支持除a之外的元素设置*)

- 获取焦点 **`:focus`**

```html
<input type="text" />
<style>
	input:focus{background-color: yellow;}
</style>
```

### 10、伪元素(选择特殊的位置)

段落定义

- 文本的第一个字母或字 `::first-letter`

```css
/* 首字下沉 */
p::first-letter{
  font-size: 20px;
  float: left;  /* 文本环绕 */
}
```

- 文本第一行` ::first-line`

如果同时设置了first-letter，则无法影响这个字/字母

- `::selection` 可改变选中文本的样式，只能设置显示的样式，不能改变内容大小

- `::before`和`::after`伪元素

i. 是一个行内元素，如果想要设置宽高需要转换为块(`display:block` / `float:**` / `position:**`)

ii. 必须添加 content，即使没有内容，也要加上 `content: “”`

iii. `E:before`、`E:after` 在旧版本里是伪类，在新版本中是伪元素，新版本中单冒号的会被自动识别为`E::befor`、`E::after`，按伪元素来对待，这样做的目的是兼容性处理

iv. `E::before`：定义在一个元素的内容之前插入content属性定义的内容与样式

v. `E::after`：定义在一个元素的内容之后插入content属性定义的内容与样式

vi. 注意：

a) IE6、IE7与IE8(怪异模式Quirks Mode)不支持此伪元素

b) CSS2中E`:before`、`E:after`属于伪类，并且没有伪元素的概念，CSS3中提出伪元素的概念`E::before`、`E::after`，并且归属到了伪元素当中，伪类中就不再存在`E:before`、`E:after`伪类

c) 功能完全等同于一个 DOM 元素，但是不会在 DOM 树中生成

### 11、属性选择器

`title 属性` 可以给任何标签指定，光标移动到元素上时，元素中的 `title 属性`的值将会作为提示文字显示。

作用：可以根据元素中的属性或属性值来选取指定元素

语法：元素(可以是元素选择器、类选择器、id选择器等)后跟

- `[属性名]` 选取含有指定属性的元素

  ` E[attr]`: 查找拥有 attr 属性的E标签

- `[属性名=”属性值”]` 选取含有指定属性值的元素

  `E[attr=value]`: 查找拥有attr属性且属性值为value的E标签(严格匹配)

- `[属性名^=”属性值”]` 选取属性值以指定内容开头的元素

 `E[attr^=value]`: 查找拥有attr属性且属性值是以value开头的E标签

- `[属性名*=”属性值”]` 选取属性值包含指定内容的元素

  `E[attr*=value]`: 查找拥有attr属性且属性值中包含value(可以在任何位置)的E标签

- `[属性名$=”属性值”]` 选取属性值以指定内容结尾的元素

  `E[attr$=value]`: 查找拥有attr属性且属性值是以value结尾的E标签

eg:

```css
p[title] {background-color:green;}
p[title=hello] {background-color:yellow;} // 也可给title值加上双引号
p[title^=”ab”] {background-color:purple;} // 以ab开头的
p[title$=”c”] {background-color:pink;} // 以c结尾的
p[title*=”c”] {background-color:purple;} // 包含c的
```

### 12、子元素选择器

- `父元素>子元素` : 比如`div>a`代表选择`div`下的子元素`a`

其他子元素选择器(相对于父元素的结构伪类)

- `:first-child`：选择该元素父标签下第一个子标签

`E:first-child`: 查找E元素的父元素下的第一个E元素

- `:last-child`：选择该元素父标签下最后一个子标签

`E:last-child`: 查找E元素中最后一个指定类型的子元素

- `:nth-child(n)`：选择指定位置的子元素，里面的n可以传
  - 数字：从1开始的数字，选择该元素父标签下的第几个子标签
  - n的表达式：`n`代表所有的该标签，`2n`代表父标签下偶数个子标签，`3n`代表选择第三个……，`3n-1`
  - `even`/`odd`：偶数/奇数

`E:nth-child(n)`: 指定索引位置，n是从1开始的数字 也可以是偶数：even 奇数：odd

上面这三个是既需要满足最后一个，又得是这个标签，例如：

```css
// p*3+ul>(span{span1}+li{$}*6+span{span2})
li:first-child{font-size: 30px;}  // 选择不到，因为li的父元素ul下第一个子元素是span，不满足li
span:last-child{color: green;} // 可以选择到，因为span的父元素ul下最后一个子元素是span
li:nth-child(2){background-color: red;} // 1的话选择不到，2能选择到<li>1</li>(在父元素下第二个，且为li标签)
body > p:first-child{color: red;} // body子元素p如果p是在第一个元素则选中，若p前还有其他类型的元素，则选不到了(所有元素中排)
P:last-child{color: green;}  // 如果最后一个p后面还有其他元素则选择不到
P:nth-child(2){background-color:yellow;} // 任意位置，传值，可以设置数字、even(偶数)、odd(奇数)
```

- `:first-of-type`
- `:last-of-type`
- `:nth-of-tyle(n)` 这三个分别表示同类型中的第一个、最后一个、第几个

`E:nth-of-type(n)`: (限定类型) n也可以是数字、even、odd、还可以是n(代表默认取值范围为0~子元素的长度)、还可以利用n取前几个(-n+5就是代表前5个，当n<=0时无效)

这三个选择指定类型的子元素，推荐使用这个

- `:nth-last-of-tyle(n)`

`E:nth-last-of-type(n)`: 同上(-n+5代表最后5个) （n——索引、关键字、表达式）

```css
p:first-of-type{font-size: 20px;} // 所有p中的第一个(同一类型中排)
```

- `E:empty`: 选中没有任何子节点的E元素(空格也算子元素)

- `E:target`: 可以为锚点目标元素添加样式，当目标元素被触发为当前锚链接的目标时，调用此伪类样式  

```html
<style>
  h2:target{
    color: red;
  }
</style>
<a href="#title1">跳转到title1</a>
<a href="#title2">跳转到title2</a>
<h2 id="title1">title1</h2>
<p>……</p>
<h2 id="title2">title2</h2>
<p>……</p>
```

### 13、兄弟元素选择器(兄弟伪类)

(1) **后一个**兄弟选择器

 作用：选中一个元素后紧跟着的指定的兄弟元素

 语法：`前一个+后一个`

```css
span+p{} // span后紧挨着的p
```

(2) 选中**后边的所有兄弟**元素

 语法：`前一个~后边所有`

```css
span~p{}
```

### 14、否定伪类

 作用：可以从已选中的元素中剔除出某些元素

 语法： :`not(选择器)`

```css
p:not(.hello){} // 选择所有不带hello类的p标签
```

## 三、样式的继承

和儿子继承父亲的遗产一样，在CSS中，祖先元素上的样式，也会被他的后代元素所继承。eg：

```html
<p>
  这个是p中文字
  <span>p中的span</span>
</p>
```

利用继承，可以将一些基本的样式设置给祖先元素，这样所有的后代元素将会自动继承这些样式。但是并不是所有的样式都会被子元素所继承，例如**背景相关**、**边框相关**、**定位相关**的样式都**不会被继承**。

## 四、选择器的优先级

当使用不同的选择器，选中同一个元素并且设置相同的样式时，这时样式之间产生了冲突，最终到底采用哪个选择器定义歌样式，由选择器的优先级(权重)决定，优先级高的优先显示。

### 1、优先级的规则

内联样式，优先级 1000

id选择器，优先级 100

类和伪类，优先级 10

元素选择器，优先级 1

通配*，优先级 0

继承的样式，没有优先级

当选择器中包含多种选择器时，需要将多种选择器的优先级相加然后再比较，但是注意，选择器优先级计算不会超过他的最大的数量级。**如果选择器优先级一样，则使用靠后的样式(会覆盖前一个)。**

并集选择器的优先级是单独计算的。

可以在样式的最后，添加一个`!important`，则此时该样式将会获得一个最高的优先级。

```css
p{
  color: skyblue !important;
}
```

### 2、伪类的顺序

涉及到a的伪类一共有四个

这四个选择器的优先级是一样的

active应写在hover后面，前两个要写在后两个前面，即下面的顺序：

1. **`a:link{}`**

2. **`a:visited{}`**

3. **`a:hover{}`**

4. **`a:active{}`**

## 五、HTML 中一些标签

HTML 中有些标签需要拿出来讲解一下

### 1、文本标签

下面两个强调

- `<strong></strong>`内容上的强调 显示为粗体

- `<em></em>`   语气上的强调 显示为斜体

下面两个无语义，单纯加粗、斜体

- `<b></b>`   内容以粗体显示
- `<i></i>`    内容以斜体显示

大小

- `<small></small>` `small`标签中的内容会比他的父元素中的文字要小一些，在H5中表示一些细则一类的内容，比如：合同中的小字、网站的版权声明等

- `big`无语义，淘汰

引用

- `<cite></cite>`网页中所有的加书名号的内容，表示参考的内容

- `q`标签表示短的引用(行内引用) 自动加双引号
- `blockquote`标签表示一个长引用(块级引用)

上下标

- `sup` 设置上标

- `sub` 设置下标

文字上的线

- `del` 表示删除的内容 自动添加删除线
- `ins`表示一个插入的内容 自动添加下划线

代码片段

- `pre`标签是一个预格式标签，将会将代码中的格式保存，不会忽略多个空格

- `code`专门用来表示代码，一般结合`pre`和`code`来表示一段代码

### 2、列表

(1) 无序列表

`ul`标签来创建一个无序列表

使用`li`在`ul`中创建一个一个的列表项，一个`li`就是一个列表项

```html
<ul type=”disc”>
  <li>北京</li>
  <li>上海</li>
</ul>
```

通过`type`属性可以修改无序列表的项目符号。默认的项目符号一般都不使用！非要加项目符号，采用为`li`设置背景方式实现。

- `disc` 默认，实心的原点

- `square` 实心方块

- `circle` 空心圆球

去掉项目符号：

```css
ul{
  list-style: none;
}
```

导航栏中的一般都是用的无序列表

`ul`、`li`都是块元素

(2) 有序列表

`ol`来创建一个有序列表

```html
<ol>
  <li>结构</li>
  <li>表现</li>
  <li>行为</li>
</ol>
```

有序列表使用有序的序号作为项目符号。

`type`属性可以指定序号的类型

- `默认值`，使用阿拉伯数字

- `a`/`A`，小/大写

- `i`/`I`，罗马数字

列表之间都是可以相互嵌套的，可以在无序列表中放有序列表，也可以在有序中放无序。当然嵌套的`ul`、`ol`都是放在`li`中。

(3) 定义列表

用来对一些词汇或内容进行定义

使用`dl`创建

`dl`中有两个子标签

`dt`：被定义的内容 `dd`：对定义的内容进行描述

```html
<dl>
 <dt>胡萝卜<dt>
 <dd>蔬菜</dd>
 <dd>好吃</dd>
 <dd>含维生素E</dd>
 <dt>西瓜</dt>
 <dd>水果</dd>
</dl>
```

制作下拉菜单的时候可以用

### 3、表格

表格在日常生活中使用的非常多，比如excel就是专门用来创建表格的工具，表格就是用来表示一些格式化的数据的，比如：课程表、银行对账单等

在网页中也可以来创建出不同的表格

在HTML中使用`table`标签来创建一个表格

在`table`标签中使用`tr`来表示表格中的一行，有几行就写几个`tr`

在`tr`中需要使用`td`来创建一个单元格，有几个单元格就写几个`td`

可以使用`th`标签来表示表头中的内容，它的用法和`td`一样，不同的是它会有一些默认效果

使用`<td colspan="2"></td>`横向合并单元格

使用`<td rowspan="2"></td>`纵向合并单元格

直接用案例来看表格样式：

```html
<style>
  table{
    width: 500px;
    margin: 30px auto;
    /* 设置边框 */
    border: 1px solid silver;
    /* 
     * table和td边框之间默认有一个距离，通过border-spacing属性可以设置这个距离
     */
     border-spacing: 10px;
     /* 
      * border-collapse可以用来设置表格的边框合并，如果设置了边框合并，则border-spacing自动失效
      */
     border-collapse: collapse;
  }
  /* 设置隔行变色 */
  tr:nth-child(even){
    background-color: skyblue;
  }
  /* 鼠标移入tr后，改变颜色 */
  tr:hover{
    background-color: #ff0;
  }
</style>
<table>
  <tr>
    <th>姓名</th>
    <th>性别</th>
    <th>年龄</th>
    <th>地址</th>
  </tr>
  <tr>
    <td>孙悟空</td>
    <td rowspan="2">男</td>
    <td>未知</td>
    <td>花果山</td>
  </tr>
  <tr>
    <td>猪八戒</td>
    <td>未知</td>
    <td>高老庄</td>
  </tr>
</table>
```

长表格

有一些情况下表格是非常长的，这时就需要将表格分为三个部分，表头、表格的主体、表格底部，分别用三个标签`thead`、`tbody`、`tfoot`表示

这三个标签的作用就是区分表格的不同部分，它们都是table的子标签，都需要直接写到table中，tr需要写在这些标签当中

标签`thead`、`tbody`、`tfoot`中的内容，永远会显示在表格的头部、中间、底部

如果表格中没有写tbody，浏览器会自动在表格中添加tbody，并且将所有的tr都放到tbody中，所以注意tr并不是table的子元素，而是tbody的子元素，通过`table>tr`无法选中行，需要通过`tbody>tr`

表格的列数由td最多的那行决定

表格是可以嵌套的，可以在td中再嵌套一个表格

使用表格布局--了解即可

以前表格很多情况实际上是用来对页面进行布局的，但是这种方式早已被CSS所淘汰了

演示一个吧：

```html
<style>
  *{
    margin: 0;
    padding: 0;
  }
  table{
    width: 1200px;
    margin: 0 auto;
    border: none;
    border-spacing: 0;
  }
  .header, .footer{
    width: 1200px;
    height: 200px;
    background-color: yellow;
  }
  .nav{
    width: 200px;
    height: 516px;
    background-color: green;
  }
  .content{
    width: 780px;
    height: 516px;
    margin: 10px;
    background-color: skyblue;
  }
  .aside{
    width: 200px;
    height: 516px;
    background-color: pink;
  }
</style>
<table>
  <tr>
    <td colspan="3"><div class="header"></div></td>
  </tr>
  <tr>
    <td><div class="nav"></div></td>
    <td><div class="content"></div></td>
    <td><div class="aside"></div></td>
  </tr>
  <tr>
    <td colspan="3"><div class="footer"></div></td>
  </tr>
</table>
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200811172343.png)

写起来是真的很方便啊，但是改起来会想哭的

### 4、表单

表单的作用就是用来将用户信息提交给服务器的，比如：百度搜索框、登录这些操作都需要填写表单

使用 `form` 标签创建表单，`form` 标签中必须制定一个 `action` 属性，该属性指向的是一个服务器的地址，当我们提交表单时将会提交到 `action` 属性对应的地址

使用 `form` 创建的仅仅是一个空白的表单，我们还需要向 `form` 中添加不同的表单项

- 使用 `input` 来创建一个文本框，它的 `type` 属性是 `text`，如果希望表单项中的数据提交到服务器中，还需要给表单项指定一个 `name` 属性，`name` 表示提交内容的名字。用户填写的信息会负载url地址的后面以查询字符串的形式发送给服务器。在文本框中指定 `value` 属性值，将会作为默认值

`url地址?查询字符串`

`属性名=属性值&属性名=属性值`

- 使用 `input` 创建密码框，它的 `type` 值为 `password`

- 使用 `input` 来创建单选按钮，它的 `type` 属性使用 `radio`。单选按钮通过 `name` 属性进行分组，`name` 属性值相同的是一组按钮。像这种需要用户选择，但是不需要用户直接填写内容的表单项，还必须指定一个 `value` 属性，这样被选中的表单项的 `value` 属性值将会最终提交给服务器

- 使用 `input` 创建一个多选框，它的 `type` 属性使用 `checkbox`

- 使用 `select` 创建一个下拉列表，在下拉列表中使用 `option` 标签来创建一个个列表项.下拉列表的 `name` 属性指定给 `select`，`value` 属性指定给 `option`

`multiple=”multiple”` 可以选中多个

在 `select` 中可以使用 `optgroup` 对选项进行分组，同一个 `optgroup` 中的选项是一组，通过 `label` 属性来指定分组的名字

如果希望在单选按钮或者是多选框中指定默认选中的选项，可以在想选中的项中，添加 `checked=”checked”` 属性

下拉列表可以通过在 `option` 中添加 `selected=”selected”` 将选项设置为默认选中

- 使用 `textarea` 创建一个文本域

- 提交按钮可以将表单中的信息提交给服务器，使用 `input` 创建一个提交按钮，它的 `type` 属性是 `submit`，在提交按钮中，可以通过 `value` 属性来指定按钮上的文字

`<button type="reset">重置</button>`、`<input type="reset" />` 重置按钮，点击之后表单中的内容都会恢复为默认值

`<button type="button">按钮</button>`、`<input type="button" value="按钮">` 普通按钮，这个按钮没有任何功能，只能被点击，一般 js 设置功能

`<button type="submit">提交</button>`、`<input type="submit" value="提交">` 提交按钮，放在 form 中点击的时候将触发表单的 submit 事件

`button` 这种方式和使用 `input` 类似，但是更灵活

- 在 HTML 中提供了一个标签，专门用来选中表单中的提示文字的 `label` 标签，该标签可以指定一个 `for` 属性，该属性的值需要指定一个表单项的 `id值`，也可以直接包裹表单项

- 可以使用 `fieldset` 对表单项进行分组，在 `fieldset` 中使用 `legend` 子标签来指定组名

```html
<form action=”target.html”>
  <fieldset>
    <legend>用户信息</legend>
    <label for="usrname">用户名：</label><input type="text" name="username" id="usrname" /><br />
    <label>联系电话：<input type="text" name="num" /> </label><br />
    密码：<input type="password" name="pwd" /><br />
    性别：<input type="radio" name="gender" value="male" />
    <input type="radio" name="gender" value="female" checked="checked" />女<br />
  </fieldset>
  <fieldset>
    <legend>爱好</legend>
    爱好：<input type="checkbox" name="hobby" value="lq" />篮球
    <input type="checkbox" name="hobby" value="zq" />足球
    <input type="checkbox" name="hobby" value="pq" checked="checked" />排球
    <input type="checkbox" name="hobby" value="ymq" checked="checked" />羽毛球
    喜欢的明星：<select name="star">
      <optgroup lable="女明星">
        <option value="lxr">林心如</option>
        <option value="ym" selected="selected">杨幂</option>
        <option value="fbb">范冰冰</option>
      </optgroup>
      <optgroup label="男明星">
        <option value="lxr">林心如</option>
        <option value="ym" selected="selected">杨幂</option>
        <option value="fbb">范冰冰</option>
      </optgroup>
    </select>
  </fieldset>
  自我介绍：<textarea name="info"></textarea>
  <input type="submit" value="提交" />
  <input type="reset" />
  <input type="button" value="按钮">
</form>
```

## 六、文本格式化

### 1、单位

- px 像素

一个像素就相当于我们屏幕中的一个小点，我们的屏幕实际上就是由这些像素点构成的。但是这些像素点，是不能直接看见。不同显示器一个像素的大小也不相同，显示效果越好越清晰，像素就越小，反之像素越大

- 百分比

根据其父元素的样式计算该值。

自适应页面常使用百分比作为单位。

- em

em 相对当前元素的字体大小来计算的

`1em=1font-size`

当设置字体相关的样式时，经常会使用em

- rem

rem 相对根元素的字体大小来计算

- vw/vh

分别是视口宽度/高度的百分之一

- vmin/vmax

取 vw 和 vm 中的较小/较大值

### 2、颜色

CSS3 中的颜色也到这里讲

- 预设常量值：

  颜色单词 red、blue、green、orange……

- RGB

  各颜色浓度

  rgb(红, 绿, 蓝)，取值在0~255之间，还可以按百分比取

  rgb(255,0,0) rgb(200,0,0) rgb(0%,100%,0%)

- HEX

  和上面类似，但以十六进制显示 ，前两位表示红，中间两位表示绿，后两位表示蓝，最后两位表示透明度(00~ff)

  #FFFFFF 重复的两位可简写 #ff00aa #f0a

- HSL

  H：Hue(色调、色相)，0或360表示红色、120表示绿色、240表示蓝色。0~360，过渡也是红橙黄绿青蓝紫

  S：Saturation(饱和度)。0.0%~100.0%

  L：Lightness(亮度)。0.0%~100.0%，50%是平衡值 brightness

 rgb、hsl、HEX表示颜色，都是按<font color=red>红</font>橙黄<font color=green>绿</font>青<font color=blue>蓝</font>紫顺序过去的，因此改变该颜色值，可以调到相邻的另一种颜色，比如rgb(255, 0, 0)表示红色，那么取一半

- rgba rgba(128,128,0, .5)
- hsla hsla(120, 1%, 50%, .5)

这两个只是多了一个透明通道alpha，都是在最后一个参数，取值0~1，这样设置的透明度不会影响子元素

后面讲的`opacity`：透明度 0~1 设置父容器，则父容器中的所有子元素也会透明

透明`transparent`不可调节透明度，始终完全透明

### 3、字体

**(1) 字体颜色** 

格式：`color: 颜色值;`

例如：`color: red;`，`color: rgb(255, 0, 0);`，`color: #f00;`

**(2) 字体大小** 

格式：`font-size: 大小;`

基本上填数值，而不使用 large、small 等属性值

`font-size: 20px; `

默认大小16px 并不是文字本身的大小 在页面中，每个文字都是处在一个看不见的框中 设置的实际上是格的高度，一般文字都要比这个格要小一些，有时会比格大 根据字体不同，显示效果也不同

**(3) 字体**

格式：`font-family: 字体;`

 `font-family: "微软雅黑";` 

如果浏览器支持该字体，则以该字体显示，不支持则用默认字体 可指定多个，`font-family: arial, 宋体 ; `优先使用前面字体，没有则尝试下一个 浏览器使用的字体默认使用计算机中字体 在开发中，字体用的少，尽量不要使用 。字体在后面还会讲到。

字体分类：(浏览器会自动选择大分类的一种字体)

- serif(衬线字体)：有粗细变化
- sans-serif(非衬线字体)：无粗细变化
- monospace(等宽字体)：上下同宽
- cursive 草书字体
- fantasy 虚幻字体

指定字体类型：`font-family: sans-serif;`

一般会将字体的大分类，指定为font-family中的最后一个字体。

`font-family: arial， 微软雅黑, 华文彩云, serif;` (前面字体找不到就会找后面的)

**(4) 字体样式** 

格式：`font-style: 样式;`

可选值：

- `normal`正常字体
- `italic`斜体
- `oblique`斜体
- `inherit`继承父元素样式
- `initial`默认
- `unset`不设置(正常)

**(5)文本粗细/字重**

格式：`font-weight: 样式值;`

可选值：

- normal 正常
- bold 加粗
- lighter 定义更细的字符
- border 更粗一点
- 100、200、300……900 定义由粗到细的字符。400 等同于 normal，而 700 等同于 bold。

需要字体支持

**(6) 小型大写字母** 

格式：`font-variant: 样式值;`

可选值：

- normal 正常
- small-caps 设置为小型大写字母字体

**(7) font简写**

`font: italic small-caps bold 60px “微软雅黑”;`

使用这个font属性最后两个属性值有顺序(位置必须倒一、倒二)，且必须有这两个属性值。

**(8) 行间距** 

通过设置行高 行高越大、行间距越大

`line-height: 40px;`

行高类似于单线本，两线之间的高度就是行高

网页中的文字实际上也是写在一个看不见的行中，文字会默认在行高中垂直居中 行间距=行高-字体大小

`line-height: 120%;` 相对于字体大小，继承的是固定的数值

`line-height: 1.5;` 相对于当前字体大小，继承的是 1.5 这个值

对于单行文本来说，可以将行高设置为和父元素高度一致，可以使单行文本在父元素中垂直居中

**font的完整缩写**：`font: font-style font-variant font-weight font-size/line-height font-family`

`font: 30px/40px “宋体”;` 字体大小/行高 字体

### 4、文本

(1) 大小写

格式：`text-transform: 值;`

可选值：

- none 默认值，定义带有小写字母和大写字母的标准的文本
- capitalize 文本中每个单词开头字母大写
- uppercase 所有字母大写
- lowercase 所有字母小写

(2) 文本修饰

- `text-decoration-line: 线的位置;`
  - none 没有线
  - overline 文字上方
  - line-through 穿过文字
  - underline 文字下方
- `text-decoration-style: 线的样式;`
  - none 默认的样式，一条直线
  - dashed 虚线
  - dotted 点
  - solid 直线
  - wavy 波浪线
- `text-decoration-color: 颜色值;`
- 其他的不重要

可以简写：`text-decoration: underline dashed red;`

(3) 字母间距

`letter-spacing: 10px;`

(4) 单词间距

`word-spacing: 1em;`

(5) 文本对齐

`text-align: 值;`

- left 左对齐
- center 水平居中
- right 右对齐
- justify 两端对齐

(6) 首行缩进 `text-indent: 2em;`

可用于隐藏文字 `text-indent: -99999px;`

## 七、、盒子模型(框模型 Box Module)

### 1、盒子

- CSS 处理网页时，它认为每个元素都包含在一个不可见的盒子里
- 我们只需要将相应的盒子摆放到网页中相应的位置即可完成网页的布局

### 2、盒子模型

一个盒子具有内容区(content)、内边距(padding)、边框(border)、外边距(margin)

![盒模型](https://cdn.wallleap.cn/img/pic/illustration/20200811142849.jpg)

盒模型包括标准盒模型(W3C盒模型)和怪异盒模型(IE盒模型)

- 标准盒模型**width**指的是内容区域**content**的宽度；**height**指的是内容区域**content**的高度。

**标准盒模型下盒子的大小** = **content** + **border** + **padding** + **margin**

- 怪异盒模型**width**指的是内容、边框、内边距总的宽度（content + border + padding）；**height**指的是内容、边框、内边距总的高度

**怪异盒模型下盒子的大小=width（content + border + padding） + margin**

在默认情况下，CSS设置的盒子宽度仅仅是内容区的宽度，而非盒子的宽度。同样的高度类似。真正的盒子的宽度(在页面上呈现出来的宽度)和高度，需要加上一些其他的属性。

很明显，这种盒模型不直观，很容易出错，造成网页中其他元素的错位。

CSS3中可以通过 `box-sizing` 来指定盒模型，即可指定为

- `content-box`：标准盒模型
- `border-box`：IE盒模型

(1) `width`、`height` 设置内容区/盒子的宽高

(2) `border-width`、`border-color`、`border-style` 设置边框宽、颜色、样式

- `border-width: 10px 2px 3px 5px;` 四个值：上、右、下、左 (顺时针)

- `border-width: 10px 2px 3px;`  三个值：上、左右、下

- `border-width: 10px 3px;`  两个值：上下、左右

- `border-width: 10px ;` 一个值：上下左右

- 除此之外，还可以分别设置每边的宽：`border-xxx-width: 10px;` 其中xxx表示`top`、`right`、` bottom `、`left`

- `border-color: red blue green pink;` 与上方类似(四个值、三个值……)

- 单独一边的颜色`border-xxx-color: red;` 其中xxx表示`top`、`right`、` bottom `、`left`

- `border-style: none;`
  - `solid`实线
  - `dotted`点状
  - `dashed`虚线
  - `double`双线

- `border-style: solid dotted dashed double;`

- 某一边的样式`border-xxx-style: solid;` 其中xxx表示`top`、`right`、` bottom `、`left`

大部分浏览器中，边框的宽度和颜色都是有默认值的，而边框的样式默认值都是 `none`

- **简写** `border: 10px red solid;` 没顺序要求，不能分别指定四边

- 单独指定边：`border-xxx: 10px red solid;` 其中xxx表示`top`、`right`、` bottom `、`left`

(3) 内边距：指的是从边框到内容的距离

- `padding-xxx: 10px;` 分别指定四个内边距 ，其中xxx表示`top`、`right`、` bottom `、`left`

- `padding: 10px 20px 30px 40px;` 和上面类似(四个值、三个值……)

盒子可见框的大小由内容区、内边距、边框决定

(4) 外边距是当前盒子与其他盒子之间的距离，不会影响可见框的大小，而是影响盒子的位置

- 分别设置四面外边距 `margin-xxx: 10px;` 其中xxx表示`top`、`right`、` bottom `、`left`

还可以设置为 `auto`，一般设置在水平方向，如 `margin: 0 auto;`

如果只给左右设置 `auto`，那么那侧值会变成最大

- 垂直方向，外边距默认就是 0

- 如果左右同时设置为 auto，两侧外边距会设置为相同值，就可以使元素自动在父元素中居中 `margin: 0 auto;`

**※ 垂直外边距的重叠**：

- 在网页中**垂直方向**的**相邻外边距**会发生外边距的重叠，即兄弟元素之间相邻外边距会**取最大值**而不是取和。

- 如果父子元素的**垂直外边距相邻**了，则子元素的外边距会设置给父元素

可以使用 border 和 padding 隔开相邻，但需要将其长度从内容宽高中去掉

浏览器为了在页面中没有样式时，也可以有一个比较好的现实效果，所以为很多的元素都设置了一些默认的 margin 和 padding，而我们往往都是不需要的，因此要去掉

清除浏览器的默认样式：

```css
*{
  margin: 0; 
  padding: 0;
}
```

内联元素盒子 `<span></span>`

内联元素不能设置宽高，可以设置水平方向的内边距，可以设置垂直方向的内边距(但不会影响页面布局)，可以设置边框(垂直的还是不会影响页面布局)，支持水平方向外边距，不支持垂直外边距

通过 `display` 样式可以修改元素的类型

可选值：

- `inline`: 内联元素

- `block`: 块元素

- `inline-block`: 行内块元素(有两者的特点，支持宽高，不独占一行)例如img

- `none`：不会显示，并且元素不会在页面中继续占有位置

还有隐藏元素的方式

- `visibility: visible;` 隐藏和显示 (默认显示)

- `hidden` 隐藏 不显示但还是**占位置**

- `opacity: 0;` 透明度为0

子元素默认是存在于父元素的内容区中，理论上子元素的最大可以等于父元素内容区的大小。如果子元素的大小超过了父元素的内容区，则超过的大小会在父元素以外的位置显示，超出父元素的内容，我们称为溢出的内容。通过 overflow 可以设置父元素如何处理溢出内容。

`overflow: visible;` 默认在外面显示

- hidden 溢出内容会被修剪，不会显示

- scroll 为父元素添加滚动条，可以通过滑动滚动条查看，不论是否溢出均会添加滚动条

- auto 根据需求自动添加滚动条

## 八、布局

### 1、概念

文档：就是一个网页

文档流：处在网页的最底层，它表示的是一个页面中的位置。我们创建的元素默认都处在文档流中。

元素在文档流中的特点：

块元素：独占一行(自上向下排列)。块元素默认宽度是父元素的100%。块元素的默认高度被内容/子元素撑开。

内联元素：只占自身大小，会默认自左向右排列。如果一行中不足以容纳所有的内联元素，则换到下一行，继续自左向右。在文档流中，内联元素的宽度和高度默认都被内容撑开。

当元素的宽度的值设置为auto时，此时指定内边距不会影响可见框的大小，但是会自动修改宽度，以适应内边距。

块元素在文档流中默认垂直排列，自上向下依次排开。

如果希望块元素在页面中水平排列，可以使块元素**脱离文档流**

### 2、浮动

`float: none;` 默认值，不浮动

- left 元素脱离文档流，向左侧浮动

- right 脱离文档流，向页面右侧浮动

当为一个元素设置浮动以后，元素会**立即脱离文档流**，元素脱离文档流以后，它下边的元素会立即向上移动。

元素浮动以后，会尽量向页面的左上或者右上浮动，直到遇到父元素的边框或其他的浮动元素。

如果浮动元素上边是一个没有浮动的块元素，则浮动元素不会超过块元素。

浮动的元素不会超过他上边的兄弟元素，最多和他一边齐

浮动的元素不会盖住文字，文字会自动**环绕**在浮动元素的周围，所以我们可以使用浮动来设置文字环绕图片的效果。

**块元素脱离文档流以后，高度和宽度都被内容撑开。内联元素脱离文档流以后，会变成块元素。**浮动之后不区分内联、块元素。

学完盒模型和浮动就可以完成大部分的布局了，布局分为固定布局和自适应布局

- 固定布局：网页大小固定不变，不随设备不同改变
- 自适应布局(响应)：根据浏览器屏幕不同，布局发生改变

利用浮动进行简单布局

![](https://cdn.wallleap.cn/img/pic/illustration/20200811150253.jpg)

注：盒子套盒子，垂直摆放 div，水平摆放 float，看好宽高不越界，水平居中 `margin: 0 auto;`

![](https://cdn.wallleap.cn/img/pic/illustration/20200811150237.jpg)

我们做一下上面这个效果：

```html
<style>
  *{
    margin: 0;
    padding: 0;
  }
  body{
    min-width: 1200px;
  }
  .container{
    width: 1200px;
    margin: 0 auto;
  }
  header{
    width: 100%;
    height: 18vh;
    background-color: green;
  }
  footer{
    width: 100%;
    height: 18vh;
    background-color: #ddd;
  }
  main{
    width: 100%;
    height: 62vh;
    background-color: orange;
    margin: 1vh 0;
  }
  nav{
    float: left;
    width: 250px;
    height: 100%;
    background-color: skyblue;
  }
  article{
    float: left;
    width: 680px;
    height: 100%;
    background-color: #fffe03;
    margin: 0 10px;
  }
  aside{
    float: left;
    width: 250px;
    height: 100%;
    background-color: pink;
  }
</style>
<div class="container">
  <header></header>
  <main>
    <nav></nav>
    <article></article>
    <aside></aside>
  </main>
  <footer></footer>
</div>
```

甚至还可以嵌套更多：

![](https://cdn.wallleap.cn/img/pic/illustration/20200811153407.jpg)

### 3、高度塌陷问题

(1) 问题说明

在文档流中，父元素的高度默认被子元素撑开，即父元素不设置高度，子元素多高，父元素就有多高。但是当为**子元素设置浮动**以后，子元素会完全脱离文档流，此时将会导致**子元素无法撑起父元素的高度**，导致**父元素高度塌陷**，父元素下的所有元素都会向上移动，这样会导致**网页布局混乱**。

可以将父元素写死，但是父元素的高度将不能自动适应子元素的高度，不建议使用

(2) BFC

根据W3C标准，页面中元素都有一个隐含的属性交Block Formatting Contex(BFC，块级格式化上下文)，该属性可以设置打开，默认关闭

当开启元素的BFC以后，元素将会具有如下的特性：

- 父元素的垂直外边距不会和子元素重叠

- 该元素不会被浮动元素所覆盖

- 该元素可以包含浮动的子元素

间接**开启BFC**

- 设置元素**浮动**   父元素、子元素都浮动 使用这种方式，可以撑开父元素，但是父元素的宽度会丢失，也会导致下边的元素上移，不推荐

- 设置元素**绝对定位**

- 设置元素为**inline-block** 宽度也会丢失，不推荐

- 将元素的**overflow**设置一个非visible的值

`overflow: auto;`

将**overflow设置为`hidden`**是副作用最小的开启BFC的方式。IE6不支持，IE6具有另一个隐含属性hasLayout，与BFC类似，开启hasLayout副作用最小的**zoom设置为1**即可 放大1倍

zoom 只在 IE 中支持，由于 css 不对的那条将会直接忽略，因此可以两种都写上

利用 float 写导航条

```html
<style>
  *{
    margin: 0;
    padding: 0;
  }
  .nav{
    width: 1000px;
    margin: 50px auto;
    list-style: none;
    background-color: #bfa;
    overflow: auto;
    zoom: 1;
  }
  .nav li{
    float: left;
    width: 249px;
    height: 30px;
    line-height: 30px;
    text-align: center;
    background-color: #6495ed;
    
  }
  .nav li:not(:last-of-type){
    border-right: 1px solid #ddd;
  }
  .nav li a{
    display: block;
    width: 100%;
    height: 100%;
    text-decoration: none;
    font-weight: bold;
  }
  .nav li a:hover{
    background-color: #cc0000;
  }
</style>
<ul class="nav">
  <li><a href="#">首页</a></li>
  <li><a href="#">新闻</a></li>
  <li><a href="#">联系</a></li>
  <li><a href="#">关于</a></li>
</ul>
```

### 4、清除浮动

有时希望清除其他元素浮动对当前元素产生的影响，可以使用 clear

`clear: none;` 默认值，不清除浮动影响

- left 清除左侧浮动元素对当前元素的影响

- right 清除右侧……

- both 清除两侧……实际是清除对它影响最大的那个

可以在高度塌陷的父元素的最后，添加一个撑开父元素的空白div，对其进行清除浮动，但是添加了一个无用的结构，因此可以借用伪类：

```css
.clearfix:after{
  content:””;
  display: block;
  clear:both;
}
.clearfix{zoom:1;} /*IE6*/
```

父元素多加一个类名 clearfix

### 5、高度塌陷最终解决方案

经过修改后的 clearfix 是一个多功能的，既可以解决高度塌陷，又可以确保父元素和子元素的垂直外边距不会重叠

为父元素添加类名 `clearfix`

```html
<div class="parent clearfix">
  <div class="child"></div>
</div>
```

添加样式

```css
.clearfix:before,.clearfix:after{
  content: '';
  display: table;
  clear: both;
}
.clearfix{
  zoom: 1;
}
```

### 6、定位

定位：将指定的元素摆放到页面的任意位置

`position: static;` 默认值，元素没有开启定位

- relative 开启元素的相对定位

- absolute 绝对定位

- fixed 固定定位

当开启了元素的定位，可以通过left、right、top、bottom四个属性来设置元素的偏移量，通常偏移量只使用两个就可以对一个元素进行定位，水平一个+垂直一个

相对定位

- 开启了相对定位，而不设置偏移量时，元素不会发生任何变化

- 相对定位是相对于元素在文档流中**原来的位置**进行定位

- 相对定位的元素不会脱离文档流

- 相对定位会使元素**提升一个层级**(覆盖底下的)

- 相对定位不会改变元素的性质，块还是块，内联还是内联

绝对定位

- 开启绝对定位会使元素**脱离文档流**

- 开启绝对定位如果不设置偏移量，元素位置不会发生变化

- 绝对定位是相对于离他最近的开启了定位的祖先元素进行定位的(一般情况，开启了子元素的绝对定位，会同时开启父元素的相对定位)；如果所有的祖先元素没有开启定位，则相对于浏览器窗口进行定位  

- 绝对定位会使元素提升一个层级

- 绝对定位会改变元素的性质，内联元素变成块元素，块元素的宽度和高度默认都被内容撑开

固定定位

固定定位也是一种绝对定位，它的大部分特点都和绝对定位一样，不同的是：

- 固定定位永远都会相对于浏览器窗口进行定位

- 固定定位会固定在浏览器窗口的某个位置，不会随滚动条滚动

IE6不支持固定定位

元素的层级

如果定位元素的层级是一样的，则下边的元素会盖住上边的

通过`z-index`属性可以用来设置元素的层级

可以为`z-index`指定一个正整数作为值，该值将会作为当前元素的层级，层级越高，越优先显示

- 对于没有开启定位的元素不能使用z-index

- 父元素的层级再高，也不会盖住子元素

## 九、背景

### 1、设置元素的透明背景

`opacity: 1;` 0~1之间的值 

- 0完全透明
- 1完全不透明
- 0.5半透明

IE8及以下的浏览器不支持，可以使用`filter: alpha(opacity=50);` 透明度0~100 

### 2、背景颜色

`background-color: red;` 背景色，色值支持所有的颜色值

`background-color: transparent` 背景完全透明

`background-color: currentColor` 背景色为文字色，一般不会这样用，否则文字完全看不清了

### 3、背景图

(1) 添加背景图片

`background-image: url(../img/1.jpg);`

- 如果背景图片大于元素，默认会显示图片的左上角

- 如果背景图片与元素一样大，则背景图片将会完全显示

- 如果背景图片小于元素大小，则会默认将背景图片平铺以充满元素

- 可以同时为一个元素指定背景颜色和背景图片，这样背景颜色将会作为背景图片的底色，一般情况下设置背景图片时都会同时指定一个背景颜色

(2) 图片平铺

`background-repeat: repert;` 默认值，背景图片会双方向重复(平铺)

- no-repeat  背景图片不会重复

- repeat-x  背景图片沿水平方向重复

- repeat-y  背景图片沿垂直方向重复
- round 会将图片缩放之后进行平铺
- space 产生相同的间距

(3) 图片位置

`background-position: 0% 0%;` 默认值，图片在左上角显示，水平 垂直

- center center  只给一个值，第二个值默认为center

- 1% 1%  左上角是0% 0%，右下角是100% 100%，只给一个值，第二个值默认为50%

- 10px 0px 只设置一个值，另一个值将是50%

(4) 图片滚动

`background-attachment: scroll;` 默认值，背景图片随着页面一起滚动

- fixed; 背景图片固定在某个位置，不随页面滚动。背景图片定位永远相对于浏览器窗口。

```css
/* 容器滚动时，背景图片动作 */
background-attachment: fixed; 背景图片位置固定不变
background-attachment: scroll; 跟随滚动
/* 当前容器滚动时 */
background-attachment: scroll; 不会随内容一起滚动
background-attachment: local; 跟随滚动
```

在IE6中对图片格式png24支持度不高，如皋使用的图片格式是png24，则会导致透明效果无法正常显示。

- 可以使用png8代替png24，图片清晰度会下降。

- 使用JavaScript解决，在body标签的最后引入js文件

```html
<!--[if IE 6]>
<script src="https://cdn.bootcdn.net/ajax/libs/dd_belatedpng/0.0.8/dd_belatedpng.min.js"></script>
<script>
    DD_belatedPNG.fixed(“div,img”); // 选择器
</script>
<![endif]-->
```

### 4、精灵/雪碧图(CSS-Sprite)

先看需求：给超链接和按钮设置背景图片、宽高、`:link`、`:hover`、`:active`

设置完成之后会发现第一次切换图片的时候，会发现图片有一个非常快的闪烁，这个闪烁会造成一次不佳的用户体验。

产生问题的原因：

背景图片是以外部资源的形式加载进网页的，浏览器每加载一个外部资源就需要单独地发送一次请求，但是我们外部资源并不是同时加载，浏览器会在资源被使用时才去加载资源。在这个案例中，一上来浏览器只会加载`link.png`，由于hover和active的状态没有马上出发，所以hover.png、active.png并不是立即加载的；只有当hover、active被触发时浏览器才去加载hover.png、active.png；由于加载图片需要一定的时间，所以在加载和显示过程会有一段时间，背景图片无法显示，导致出现闪烁的情况。

解决方案：图片整合技术(CSS-Sprite)，将所有的小的背景素材放到同一张图片中，利用`background-position`进行位置调整得到想要的素材。

优点：

- 将多个图片整合为一张图片，浏览器只需要发送一次请求，可以同时加载多个图片，提高访问效率，优化了用户体验

- 减小了图片的总大小

### 5、背景图片简写属性

例如：

```css
background-color: #bfa; /* 设置一个背景颜色 */
background-image: url(img/pic.png); /* 设置一个背景图片 */
background-repeat: no-repeat; /* 设置背景图片是否平铺 */
background-position: center center; /* 设置背景图片的位置 */
background-attachment: fixed; /* 设置背景图片不随滚动条滚动 */
```

简写

```css
background: #bfa url(../img/1.png) center center no-repeat fixed;
```

没有顺序要求，没有数量要求，不设置采用默认值

## 十、CSS Hack

有一些情况，有一些特殊的代码我们只需要在某些特定的浏览器中执行，而在其他的浏览器中不需要执行，这时就可以使用CSS Hack来解决该问题

CSS Hack实际上指的是一个特殊的代码，这段代码只在某些浏览器中可以识别，而其他浏览器都不能识别，通过这种方式，来为一些浏览器设置特殊的代码

### 1、条件Hack

![img](https://cdn.wallleap.cn/img/pic/illustration/20200811175041.gif)

条件Hack只对IE浏览器有效，其他的浏览器都会将它识别为注释，IE10及以上的浏览器已经不支持这种方式

```html
<!--[if IE]>
  <p>这是IE6</p>
<![endif]-->
<!--[if IE 6]>
  <p>这是IE6</p>
<![endif]-->
<!--[if IE 8]>
  <p>这是IE8</p>
<![endif]-->
<!--[if lte IE 9]>
  <p>您使用的浏览器是IE及以下的</p>
<![endif]-->
```

`lt` 小于 `gt`大于 `lte`小于等于

可以利用条件Hack，为IE浏览器单独引入样式

```html
<link rel="stylesheet" href="style.css">
<!--[if IE 8]>
  <link rel="stylesheet" href="style-ie8.css">
<![endif]-->
```

### 2、属性级Hack

![img](https://cdn.wallleap.cn/img/pic/illustration/20200811175712.gif)

![img](https://cdn.wallleap.cn/img/pic/illustration/20200811175725.gif)

### 3、选择符级Hack

![img](https://cdn.wallleap.cn/img/pic/illustration/20200811175741.gif)

 CSS Hack不到万不得已的情况尽量不要使用

## 十一、CSS3中其他属性

上面提到过CSS3中的选择器、盒模型、颜色，这里讲一下其他的

### 1、文本阴影(text-shadow)

`text-shadow: none | <length> none | [<shadow>,]*<shadow> 或 none | <color> [,<color>]*`

即：

`text-shadow: [颜色(color) x轴(X Offset) y轴(Y Offset) 模糊半径(Blur)],[颜色 x轴 y轴 模糊半径],……`

或

`text-shadow: [x轴 y轴 模糊半径 颜色],[x轴 y轴 模糊半径 颜色],……`

例如：

```css
div{
  text-shadow: -2px -2px 5px red;
  /* text-shadow: 0px 0px 30px #fff;
  text-shadow: 0px 0px 30px #fff,
               0px 0px 50px red,
               0px 0px 70px #fff;
  text-shadow: 0px 1px 0px #fff;
  text-shadow: -1px -1px 0px #fff,
               -2px -2px 0px #eee,
               -3px -3px 0px #ddd,
               -4px -4px 0px #ccc;
  text-shadow:  0 0 8px hsla(30,100%,40%,1); */
}
```

### 2、边框圆角

`border-radius: 值;`

单独设置，`border-xxx-radius` 设置不同方向

整合写为 `border-radius: 左上 右上 右下 左上;`

两个值：左上/右下 右上/左下;

三个值：左上 右上/左下 右下;

设置不同方向的半径值 水平/垂直

`border-radius: 100px/50px;`

`border-radius: 100px 80px 50px 30px/20px 30px 40px 50px;`

### 3、渐变

渐变是CSS3中比较丰富多彩的一个特性，通过渐变我们可以实现许多绚丽的效果，有效减少图片的使用数量，并且具有很强的适应性和可扩展性。

(1) 线性渐变

`linear-gradient([<point> || <angle>,]?<stop>,<stop>[,<stop>]]*)`

- 第一个参数表示线性渐变的方向
  - to left：设置渐变从右到左，相当于270deg
  - to right：设置渐变从左到右，相当于90deg
  - to top：设置渐变从下到上，相当于0deg
  - to bottom：设置渐变从下到上，相当于180deg，这个是默认值，等同于留空不写
  - 还可以指定度数，如45deg
- 第二个参数是起点颜色，可以指定颜色的位置
- 第三个参数是终点颜色，可以在后面添加更多的参数，表示多种颜色的渐变

例如：

```css
background: linear-gradient(40deg, red 0%, red 10%, orange 12%, orange 15%, yellow 25%, green, blue, pink 60%);
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200811185826.png)

(2) 径向渐变

`radial-gradient([[<shape>||<size>] [at <position>]? , | at <position>,]?<color-stop>[,<color-stop>]+)`

- position：确定圆心的位置。如果提供两个参数，第一个表示横坐标，第二个表示纵坐标；如果只提供一个，第二值默认为50%，即center
- shape：渐变的形状，ellipse表示椭圆形，circle表示圆形。默认为ellipse，如果元素的形状为正方形，啧ellipse和circle显示一样
- size：渐变的大小，即渐变到哪里停止，它有四个值。closest-side：最近边，farthest-side：最远边，closest-corner：最近角，farthest-corner：最远角。默认是最远角farthest-corner
- color：指定颜色

```css
background: radial-gradient(red, blue)
background: radial-gradient(ellipse, red, blue) 或者circle(在非正方形中有区别，circle不会压缩、ellipse会压缩) 形状
background: radial-gradient(at 50px 50px, red, blue) 位置(坐标)
background: radial-gradient(circle closest-corner at 50px 50px, red, blue) 大小
background: radial-gradient(red, red 50%, blue 50%, blue)
```

(3) 重复渐变

```css
background: repeating-linear-gradient(45deg, #fff 0%, #fff 10%, #000 10%, #000 20%)

background: repeating-radial-gradient(circle at center center, #fff 0%, #fff 10%, #000 10%, #000 20%)
```

### 4、背景样式

设置背景图片的大小

`background-size`: `auto`(原始图片大小) || number(数值) || percentage(百分比) || `cover`(放大铺满) || `contain`(缩小铺满)

`background-size: 300px 500px` 同时设置宽高，建议保持与图片同比例，否则会造成图片失真变形

`background-size: 300px;` 只设置宽度，高度auto也是一种选择(图片会保持比例自动缩放)

设置百分比是参照父容器可放置内容区域的百分比`background-size: 50% 50%`

设置`contain`：按比例调整图片大小，使用图片宽高自适应整个元素的背景区域，使图片全部包含在容器中

- 图片大于容器：有可能造成容器的空白区域，将图片缩小
- 图片小于容器：有可能造成容器的空白区域，将图片放大

设置`cover`：与contain刚好相反，背景图片会按比例缩放至适应整个背景区域，如果背景区域不足以包含所有背景图片，图片内容会溢出

- 图片大于容器：等比例缩小，会填满整个背景区域，有可能造成图片的某些区域不可见
- 图片小于容器：等比例放大，填满整个背景区域，图片有可能造成某个方向上内容的溢出

一般轮播图就使用cover，方便在不同分辨率下显示完全

![](https://cdn.wallleap.cn/img/pic/illustration/20200811200801.png)

精灵图的部分使其居中并且放大，提升相应区域

![](https://cdn.wallleap.cn/img/pic/illustration/20200811200923.png)

### 5、边框背景图片

如下图所示，将图片等分为9个区域，将会和div平分为九个区域之后的格子一一对应

![](https://cdn.wallleap.cn/img/pic/illustration/20200811202120.png)

```css
div {
  margin: 20px auto;
  width: 300px;
  height: 300px;
  border: 54px solid red;
  /* 添加边框图片 */
  /* border-image-source：可以指定边框图片的路径，默认知识填充到容器的四个角 */
  border-image-source: url('img/borderbg.jpg');
  /* 让它成为九宫格：border-imgage-slice：设置四个方向上的裁切距离, fill：做内容的内部填充 */
  border-image-slice: 54 fill;
}
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200811202858.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811202922.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811202930.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811202943.png)

案例：按钮变形(上、右、下、左不变形，中间拉伸)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811203003.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811203014.png)

如果是纹理、渐变的背景，需要设置round或repeat(纯色可以默认stretch)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811203027.png)

### 6、过渡

通过过渡transition,我们可以在不使用Flash 动画或JavaScript 的情况下，当元素从一种样式变换为另一种样式时为元素添加效果.要实现这一点，必须规定两项内容: 1.规定希望把效果添加到哪个CSS属性上，2.规定效果的时长

(1) 语法:

`transition: property duration timing-function delay;`

(2)参数说明:

transition属性是-一个简写属性，用于设置四个过渡属性:

| 值                         | 描述                            |
| -------------------------- | ------------------------------- |
| transition-property        | 规定设置过渡效果的CSS属性的名称 |
| transition-duration        | 规定完成过渡效果费多少秒或毫秒  |
| transition-timing-function | 规定速度效果的速度曲线          |
| transition-delay           | 定义过渡效果何时开始            |

(3) 补充说明tansition-timing-function:属性规定过渡效果的速度曲线

| 值                            | 描述                                                         |
| :---------------------------- | :----------------------------------------------------------- |
| linear                        | 规定以相同速度开始至结束的过渡效果（等于 cubic-bezier(0,0,1,1)）。 |
| ease                          | 规定慢速开始，然后变快，然后慢速结束的过渡效果（cubic-bezier(0.25,0.1,0.25,1)）。 |
| ease-in                       | 规定以慢速开始的过渡效果（等于 cubic-bezier(0.42,0,1,1)）。  |
| ease-out                      | 规定以慢速结束的过渡效果（等于 cubic-bezier(0,0,0.58,1)）。  |
| ease-in-out                   | 规定以慢速开始和结束的过渡效果（等于 cubic-bezier(0.42,0,0.58,1)）。 |
| cubic-bezier(*n*,*n*,*n*,*n*) | 在 cubic-bezier 函数中定义自己的值。可能的值是 0 至 1 之间的数值。 |

cubic-bezier 函数可以到[这个网站](https://cubic-bezier.com/#.17,.67,.83,.67)上查看

`steps(<integer>[,start| end]?) <integer>`：用于指定间隔个数（该值只能是正整数） 第二个参数可选，默认是end,表示开始值保持一次，若参数为start，表示开始值不保持

step-start: 直接位于结束处。相当于steps(1,start)

step-end: 位于开始处经过时间间隔后结束。相当于steps(1,end)

(4) eg: 点击之后移动到某位置，显示移动过程

![](https://cdn.wallleap.cn/img/pic/illustration/20200811205702.png)

简写：`transition: 属性名称 过渡时间 时间函数 延迟`

即

```css
transition: left 2s linear 0s;
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200811205845.png)

(5) 使用建议

因为transition最早是由webkit内核河克确提出来的，moila和opera都量最近版本才支持这个属性，而IE浏览器是不支持，另外由于各大现代浏览器firefox、Safari、Chrome、Opera都还不支持W3C的标准，所以在应用transition时有必要加上各自的前缀（可以由 webpack 等自动加上）

```css
-moz-transition: all 5s ease 1s;
-webkit-transition: all 1s ease 1s;
-o-transition: all 1s ease 1s;
transition: all 1s ease 1s;
```

### 7、 transform

通过CSS3 transform 转换，我们能够对元素进行移动、缩放、旋转、斜切等操作。

(1) 2D移动 translate()

使用translate()函数,你可以把元素从原来的位置移动，移动参照元素左上角原点

- 语法: translate(tx) I translate(tx,tE)
- tx是一个代表X轴(横坐标)移动的向量长度，当其值为正值时，元素向X轴右方向移动，反之其值为负值时，元素向X轴左方向移动。
- ty是一个代表 Y轴(纵向标)移动的向量长度，当其值为正值时，元素向Y轴下方向移动，反之其值为负值时，元素向Y轴上方向移动。如果ty没有显式设置时,相当于ty=0。
- 也可以使用translateX(x)或者translateY(ty)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811211227.png)

(2) 2D缩放: scale()

缩放scale()函数让元素根据中心原点对对象进行缩放。
默认的值1，因此0.01到0.99之间的任何值都会使一个元素缩小；而任何大
于或等于1.01 的值都会让元素显得更大。缩放是参照元素中心点。

- 语法: scale(sx|ty) | scale(sx,sy)
- sx: 用来指定横向坐标(X轴)方向的缩放向量，如果值为0.01~0.99之间，会让对象在X轴方向缩小，如果值大于或等于1.01，对象在Y轴方向放大。
- sy: 用来指定纵向坐标(Y轴)方向的缩放量，如果值为0.01~0.99之间，会让对象在Y轴方向缩小，如果值大于或等于1.01，对象在Y轴方向放大
- 也可以使用scaleX(sx)或者scaleY(sy)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811211659.png)

(3)2D旋转: rotate()

旋转rotate()函数通过指定的角度参数对元素根据对象原点指定一个2D旋转。它主要在二维空间内进行操作，接受一个角度值，用来指定旋转的幅度。如果这个值为正值，元素相对原点中心顺时针旋转；如果这个值为负值，元素相对原点中心逆时针旋转

- 语法: rotate(a)
- a: 代表的是一个旋转的角度值。 其取值可以是正的,也可以是负的。
  如果取值为正值时，元素默认之下相对元素中心点顺时针旋转；如果
  取值为负值时，元素默认之下相对元素中心点逆时针旋转

![](https://cdn.wallleap.cn/img/pic/illustration/20200811211907.png)

(4) 2D斜切: skew()

能够让元素倾斜显示。它可以将一个对象以其中心位置围绕看X轴和Y轴按照一定的角度倾斜。这与rotate()函数的旋转不同，rotate()函数只是旋转，而不会改变元素的形状。skew()函数不会旋转，而只会改变元素的形状

- 语法:skew(ax) | skew(ax,ay)
- ax：用来指定元素水平方向(X轴方向)倾鈄的角度。
- ay：用来指定元素垂直方向(Y轴方向)倾斜的角度。如果未显式的设置这个值,其默认为
- 也可以使用 skewX(sx)或者skewY(sy)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811212119.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811212128.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811212138.png)

同时设置多个transform属性值

```css
transform: translateX(700px) rotate(-90deg);
```

注意书写顺序

![](https://cdn.wallleap.cn/img/pic/illustration/20200811212258.png)

备注：可利用定位和translate实现任意元素居中

定位中left、top的百分比是参照父容器的宽高

translate的百分比是参照元素本身的宽高

### 8、3D转换

三维变换使用基于二维变换相同的属性，可以让我们基于三个坐标方向对元素进行变换。

(1) 3D移动
方法：translate3d(x, y, z)使元素在这三个维度中移动，也可以分开写.如:
translateX(length)，translateY(length)，translateZ(length)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811212650.png)

(2) 3D缩放
scale3d(number,number,numben)使元素在这三个纬度中缩故，也可分开写，
如: scaleX()，scaleY()，scalZ()

![](https://cdn.wallleap.cn/img/pic/illustration/20200811212837.png)

(3) 3D旋转

- rotate3d(x, y, z, angle) ，指定需要进行旋转的坐标轴
- rotatX(angle) 是元素依照x轴旋转;
- rotateY(angle) 是元素依照y轴旋转;
- rotateZ(angle) 是元素依照z轴旋转

![](https://cdn.wallleap.cn/img/pic/illustration/20200811213004.png)

### 9、透视/景深

左手法则：大拇指指向当前坐标轴的下方向，手指环绕的方向就是正方向

- perspective(length) 为一个元素设置三维透视的距高。仅作用于元素的后代，而
  不是其元素本身。当perspective:none/0时，相当于没有设perspetive(length)， 比如你要建立一个小立方体，长宽高都是200px，如果你的perspective< 200px，那就相当于站在盒子里面看的结果，如果perspective非常大那就是站在非常远的地方看(立方体已经成了小正方形了) ， 意味着perspective属性指定了观察者与z=0平面的距离，使具有三维位置变换的元素产生透视效果
- perspective-origin属性规定了镜头在平面上的位置，默认是放在元素的中心
- tasom-style：使被蠡换的子元素保留其3D转换需要设置在父元素中

| 值         | 描述                             |
| ---------- | -------------------------------- |
| flat       | 子元素将不保留其3D位置中面方式。 |
| preseve-3d | 子元素将保留其3D位置-立体方式。  |

### 10、 动画

![](https://cdn.wallleap.cn/img/pic/illustration/20200811213732.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811213740.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811213749.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811213757.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811213808.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811213815.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811213823.png)

### 11、 Web字体、字体图标

开发人员可以为自己的网页指定特殊的字体，无序考虑用户电脑上是否安装了此特殊字体

(1) 字体格式

不同浏览器所支持的字体格式不同

![](https://cdn.wallleap.cn/img/pic/illustration/20200811204306.png)

获取这些种类的字体文件：

<https://www.iconfont.cn/webfont?spm=a313x.7781069.1998910419.d81ec59f2#!/webfont/index>

选中一种字体-本地下载-解压-根据demo在自己的项目中使用字体

```html
<style>
  @font-face{
    font-family: ‘字体名’,
    src: url(‘路径/字体文件’);
    src: url(‘路径/字体文件’) format(‘格式’),
    url……
  }
  .myFont{
    font-family: 上面的字体名’
  }
</style>
<span class=”myFont>之前生成的文字</span>
```

注意：

- 得自定义想生成对应字体文件的内容

- 使用网络资源生成web字体

- 使用：
  - 定义自定义字体
  - 定义样式使用自定义字体
  - 指定样式，调用样式

(2) 字体图标

常见的就是把网页常用的一些小图标，借助工具生成一个字体包，然后就可以像使用文字一样使用图标了

优点

- 将所有图标打包成字体库，减少请求
- 具有矢量性，可保证清晰度
- 使用灵活，便于维护

fonticon 或者 fontawsome

## 十二、多列布局和弹性(伸缩)布局

### 1、多列布局

![](https://cdn.wallleap.cn/img/pic/illustration/20200811203754.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811203747.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811203737.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811203729.png)

### 2、伸缩布局

传统布局方式的局限：

![](https://cdn.wallleap.cn/img/pic/illustration/20200811203624.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811203602.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811203554.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811203546.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811203528.png)

d 中的所有属性都是在子元素中设置的

![](https://cdn.wallleap.cn/img/pic/illustration/20200811203446.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811203455.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811203503.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811203511.png)

案例：弹性导航栏

![](https://cdn.wallleap.cn/img/pic/illustration/20200811203410.png)

案例：宽高自动适应

![](https://cdn.wallleap.cn/img/pic/illustration/20200811203322.png)

```html
<div class="layout">
  <header>header</header>
  <main>
    <aside>left</aside>
    <article>right</article>
  </main>
  <footer>footer</footer>
</div>
<style>
*{
  margin: 0;
  padding: 0;
}
.layout{
  width: 500px;
  height: 600px;
  background-color: #ccc;
  margin: 10px auto;
  /* 设置父容器为伸缩盒子 */
  display: flex;
  /* 修改主轴方向 */
  flex-direction: column;
}
header{
  width: 100%;
  height: 60px;
  background-color: red;
}
main{
  width: 100%;
  background-color: green;
  /* 让当前伸缩项占据父容器的剩余空间 */
  flex: 1;
  /* 让main称为弹性盒子 */
  display: flex;
}
main > aside{
  height: 100%;
  flex: 1;
  background-color: pink;
}
main > article{
  height: 100%;
  flex: 3;
  background-color: purple;
}
footer{
  width: 100%;
  height: 80px;
  background-color: blue;
}
</style>
```

### 3、网格布局

```css
.container {
  display: grid;
}
```

jQuery全屏滚动插件

http://www.jq22.com/jquery-info1124

## 十三、其他

### 1、重置样式表和默认样式表

![](https://cdn.wallleap.cn/img/pic/illustration/20200811214420.gif)

### 2、对元素 id 和 class 还有文件的命名规范

![](https://cdn.wallleap.cn/img/pic/illustration/20200811214431.gif)

### 3、设置指针

`cursor: point;`

### 4、解决 IE6 双边距

![](https://cdn.wallleap.cn/img/pic/illustration/20200811214441.gif)

![](https://cdn.wallleap.cn/img/pic/illustration/20200811214449.gif)

### 5、利用 jsCssZip 对 CSS、js 压缩
