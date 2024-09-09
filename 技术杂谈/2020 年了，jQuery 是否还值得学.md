---
title: 2020 年了，jQuery 是否还值得学
date: 2020-04-26 20:33
updated: 2020-04-26 20:33
cover: //cdn.wallleap.cn/img/pic/cover/202302lplEqL.jpg
category: 技术杂谈
tags:
  - web
  - 前端
description: 2020 年了，jQuery 是否还值得学
---

jQuery 是一个 JavaScript 库，极大地简化了原生 JavaScript 编程，源码值得学习。

可以先了解 jQuery 的一些基本用法，然后再去看源码，这样会更容易理解。

- 初识 jQuery
- jQuery 的两把利器
- 使用 jQuery 核心函数
- 使用 jQuery 对象
- jQuery 对象
- 练习

## 一、初识 jQuery

### 1、一个 JS 库

- 官网：<http://jquery.com/>
- 一个优秀的 JS 函数库
- 使用了 jQuery 的网站超过90%中大型 WEB 项目开发首选
- Write Less, Do More!!!

### 2、操作更方便

- HTML 元素选取（选择器）
- HTML 元素操作
- CSS 操作
- HTML 事件处理
- JS 动画效果
- 链式调用
- 读写合一
- 浏览器兼容
- 易扩展插件
- Ajax 封装
- ......

> 封装简化 DOM 操作（CRUD）/ Ajax
>
> 强大选择器：方便快速查找 DOM 元素
>
> 隐式遍历（迭代）：一次操作多个元素
>
> 读写合一：读数据/写数据用的是一个函数
>
> 事件处理、链式调用、DOM 操作、样式操作……

### 3、jQuery 的使用

