---
title: 使用 CSS 计数器更改有序列表序号样式
date: 2022-10-13 17:18
updated: 2022-10-13 17:18
cover: //cdn.wallleap.cn/img/pic/illustrtion/202210131442411.jpg
category: 技术杂谈
tags:
  - web
  - 前端
description: 使用 CSS 计数器更改有序列表序号样式
---

**CSS 计数器**可让你根据内容在文档中的位置调整其显示的外观。例如，你可以使用计数器自动为网页中的标题编号，或者更改有序列表的编号。

文档：[CSS Counter Styles](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Counter_Styles)

## 使用计数器

例如：生成 HTML，四个 Section，包裹着 `h3` 和 `p`

```html
article>section*4>h2{Section}+(h3{话题}+p{段落111111111}+p{段落aaaaaaaaaaaaaa})*4
```

![HTML](https://cdn.wallleap.cn/img/pic/illustrtion/202210121755148.png)

### 1、使用 `counter-reset` 属性初始化计数器的值

在使用计数器之前，需要使用 [`counter-reset`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/counter-reset) 属性来初始化它的值。这个属性也可用于指定计数器的初始值。

#### 正序计数器

`counter-reset` 属性值为 `计数器名称 初始值`，初始值不指定则为 0

例如，将名为 `section` 的计数器初始化为默认值（`0`），将名为 `topic` 的计数器初始化为 `-13`， 将名为 `paragraph` 的计数器初始化为 `1`：

```css
counter-reset: section;
counter-reset: topic -13; /* 中间空格隔开 */
counter-reset: paragraph 1;
```

也可以同时初始化多个计数器，并指定其初始值：

```css
article {
  counter-reset: section topic -13 paragraph 1;
}
```

#### 反向计数器

反向计数器可以通过在 [`counter-reset`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/counter-reset) 属性中将计数器的名称使用 `reversed()` 函数包裹来创建，大多用于有序列表反转编号

```css
counter-reset: reversed(topic) 2;
```

目前 `reversed()` 兼容性好像不太好，这里就不添加了

![兼容性](https://cdn.wallleap.cn/img/pic/illustrtion/202210130954165.png)

> 计数器只能在可以生成盒子的元素中使用（设值或重设值、递增）。例如，如果一个元素被设置为了 `display: none`，那么在这个元素上的任何计数器操作都会被忽略。
>
> 计数器的名称不可以为 `none`、`unset`、`inherit` 或 `initial`，否则，相应的声明会被忽略。

### 2、计数器可通过 `counter-increment` 属性指定其值为递增或递减

在初始化之后，计数器的值就可以使用 [`counter-increment`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/counter-increment) 来指定其为递增或递减，可以在计数器的名称后指定单次递增或递减的值（正数或负数）：

```css
section h2 {
  counter-increment: section; /* 默认以 1 增加 */
}
section h3 {
  counter-increment: topic 1; /* 可以手动指定增加的数值 */
}
section p {
  counter-increment: paragraph -2; /* 可以是负数 */
}
```

如果是同一个选择器，也可写成：

```css
counter-increment: section topic 1 paragraph -2;
```

### 3、当前计数器的值通过 `counter()` 或 `counters()` 函数显示出来

这两个函数通常在[伪元素](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Pseudo-elements)的 [`content`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/content) 属性中使用。

当不需要包含父级上下文的编号，而仅需要嵌套内容的编号时，应使用 [`counter()`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/counter) 函数；当需要同时包含父级上下文和嵌套内容的编号时，应使用 [`counters()`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/counters) 函数（一般在有序列表或目录中使用）。

[`counter()`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/counter) 函数有两种形式： `counter(<counter-name>)` 和 `counter(<counter-name>, <counter-style>)`。生成的文本是伪元素范围内指定名称的最内层计数器的值。

[`counters()`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/counters) 函数也同样有两种形式：`counters(<counter-name>, <separator>)` 和 `counters(<counter-name>, <separator>, <counter-style>)`。生成的文本由在伪元素范围内所有指定名称的计数器的值组成。这些值从最外层到最内层，使用指定的字符串（`<separator>`）分隔。

- 可以直接传入计数器名称（`counters` 传入计数器名称和分隔符）

- 计数器样式默认为十进制数字，可选值：`decimal`(十进制阿拉伯数字)、`decimal-leading-zero`(十进制数字前置补0)、`upper-roman`(大写罗马)、`lower-roman`(小写罗马)、`upper-alpha`/`upper-latin`(大写字母)、`lower-alpha`/`lower-latin`(小写字母)、`lower-greek`(阿尔法、贝塔、伽马…)、`disc`(实心圆点)、`circle`(空心圆点)、`square`(大写字母)……

  - 可参考：[CSS Lists and Counters Module Level 3 (w3c.github.io)](https://w3c.github.io/csswg-drafts/css-lists-3/#counter-functions)

  - 需要自定义符号可以看下这个：[@counter-style](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@counter-style)

接着上面的样式：

```css
section h2::after {
  content: counter(section, decimal-leading-zero);
}
section h3::before {
  content: counter(section) counter(topic) " "; /* content 中拼接不需要用加号 */
}
section p::before {
  content: counter(section) counter(topic) counter(paragraph) " ";
}
```

显示：

![显示效果](https://cdn.wallleap.cn/img/pic/illustrtion/202210131119166.png)

## 特殊的计数器——有序列表（list item）计数器

使用 `ol` 元素创建的有序列表，会自动应用名为 `list-item` 的计数器。

和其它的计数器一样，它也是一个默认自增（+1）且初始值为 0 的计数器；对于反向计数器（`reversed()`），则以元素数量为初始值，且默认自减（-1）。与自定义的计数器不同，`list-item` 是根据其是否为反向计数器而*自动*自增或自减的。

可以通过 CSS 修改 `list-item` 计数器应用在有序列表上的默认行为。例如，你可以改变默认初始值，或使用 [`counter-increment`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/counter-increment) 改变递增或递减的方式。

计数器嵌套示例：

```html
<ol>
  <li>item</li>          <!-- 1     -->
  <li>item               <!-- 2     -->
    <ol>
      <li>item</li>      <!-- 2.1   -->
      <li>item</li>      <!-- 2.2   -->
      <li>item           <!-- 2.3   -->
        <ol>
          <li>item</li>  <!-- 2.3.1 -->
          <li>item</li>  <!-- 2.3.2 -->
        </ol>
        <ol>
          <li>item</li>  <!-- 2.3.1 -->
          <li>item</li>  <!-- 2.3.2 -->
          <li>item</li>  <!-- 2.3.3 -->
        </ol>
      </li>
      <li>item</li>      <!-- 2.4   -->
    </ol>
  </li>
  <li>item</li>          <!-- 3     -->
  <li>item</li>          <!-- 4     -->
</ol>
<ol>
  <li>item</li>          <!-- 1     -->
  <li>item</li>          <!-- 2     -->
</ol>
<style>
ol {
  list-style-type: none;
}
li::before {
  content: counters(list-item, ".") " ";
}
</style>
```

显示：

![显示效果](https://cdn.wallleap.cn/img/pic/illustrtion/202210131121570.png)

## 实现自定义列表序号

有序列表仍使用上面的 HTML 代码，无序列表添加下列代码：

```html
<h2>无序列表嵌套</h2>
<ul>
  <li>无序列表 item</li>
  <li>无序列表 item
    <ul>
      <li>item</li>
    </ul>
  </li>
  <li>无序 item
    <ol>
      <li>有序 item1</li>
      <li>有序 item2</li>
      <li>有序 item3</li>
    </ol>
  </li>
  <li>无序列表 item</li>
</ul>
```

之后就可以直接写样式了：

```css
* {
  margin: 0;
  padding: 0;
}
:root {
  --primary: #5A80F7;
  --magnetic-white: #f8fbf8;
}
html {
  font-size: 15px;
}
body {
  padding-left: 3rem;
  padding-top: 1rem;
}
h2 {
  margin-top: .6rem;
  margin-bottom: .2rem;
}
ul, ol {
  list-style: none; /* 去除列表默认样式 */
}
ul>li, ol>li {
  position: relative; /* 父相子绝，方便定位 */
  margin-left: 1rem; /* 每层进行缩进 */
  line-height: 1.6;
}
ol>li {
  margin-left: 1.4rem;
}
ul>li::before {
  content: '';
  position: absolute;
  left: -1rem;
  top: .5rem; /* 视觉上居中 */
  width: .6rem;
  height: .6rem;
  background: var(--primary);
  border-radius: 50%; /* 方形变圆形 */
}
ol>li::before {
  content: counter(list-item); /* 显示序号 */
  position: absolute;
  left: -1.4rem;
  top: .4rem;
  width: 1rem;
  height: 1rem;
  background: var(--primary);
  border-radius: 50%;
  color: var(--magnetic-white);
  font-size: .8rem;
  /* 文字视觉上居中 */
  text-align: center;
  line-height: 1.2;
}
```

代码：[自定义列表序号 - JS Bin](http://js.jirengu.com/bicoq/1/edit)

具体显示如下：

![显示效果](https://cdn.wallleap.cn/img/pic/illustrtion/202210131351745.png)