![使用](https://cdn.wallleap.cn/img/pic/illustration/20200815145128.png)

(1) 引入库：本地引入、CDN 远程引入，测试版、生产版（压缩版）

(2) 使用库：函数（`$`/`jQuery`）、对象（`$xxx`）

```html
<!--
需求: 点击"确定"按钮, 提示输入的值
-->
用户名: <input type="text" id="username">
<button id="btn1">确定(原生版)</button>
<button id="btn2">确定(jQuery版)</button>
<!--使用原生DOM-->
<script type="text/javascript">
  window.onload = function () {
    var btn1 = document.getElementById('btn1')
    btn1.onclick = function () {
      var username = document.getElementById('username').value
      alert(username)
    }
  }
</script>
<!--使用 jQuery 实现-->
  <!--本地引入-->
<script type="text/javascript" src="js/jquery-1.12.3.js"></script>
  <!--远程引入-->
<!--<script src="https://cdn.bootcss.com/jquery/1.12.4/jquery.js"></script>-->
<script type="text/javascript">
  //绑定文档加载完成的监听
  jQuery(function () {
    var $btn2 = $('#btn2')
    $btn2.click(function () { // 给 btn2 绑定点击监听
      var username = $('#username').val()
      alert(username)
    })
  })
  /*
  1. 使用 jQuery 核心函数：$/jQuery
  2. 使用 jQuery 核心对象：执行 $() 返回的对象
    */
</script>
```

## 二、jQuery 的 2 把利器

- jQuery 函数：`$`/`jQuery`
  - jQuery 向外暴露的就是 jQuery 函数，可以直接使用
  - 当成一般函数使用：`$(param)` 或 `jQuery(param)`
    - param 是 Function：相当于 `window.onload = function`（文档加载完成的监听）
    - param 是选择器字符串：查找所有匹配的 DOM 元素，返回包含所有 DOM 元素的 jQuery 对象
    - param 是 DOM 元素：将 DOM 元素对象包装为 jQuery 对象返回 `$(this)`
    - param 是标签字符串：创建标签 DOM 元素对象并包装为 jQuery 对象返回
  - 当成对象使用：`$.xxx`
    - `$.each(obj/arr, function(key, value){})`：隐式遍历 obj/arr
    - `$.trim(str)`：去除字符串两端的空格
- jQuery 对象
  - 包含所有匹配的 n 个 DOM 元素的伪数组对象
  - 执行 `$()` 返回的就是 jQuery 对象
  - 基本行为:
    - `length`/`size()`：得到 DOM 元素的个数
    - `[index]`：得到指定下标对应的 DOM 元素
    - `each(function(index, domEle){})`：遍历所有 DOM 元素
    - `index()`：得到当前 DOM 元素在所有兄弟中的下标

### 1、jQuery 核心函数

- 简称: jQuery 函数（`$`/`jQuery`）

- jQuery 库向外直接暴露的就是 `$`/`jQuery`

- 引入 jQuery 库后，直接使用 `$` 即可
  - 当函数用：`$(xxx)`
  - 当对象用：`$.xxx()`

```html
<script type="text/javascript" src="js/jquery-1.12.3.js"></script>
<script type="text/javascript">
  //1. jQuery 函数：直接可用
  console.log($, typeof $) // f(){}
  console.log(jQuery===$) // true
  /*
  (function (window) {
    var jQuery = function () {
      return new xxx()
    }
    window.$ = window.jQuery = jQuery
  })(window)
  */
</script>
```

理解：

- 即 `$` 或 `jQuery`
- jQuery 定义了这个全局的函数供我们调用
- 它既可作为一般函数调用，且传递的参数类型不同/格式不同功能就完全不同
- 也可作为对象调用其定义好的方法，此时 `$` 就是一个工具对象

作为函数调用：

- 参数为函数 `$(fun)`
- 参数为选择器（selector）字符串 `$("#div1")`
- 参数为 DOM 对象 `$(div1Ele)`
- 参数为 HTML 标签字符串 `$("<div>")`

作为对象使用：

- 发送 ajax 请求的方法
  - `$.ajax()`
  - `$.get()`
  - `$.post()`
  - ......
- 其它工具方法
  - `$.each()`
  - `$.trim()`
  - `$.parseJSON()`
  - ......
  
```html
<div>
  <button id="btn">测试</button>
  <br/>
  <input type="text" name="msg1"/><br/>
  <input type="text" name="msg2"/><br/>
</div>
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  /*
   需求1. 点击按钮: 显示按钮的文本, 显示一个新的输入框
   需求2. 遍历输出数组中所有元素值
   需求3. 去掉 "  lu wang  " 两端的空格
   */
  /*需求1. 点击按钮: 显示按钮的文本, 显示一个新的输入框*/
  //1.1). 参数为函数：当DOM加载完成后，执行此回调函数
  $(function () { // 绑定文档加载完成的监听
    // 1.2) 参数为选择器字符串: 查找所有匹配的标签, 并将它们封装成jQuery对象
    $('#btn').click(function () { // 绑定点击事件监听
      // this是什么? 发生事件的dom元素(<button>)
      // alert(this.innerHTML)
      // 1.3). 参数为DOM对象: 将dom对象封装成jQuery对象
      alert($(this).html())
      // 1.4). 参数为html标签字符串 (用得少): 创建标签对象并封装成jQuery对象
      $('<input type="text" name="msg3"/><br/>').appendTo('div')
    })
  })
  /*需求2. 遍历输出数组中所有元素值*/
  var arr = [2, 4, 7]
  // 1). $.each()：隐式遍历数组
  $.each(arr, function (index, item) {
    console.log(index, item)
  })
  // 2). $.trim()：去除两端的空格
  var str = ' lu wang  '
  // console.log('---'+str.trim()+'---')
  console.log('---'+$.trim(str)+'---')
</script>
```

### 2、jQuery 核心对象

- 简称：jQuery 对象

- 得到 jQuery 对象：执行 jQuery 函数返回的就是 jQuery 对象

- 使用 jQuery 对象：`$obj.xxx()`

```html
<script type="text/javascript" src="js/jquery-1.12.3.js"></script>
<script type="text/javascript">
  //2. jQuery 对象：执行 jQuery 函数得到它
  console.log($() instanceof Object) // true
</script>
```

理解：

- 即执行 jQuery 核心函数返回的对象
- jQuery 对象内部包含的是 DOM 元素对象的伪数组（可能只有一个元素）
- jQuery 对象拥有很多有用的属性和方法，让程序员能方便的操作 DOM

属性/方法：

- 基本行为
  - `size()`/`length`：包含的 DOM 元素个数
  - `[index]`/`get(index)`：得到对应位置的 DOM 元素
  - `each()`：遍历包含的所有 DOM 元素
  - `index()`：得到在所在兄弟元素中的下标

- 属性：操作内部标签的属性或值

- CSS：操作标签的样式

- 文档：对标签进行增删改操作

- 筛选：根据指定的规则过滤内部的标签

- 事件：处理事件监听相关

- 效果：实现一些动画效果

```html
<button>测试一</button>
<button>测试二</button>
<button id="btn3">测试三</button>
<button>测试四</button>
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  /*
   需求:
   需求1. 统计一共有多少个按钮
   需求2. 取出第2个button的文本
   需求3. 输出所有button标签的文本
   需求4. 输出'测试三'按钮是所有按钮中的第几个
   */
  //需求1. 统计一共有多少个按钮
  var $buttons = $('button')
  /*size()/length: 包含的DOM元素个数*/
  console.log($buttons.size(), $buttons.length)
  //需求2. 取出第2个button的文本
  /*[index]/get(index): 得到对应位置的DOM元素*/
  console.log($buttons[1].innerHTML, $buttons.get(1).innerHTML)
  //需求3. 输出所有button标签的文本
  /*each(): 遍历包含的所有DOM元素*/
  /*$buttons.each(function (index, domEle) {
    console.log(index, domEle.innerHTML, this)
  })*/
  $buttons.each(function () {
    console.log(this.innerHTML)
  })
  //需求4. 输出'测试三'按钮是所有按钮中的第几个
  /*index(): 得到在所在兄弟元素中的下标*/
  console.log($('#btn3').index())  //2
  /*
  1. 伪数组
    * Object对象
    * length属性
    * 数值下标属性
    * 没有数组特别的方法: forEach(), push(), pop(), splice()
   */
  console.log($buttons instanceof Array) // false
  // 自定义一个伪数组
  var weiArr = {}
  weiArr.length = 0
  weiArr[0] = 'luwang'
  weiArr.length = 1
  weiArr[1] = 123
  weiArr.length = 2
  for (var i = 0; i < weiArr.length; i++) {
    var obj = weiArr[i]
    console.log(i, obj)
  }
  console.log(weiArr.forEach, $buttons.forEach) //undefined, undefined
</script>
```

## 三、使用 jQuery 核心函数

### 1、选择器

(1) 说明

- 选择器本身只是一个有特定语法规则的字符串，没有实质用处
- 它的基本语法规则使用的就是 CSS 的选择器语法，并对基进行了扩展
- 只有调用 `$()`，并将选择器作为参数传入才能起作用
- `$(selector)` 作用：根据选择器规则在整个文档中查找所有匹配的标签的数组，并封装成 jQuery 对象返回（用来查找特定页面元素）

(2) 分类

基本选择器

- `#id`：id 选择器
- `element`：元素选择器
- `.class`：类选择器
- `*`：任意标签
- `selector1,selector2,selectorN`：取多个选择器的并集（组合选择器）
- `selector1selector2selectorN`：取多个选择器的交集(相交选择器)

```html
<div id="div1" class="box">div1(class="box")</div>
<div id="div2" class="box">div2(class="box")</div>
<div id="div3">div3</div>
<span class="box">span(class="box")</span>
<br>
<ul>
  <li>AAAAA</li>
  <li title="hello">BBBBB(title="hello")</li>
  <li class="box">CCCCC(class="box")</li>
  <li title="hello">DDDDDD(title="hello")</li>
</ul>
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  /*
    需求:
    1. 选择id为div1的元素
    2. 选择所有的div元素
    3. 选择所有class属性为box的元素
    4. 选择所有的div和span元素
    5. 选择所有class属性为box的div元素
    */
  //1. 选择id为div1的元素
  // $('#div1').css('background', 'red')
  //2. 选择所有的div元素
  // $('div').css('background', 'red')
  //3. 选择所有class属性为box的元素
  //$('.box').css('background', 'red')
  //4. 选择所有的div和span元素
  // $('div,span').css('background', 'red')
  //5. 选择所有class属性为box的div元素
  //$('div.box').css('background', 'red')
  //$('*').css('background', 'red')
</script>
```

层次选择器（查找子元素、后代元素、兄弟元素的选择器）

- `ancestor descendant`：在给定的祖先元素下的后代元素中匹配元素
- `parent > child`：在给定的父元素下的子元素中匹配元素
- `prev + next`：匹配所有紧接在 prev 元素后的 next 元素
- `prev ~ siblings`：匹配 prev 元素之后的所有 siblings 元素

```html
<ul>
  <li>AAAAA</li>
  <li class="box">CCCCC</li>
  <li title="hello"><span>BBBBB</span></li>
  <li title="hello"><span class="box">DDDD</span></li>
  <span>EEEEE</span>
</ul>
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  /*
    需求:
    1. 选中ul下所有的的span
    2. 选中ul下所有的子元素span
    3. 选中class为box的下一个li
    4. 选中ul下的class为box的元素后面的所有兄弟元素
    */
  //1. 选中ul下所有的的span
  // $('ul span').css('background', 'yellow')
  //2. 选中ul下所有的子元素span
  // $('ul>span').css('background', 'yellow')
  //3. 选中class为box的下一个li
  // $('.box+li').css('background', 'yellow')
  //4. 选中ul下的class为box的元素后面的所有兄弟元素
  $('ul .box~*').css('background', 'yellow')
</script>
```

过滤选择器（在原有选择器匹配的元素中进一步进行过滤的选择器）

- 基本
  - `:first`
  - `:last`
  - `:eq(index)`
  - `:lt`
  - `:gt`
  - `:odd`
  - `:even`
  - `:not(selector)`
  - `:header`
  - `:animated`
  - `:focus`
- 内容
  - `:contains(text)`
  - `:empty`
  - `:has(selector)`
  - `:parent`
- 可见性
  - `:hidden`
  - `:visible`
- 属性
  - `[attribute]`
  - `[attrName=value]`
  - `[attribute!=value]`
  - `[attribute^=value]`
  - `[attribute$=value]`
  - `[attribute*=value]`
  - `[attrSel1][attrSel2][attrSelN]`

```html
<div id="div1" class="box">class为box的div1</div>
<div id="div2" class="box">class为box的div2</div>
<div id="div3">div3</div>
<span class="box">class为box的span</span>
<br/>
<ul>
  <li>AAAAA</li>
  <li title="hello">BBBBB</li>
  <li class="box">CCCCC</li>
  <li title="hello">DDDDDD</li>
  <li title="two">BBBBB</li>
  <li style="display:none">我本来是隐藏的</li>
</ul>
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">

  /*
    需求:
    1. 选择第一个div
    2. 选择最后一个class为box的元素
    3. 选择所有class属性不为box的div
    4. 选择第二个和第三个li元素
    5. 选择内容为BBBBB的li
    6. 选择隐藏的li
    7. 选择有title属性的li元素
    8. 选择所有属性title为hello的li元素
    */
  //1. 选择第一个div
  // $('div:first').css('background', 'red')
  //2. 选择最后一个class为box的元素
  //$('.box:last').css('background', 'red')
  //3. 选择所有class属性不为box的div
  // $('div:not(.box)').css('background', 'red')  //没有class属性也可以
  //4. 选择第二个和第三个li元素
  // $('li:gt(0):lt(2)').css('background', 'red') // 多个过滤选择器不是同时执行, 而是依次
  //$('li:lt(3):gt(0)').css('background', 'red')
  //5. 选择内容为BBBBB的li
  // $('li:contains("BBBBB")').css('background', 'red')
  //6. 选择隐藏的li
  // console.log($('li:hidden').length, $('li:hidden')[0])
  //7. 选择有title属性的li元素
  // $('li[title]').css('background', 'red')
  //8. 选择所有属性title为hello的li元素
  $('li[title="hello"]').css('background', 'red')
</script>
```

练习：表格隔行变色

![](https://cdn.wallleap.cn/img/pic/illustration/20200815163734.png)

```html
<style>
div, span, p {
  width: 140px;
  height: 140px;
  margin: 5px;
  background: #aaa;
  border: #000 1px solid;
  float: left;
  font-size: 17px;
  font-family: Verdana;
}

div.mini {
  width: 55px;
  height: 55px;
  background-color: #aaa;
  font-size: 12px;
}

div.hide {
  display: none;
}

#data {
  width: 600px;
}

#data, td, th {
  border-collapse: collapse;
  border: 1px solid #aaaaaa;
}

th, td {
  height: 28px;
}

#data thead {
  background-color: #333399;
  color: #ffffff;
}

.odd {
  background-color: #ccccff;
}
</style>
<table id="data">
  <thead>
    <tr>
      <th>姓名</th>
      <th>工资</th>
      <th>入职时间</th>
      <th>操作</th>
    </tr>
  </thead>
  <tbody>
  <tr>
    <td>Tom</td>
    <td>$3500</td>
    <td>2010-10-25</td>
    <td><a href="javascript:void(0)">删除</a></td>
  </tr>
  <tr>
    <td>Mary</td>
    <td>$3400</td>
    <td>2010-12-1</td>
    <td><a href="javascript:void(0)">删除</a></td>
  </tr>
  <tr>
    <td>King</td>
    <td>$5900</td>
    <td>2009-08-17</td>
    <td><a href="javascript:void(0)">删除</a></td>
  </tr>
  <tr>
    <td>Scott</td>
    <td>$3800</td>
    <td>2012-11-17</td>
    <td><a href="javascript:void(0)">删除</a></td>
  </tr>
  <tr>
    <td>Smith</td>
    <td>$3100</td>
    <td>2014-01-27</td>
    <td><a href="javascript:void(0)">删除</a></td>
  </tr>
  <tr>
    <td>Allen</td>
    <td>$3700</td>
    <td>2011-12-05</td>
    <td><a href="javascript:void(0)">删除</a></td>
  </tr>
  </tbody>
</table>
<script type="text/javascript" src="jquery-1.10.1.js"></script>
<script type="text/javascript">
  $('#data>tbody>tr:odd').css('background', '#ccccff')
</script>
```

表单选择器

- 表单
  - `:input`
  - `:text`
  - `:checkbox`
  - `:radio`
- 表单对象属性
  - `:checked`：选中的

```html
<form>
  用户名: <input type="text"/><br>
  密 码: <input type="password"/><br>
  爱 好:
  <input type="checkbox" checked="checked"/>篮球
  <input type="checkbox"/>足球
  <input type="checkbox" checked="checked"/>羽毛球 <br>
  性 别:
  <input type="radio" name="sex" value='male'/>男
  <input type="radio" name="sex" value='female'/>女<br>
  邮 箱: <input type="text" name="email" disabled="disabled"/><br>
  所在地:
  <select>
    <option value="1">北京</option>
    <option value="2" selected="selected">天津</option>
    <option value="3">河北</option>
  </select><br>
  <input type="submit" value="提交"/>
</form>
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  /*
    需求:
    1. 选择不可用的文本输入框
    2. 显示选择爱好 的个数
    3. 显示选择的城市名称
    */
  //1. 选择不可用的文本输入框
  // $(':text:disabled').css('background', 'red')
  //2. 显示选择爱好 的个数
  console.log($(':checkbox:checked').length)
  //3. 显示选择的城市名称
  $(':submit').click(function () {
    var city = $('select>option:selected').html() // 选择的option的标签体文本
    city = $('select').val()  // 选择的option的value属性值
    alert(city)
  })
</script>
```

### 2、`$` 工具方法

1. `$.each()`：遍历数组或对象中的数据
2. `$.trim()`：去除字符串两边的空格
3. `$.type(obj)`：得到数据的类型
4. `$.isArray(obj)`：判断是否是数组
5. `$.isFunction(obj)`：判断是否是函数
6. `$.parseJSON(json)`：解析 json 字符串转换为 js 对象/数组

```html
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  //1. $.each(): 遍历数组或对象中的数据
  var obj = {
    name: 'Tom',
    setName: function (name) {
      this.name = name
    }
  }
  $.each(obj, function (key, value) {
    console.log(key, value)
  })
  
  //2. $.trim(): 去除字符串两边的空格
  //3. $.type(obj): 得到数据的类型
  console.log($.type($)) // 'function'

  //4. $.isArray(obj): 判断是否是数组
  console.log($.isArray($('body')), $.isArray([])) // false true
  //5. $.isFunction(obj): 判断是否是函数
  console.log($.isFunction($)) // true
  //6. $.parseJSON(json) : 解析json字符串转换为js对象/数组
  var json = '{"name":"Tom", "age":12}'  // json对象: {}
  // json对象===>JS对象
  console.log($.parseJSON(json))
  json = '[{"name":"Tom", "age":12}, {"name":"JACK", "age":13}]' // json数组: []
  // json数组===>JS数组
  console.log($.parseJSON(json))
  /*
  JSON.parse(jsonString)   json字符串--->js对象/数组
  JSON.stringify(jsObj/jsArr)  js对象/数组--->json字符串
  */
</script>
```

练习：多 Tab 点击切换

![](https://cdn.wallleap.cn/img/pic/illustration/20200815163919.png)

```html
<style>
*{margin:0;padding:0}#tab li{float:left;list-style:none;width:80px;height:40px;line-height:40px;cursor:pointer;text-align:center}#container{position:relative}#content1,#content2,#content3{width:300px;height:100px;padding:30px;position:absolute;top:40px;left:0}#tab1,#content1{background-color:#fc0}#tab2,#content2{background-color:#f0c}#tab3,#content3{background-color:#0cf}
</style>
<h2>多Tab点击切换</h2>
<ul id="tab">
  <li id="tab1" value="1">10元套餐</li>
  <li id="tab2" value="2">30元套餐</li>
  <li id="tab3" value="3">50元包月</li>
</ul>
<div id="container">
  <div id="content1">
    10元套餐详情：<br/>&nbsp;每月套餐内拨打100分钟，超出部分2毛/分钟
  </div>
  <div id="content2" style="display: none">
    30元套餐详情：<br/>&nbsp;每月套餐内拨打300分钟，超出部分1.5毛/分钟
  </div>
  <div id="content3" style="display: none">
    50元包月详情：<br/>&nbsp;每月无限量随心打
  </div>
</div>
<script type="text/javascript" src="jquery-1.10.1.js"></script>
<script type="text/javascript">
  var $contents = $('#container>div')
  // 给3个li加监听
  /*$('#tab>li').click(function () { // 隐式遍历
    //alert('----')
    // 隐隐藏所有内容div
    $contents.css('display', 'none')
    // 显示对应的内容div
    // 得到当前点击的li在兄弟中下标
    var index = $(this).index()
    // 找到对应的内容div, 并显示
    $contents[index].style.display = 'block'
    // $($contents[index]).css('display', 'block')
  })*/
  // 改进——第二三个div默认none，不需要全部设置隐藏
  var currIndex = 0 //当前显示的内容div的下标
  $('#tab>li').click(function () { // 隐式遍历
    //alert('----')
    // 隐藏当前已经显示的内容div
    $contents[currIndex].style.display = 'none'
    // 显示对应的内容div
      // 得到当前点击的li在兄弟中下标
    var index = $(this).index()
      // 找到对应的内容div, 并显示
    $contents[index].style.display = 'block'
    // 更新下标
    currIndex = index
  })
</script>
```

### 3、ajax

- `ajax()`

- `get()`

- `post`

- ……

## 四、使用 jQuery 对象

### 1、属性/文本

操作标签的属性, 标签体文本

操作任意属性

- `attr(name)` /`attr(name, value)`: 读写非布尔值的标签属性
- `prop(name)` / `prop(name, value)`: 读写布尔值的标签属性
- `removeAttr(name)`/`removeProp(name)`: 删除属性

操作 class 属性

- `addClass(classValue)`：添加 class
- `removeClass(classValue)`：移除指定 class

操作HTML代码/文本/值

- `val()` / `val(value)`：读写标签的value
- `html()` / `html(htmlString)`：读写标签体文本

```html
<div id="div1" class="box" title="one">class为box的div1</div>
<div id="div2" class="box" title="two">class为box的div2</div>
<div id="div3">div3</div>
<span class="box">class为box的span</span>
<br/>
<ul>
  <li>AAAAA</li>
  <li title="hello" class="box2">BBBBB</li>
  <li class="box">CCCCC</li>
  <li title="hello">DDDDDD</li>
  <li title="two"><span>BBBBB</span></li>
</ul>

<input type="text" name="username" value="guiguClass"/>
<br>
<input type="checkbox">
<input type="checkbox">
<br>
<button>选中</button>
<button>不选中</button>
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  //1. 读取第一个div的title属性
  // console.log($('div:first').attr('title')) // one
  //2. 给所有的div设置name属性(value为atguigu)
  // $('div').attr('name', 'atguigu')
  //3. 移除所有div的title属性
  // $('div').removeAttr('title')
  //4. 给所有的div设置class='guiguClass'
  //$('div').attr('class', 'guiguClass')
  //5. 给所有的div添加class='abc'
  //$('div').addClass('abc')
  //6. 移除所有div的guiguClass的class
  //$('div').removeClass('guiguClass')
  //7. 得到最后一个li的标签体文本
  //console.log($('li:last').html())
  //8. 设置第一个li的标签体为"<h1>mmmmmmmmm</h1>"
  //$('li:first').html('<h1>mmmmmmmmm</h1>')
  //9. 得到输入框中的value值
  //console.log($(':text').val()) // 读取
  //10. 将输入框的值设置为atguigu
  //$(':text').val('atguigu') // 设置      读写合一
  //11. 点击'全选'按钮实现全选
    // attr(): 操作属性值为非布尔值的属性
    // prop(): 专门操作属性值为布尔值的属性
  var $checkboxs = $(':checkbox')
  $('button:first').click(function () {
    $checkboxs.prop('checked', true)
  })
  //12. 点击'全不选'按钮实现全不选
  $('button:last').click(function () {
    $checkboxs.prop('checked', false)
  })
</script>
```

练习表格隔行变色改进--->odd样式类

![](https://cdn.wallleap.cn/img/pic/illustration/20200815164644.png)

### 2、CSS

(1) style 样式（设置 CSS 样式/读取 CSS 值）

- `css(styleName)`: 根据样式名得到对应的值
- `css(styleName, value)`: 设置一个样式
- `css({多个样式对})`: 设置多个样式

```html
<p style="color: blue;">HTML</p>
<p style="color: green;">CSS</p>
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  //1. 得到第一个p标签的颜色
  //console.log($('p:first').css('color'))
  //2. 设置所有p标签的文本颜色为red
  //$('p').css('color', 'red')
  //3. 设置第2个p的字体颜色(#ff0011),背景(blue),宽(300px), 高(30px)
  $('p:eq(1)').css({
    color: '#ff0011',
    background: 'blue',
    width: 300,
    height: 30
  })
</script>
```

(2) 位置坐标（获取/设置标签的位置数据）

- `offset()`：读/写当前元素坐标（原点是页面左上角）
- `position()`：读当前元素坐标（原点是父元素左上角）
- `scrollTop()`/`scrollLeft()`：读/写元素/页面的滚动条坐标

```html
<style type="text/css">
  * {
    margin: 0px;
  }
  .div1 {
    position: absolute;
    width: 200px;
    height: 200px;
    top: 20px;
    left: 10px;
    background: blue;
  }
  .div2 {
    position: absolute;
    width: 100px;
    height: 100px;
    top: 50px;
    background: red;
  }
  .div3 {
    position: absolute;
    top: 250px;
  }
</style>
<body style="height: 2000px;">
<div class="div1">
  <div class="div2">测试offset</div>
</div>
<div class='div3'>
  <button id="btn1">读取offset和position</button>
  <button id="btn2">设置offset</button>
</div>
<!--
获取/设置标签的位置数据
  * offset(): 相对页面左上角的坐标
  * position(): 相对于父元素左上角的坐标
-->
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  $('#btn1').click(function () {
  // 打印 div1 相对于页面左上角的位置
    var offset = $('.div1').offset()
    console.log(offset.left, offset.top) // 10 20
  // 打印 div2 相对于页面左上角的位置
    offset = $('.div2').offset()
    console.log(offset.left, offset.top) // 10 70
  // 打印 div1 相对于父元素左上角的位置
    var position = $('.div1').position()
    console.log(position.left, position.top) // 10 20
  // 打印 div2 相对于父元素左上角的位置
    position = $('.div2').position()
    console.log(position.left, position.top) // 0 50
  })
  $('#btn2').click(function () {
    // 设置 div2 相对于页面的左上角的位置
    $('.div2').offset({
      left: 50,
      top: 100
    })
  })
</script>
```

1. `scrollTop()`：读取/设置滚动条的Y坐标

2. `$(document.body).scrollTop()+$(document.documentElement).scrollTop()`：读取页面滚动条的 Y 坐标

3. `$('body,html').scrollTop(60);`：滚动到指定位置

```html
<body style="height: 2000px;">
<div style="border:1px solid black;width:100px;height:150px;overflow:auto">
  This is some text. This is some text. This is some text. This is some text.
  This is some text. This is some text. This is some text. This is some text.
  This is some text. This is some text. This is some text. This is some text.
  This is some text. This is some text. This is some text. This is some text.
  This is some text. This is some text. This is some text. This is some text.
  This is some text. This is some text. This is some text. This is some text.
  his is some text.
</div>
<br>
<br>
<br>
<button id="btn1">得到scrollTop</button>
<button id="btn2">设置scrollTop</button>
<script src="js/jquery-1.10.1.js"></script>
<script>
  //1. 得到div或页面滚动条的坐标
  $('#btn1').click(function () {
    console.log($('div').scrollTop())
    // console.log($('html').scrollTop()+$('body').scrollTop())
    console.log($(document.documentElement).scrollTop()+$(document.body).scrollTop()) // 兼容IE/Chrome
  })
  //2. 让div或页面的滚动条滚动到指定位置
  $('#btn2').click(function () {
    $('div').scrollTop(200)
    $('html,body').scrollTop(300)
  })
</script>
</body>
```

(3) 尺寸（获取/设置标签的尺寸数据）

![](https://cdn.wallleap.cn/img/pic/illustration/20200815171021.png)

- 内容尺寸
  - `height()`：height
  - `width()`：width
- 内部尺寸
  - `innerHeight()`：height + padding
  - `innerWidth()`：width + padding

- 外部尺寸
  - `outerHeight(false/true)`：height + padding + border 如果是 true，加上 margin
  - `outerWidth(false/true)`：width + padding + border 如果是 true，加上 margin

```html
<style>
  div {
    width: 100px;
    height: 150px;
    background: red;
    padding: 10px;
    border: 10px #fbd850 solid;
    margin: 10px;
  }
</style>
<div>div</div>
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script>
  var $div = $('div')
  // 1. 内容尺寸
  console.log($div.width(), $div.height())  // 100 150
  // 2. 内部尺寸
  console.log($div.innerWidth(), $div.innerHeight()) //120 170
  // 3. 外部尺寸
  console.log($div.outerWidth(), $div.outerHeight()) //140 190
  console.log($div.outerWidth(true), $div.outerHeight(true)) //160 210
</script>
```

### 3、筛选

(1) 过滤

在 jQuery 对象中的元素对象数组中过滤出一部分元素来

1. `first()`

2. `last()`

3. `eq(index|-index)`：index 为正数，从前往后数；index 为负数，从后往前数

4. `filter(selector)`：对当前元素提要求

5. `not(selector)`：对当前元素提要求，并取反

6. `has(selector)`：对子孙元素提要求

```html
<ul>
  <li>AAAAA</li>
  <li title="hello" class="box2">BBBBB</li>
  <li class="box">CCCCC</li>
  <li title="hello">DDDDDD</li>
  <li title="two"><span>BBBBB</span></li>
</ul>
<li>eeeee</li>
<li>EEEEE</li>
<br>
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  var $lis = $('ul>li')
  //1. ul下li标签第一个
  // $lis.first().css('background', 'red')
  // $lis[0].style.background = 'red'

  //2. ul下li标签的最后一个
  // $lis.last().css('background', 'red')

  //3. ul下li标签的第二个
  // $lis.eq(1).css('background', 'red')

  //4. ul下li标签中title属性为hello的
  // $lis.filter('[title=hello]').css('background', 'red')

  //5. ul下li标签中title属性不为hello的
  // $lis.not('[title=hello]').css('background', 'red')
  // $lis.filter('[title!=hello]').filter('[title]').css('background', 'red')

  //6. ul下li标签中有span子标签的
  $lis.has('span').css('background', 'red')
</script>
```

(2) 查找

在已经匹配出的元素集合中根据选择器查找孩子/父母/兄弟标签

1. `children()`：子标签中找

2. `find()`：后代标签中找

3. `parent()`：父标签

4. `prevAll()`：前面所有的兄弟标签

5. `nextAll()`：后面所有的兄弟标签

6. `siblings()`：前后所有的兄弟标签

```html
<div id="div1" class="box" title="one">class为box的div1</div>
<div id="div2" class="box">class为box的div2</div>
<div id="div3">div3</div>
<span class="box">class为box的span</span>
<br/>
<div>
  <ul>
    <span>span文本1</span>
    <li>AAAAA</li>
    <li title="hello" class="box2">BBBBB</li>
    <li class="box" id='cc'>CCCCC</li>
    <li title="hello">DDDDDD</li>
    <li title="two"><span>span文本2</span></li>
    <span>span文本3</span>
  </ul>
  <span>span文本444</span><br>
  <li>eeeee</li>
  <li>EEEEE</li>
  <br>
</div>
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  var $ul = $('ul')
  //1. ul标签的第2个span子标签
  //$ul.children('span:eq(1)').css('background', 'red')

  //2. ul标签的第2个span后代标签
  // $ul.find('span:eq(1)').css('background', 'red')

  //3. ul标签的父标签
  // $ul.parent().css('background', 'red')

  //4. id为cc的li标签的前面的所有li标签
  var $li = $('#cc')
  // $li.prevAll('li').css('background', 'red')

  //5. id为cc的li标签的所有兄弟li标签
  $li.siblings('li').css('background', 'red')
</script>
```

### 4、文档处理

- 增加
  - `append()` / `appendTo()`：向当前匹配的所有元素内部的最后插入指定内容
  - `preppend()` / `preppendTo()`：向当前匹配的所有元素内部的最前面插入指定内容
  - `before()`：将指定内容插入到当前所有匹配元素的前面
  - `after()`：将指定内容插入到当前所有匹配元素的后面替换节点
- 删除
  - `remove()`：将自己及内部的孩子都删除
  - `empty()`：掏空（自己还在）
- 更新
  - `replaceWith()`：用指定内容替换所有匹配的标签删除节点

```html
<style type="text/css">
  * {
    margin: 0px;
  }
  .div1 {
    position: absolute;
    width: 200px;
    height: 200px;
    top: 20px;
    left: 10px;
    background: blue;
  }
  .div2 {
    position: absolute;
    width: 100px;
    height: 100px;
    /*top: 50px;*/
    background: red;
  }
  .div3 {
    position: absolute;
    top: 250px;
  }
</style>
<ul id="ul1">
  <li>AAAAA</li>
  <li title="hello">BBBBB</li>
  <li class="box">CCCCC</li>
  <li title="hello">DDDDDD</li>
  <li title="two">EEEEE</li>
  <li>FFFFF</li>
</ul>
<br>
<br>
<ul id="ul2">
  <li>aaa</li>
  <li title="hello">bbb</li>
  <li class="box">ccc</li>
  <li title="hello">ddd</li>
  <li title="two">eee</li>
</ul>
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  //1. 向id为ul1的ul下添加一个span(最后)
  var $ul1 = $('#ul1')
  // $ul1.append('<span>append()添加的span</span>')
  $('<span>appendTo()添加的span</span>').appendTo($ul1)

  //2. 向id为ul1的ul下添加一个span(最前)
  // $ul1.prepend('<span>prepend()添加的span</span>')
  $('<span>prependTo()添加的span</span>').prependTo($ul1)

  //3. 在id为ul1的ul下的li(title为hello)的前面添加span
  $ul1.children('li[title=hello]').before('<span>before()添加的span</span>')

  //4. 在id为ul1的ul下的li(title为hello)的后面添加span
  $ul1.children('li[title=hello]').after('<span>after()添加的span</span>')

  //5. 将在id为ul2的ul下的li(title为hello)全部替换为p
  $('#ul2>li[title=hello]').replaceWith('<p>replaceAll()替换的p</p>')
  //6. 移除id为ul2的ul下的所有li
  // $('#ul2').empty()  // <p>也会删除
  $('#ul2>li').remove()
</script>
```

### 5、事件

(1) 事件处理

- 绑定事件
  - `eventName(function(){})`：绑定对应事件名的监听，例如 `$('#div').click(function(){});`
  - `on('eventName', function(){})`： 通用的绑定事件监听，例如 `$('#div').on('click', function(){})`
    - 常用：`click`, `mouseenter`/`mouseleave` `mouseover`/`mouseout` `focus`/`blur`

    - 优缺点:

      - `eventName`：编码方便，但只能加一个监听，且有的事件监听不支持

      - `on`：编码不方便，可以添加多个监听，且更通用

- 解绑事件

  - `off('eventName')`：解绑对应事件名的监听，例如 `$('#div').off('click');`

```html
<style type="text/css">
  * {
    margin: 0px;
  }
  .out {
    position: absolute;
    width: 200px;
    height: 200px;
    top: 20px;
    left: 10px;
    background: blue;
  }
  .inner {
    position: absolute;
    width: 100px;
    height: 100px;
    top: 50px;
    background: red;
  }
  .divBtn {
    position: absolute;
    top: 250px;
  }
</style>
<body style="height: 2000px;">
<div class="out">
  外部DIV
  <div class="inner">内部div</div>
</div>
<div class='divBtn'>
  <button id="btn1">取消绑定所有事件</button>
  <button id="btn2">取消绑定mouseover事件</button>
  <button id="btn3">测试事件坐标</button>
  <a href="http://www.baidu.com" id="test4">百度一下</a>
</div>
<script src="js/jquery-1.10.1.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
  //1. 给.out绑定点击监听(用两种方法绑定)
  /*$('.out').click(function () {
   console.log('click out')
   })*/
  $('.out').on('click', function () {
    console.log('on click out')
  })

  //2. 给.inner绑定鼠标移入和移出的事件监听(用3种方法绑定)
  /*
   $('.inner')
   .mouseenter(function () { // 进入
    console.log('进入')
   })
   .mouseleave(function () { // 离开
   console.log('离开')
   })
   */
  /*
   $('.inner')
   .on('mouseenter', function () {
   console.log('进入2')
   })
   .on('mouseleave', function () {
   console.log('离开2')
   })
   */
  $('.inner').hover(function () {
    console.log('进入3')
  }, function () {
    console.log('离开3')
  })


  //3. 点击btn1解除.inner上的所有事件监听
  $('#btn1').click(function () {
    $('.inner').off()
  })

  //4. 点击btn2解除.inner上的mouseenter事件
  $('#btn2').click(function () {
    $('.inner').off('mouseenter')
  })

  //5. 点击btn3得到事件坐标
  $('#btn3').click(function (event) { // event事件对象
    console.log(event.offsetX, event.offsetY) // 原点为事件元素的左上角
    console.log(event.clientX, event.clientY) // 原点为窗口的左上角
    console.log(event.pageX, event.pageY) // 原点为页面的左上角
  })

  //6. 点击.inner区域, 外部点击监听不响应
  $('.inner').click(function (event) {
    console.log('click inner')
    //停止事件冒泡
    event.stopPropagation()
  })
  
  //7. 点击链接, 如果当前时间是偶数不跳转
  $('#test4').click(function (event) {
    if(Date.now()%2===0) {
      event.preventDefault()
    }
  })
</script>
```

(2) 事件切换

`hover(function(){}, function(){})`：同时绑定鼠标移入和移出监听

区别 `mouseover` 与 `mouseenter`?

- `mouseover`：在移入子元素时也会触发，对应 `mouseout`

- `mouseenter`：只在移入当前元素时才触发，对应 `mouseleave`

`hover()` 使用的就是 `mouseenter()` 和 `mouseleave()`

区别 `on('eventName', fun)` 与 `eventName(fun)`

- `on('eventName', fun)`：通用，但编码麻烦

- `eventName(fun)`：编码简单，但有的事件没有对应的方法

```html
<style type="text/css">
  * {
    margin: 0px;
  }
  .div1 {
    position: absolute;
    width: 200px;
    height: 200px;
    top: 50px;
    left: 10px;
    background: olive;
  }
  .div2 {
    position: absolute;
    width: 100px;
    height: 100px;
    top: 50px;
    background: red;
  }
  .div3 {
    position: absolute;
    width: 200px;
    height: 200px;
    top: 50px;
    left: 230px;
    background: olive;
  }
  .div4 {
    position: absolute;
    width: 100px;
    height: 100px;
    top: 50px;
    background: yellow;
  }
  .divText{
    position: absolute;
    top: 330px;
    left: 10px;
  }
</style>
<div class="divText">
  区分鼠标的事件
</div>
<div class="div1">
  div1.....
  <div class="div2">div2....</div>
</div>
<div class="div3">
  div3.....
  <div class="div4">div4....</div>
</div>
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
$('.div1')
  .mouseover(function () {
    console.log('mouseover 进入')
  })
  .mouseout(function () {
    console.log('mouseout 离开')
  })
$('.div3')
  .mouseenter(function () {
    console.log('mouseenter 进入')
  })
  .mouseleave(function () {
    console.log('mouseleave 离开')
  })
</script>
```

(3) 事件委托

- 理解：将子元素的事件委托给父辈元素处理
  - 事件监听绑定在父元素上，但事件发生在子元素上（事件会冒泡到父元素）
  - 但最终调用的事件回调函数的是子元素：`event.target`
- 好处
  - 新增的元素没有事件监听
  - 减少监听的数量（n==>1）
- 编码
  - `delegate(selector, 'eventName', function(event){}) // 回调函数中的this是子元素`
  - `undelegate('eventName')`

```html
<ul>
  <li>11111</li>
  <li>1111111</li>
  <li>111111111</li>
  <li>11111111111</li>
</ul>
<li>22222</li>
<br>
<button id="btn">添加新的li</button>
<br>
<script src="js/jquery-1.10.1.js"></script>
<script>
  /*
   需求：
   1. 点击 li 背景就会变为红色
   2. 点击 btn 就添加一个 li
  */
  $('ul>li').click(function () {
    this.style.background = 'red'
  })

  $('#btn').click(function () {
    $('ul').append('<li>新增的li....</li>')
  })
</script>
```

引入：绑定事件监听的问题（新加的元素没有监听）

1、事件委托（委派/代理）：

- 将多个子元素（li）的事件监听委托给父辈元素（ul）处理

- 监听回调是加在了父辈元素上

- 当操作任何一个子元素（li）时，事件会冒泡到父辈元素（ul）

- 父辈元素不会直接处理事件，而是根据 `event.target` 得到发生事件的子元素（li），通过这个子元素调用事件回调函数

2、事件委托的 2 方：

- 委托方：业主 li

- 被委托方：中介 ul

3、使用事件委托的好处

- 添加新的子元素，自动有事件响应处理

- 减少事件监听的数量：n==>1

4、jQuery 的事件委托 API

- 设置事件委托：`$(parentSelector).delegate(childrenSelector, eventName, callback)`

- 移除事件委托：`$(parentSelector).undelegate(eventName)`

```html
<ul>
  <li>1111</li>
  <li>2222</li>
  <li>3333</li>
  <li>4444</li>
</ul>
<li>22222</li>
<br>
<button id="btn1">添加新的li</button>
<button id="btn2">删除ul上的事件委托的监听器</button>
<script src="js/jquery-1.10.1.js"></script>
<script>
  // 设置事件委托
  $('ul').delegate('li', 'click', function () {
    // console.log(this)
    this.style.background = 'red'
  })
  $('#btn1').click(function () {
    $('ul').append('<li>新增的li....</li>')
  })
  $('#btn2').click(function () {
    // 移除事件委托
    $('ul').undelegate('click')
  })
</script>
```

- 事件坐标
  - `event.offsetX`/`event.offsetY`：原点是当前元素左上角（相对于事件元素左上角）
  - `event.clientX`/`event.clientY`：原点是窗口左上角（相对于视口的左上角）
  - `event.pageX`/`event.pageY`：原点是页面左上角（相对于页面的左上角）

![](https://cdn.wallleap.cn/img/pic/illustration/20200815173853.png)

- 事件相关处理
  - 停止事件冒泡：`event.stopPropagation()`
  - 阻止事件的默认行为：`event.preventDefault()`

### 6、动画效果

在一定的时间内，不断改变元素样式

(1) 滑动动画（不断改变元素的高度来实现的）

- `slideDown()`：带动画的展开
- `slideUp()`：带动画的收缩
- `slideToggle()`：带动画的切换展开/收缩

```html
<style type="text/css">
  * {
    margin: 0px;
  }
  .div1 {
    position: absolute;
    width: 200px;
    height: 200px;
    top: 50px;
    left: 10px;
    background: red;
  }
</style>
<body>
<button id="btn1">慢慢收缩</button>
<button id="btn2">慢慢展开</button>
<button id="btn3">收缩/展开切换</button>
<div class="div1">
</div>
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  /*
   需求：
   1. 点击btn1, 向上滑动
   2. 点击btn2, 向下滑动
   3. 点击btn3, 向上/向下切换
   */
  var $div1 = $('.div1')
  // 1. 点击btn1, 向上滑动
  $('#btn1').click(function () {
    $div1.slideUp(3000)
  })
  // 2. 点击btn2, 向下滑动
  $('#btn2').click(function () {
    $div1.slideDown()
  })
  // 3. 点击btn3, 向上/向下切换
  $('#btn3').click(function () {
    $div1.slideToggle()
  })
</script>
```

(2) 淡入淡出动画（不断改变元素的透明度来实现的）

- `fadeIn()`：带动画的显示
- `fadeOut()`：带动画隐藏
- `fadeToggle()`：带动画切换显示/隐藏

```html
<style type="text/css">
  * {
    margin: 0px;
  }
  .div1 {
    position: absolute;
    width: 200px;
    height: 200px;
    top: 50px;
    left: 10px;
    background: red;
  }
</style>
<body>
<button id="btn1">慢慢淡出</button>
<button id="btn2">慢慢淡入</button>
<button id="btn3">淡出/淡入切换</button>
<div class="div1">
</div>
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  /*
   需求：
   1. 点击btn1, 慢慢淡出
     * 无参
     * 有参
       * 字符串参数
       * 数字参数
   2. 点击btn3, 慢慢淡入
   3. 点击btn3, 淡出/淡入切换，动画结束时提示“动画结束了”
   */
  var $div1 = $('.div1')
  $('#btn1').click(function () {
    // $div1.fadeOut()
    // $div1.fadeOut('slow')
    $div1.fadeOut(1000, function () {
      alert('动画完成了!!!')
    })
  })
  $('#btn2').click(function () {
    $div1.fadeIn()
  })
  $('#btn3').click(function () {
    $div1.fadeToggle()
  })
</script>
```

(3) 显示/隐藏动画（不断改变元素的尺寸和透明度来实现）

- `show()`：(不)带动画的显示
- `hide()`：(不)带动画的隐藏
- `toggle()`：(不)带动画的切换显示/隐藏

```html
<style type="text/css">
  * {
    margin: 0px;
  }
  .div1 {
    position: absolute;
    width: 200px;
    height: 200px;
    top: 50px;
    left: 10px;
    background: red;
    display: none;
  }
</style>
<body>
<button id="btn1">瞬间显示</button>
<button id="btn2">慢慢显示</button>
<button id="btn3">慢慢隐藏</button>
<button id="btn4">显示隐藏切换</button>
<div class="div1">
</div>
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  /*
  需求:
  1. 点击btn1, 立即显示
  2. 点击btn2, 慢慢显示
  3. 点击btn3, 慢慢隐藏
  4. 点击btn4, 切换显示/隐藏
   */
  var $div1 = $('.div1')
  //1. 点击btn1, 立即显示
  $('#btn1').click(function () {
    $div1.show()
  })
  //2. 点击btn2, 慢慢显示
  $('#btn2').click(function () {
    $div1.show(1000)
  })
  //3. 点击btn3, 慢慢隐藏
  $('#btn3').click(function () {
    $div1.hide(1000)
  })
  //4. 点击btn4, 切换显示/隐藏
  $('#btn4').click(function () {
    $div1.toggle(1000)
  })
</script>
```

(4) 自定义动画

- `animate({结束时的样式}, time, fun)`：自定义动画效果的动画
- `stop()`：停止动画

```html
<style type="text/css">
  * {
    margin: 0px;
  }

  .div1 {
    position: absolute;
    width: 100px;
    height: 100px;
    top: 50px;
    left: 300px;
    background: red;
  }
</style>
</head>
<body>
<button id="btn1">逐渐扩大</button>
<button id="btn2">移动到指定位置</button>
<button id="btn3">移动指定距离</button>
<button id="btn4">停止动画</button>

<div class="div1">
  花满田间，月照人影
</div>
<!--
jQuery动画本质 : 在指定时间内不断改变元素样式值来实现的
1. animate(): 自定义动画效果的动画
2. stop(): 停止动画
-->
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  /*
   需求：
    1. 逐渐扩大
      1). 宽/高都扩为200px
      2). 宽先扩为200px, 高后扩为200px
    2. 移动到指定位置
      1).移动到(500, 100)处
      2).移动到(100, 20)处
    3.移动指定的距离
      1). 移动距离为(100, 50)
      2). 移动距离为(-100, -20)
    4. 停止动画
   */
  var $div1 = $('.div1')

  /*
   1. 逐渐扩大
     1). 宽/高都扩为200px
     2). 宽先扩为200px, 高后扩为200px
   */
  $('#btn1').click(function () {
    /*
    $div1.animate({
      width: 200,
      height: 200
    }, 1000)
    */
    $div1
      .animate({
        width: 200
      }, 1000)
      .animate({
        height: 200
      }, 1000)
  })
  /*
   2. 移动到指定位置
     1).移动到(500, 100)处
     2).移动到(100, 20)处
   */
  $('#btn2').click(function () {
    // 1).移动到(500, 100)处
    /*
    $div1.animate({ // 向右下移动
      left: 500,
      top: 100
    }, 1000)
    */

    // 2).移动到(100, 20)处
    $div1.animate({ // 向左上移动
      left: 100,  // 300
      top: 20  // 50
    }, 1000)
  })
  /*
   3.移动指定的距离
     1). 移动距离为(100, 50)
     2). 移动距离为(-100, -20)
   */
  $('#btn3').click(function () {
    // 1). 移动距离为(100, 50)
    /*$div1.animate({
      left: '+=100',
      top: '+=50'
    }, 1000)*/
    // 2). 移动距离为(-100, -20)
    $div1.animate({
      left: '-=100',
      top: '-=20'
    }, 3000)
  })
  $('#btn4').click(function () {
    $div1.stop()
  })
</script>
```

jQuery 对象使用特点

- 链式调用：调用 jQuery 对象的任何方法后返回的还是当前 jQuery 对象

```javascript
$('.div1')
  .mouseover(function () {
   console.log('mouseover 进入')
  })
  .mouseout(function () {
   console.log('mouseout 离开')
  })
```

- 读写合一
  - 读：内部第一个 DOM 元素
  - 写：内部所有的 DOM 元素

## 五、jQuery 插件

### 1、扩展插件

扩展 jQuery 的工具方法

```javascript
$.extend({
  xxx: function () {} // this 是 $
})
$.xxx()
```

扩展 jQuery 对象的方法

```javascript
$.fn.extend({
  xxx: function(){}  // this 是 jQuery 对象
})
$obj.xxx()
```

例子：

```html
<style type="text/css">
  * {
    margin: 0px;
  }
  .div1 {
    position: absolute;
    width: 100px;
    height: 100px;
    top: 50px;
    left: 10px;
    background: red;
  }
</style>
<input type="checkbox" name="items" value="足球"/>足球
<input type="checkbox" name="items" value="篮球"/>篮球
<input type="checkbox" name="items" value="羽毛球"/>羽毛球
<input type="checkbox" name="items" value="乒乓球"/>乒乓球
<br/>
<input type="button" id="checkedAllBtn" value="全　选"/>
<input type="button" id="checkedNoBtn" value="全不选"/>
<input type="button" id="reverseCheckedBtn" value="反选"/>
<!--
1. 扩展jQuery的工具方法
  $.extend(object)
1. 扩展jQuery对象的方法
  $.fn.extend(object)
-->
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript" src="js/my_jQuery-plugin.js"></script>
<script type="text/javascript">
  /*
   需求：
   1. 给 $ 添加4个工具方法:
     * min(a, b) : 返回较小的值
     * max(c, d) : 返回较大的值
     * leftTrim() : 去掉字符串左边的空格
     * rightTrim() : 去掉字符串右边的空格
   2. 给jQuery对象 添加3个功能方法:
     * checkAll() : 全选
     * unCheckAll() : 全不选
     * reverseCheck() : 全反选
   */
  console.log($.min(3, 5), $.max(3, 5))
  var string = '   my atguigu    '
  console.log('-----' + $.leftTrim(string) + '-----')
  console.log('-----' + $.rightTrim(string) + '-----')
  var $items = $(':checkbox[name=items]')
  $('#checkedAllBtn').click(function () {
    $items.checkAll()
  })
  $('#checkedNoBtn').click(function () {
    $items.unCheckAll()
  })
  $('#reverseCheckedBtn').click(function () {
    $items.reverseCheck()
  })
</script>
```

### 2、jQuery 插件

- 理解
  - 基于 jQuery 编写的扩展库
  - <http://plugins.jquery.com/>
- jquery-validation
  - 表单验证插件
  - 参考"菜鸟教程"学习 <https://www.runoob.com/jquery/jquery-plugin-validate.html>
  - 使用
    - 下载
    - 引入 js
      - jquery-1.11.1.js
      - jquery.validate.js
      - messages_zh.js
    - 定义验证
      - 直接在标签中指定
      - js 编码指定

- jquery UI  <http://jqueryui.com/>
- laydate   <http://www.layui.com/laydate/>

## 六、其他

### 1、多库共存

```html
<style type="text/css">
  * {
    margin: 0px;
  }
  .div1 {
    position: absolute;
    width: 100px;
    height: 100px;
    top: 50px;
    left: 10px;
    background: red;
  }
</style>
</head>
<body>
<!--
问题：如果有 2 个库都有 $，就存在冲突
解决：jQuery 库可以释放 $ 的使用权，让另一个库可以正常使用，此时 jQuery 库只能使用 jQuery 了
API：jQuery.noConflict()
-->
<script type="text/javascript" src="js/myLib.js"></script>
<script type="text/javascript" src="js/jquery-1.10.1.js"></script>
<script type="text/javascript">
  // 释放 $ 的使用权
  jQuery.noConflict()
  // 调用 myLib 中的 $
  $()
  // 要想使用 jQuery 的功能，只能使用 jQuery
  jQuery(function () {
    console.log('文档加载完成')
  })
</script>
```

### 2、jQuery 中的 `$(function(){})`

```html
<h1>测试window.onload与$(document).ready()</h1>
<img id="logo" src="https://gss0.bdstatic.com/5bVWsj_p_tVS5dKfpU_Y_D3/res/r/image/2017-05-19/6fec71d56242b74eb24b4ac80b817eac.png">
<!--
区别: window.onload与 $(document).ready()
  * window.onload
    * 包括页面的图片加载完后才会回调(晚)
    * 只能有一个监听回调
  * $(document).ready()
    * 等同于: $(function(){})
    * 页面加载完就回调(早)
    * 可以有多个监听回调
-->
<script type="text/javascript" src="js/jquery-1.10.1.js"></script>
<script type="text/javascript">
  /*
   需求：
   1. 直接打印img的宽度，观察其值
   2. 在 $(function(){}) 中 打印 img 的宽度
   3. 在 window.onload 中打印宽度
   4. 在 img 加载完成后打印宽度
   */
  // 1. 直接打印img的宽度，观察其值
  console.log('直接', $('#logo').width())
  window.onload = function () {
    console.log('onload', $('#logo').width())
  }
  window.onload = function () {
    console.log('onload2', $('#logo').width())
  }
  $(function () {
    console.log('ready', $('#logo').width())
  })
  $(function () {
    console.log('ready2', $('#logo').width())
  })
  $('#logo').on('load', function () {
    console.log('img load', $(this).width())
  })
  /*$(document).ready(function () {

  })*/
</script>
```

### 3、练习

以前用原生 js 实现过的用 jQuery 来一遍

(1) 爱好选择器

![](https://cdn.wallleap.cn/img/pic/illustration/20200815180658.png)

```html
<form>
  你爱好的运动是？<input type="checkbox" id="checkedAllBox"/>全选/全不选

  <br/>
  <input type="checkbox" name="items" value="足球"/>足球
  <input type="checkbox" name="items" value="篮球"/>篮球
  <input type="checkbox" name="items" value="羽毛球"/>羽毛球
  <input type="checkbox" name="items" value="乒乓球"/>乒乓球
  <br/>
  <input type="button" id="checkedAllBtn" value="全　选"/>
  <input type="button" id="checkedNoBtn" value="全不选"/>
  <input type="button" id="checkedRevBtn" value="反　选"/>
  <input type="button" id="sendBtn" value="提　交"/>
</form>

<script type="text/javascript" src="jquery-1.10.1.js"></script>
<script type="text/javascript">
  /*
   功能说明:
   1. 点击'全选': 选中所有爱好
   2. 点击'全不选': 所有爱好都不勾选
   3. 点击'反选': 改变所有爱好的勾选状态
   4. 点击'提交': 提示所有勾选的爱好
   5. 点击'全选/全不选': 选中所有爱好, 或者全不选中
   6. 点击某个爱好时, 必要时更新'全选/全不选'的选中状态
   */
  var $checkedAllBox = $('#checkedAllBox')
  var $items = $(':checkbox[name=items]')

  // 1. 点击'全选': 选中所有爱好
  $('#checkedAllBtn').click(function () {
    $items.prop('checked', true)
    $checkedAllBox.prop('checked', true)
  })

  // 2. 点击'全不选': 所有爱好都不勾选
  $('#checkedNoBtn').click(function () {
    $items.prop('checked', false)
    $checkedAllBox.prop('checked', false)
  })

  // 3. 点击'反选': 改变所有爱好的勾选状态
  $('#checkedRevBtn').click(function () {
    $items.each(function () {
      this.checked = !this.checked
    })
    $checkedAllBox.prop('checked', $items.filter(':not(:checked)').length===0)
  })

  //4. 点击'提交': 提示所有勾选的爱好
  $('#sendBtn').click(function () {
    $items.filter(':checked').each(function () {
      alert(this.value)
    })
  })

  // 5. 点击'全选/全不选': 选中所有爱好, 或者全不选中
  $checkedAllBox.click(function () {
    $items.prop('checked', this.checked)
  })

  // 6. 点击某个爱好时, 必要时更新'全选/全不选'的选中状态
  $items.click(function () {
    $checkedAllBox.prop('checked', $items.filter(':not(:checked)').length===0)
  })
</script>
```

(2) 增删员工记录

![](https://cdn.wallleap.cn/img/pic/illustration/20200815180844.png)

```html
<style>
#total{width:450px;margin-left:auto;margin-right:auto}ul{list-style-type:none}li{border-style:solid;border-width:1px;padding:5px;margin:5px;background-color:#9f9;float:left}.inner{width:400px;border-style:solid;border-width:1px;margin:10px;padding:10px;float:left}#employeeTable{border-spacing:1px;background-color:black;margin:80px auto 10px auto}th,td{background-color:white}#formDiv{width:250px;border-style:solid;border-width:1px;margin:50px auto 10px auto;padding:10px}#formDiv input{width:100%}.word{width:40px}.inp{width:200px}#employeeTable,#employeeTable th,#employeeTable td{border:1px solid;border-spacing:0}
</style>
<table id="employeeTable">
  <tr>
    <th>Name</th>
    <th>Email</th>
    <th>Salary</th>
    <th>&nbsp;</th>
  </tr>
  <tr>
    <td>Tom</td>
    <td>tom@tom.com</td>
    <td>5000</td>
    <td><a href="deleteEmp?id=001">Delete</a></td>
  </tr>
  <tr>
    <td>Jerry</td>
    <td>jerry@sohu.com</td>
    <td>8000</td>
    <td><a href="deleteEmp?id=002">Delete</a></td>
  </tr>
  <tr>
    <td>Bob</td>
    <td>bob@tom.com</td>
    <td>10000</td>
    <td><a href="deleteEmp?id=003">Delete</a></td>
  </tr>
</table>
<div id="formDiv">
  <h4>添加新员工</h4>
  <table>
    <tr>
      <td class="word">name:</td>
      <td class="inp">
        <input type="text" name="empName" id="empName"/>
      </td>
    </tr>
    <tr>
      <td class="word">email:</td>
      <td class="inp">
        <input type="text" name="email" id="email"/>
      </td>
    </tr>
    <tr>
      <td class="word">salary:</td>
      <td class="inp">
        <input type="text" name="salary" id="salary"/>
      </td>
    </tr>
    <tr>
      <td colspan="2" align="center">
        <button id="addEmpButton" value="abc">
          Submit
        </button>
      </td>
    </tr>
  </table>
</div>
```

初级版本

```html
<script type="text/javascript" src="jquery-1.10.1.js"></script>
<script type="text/javascript">
  /*
  1. 添加
  2. 删除
   */
  $('#addEmpButton').click(function () {
    //1. 收集输入的数据
    var $empName = $('#empName')
    var $email = $('#email')
    var $salary = $('#salary')
    var empName = $empName.val()
    var email = $email.val()
    var salary = $salary.val()

    //2. 生成对应的<tr>标签结构, 并插入#employeeTable的tbody中
    /*
     <tr>
       <td>Bob</td>
       <td>bob@tom.com</td>
       <td>10000</td>
       <td><a href="deleteEmp?id=003">Delete</a></td>
     </tr>
     */
    var $xxx = $('<tr></tr>')
      .append('<td>'+empName+'</td>') // 拼串
      .append('<td>'+email+'</td>')
      .append('<td>'+salary+'</td>')
      .append('<td><a href="deleteEmp?id="'+Date.now()+'>Delete</a></td>')
      .appendTo('#employeeTable>tbody')
      .find('a')
      .click(clickDelete)

    //3. 清除输入
    $empName.val('')
    $email.val('')
    $salary.val('')
  })

  // 给所有删除链接绑定点击监听
  $('#employeeTable a').click(clickDelete)

  /*
  点击删除的回调函数
   */
  function clickDelete () {
    var $tr = $(this).parent().parent()
    var name = $tr.children(':first').html()
    if(confirm('确定删除'+name+'吗?')) {
      $tr.remove()
    }

    return false
  }
  
</script>
```

进阶版本

```html
<script type="text/javascript" src="jquery-1.10.1.js"></script>
<script type="text/javascript">
  /*
  1. 添加
  2. 删除
   */
  $('#addEmpButton').click(function () {
    //1. 收集输入的数据
    var $empName = $('#empName')
    var $email = $('#email')
    var $salary = $('#salary')
    var empName = $empName.val()
    var email = $email.val()
    var salary = $salary.val()

    //2. 生成对应的<tr>标签结构, 并插入#employeeTable的tbody中
    /*
     <tr>
       <td>Bob</td>
       <td>bob@tom.com</td>
       <td>10000</td>
       <td><a href="deleteEmp?id=003">Delete</a></td>
     </tr>
     */
    var $xxx = $('<tr></tr>')
      .append('<td>'+empName+'</td>') // 拼串
      .append('<td>'+email+'</td>')
      .append('<td>'+salary+'</td>')
      .append('<td><a href="deleteEmp?id="'+Date.now()+'>Delete</a></td>')
      .appendTo('#employeeTable>tbody')

    //3. 清除输入
    $empName.val('')
    $email.val('')
    $salary.val('')
  })

  // 通过table实现对所有a的click事件委托
  $('#employeeTable').delegate('a', 'click', clickDelete)

  /*
  点击删除的回调函数
   */
  function clickDelete () {
    var $tr = $(this).parent().parent()
    var name = $tr.children(':first').html()
    if(confirm('确定删除'+name+'吗?')) {
      $tr.remove()
    }
    return false
  }
</script>
```

(3) 轮播图

```html
<style type="text/css">
/*去除内边距,没有链接下划线*/
* {
  margin: 0;
  padding: 0;
  text-decoration: none;
}
/*让<body有20px的内边距*/
body {
  padding: 20px;
}
/*最外围的div*/
#container {
width: 600px;
height: 400px;
overflow: hidden;
position: relative; /*相对定位*/
margin: 0 auto;
}
/*包含所有图片的<div>*/
#list {
width: 4200px; /*7张图片的宽: 7*600 */
height: 400px;
position: absolute; /*绝对定位*/
z-index: 1;
}
/*所有的图片<img>*/
#list img {
float: left; /*浮在左侧*/
}
/*包含所有圆点按钮的<div>*/
#pointsDiv {
position: absolute;
height: 10px;
width: 100px;
z-index: 2;
bottom: 20px;
left: 250px;
}
/*所有的圆点<span>*/
#pointsDiv span {
cursor: pointer;
float: left;
border: 1px solid #fff;
width: 10px;
height: 10px;
border-radius: 50%;
background: #333;
margin-right: 5px;
}
/*第一个<span>*/
#pointsDiv .on {
background: orangered;
}
/*切换图标<a>*/
.arrow {
  cursor: pointer;
  display: none;
  line-height: 39px;
  text-align: center;
  font-size: 36px;
  font-weight: bold;
  width: 40px;
  height: 40px;
  position: absolute;
  z-index: 2;
  top: 180px;
  background-color: RGBA(0, 0, 0, 0.3);
  color: #fff;
}
/*鼠标移到切换图标上时*/
.arrow:hover {
  background-color: RGBA(0, 0, 0, 0.7);
}
/*鼠标移到整个div区域时*/
#container:hover .arrow {
display: block; /*显示*/
}
/*上一个切换图标的左外边距*/
#prev {
left: 20px;
}
/*下一个切换图标的右外边距*/
#next {
right: 20px;
}
</style>
<div id="container">
  <div id="list" style="left: -600px;">
    <img src="img/5.jpg" alt="5"/>
    <img src="img/1.jpg" alt="1"/>
    <img src="img/2.jpg" alt="2"/>
    <img src="img/3.jpg" alt="3"/>
    <img src="img/4.jpg" alt="4"/>
    <img src="img/5.jpg" alt="5"/>
    <img src="img/1.jpg" alt="1"/>
  </div>
  <div id="pointsDiv">
    <span index="1" class="on"></span>
    <span index="2"></span>
    <span index="3"></span>
    <span index="4"></span>
    <span index="5"></span>
  </div>
  <a href="javascript:;" id="prev" class="arrow">&lt;</a>
  <a href="javascript:;" id="next" class="arrow">&gt;</a>
</div>
<script type="text/javascript" src="jquery-1.10.1.js"></script>
<script>
  /*
 功能说明:
 1. 点击向右(左)的图标, 平滑切换到下(上)一页
 2. 无限循环切换: 第一页的上一页为最后页, 最后一页的下一页是第一页
 3. 每隔3s自动滑动到下一页
 4. 当鼠标进入图片区域时, 自动切换停止, 当鼠标离开后,又开始自动切换
 5. 切换页面时, 下面的圆点也同步更新
 6. 点击圆点图标切换到对应的页

 bug: 快速点击时, 翻页不正常
 */
$(function () {

  var $container = $('#container')
  var $list = $('#list')
  var $points = $('#pointsDiv>span')
  var $prev = $('#prev')
  var $next = $('#next')
  var PAGE_WIDTH = 600 //一页的宽度
  var TIME = 400 // 翻页的持续时间
  var ITEM_TIME = 20 // 单元移动的间隔时间
  var imgCount = $points.length
  var index = 0 //当前下标
  var moving = false // 标识是否正在翻页(默认没有)


  // 1. 点击向右(左)的图标, 平滑切换到下(上)一页
  $next.click(function () {
    // 平滑翻到下一页
    nextPage(true)
  })
  $prev.click(function () {
    // 平滑翻到上一页
    nextPage(false)
  })

  // 3. 每隔3s自动滑动到下一页
  var intervalId = setInterval(function () {
    nextPage(true)
  }, 1000)

  // 4. 当鼠标进入图片区域时, 自动切换停止, 当鼠标离开后,又开始自动切换
  $container.hover(function () {
    // 清除定时器
    clearInterval(intervalId)
  }, function () {
    intervalId = setInterval(function () {
      nextPage(true)
    }, 1000)
  })

  // 6. 点击圆点图标切换到对应的页
  $points.click(function () {
    // 目标页的下标
    var targetIndex = $(this).index()
    // 只有当点击的不是当前页的圆点时才翻页
    if(targetIndex!=index) {
      nextPage(targetIndex)
    }
  })

  /**
   * 平滑翻页
   * @param next
   * true: 下一页
   * false: 上一页
   * 数值: 指定下标页
   */
  function nextPage (next) {
    /*
      总的时间: TIME=400
      单元移动的间隔时间: ITEM_TIME = 20
      总的偏移量: offset
      单元移动的偏移量: itemOffset = offset/(TIME/ITEM_TIME)

      启动循环定时器不断更新$list的left, 到达目标处停止停止定时器
     */
    //如果正在翻页, 直接结束
    if(moving) { //已经正在翻页中
      return
    }
    moving = true // 标识正在翻页
    // 总的偏移量: offset
    var offset = 0
    // 计算offset
    if(typeof next==='boolean') {
      offset = next ? -PAGE_WIDTH : PAGE_WIDTH
    } else {
      offset = -(next-index)* PAGE_WIDTH
    }
    // 计算单元移动的偏移量: itemOffset
    var itemOffset = offset/(TIME/ITEM_TIME)
    // 得到当前的left值
    var currLeft = $list.position().left
    // 计算出目标处的left值
    var targetLeft = currLeft + offset
    // 启动循环定时器不断更新$list的left, 到达目标处停止停止定时器
    var intervalId = setInterval(function () {
      // 计算出最新的currLeft
      currLeft += itemOffset
      if(currLeft===targetLeft) { // 到达目标位置
        // 清除定时器
        clearInterval(intervalId)
        // 标识翻页停止
        moving = false
        // 如果到达了最右边的图片(1.jpg), 跳转到最左边的第2张图片(1.jpg)
        if(currLeft===-(imgCount+1) * PAGE_WIDTH) {
          currLeft = -PAGE_WIDTH
        } else if(currLeft===0){
          // 如果到达了最左边的图片(5.jpg), 跳转到最右边的第2张图片(5.jpg)
          currLeft = -imgCount * PAGE_WIDTH
        }
      }
      // 设置 left
      $list.css('left', currLeft)
    }, ITEM_TIME)

    // 更新圆点
    updatePoints(next)
  }
  /**
   * 更新圆点
   * @param next
   */
  function updatePoints (next) {

    // 计算出目标圆点的下标 targetIndex
    var targetIndex = 0
    if(typeof next === 'boolean') {
      if(next) {
        targetIndex = index + 1   // [0, imgCount-1]
        if(targetIndex===imgCount) {// 此时看到的是1.jpg-->第1个圆点
          targetIndex = 0
        }
      } else {
        targetIndex = index - 1
        if(targetIndex===-1) { // 此时看到的是5.jpg-->第5个圆点
          targetIndex = imgCount-1
        }
      }
    } else {
      targetIndex = next
    }
    // 将当前index的<span>的class移除
    // $points.eq(index).removeClass('on')
    $points[index].className = ''
    // 给目标圆点添加class='on'
    // $points.eq(targetIndex).addClass('on')
    $points[targetIndex].className = 'on'

    // 将index更新为targetIndex
    index = targetIndex
  }
})
</script>
```

jQuery 文档的结构图

![](https://cdn.wallleap.cn/img/pic/illustration/20200815175515.png)
