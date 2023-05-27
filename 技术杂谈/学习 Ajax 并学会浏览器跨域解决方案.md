---
title: 学习 Ajax 并学会浏览器跨域解决方案
date: 2020-07-04 23:33
updated: 2020-07-04 23:33
cover: //cdn.wallleap.cn/img/pic/cover/202302oGzHLq.jpg
category: 技术杂谈
tags:
  - web
  - 前端
description: 学习 Ajax 并学会浏览器跨域解决方案
---

AJAX 全称为 Asynchronous JavaScript and XML，异步的 JS 和 XML，是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。

## 一、概述

> Web 程序的最初的目的就是将信息(数据)放到公共的服务器，让所有的网络用户都可以通过浏览器访问

![](https://cdn.wallleap.cn/img/pic/illustration/20200815183452.png)

在此之前，我们可以通过以下几种方式让浏览器发出服务端的请求，获得服务端的数据：

- 地址栏输入地址，回车，刷新

- 特定元素的 href 或 src 属性

- 表单提交

这些方案都是我们无法通过或者很难通过代码的方式进行编程(对服务器发出请求并且接收服务端返回的响应)，如果我们可以通过 JavaScript 直接发送网络请求，那么 web 的可能就会更多，随之能够实现的功能也会更多，至少不再是“单机游戏”。

1、AJAX(Asynchronous JavaScript and XML,异步的JS和XML)，最早出现在2005年的Google Suggest，是在浏览器端进行网络编程(发送请求，接收响应)的技术方案，它使我们可以**通过 JavaScript 直接获取服务端最新的内容而不必重新加载页面**，让 web 更能接近桌面应用的用户体验。

说白了，AJAX 就是**浏览器提供的一套 API**，可以通过 JavaScript 调用，从而实现代码控制请求与响应，实现网络编程。(AJAX 不是新的编程语言，而是一种将现有标准组合在一起使用的新的方式)

> 能力不够 API 凑。
> 对xxx进行编程指的就是用代码的方式操作它

2、XML

可扩展标记语言，被设计用来传输和存储数据，和 HTML 有点像，但是 HTML 中都是预定义标签，而 XML 中没有预定义标签，全都是自定义标签，用来表示一些数据。

现在已经被 JSON 取代了。

3、AJAX的特点

(1) 优点

可以无需刷新页面而与服务器端进行通信。

允许你根据用户事件来更新部分页面内容。

(2) 缺点

没有浏览历史，不能回退

存在跨域问题(同源)

SEO 不友好

补充：搭建环境

**使用 NodeJS 搭建后台**

1、安装

先下载安装 [nodejs](https://nodejs.org/en/)

进入一个文件夹，输入命令创建 node 应用

```bash
npm init --yes
```

![node 初始化命令](https://cdn.wallleap.cn/img/pic/illustration/image-20200810090417637.png)

接着输入命令，安装 express

```bash
npm install express
```

![express 安装](https://cdn.wallleap.cn/img/pic/illustration/image-20200810090617412.png)

2、基本使用

(1) 编写代码

```javascript
// 1、引入 express
const express = require('express')
const { response } = require('express')

// 2、创建应用对象
const app = express()

// 3、创建路由规则 
// request 是对请求报文的封装；response 是对响应报文的封装
app.get('/', (request, response) => { // 前端访问http://localhost:8000/
  // 设置响应
  response.send('Hello Express')
})

// 4、监听端口启动服务
app.listen(8000, () => {
  console.log('服务已经启动，8000端口监听中，请访问http://localhost:8000/')
})
```

(2) 运行代码

在该目录下输入命令

```bash
node 文件名.js
```

eg:

```bash
node expressTest.js
```

接着访问地址 <http://localhost:8000/> 即可

3、准备服务端代码

`server.js`

```javascript
const express = require('express')
const { response } = require('express')
const app = express()
// 设置 get 请求，并且设置请求路径为 '/'，之后的 AJAX 代码写在这里，可以通过浏览器访问 http://localhost:8000
app.get('/', (request, response) => {
  // 设置响应体
  response.send(`
    <!Doctype html>
    <html lang="zh-CN">
      <head>
        <meta charset="UTF-8">
        <title>AJAX 学习</title>
      </head>
      <body>
        <h1>这是一个页面</h1>
      </body>
    </html>
  `)
})
// 这里设置为 get，则请求方式为 GET，'/server' 则请求 url 需要加上这个
// 之后的服务器端数据就放在这下面
app.get('/server', (request, response) => {
  // 设置响应头
  // response.setHeader('Access-Control-Allow-origin','*') // 设置允许跨域，暂时不需要
  // 设置响应体
  response.send('Hello AJAX')
})
// 在这里接着加上接口
app.listen(8000, () => {
  console.log('服务已经启动，8000端口监听中，请访问 http://localhost:8000/')
})
```

关闭上面那个，将这个启动：

```bash
node server.js
```

现在每次修改 `server.js` 都需要重新运行一遍命令，我们可以使用热更新，借助 reload 包——nodemon

自动检测 js 代码变化，restart 服务

1、安装

```sh
npm install -g nodemon
```

2、利用nodemon执行文件

```sh
nodemon 文件名.js
```

例如：

```sh
nodemon server.js
```

可以把这个命令写到 `package.json` 中，这样就可以直接使用 `npm run dev` 来启动服务了

```json
"scripts": {
  "dev": "nodemon server.js"
},
```

## 二、快速上手

### 1、AJAX 基础

(一个构造函数、两个方法、一个事件)

修改 `app.get('/')` 中的代码，即浏览器访问的页面，进行发送请求

```js
app.get('/', (request, response) => {
  // 设置响应体
  response.send(`
    <!Doctype html>
    <html lang="zh-CN">
      <head>
        <meta charset="UTF-8">
        <title>AJAX 学习</title>
        <style>
          #result{
            width:200px;
            height:100px;
            border:1px solid skyblue;
          }
        </style>
      </head>
      <body>
        <button id="btn">点击发送请求</button>
        <div id="result"></div>
        <script>
          btn.onclick = function(){
            // 涉及到 AJAX 操作的页面不能使用文件协议访问（文件的方式访问）
            // AJAX 是一套 API，核心提供的类型：XMLHttpRequest XML-->JSON(现在使用的是 JSON 格式的了)
            // 1、安装浏览器（用户代理）——创建对象
            var xhr = new XMLHttpRequest() // xhr 就类似于浏览器的作用(发送请求接收响应)
            // 2、打开浏览器 输入网址——初始化 设置请求方式和 url
            xhr.open('GET', 'http://localhost:8000/server')  // 这一步只是在搭桥铺路
            // 3、敲回车键 开始请求——发送
            xhr.send()  // send 才是开始请求
            /* 上面三个是ajax核心代码 */
          }
        </script>
      </body>
    </html>
  `)
})
```

接着在 `onclick` 函数中写代码，接收响应

```js
/* 因为响应需要时间，所以无法通过返回值的方式返回响应 */
// var response = xhr.send()
// console.log(response) // undefine

// 4、等待响应——事件绑定 处理服务端返回的结果
/* 如果需要捕获状态的变化，需要注意代码的执行顺序的问题(不要出现来不及的情况)
* 因为客户端永远不知道服务端何时才能返回我们需要的响应，所以AJAX API采用事件的机制(通知的感觉)
*/
xhr.onreadystatechange = function(){ // 建议事件使用addEventListener方式
  // 这个事件并不是只在响应时触发，XHR状态改变就触发
  console.log(this.readyState)
  if(this.readyState!==4) return
  // 所以下面就是为4的情况
  // 5、看结果
  console.log(this.responseText) // 获取响应内容(响应体)
  result.innerHTML = xhr.response
}
```

![ajax基础操作](https://cdn.wallleap.cn/img/pic/illustration/20200815183735.png)

点击按钮

![发送请求得到响应](https://cdn.wallleap.cn/img/pic/illustration/202305271458411.gif)

### 2、理解 readyState

`onreadystatechange` 是 XHR 状态改变时触发的

```js
var xhr = new XMLHttpRequest()
console.log(xhr.readyState) // 0
xhr.open('GET', './time.php')
console.log(xhr.readyState) // 1
xhr.send()
// console.log(xhr.readyState) // 1 取上面那个
xhr.addEventListener('readystatechange', function(){
  // if(this.readyState !== 4) return
  // console.log(this.responseText)
  console.log(this.readyState) // 2 3 4
})
```

readyState：

![readyState代码](https://cdn.wallleap.cn/img/pic/illustration/20200815183844.png)

0 -->  `new XMLHttpRequest` 初始化 **请求代理对象**

1 –-> `open` 方法已经调用，**建立**一个与服务端特定端口的**连接**

2  –-> 已经**接收**到了响应报文的**响应头** `console.log(this.getAllResponseHeaders())` 可以拿到响应头，拿不到响应体

拆分：`console.log(this.getAllResponseHeaders().splite(‘\n’).splite(‘:’))`

获取指定键：`console.log(this.getAllResponseHeaders(‘data’))`

3 –-> **正在下载响应报文的响应体**，可能响应体为空或不完整

4 –-> 一切 OK，**整个响应报文已经下载下来**了 `console.log(this.responseText)`

![readyState](https://cdn.wallleap.cn/img/pic/illustration/20200815183915.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200815183935.png)

所以应该**在 readyState 的值为 4** 时，才去处理后续的逻辑

可以用 `xhr.onload` 替代

```js
var xhr = new XMLHttpRequest()
xhr.open('GET', 'time.php')
xhr.send(null) // send可以传请求体，传null代表没有请求体
xhr.onload = function (){ // 加载完成 H5 中提供的 XMLHttpRequest version 2.0 定义的
  // 相当于 readyState 为 4 之后的
  console.log(this.responseText)
}
```

ps: `console.log(this)` 显示 readyState 是 2、3、4 可展开来全都是4，这个是 `console.log` 的机制问题，展开的时候只会显示此时的状态

例如：

![log机制测试](https://cdn.wallleap.cn/img/pic/illustration/20200815184045.png)

在浏览器上看，不展开没问题显示123，展开的一瞬间都是456

### 3、AJAX 遵循 HTTP 协议

HTTP 协议(Hypertext Transport Protocol，超文本传输协议)详细规定了浏览器和万维网服务器之间互相通信的规则。

本质上 XMLHttpRequest 就是 JavaScript 在 web 平台中发送 HTTP 请求的手段，所以我们发送出去的请求仍然是 HTTP 请求，同样符合 HTTP 约定的格式

请求报文：

- 请求行
  
  - `POST /s?ie=utf-8 HTTP/1.1`
  - `GET /s?ie=utf-8 HTTP/1.1`

- 请求头
  
  - `Host: wallleap.cn`
  - `Cookie: name=luwang`
  - `Content-Type: application/x-www-form-urlencoded`
  - `User-Agent: chrome 83`

- 空行(必须得有)

- 请求体 (GET请求这里为空，POST 可不为空)
  
  - `username=admin&password=admin`

响应报文：

- 行
  
  - `HTTP/1.1 200 OK`
  - `HTTP/1.1 404 Not Found`
  - `HTTP/1.1 403 Forbidden`
  - `HTTP/1.1 401 Unauthorized`
  - `HTTP/1.1 500 Internal Server Error`

- 头
  
  - `Content-Type: text/html;charset=utf-8`
  - `Content-length: 2048`
  - `Content-encoding: gzip`

- 空行

- 体  

  ```html
  <html>
    <head>
    </head>
    <body>
      <h1>wallleap</h1>
    </body>
  </html>
  ```

![HTTP响应报文信息](https://cdn.wallleap.cn/img/pic/illustration/20200815184354.png)

```html
<script>
  // 1、创建对象
  var xhr = new XMLHttpRequest()
  // 2、初始化 设置请求方法和url
  xhr.open('POST', '/server') // 设置请求行
  xhr.setRequestHeader('Foo', 'Bar') // 设置一个请求头
  // 一旦请求体是urlencoded格式的内容，一定要设置请求头中的Content-Type为下面这个
  xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded;charset=utf-8') // 设置第二请求头
  xhr.send('key1=value1&key2=value2') // 以urlencoded格式设置请求体
  // xhr.send('{"foo": "123"}') // 以json格式设置请求体，上面设置 'application/json; charset=utf-8'
  xhr.onload = function (){
    // 响应行
    console.log(this.status) // 获取响应状态码
    console.log(this.statusText) // 获取响应状态描述
    // 获取响应头信息
    console.log(this.getResponseHeader('Content-Type')) // 指定响应头
    console.log(this.getAllResponseHeaders()) // 全部响应头
    // 获取响应体
    console.log(this.responseText) // 文本形式
    console.log(this.responseXML) // XML形式，了解即可
  }
</script>
```

补充：

```javascript
xhr.addEventListener('readystatechange', function(){
    if(this.readyState === 4 && this.status === 200){
      console.log(this)
    }
})
```

可能有的人会像上面一样同时判断状态码200，事实上没有必要，状态码404也需要处理,可以到里面嵌套，例如：

```javascript
xhr.onreadystatechange = function() {
  if(this.readyState === 4){
    if(this.status >= 200  && xhr.status < 300){ // 也可以用 xhr.onload = () => {}
      // 处理结果
    }else if(xhr.status >= 400) { // 也可以用 xhr.onerror = () => {}
      ...
    }
  }
})
```

Chrome 打开开发者模式

点击 Network 能够看到传输的文件

点击 XHR 查看

Request Headers——请求头

点击 view source 可以看到请求行

Response Header——响应头

点击 view source 可以看到响应行

Response——响应体

Preview——预览，对响应体解析之后的页面

## 三、具体用法

### 1、数据接口的概念

服务器端返回的响应就是一个 JSON 内容（返回的就是数据）

对于返回数据的地址一般我们称之为接口（形式上是 web 形式）

例如，豆瓣前五十电影：<http://api.douban.com/v2/movie/top250>

提供一定的能力，有输入有输出就可以称为接口

### 2、AJAX 发送 GET 请求并传递参数

```html
<script>
  var xhr = new XMLHttpRequest()
  // GET 请求传递参数通常使用URL中的问号传递数据
  xhr.open('GET', 'http://127.0.0.1:8000/server?a=100&b=200&c=300')
  // 一般在 GET 请求时无需设置响应体，可以传 null 或者干脆不传
  xhr.send(null)
  xhr.onreadystatechange = function (){
    if(this.readyState !== 4) return
    console.log(this.responseText)
  }
</script>
<!-- 一般情况下URL传递的都是参数性质的数据，而POST一般都是业务数据 -->
```

例子：将得到的四个用户名称{}放到ul>li中，点击li能够获取到该用户的年龄

```html
<ul id="list"></ul>
<script>
  var listElement = document.getElementById('list')
  /* 发送请求获取到列表数据，呈现在页面上 */
  var xhr = new XMLHttpRequest()
  xhr.open('POST', '/server?id=2')
  xhr.send(null)
  xhr.onreadystatechange = function (){
    if(this.readyState !== 4) return
    var data = JSON.parse(this.responseText)
    // console.log(data)
    for(var i = 0; i < data.length; i++){
      // console.log(data[i])
      var liElement = document.createElement('li')
      liElement.innerHTML = data[i].name
      liElement.id = data[i].id
      listElement.appendChild(liElement)
      /* 给每一个li注册点击事件 */
      // 由于li是动态创建的，因此需要移到创建li的时候
      listElement.addEventListener('click', function (){
          // TODO: 通过AJAX操作获取服务端对应数据的信息
          // 获取当前被点击元素对应数据的id
          // console.log(this.id)
          var xhr1 = new XMLHttpRequest()
          xhr1.open('GET', 'users.php?id=' + this.id)
          xhr1.send()
          xhr1.onreadystatechange = function (){
            if(this.readyState !== 4) return
            var obj = JSON.parse(this.responseText)
            alert(obj.age)
          }
      })
    }
  }
</script>
```

### 3、POST 请求

POST 请求过程中，都是采用请求体承载需要提交的数据

```javascript
// 1.创建对象
const xhr = new XMLHttpRequest()
// 2.初始化 设置类型与URL(open的第一个参数的作用就是设置请求的method)
xhr.open('POST','http://localhost:8000/server')
// 设置请求头信息
xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded') // 设置请求头中的Content-Type为application/x-www-form-urlencoded——标识这次请求得请求体格式为urlencoded以便于服务端接收数据
// xhr.setRequestHeader('name','wallleap') // 也可以自定义
// 3.发送 POST方式需要提交到服务端的数据可以通过send方法的参数传递，格式：key1=value1&key2=value2
xhr.send("key1=value1&key2=value2")
// xhr.send("key1:value1&key2:value2")
// xhr.send("value1")  // --->可以随意写，但是需要按格式，方便后台处理
// 4.事件绑定
xhr.onreadystatechange = function(){
  // 判断
  if(xhr.readyState===4){
    if(xhr.status >= 200 && xhr.status < 300){
      // 处理服务端返回的结果
      result.innerHTML = xhr.response
    }
  }
}
```

由于 `server.js` 中只设置了 get 的允许跨域，因此需要在文件中加入允许 post 跨域的代码

```javascript
// app.get('/server', (request, response) => {
app.post('/server', (request, response) => {
  // 设置响应头  设置允许跨域
  response.setHeader('Access-Control-Allow-Origin', '*');
  // 设置允许所有头信息，就比如上面设置的自定义响应头会报错，就需要加上这个
  // response.setHeader('Access-Control-Allow-Headers', '*');
  // 设置响应体
  response.send('HELLO AJAX POST');
});
```

可以改为 all

````javascript
//可以接收任意类型的请求(get/post/options/...)
app.all('/server', (request, response) => {
  //设置响应头  设置允许跨域
  response.setHeader('Access-Control-Allow-Origin', '*');
  //响应头
  response.setHeader('Access-Control-Allow-Headers', '*');
  //设置响应体
  response.send('HELLO AJAX POST');
});
````

测试

```html
<style>
#result{
  width:200px;
  height:100px;
  border:solid 1px #903;
}
</style>
</head>
<body>
<div id="result"></div>
<script>
  //获取元素对象
  const result = document.getElementById("result");
  //绑定事件
  result.addEventListener("mouseover", function(){
    //1. 创建对象
    const xhr = new XMLHttpRequest();
    //2. 初始化 设置类型与 URL
    xhr.open('POST', 'http://127.0.0.1:8000/server');
    //设置请求头
    xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded');
    xhr.setRequestHeader('name','wallleap');
    //3. 发送
    xhr.send('a=100&b=200&c=300');
    // xhr.send('a:100&b:200&c:300');
    // xhr.send('1233211234567');
    //4. 事件绑定
    xhr.onreadystatechange = function(){
      //判断
      if(xhr.readyState === 4){
        if(xhr.status >= 200 && xhr.status < 300){
          //处理服务端返回的结果
          result.innerHTML = xhr.response
        }
      }
    }
  });
</script>
```

例子：点击登录按钮不刷新页面将数据传到后台

```html
<style>
.loading{
  display: none;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #555;
  text-align: center;
  padding-top: 200px;
  opacity: .5;
}
.loading::after{
  content: '加载中……';
  font-size: 60px;
  color: #fff;
}
</style>
<div class="loading"></div>
<table border="1">
  <tr>
    <td>用户名</td>
    <td><input type="text" name="" id="username"></td>
  </tr>
  <tr>
    <td>密码</td>
    <td><input type="password" name="" id="password"></td>
  </tr>
  <tr>
    <td></td>
    <td><button id="btn">登录</button></td>
  </tr>
</table>
<script>
  // 找一个合适的时机，做一件合适的事情(时间、内容)
  // 1、获取界面上的元素 value
  var textUsername = document.getElementById('username')
  var textPassword = document.getElementById('password')
  var btn = document.getElementById('btn')
  var loading = document.querySelector('.loading')
  btn.onclick = function (){
    loading.style.display = 'block'
    var username = textUsername.value
    var password = textPassword.value
    // 2、通过XHR发送一个POST请求
    var xhr = new XMLHttpRequest
    xhr.open('POST', '/login')
    // 一定注意：如果请求体是urlencoded格式，必须设置这个请求头！
    xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
    // xhr.send('username=' + username + '&password=' + password)
    xhr.send(`username=${username}&password=${password}`)
    // 3、根据服务端的反馈，作出界面提示
    xhr.onreadystatechange = function (){
      if(this.readyState !== 4) return
      console.log(this.responseText)
      loading.style.display = 'none'
    }
  }
</script>
```

### 4、同步和异步

生活中：

同步：一个人在同一个时刻只能做一件事情，在执行一些耗时的操作(不需要看管)不去做别的事情，只是等待

异步：在执行一些耗时的操作(不需要看管)去做别的事，而不是等待

`xhr.open()` 第三个参数(async)要求传入的是一个 bool 值，其作用就是设置此次请求是否采用异步方式执行，默认为 true，如果需要同步执行可以通过传递 false 实现

![](https://cdn.wallleap.cn/img/pic/illustration/20200815184832.png)

`console.time(‘标识’)` 启动一个秒表

中间写代码

`console.timeEnd(‘标识’)` 结束这个秒表

这样就能知道用了多长时间(标识名称得相同)

![](https://cdn.wallleap.cn/img/pic/illustration/20200815184906.png)

如果采用同步方式执行，则代码会卡死在 `xhr.send()` 这一步

![](https://cdn.wallleap.cn/img/pic/illustration/20200815184921.png)

send 方法会不会出现等待情况(区分同异步)

![](https://cdn.wallleap.cn/img/pic/illustration/20200815184939.png)

知道同步模式即可(已被遗弃)

![](https://cdn.wallleap.cn/img/pic/illustration/20200815184956.png)

同步模式注册时间时机问题

![](https://cdn.wallleap.cn/img/pic/illustration/20200815185018.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200815185029.png)

### 5、响应数据格式

如果希望服务器返回一个复杂数据，该如何处理：

 服务器发出何种格式的数据，这个格式如何在客户端用JavaScript解析

5.1 XML

一种数据描述手段

老掉牙的东西，现在项目中基本不使用

淘汰的原因：数据冗余太多

![](https://cdn.wallleap.cn/img/pic/illustration/20200815185058.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200815185108.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200815185115.png)

5.2 JSON

也是一种数据描述手段，类似于 JavaScript 字面量方式

服务端采用 JSON 格式返回数据，客户端按照 JSON 格式解析数据

![](https://cdn.wallleap.cn/img/pic/illustration/20200815185141.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200815185148.png)

来测试一下 JSON 的

`server.js`中添加

```javascript
//JSON 响应
app.all('/json-server', (request, response) => {
  //设置响应头  设置允许跨域
  response.setHeader('Access-Control-Allow-Origin', '*');
  //响应头
  response.setHeader('Access-Control-Allow-Headers', '*');
  //响应一个数据
  const data = {
    name: 'wallleap'
  };
  //对对象进行字符串转换
  let str = JSON.stringify(data);
  //设置响应体
  response.send(str);
});
```

测试

```html
<style>
  #result{
    width:200px;
    height:100px;
    border:solid 1px #89b;
  }
</style>
<div id="result"></div>
<script>
  //绑定键盘按下事件
  window.onkeydown = function(){
    //发送请求
    const xhr = new XMLHttpRequest();
    //设置响应体数据的类型
    xhr.responseType = 'json'; // 自动转换
    //初始化
    xhr.open('GET','http://127.0.0.1:8000/json-server');
    //发送
    xhr.send();
    //事件绑定
    xhr.onreadystatechange = function(){
      if(xhr.readyState === 4){
        if(xhr.status >= 200 && xhr.status < 300){
          // console.log(xhr.response);
          // result.innerHTML = xhr.response;
          // 1. 手动对数据转化
          // let data = JSON.parse(xhr.response);
          // console.log(data);
          // result.innerHTML = data.name;
          // 2. 自动转换
          console.log(xhr.response);
          result.innerHTML = xhr.response.name;
        }
      }
    }
  }
</script>
```

注意：

不论是 JSON，还是 XML，只是在 AJAX 请求过程中用到，并不代表它们之间有必然的联系，它们只是数据协议罢了

不管服务器使用 XML 还是 JSON 本质上都是将数据返回给客户端

服务端应该设置一个合理的 Content-Type

### 6、处理服务器端响应的数据

动态渲染数据到表格中

![](https://cdn.wallleap.cn/img/pic/illustration/20200815185218.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200815185226.png)

现在一般都不会这样操作，太繁琐了

模板引擎

![](https://cdn.wallleap.cn/img/pic/illustration/20200815185252.png)

常见模板引擎列表：<https://github.com/tj/consolidate.js#supported-template-engines>

artTemplate： <https://aui.github.io/art-template>

模板引擎实际上就是一个 API，模板引擎有很多种，使用方式大同小异，目的为了可以更容易地将数据渲染到 HTML 中

```html
<table id="comment" border="1"></table>
<!-- // 1.选择一个模板引擎 https://github.com/tj/consolidate.js#supported-template-engines
// 2、下载模板引擎JS库
// 3、引入到页面中 -->
<script src="https://cdn.bootcdn.net/ajax/libs/art-template/4.13.2/lib/template-web.min.js"></script>
<!-- 
  script标签的特点：
  1、innerHTML永远不会显示在界面上(display: none;)
  2、如果type属性不是text/javascript，内部的内容不会作为JavaScript执行
 -->
<!-- // 4、准备一个模板 -->
<!-- 
  JavaScript中用变量保存(维护不方便、不能换行)
  ——> HTML中放到一个div中通过样式隐藏(添加误用元素、多余样式)
  ——> script标签type修改之后不会显示在页面中，建议text/x-开头
-->
<script id="tmpl" type="text/x-art-template">
{{each comments}}  
<tr>
  <td>{{$index+1}}</td>
  <td>{{$value.author}}</td>
  <td>{{$value.content}}</td>
  <td>{{$value.created}}</td>
</tr>
{{/each}}
</script>
<script>
var xhr = new XMLHttpRequest()
xhr.open('GET', 'test.php')
xhr.send()
xhr.onreadystatechange = function (){
  if(this.readyState !== 4) return
  var res = JSON.parse(this.responseText)
  // // 5、准备一个数据
  var context = {comments: res.data}  // 上面的关键词就是comments
  console.log(context)
  var html = template('tmpl', context)
  console.log(html)
  document.getElementById('comment').innerHTML = html
  
  // 6、通过模板引擎的JS提供一个函数将模板和数据整合得到渲染结果HTML
  // 7、将渲染结果的HTML设置到某个元素的innerHTML中
}
</script>
```

### 7、兼容方案

XMLHttpRequest 在老板浏览器(IE5/6)中有兼容问题，可以通过另一种方式代替

```javascript
var xhr = window.XMLHttpRequest ? new XMLHttpRequest() : new ActiveXObject('Microsoft.XMLHTTP')
```

### 8、补充

(1) response、responseText

都是获取的响应

response: 获取到的结果或根据 this.responseType 的变化而变化(可以表述二进制数据)

responseText: 永远获取的是字符串形式的响应体

```javascript
var xhr = new XMLHttpRequest
xhr.open('GET', 'test.php')
xhr.send()
xhr.responseType = 'json'  // 通过代码告诉请求代理对象，服务端响应给我们的是JSON
xhr.onreadystatechange = function (){
  if(this.readyState !== 4) return
  console.log(this)
  console.log(this.response)
  console.log(this.responseText)  // 由于设置了json，因此不存在
}
```

(2) IE 缓存问题：IE 浏览器会将 ajax 返回结果缓存起来，再次发送请求时，显示的是本地缓存，而不是最新的请求到的数据

在服务端添加一个：

```javascript
//针对 IE 缓存
app.get('/ie', (request, response) => {
  //设置响应头  设置允许跨域
  response.setHeader('Access-Control-Allow-Origin', '*');
  //设置响应体
  response.send('HELLO AJAX IE');
});
```

解决

```html
<style>
  #result{
    width:200px;
    height:100px;
    border:solid 1px #258;
  }
</style>
<button>点击发送请求</button>
<div id="result"></div>
<script>
  const btn = document.getElementsByTagName('button')[0];
  const result = document.querySelector('#result');

  btn.addEventListener('click', function(){
    const xhr = new XMLHttpRequest();
    xhr.open("GET",'http://127.0.0.1:8000/ie?t='+Date.now()); // 解决方案：加上参数，这样浏览器认为每次请求url都不一样
    xhr.send();
    xhr.onreadystatechange = function(){
      if(xhr.readyState === 4){
        if(xhr.status >= 200 && xhr.status< 300){
          result.innerHTML = xhr.response;
        }
      }
    }
  })
</script>
```

(3) 请求超时和网络异常

`server.js`中添加

```javascript
//延时响应
app.all('/delay', (request, response) => {
  //设置响应头  设置允许跨域
  response.setHeader('Access-Control-Allow-Origin', '*');
  response.setHeader('Access-Control-Allow-Headers', '*');
  // 手动设置一个延时效果
  setTimeout(() => {
    //设置响应体
    response.send('延时响应');
  }, 1000) // 3000
});
```

进行处理，在2s内还没有响应则取消

```html
<style>
  #result{
    width:200px;
    height:100px;
    border:solid 1px #90b;
  }
</style>
<button>点击发送请求</button>
<div id="result"></div>
<script>
  const btn = document.getElementsByTagName('button')[0];
  const result = document.querySelector('#result');
  btn.addEventListener('click', function(){
    const xhr = new XMLHttpRequest();
    //超时设置 2s 设置
    xhr.timeout = 2000;
    //超时回调
    xhr.ontimeout = function(){
      alert("网络异常, 请稍后重试!!");
    }
    //网络异常回调
    xhr.onerror = function(){
      alert("你的网络似乎出了一些问题!");
    }
    xhr.open("GET",'http://127.0.0.1:8000/delay');
    xhr.send();
    xhr.onreadystatechange = function(){
      if(xhr.readyState === 4){
        if(xhr.status >= 200 && xhr.status< 300){
          result.innerHTML = xhr.response;
        }
      }
    }
  })
</script>
```

网络异常可以利用浏览器调试中 Network 一栏，设置为 Offline

(3) 取消请求

利用 `abort()` 方法取消请求

```html
<button>点击发送</button>
<button>点击取消</button>
<script>
  //获取元素对象
  const btns = document.querySelectorAll('button');
  let x = null; // 由于第二个按钮也需要用到
  btns[0].onclick = function(){
    x = new XMLHttpRequest();
    x.open("GET",'http://127.0.0.1:8000/delay');
    x.send();
  }
  // abort
  btns[1].onclick = function(){
    x.abort();
  }
</script>
```

(4) ajax 重复发送请求问题：用户频繁发送请求，对服务器压力很大

请求时，可以判断，如果前面有一条这样的请求，那么将前面的请求取消掉

```html
<button>点击发送</button>
<script>
  //获取元素对象
  const btns = document.querySelectorAll('button');
  let x = null;
  //标识变量
  let isSending = false; // 是否正在发送AJAX请求
  btns[0].onclick = function(){
    //判断标识变量
    if(isSending) x.abort();// 如果正在发送, 则取消该请求, 创建一个新的请求
    x = new XMLHttpRequest();
    //修改 标识变量的值
    isSending = true;
    x.open("GET",'http://127.0.0.1:8000/delay');
    x.send();
    x.onreadystatechange = function(){
      if(x.readyState === 4){
        //修改标识变量
        isSending = false;
      }
    }
  }
</script>
```

## 四、封装

### 1、AJAX 请求封装

封装的套路：

(1)写一个相对比较完善的用例

```javascript
var xhr = new XMLHttpRequest
xhr.open('GET', '/serve')
xhr.send(null)
xhr.addEventListener('readystatechange', function(){
  if(this.readyState !== 4) return
  console.log(this.responseText)
})
```

(2)写一个空函数，没有形参，将刚刚的用例直接作为函数的函数体

```javascript
function ajax(){
  var xhr = new XMLHttpRequest
  xhr.open('GET', 'test.php', true)
  xhr.send(null)
  xhr.addEventListener('readystatechange', function(){
    if(this.readyState !== 4) return
    console.log(this.responseText)
  })
}
```

(3)根据使用过程中的需求抽象参数

```javascript
/*
Ajax请求 version1
method: 请求方式 GET/POST
url: 请求地址 'http://xxx.com/api'
*/
function ajax(method, url){
  var xhr = new XMLHttpRequest
  xhr.open(method, url, true)
  xhr.send(data)
  xhr.addEventListener('readystatechange', function(){
    if(this.readyState !== 4) return
    console.log(this.responseText)
  })
}
ajax('GET', '/server')
```

(4)send 需要传参

```javascript
/*
Ajax请求 version2
method: 请求方式 GET/POST
url: 请求地址 'http://xxx.com/api'
data: 键值对字符串、对象
*/
function ajax(method, url, data){
  var xhr = new XMLHttpRequest
  xhr.open(method, url, true)
  xhr.addEventListener('readystatechange', function(){
    if(this.readyState !== 4) return
    console.log(this.responseText)
  })
  xhr.send(data)
}
```

(5)不应该在封装的函数中主观地处理响应结果

```javascript
/*
Ajax请求 version4
method: 请求方式 GET/POST/get/post
url: 请求地址 'http://xxx.com/api'
data: 键值对字符串、对象
success: 请求成功的回调函数
fail: 请求失败的回调函数
*/
function ajax(method, url, data, success, fail){
  var xhr = new XMLHttpRequest
  xhr.open(method, url)
  xhr.addEventListener('readystatechange', function(){
    if(this.readyState !== 4) return
    if(this.status >= 200 && this.status < 300){
      success(this.responseText)
    }else if(this.status >= 400){
      fail(this.status)
    }
  })
  xhr.send(data)
}
```

(6)<font color=red>**最终版本**</font>

不能确定 data 是否需要传，回调函数也不确定，所以都放在一个对象中

```javascript
/*
发送一个 Ajax 请求 version5
@param (String) method  请求方式 GET/POST/get/post
@param (String) url     请求地址 'http://xxx.com/api'
@param (Object) options  请求参数 { data, success, fail }
  data(Object) 请求参数
  success(Function) 请求成功的回调函数
  fail(Function) 请求失败的回调函数
*/
function ajax(method, url, options){
  const { data, success, fail } = options
  const xhr = new XMLHttpRequest
  xhr.open(method, url)
  xhr.addEventListener('readystatechange', function(){
    if(xhr.readyState === 4) {
      if(xhr.status >= 200 && xhr.status < 300 || xhr.status === 304){
        const type = xhr.getResponseHeader('Content-Type')
        if(type.startsWith('application/json') || type.startsWith('text/json')){  // 帮忙处理 JSON 的情况
          success(JSON.parse(xhr.responseText), xhr)  // 可能会需要其他的信息，所以将 xhr 也传递过去
        } else {
          success(xhr.responseText, xhr)
        } else if(xhr.status >= 400){
          fail(xhr)
        }
    }
  })
  xhr.send(data)
  return {
    abort: function(){
      xhr.abort()
    }
  }
}
```

使用

```js
const btn = document.querySelector('button')
const success = (res) => {
  console.log('准备执行')
  // console.log(res)
  btn.onclick = () => {
    api.abort()
  }
  alert(res)
  console.log('执行完成了')
}
const api = ajax('post', '/server', {
  data: {key1: 'value1', key2: 'value2'},
  success,
  fail: (xhr) => {
    console.log(xhr.status)
  }
})
```

### 2、jQuery 中的 Ajax

jQuery 中有一套专门针对 AJAX 的封装，功能十分完善，经常使用，需要注意。

<https://www.jquery123.com/category/ajax/>

(1)通用方法 `$.ajax`

底层接口(其他接口依赖于这个)

```html
<script src="https://cdn.bootcdn.net/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
<script type="text/javascript">
// 1、最基础的调用
$.ajax('/server', { // url: 
  type: 'POST',  // method: 请求方法
  success: function(res){
    // res => 拿到的只是响应体
    console.log(res)
  }
})
// 可以把url写到里面去
$.ajax({ 
  url: '/server',// url: 
  type: 'POST',  // method: 请求方法
  data: {id: 1, name: '张三'}, // 用于提交到服务端的参数
  /*
    get方式通过url传递
    post方式按照请求体传递
  */
  success: function(res){
    // res => 拿到的只是响应体
    console.log(res)
  }
})
// res返回格式
$.ajax({ 
  url: '/data',// url: 请求地址
  type: 'get',  // method: 请求方法
  success: function(res){
    // res会根据服务器响应的Content-Type自动转换为对象
    // 这是jQuery内部实现的
    console.log(res)
  }
})
// 指定响应体类型
$.ajax({ 
  url: '/data',// url: 
  type: 'get',  // method: 请求方法
  // data: {id: 1, name: '张三'}, // 设置请求参数
  dataType: 'json', // 用于设置响应体的类型(与data参数没关系)
  success: function(res){
    // 一旦设置了dataType选项，就不再关心服务端响应的Content-Type了
    // 客户端会主观地认为服务端返回的就是json格式
    console.log(res)
  }
})
</script>
```

原生操作中不论请求状态码是多少都会触发回调

jQuery 中 ajax 的回调

```html
<script src="https://cdn.bootcdn.net/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
<script type="text/javascript">
// jQuery中ajax的回调
$.ajax({ 
  url: '/server', // url
  data: {key1:value1, key2:value2}, // 参数
  type: 'POST',  // method: 请求方法
  dataType: 'json', // 响应体结果
  beforeSend: function(xhr){
    // 在所有发送请求得操作(open、send)之前执行
    console.log('beforeSend', xhr)
  }
  success: function(res){ // 成功的回调
    // 只有请求成功(状态码为200)才会执行这个函数
    // res => 拿到的只是响应体
    console.log(res)
  },
  // timeout: 2000, // 超时时间
  error: function(xhr){ // 失败的回调
    // 只有请求不正常才会执行(状态码不为200)
    console.log('error',xhr)
  },
  complete: function(xhr){
    // 不管成功还是失败都是完成，都会执行这个complete函数
    console.log('complete', xhr)
  }
})
</script>
```

(2) 高级封装

```html
<script src="https://cdn.bootcdn.net/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
<script type="text/javascript">
// 2、jQuery中ajax的快捷方法
$.get('/data', function(res){
  console.log(res)
})
$.post('/server', function(res){
  console.log(res)
})
// 服务端设置了json能转换对象，没设置不行
$.get('/data', {id: 1}, function(res){
  console.log(res)
})
$.post('/server', {id: 1}, function(res){
  console.log(res)
})
// 无视服务端Content-Type，视作JSON格式
$.getJSON('/server', {id: 1}, function(res){
  console.log(res)
})
$.postJSON('/data', {id: 1}, function(res){
  console.log(res)
})
明确请求的方式，根据方式选择快捷方法
</script>
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815190207.png)

```html
<script src="https://cdn.bootcdn.net/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
<script type="text/javascript">
// 跳转其他页面，会白屏，但是有些页面只是部分不相同，可以局部刷新
$(function($){
  // 有一个独立的作用域，顺便确保页面加载完成执行
  $('a.item').on('click', function(){
    var url = $(this).attr('href')
    $('#main').load(url + ' #main>*') // 元素.load(链接+空格+选择器)
    // 阻止a的默认行为
    return false
  })
})
</script>
```

将 jQuery 的几种方式汇总一下：

`server.js`中：

```javascript
//jQuery 服务
app.all('/jquery-server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    // response.send('Hello jQuery AJAX');
    const data = {name:'wallleap'};
    response.send(JSON.stringify(data));
});
```

前端

```html
<link crossorigin="anonymous" href="https://cdn.bootcss.com/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
<script crossorigin="anonymous" src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.1/jquery.min.js"></script> <!-- crossorigin="anonymous"：跨域源请求设置，加上之后向这个资源发送请求时不会携带当前域名下的cookie -->
<div class="container">
    <h2 class="page-header">jQuery发送AJAX请求 </h2>
    <button class="btn btn-primary">GET</button>
    <button class="btn btn-danger">POST</button>
    <button class="btn btn-info">通用型方法ajax</button>
</div>
<script>
  $('button').eq(0).click(function(){
    $.get('http://127.0.0.1:8000/jquery-server', {a:100, b:200}, function(data){
      console.log(data);
    },'json');
  });
  $('button').eq(1).click(function(){
    $.post('http://127.0.0.1:8000/jquery-server', {a:100, b:200}, function(data){
      console.log(data);
    });
  });
  $('button').eq(2).click(function(){
    $.ajax({
      //url
      url: 'http://127.0.0.1:8000/jquery-server',
      //参数
      data: {a:100, b:200},
      //请求类型
      type: 'GET',
      //响应体结果
      dataType: 'json',
      //成功的回调
      success: function(data){
        console.log(data);
      },
      //超时时间
      timeout: 2000,
      //失败的回调
      error: function(){
        console.log('出错啦!!');
      },
      //头信息
      headers: {
        c:300,
        d:400
      }
    });
  });
</script>
```

(3) 全局事件及配置 NProgress 显示加载进度

```html
<style>
  .loading{
    display: none;
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    background-color: rgba(85, 85, 85, .5);
    text-align: center;
    padding-top: 200px;
    color: #fff;
    font-size: 50px;
  }
</style>
<div class="loading">正在玩命加载中……</div>
<script src="https://cdn.bootcdn.net/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
<script type="text/javascript">
// 3、jQuery全局事件处理函数
/*
$.ajax({
  url: 'time.php',
  beforeSend: function(xhr){
    // 显示加载提示
    $('.loading').fadeIn()
    console.log('即将开始请求')
  },
  complete: function(xhr){
    // 结束提示
    $('.loading').fadeOut()
    console.log('请求结束了')
  }
})
*/
// 所有的ajax请求开始和结束
$(document).ajaxStart(function(){
  // 只要有ajax请求发生就会执行
  // 显示加载提示
  $('.loading').fadeIn()
  console.log('即将开始请求')
})
$(document).ajaxStop(function(){
  // 只要有ajax请求发生就会执行
  // 显示加载提示
  $('.loading').fadeOut()
  console.log('请求结束了')
})
$('body').on('click', function(){
  // $.ajax({
  //   url: 'time.php'
  // })
  $.get('time.php')
})
</script>
```

可以写成链式的：

```javascript
$(document)
  .ajaxStart(function(){
    ……
  })
  .ajaxStop(function(){
    ……
  })
```

搭配 NProgress

```html
<link rel="stylesheet" href="https://unpkg.com/nprogress@0.2.0/nprogress.css">
<script src="https://unpkg.com/nprogress@0.2.0/nprogress.js"></script>
</head>
<body>
<div style="margin-top: 100px;text-align: center;">点击加载</div>
<script src="https://cdn.bootcdn.net/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
<script type="text/javascript">
// 3、jQuery全局事件处理函数搭配nprogress
// 所有的ajax请求开始和结束
$(document)
  .ajaxStart(function(){
    // 只要有ajax请求发生就会执行
    NProgress.start()
  })
  .ajaxStop(function(){
    // 只要有ajax请求发生就会执行
    NProgress.done()
  })
$('body').on('click', function(){
  $.get('/data')
})
</script>
</body>
```

### 3、axios

(1) 使用教程：<http://www.axios-js.com/zh-cn/docs/>

Axios 是一个基于 promise 的 HTTP 库，可以用在浏览器和 node.js 中。

(2) 特性

- 从浏览器中创建 [XMLHttpRequests](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)
- 从 node.js 创建 [http](http://nodejs.org/api/http.html) 请求
- 支持 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) API
- 拦截请求和响应
- 转换请求数据和响应数据
- 取消请求
- 自动转换 JSON 数据
- 客户端支持防御 [XSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery)

(3) 安装

使用 npm:

```sh
npm install axios
```

使用 bower:

```bash
bower install axios
```

使用 cdn:

```html
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

(4) 案例

`server.js`

```javascript
//axios 服务
app.all('/axios-server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    // response.send('Hello jQuery AJAX');
    const data = {name:'wallleap'};
    response.send(JSON.stringify(data));
});
```

axios 发送 Ajax 请求

```html
<script crossorigin="anonymous" src="https://cdn.bootcdn.net/ajax/libs/axios/0.19.2/axios.js"></script>
<button>GET</button>
<button>POST</button>
<button>AJAX</button>
<script>
  // https://github.com/axios/axios
  const btns = document.querySelectorAll('button');
  //配置 baseURL
  axios.defaults.baseURL = 'http://127.0.0.1:8000';
  btns[0].onclick = function () {
    //GET 请求 get(url, 其它配置)
    // axios.get('http://127.0.0.1:8000/axios-server', {
    axios.get('/axios-server', { // 配置了baseURL
      //url 参数——>id=100&vip=7
      params: {
        id: 100,
        vip: 7
      },
      //请求头信息
      headers: {
        name: 'wallleap',
        age: 20
      }
    }).then(value => { // 基于promise 处理返回结果 value.config、data、headers、request、status、statusText
      console.log(value);
    });
  }
  btns[1].onclick = function () {
    // POST请求 post(url, 请求体, 其它配置)
    axios.post('/axios-server', { // 请求体
      username: 'admin',
      password: 'password'
    }, {
      //url 
      params: {
        id: 200,
        vip: 9
      },
      //请求头参数
      headers: {
        height: 180,
        weight: 180,
      }
    }).then(response=>{
      // 配置
      console.log(response.config);
      // XMLHttpRequest
      console.log(response.request);
      //响应状态码
      console.log(response.status);
      //响应状态字符串
      console.log(response.statusText);
      //响应头信息
      console.log(response.headers);
      //响应体
      console.log(response.data);
    })
  }
  btns[2].onclick = function(){
    // 通用方式 axios(对象) --> {method, url, 参数, 头信息, 请求体参数}
    axios({
      //请求方法
      method : 'POST',
      //url
      url: '/axios-server',
      //url参数
      params: {
        vip:10,
        level:30
      },
      //头信息
      headers: {
        a:100,
        b:200
      },
      //请求体参数
      data: {
        username: 'admin',
        password: 'password'
      }
    }).then(response=>{
      //响应状态码
      console.log(response.status);
      //响应状态字符串
      console.log(response.statusText);
      //响应头信息
      console.log(response.headers);
      //响应体
      console.log(response.data);
    }).catch(function (error) {
      console.log(error);
    })
  }
</script>
```

## 4、fetch

fetch使用：<https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API/Using_Fetch>

fetch 发送 AJAX 请求

`server.js`

```javascript
//fetch 服务
app.all('/fetch-server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    // response.send('Hello jQuery AJAX');
    const data = {name:'wallleap'};
    response.send(JSON.stringify(data));
});
```

浏览器端

```html
<button>AJAX 请求</button>
<script>
  //文档地址
  //https://developer.mozilla.org/zh-CN/docs/Web/API/WindowOrWorkerGlobalScope/fetch
  const btn = document.querySelector('button');
  btn.onclick = function(){
    fetch('http://127.0.0.1:8000/fetch-server?vip=10', {
      //请求方法
      method: 'POST',
      //请求头
      headers: {
        name:'luwang'
      },
      //请求体
      body: 'username=admin&password=admin'
    }).then(response => {
      // return response.text();
      return response.json();
    }).then(response=>{
      console.log(response);
    });
  }
</script>
```

## 五、跨域

### 1、概念

(1) 同源策略(Same-Origin Policy)：最早由Netscape公司提出，是浏览器的一种安全策略，所谓同源是指**协议、域名、端口**完全相同，只有同源的地址才可以相互通过AJAX的方式请求。

下面来一个同源的案例：

重写一个 `server.js`

```javascript
const express = require('express');
const app = express();
app.get('/home', (request, response)=>{
    //响应一个页面
    response.sendFile(__dirname + '/index.html');
});
app.get('/data', (request, response)=>{
    response.send('用户数据');
});
app.listen(9000, ()=>{
    console.log("服务已经启动...");
});
```

运行起来

```sh
nodemon server.js
```

在这个目录下新建 `index.html`

```html
<h1>wallleap</h1>
<button>点击获取用户数据</button>
<script>
  const btn = document.querySelector('button');
  btn.onclick = function(){
    const x = new XMLHttpRequest();
    //这里因为是满足同源策略的, 所以 url 可以简写
    x.open("GET",'/data');
    //发送
    x.send();
    //
    x.onreadystatechange = function(){
      if(x.readyState === 4){
        if(x.status >= 200 && x.status < 300){
          console.log(x.response);
        }
      }
    }
  }
</script>
```

访问 <http://127.0.0.1:9000/home>，可以访问这个 index.html，点击按钮可以获取到数据

(2) 同源或者不同源说的是两个地址之间的关系，不同源地址之间请求我们称之为跨域请求。

![](https://cdn.wallleap.cn/img/pic/illustration/20200815190430.png)

跨域的案例：

![](https://cdn.wallleap.cn/img/pic/illustration/20200815190440.png)

跨域会报错：

![](https://cdn.wallleap.cn/img/pic/illustration/20200815190456.png)

### 2、解决方案

不同源地址之间如果需要相互请求，必须服务端和客户端配合才能完成

尝试找到一种可以发送不同源请求的方式

![可能可以解决跨域的方法](https://cdn.wallleap.cn/img/pic/illustration/20200815190529.png)

![正常图片标签](https://cdn.wallleap.cn/img/pic/illustration/20200815190556.png)

![尝试使用img标签解决跨域](https://cdn.wallleap.cn/img/pic/illustration/20200815190621.png)

![正常link标签](https://cdn.wallleap.cn/img/pic/illustration/20200815190650.png)

![尝试使用link标签解决跨域](https://cdn.wallleap.cn/img/pic/illustration/20200815190712.png)

![尝试使用script标签解决跨域](https://cdn.wallleap.cn/img/pic/illustration/20200815190738.png)

初级跨域解决方案

![服务器端将json用函数包裹返回](https://cdn.wallleap.cn/img/pic/illustration/20200815190812.png)

![客户端使用该函数拿到数据](https://cdn.wallleap.cn/img/pic/illustration/20200815190858.png)

(1) **JSONP**

JSON with Padding，是一种借助于`script`标签发送跨域请求的技巧。这个是非官方的跨域解决方案，是程序员们机智地想出来的，只支持get请求。

其原理就是在客户端借助`script`标签请求服务端的一个动态网页(php等)，服务端的这个动态网页返回一段带有函数调用的JavaScript全局函数调用的脚本，将原本需要返回给客户端的数据传递进去。

以后绝大多数情况都是采用JSONP的手段完成不同源地址之间的跨域请求。

- 原理演示：

当前目录下，新建`js/app.js`

```javascript
const data = {
    name: '测试jsonp'
};
/* 把这个挪走，到测试的html文件中
//处理数据
    function handle(data) {
        //获取 result 元素
        const result = document.getElementById('result');
        result.innerHTML = data.name;
    }
*/
handle(data);
```

html

```html
<style>
  #result {
    width: 300px;
    height: 100px;
    border: solid 1px #78a;
  }
</style>
<div id="result"></div>
<script>
    //处理数据
    function handle(data) {
        //获取 result 元素
        const result = document.getElementById('result');
        result.innerHTML = data.name;
    }
</script>
<!-- <script src="http://127.0.0.1:5500/jsonp/js/app.js"></script> --> <!-- 利用file://方式访问这个html页面 -->
<!-- 进阶版 -->
<script src="http://127.0.0.1:8000/jsonp-server"></script>
```

`server.js`

```javascript
//jsonp服务
app.all('/jsonp-server',(request, response) => {
    // response.send('console.log("hello jsonp")'); // 前端拿到js代码
    const data = {
        name: '测试jsonp'
    };
    //将数据转化为字符串
    let str = JSON.stringify(data);
    //返回结果
    response.end(`handle(${str})`); // 会返回一个函数调用，实参是想返回给前端的数据(前端需要先声明这个函数)
});
```

- 用php演示一下

`server.php`

```php
<?php
$conn = mysqli_connect('localhost', 'root', '123456', 'demo');
$query = mysqli_query($conn, 'select * from users');
while ($row = mysqli_fetch_assoc($query)) {
  $data[] = $row;
}
if (empty($_GET['callback'])) {
  header('Content-Type: application/json');
  echo json_encode($data);
  exit();
}
// 如果客户端采用的是 script 标记对我发送的请求
// 一定要返回一段 JavaScript
header('Content-Type: application/javascript');
$result = json_encode($data);
$callback_name = $_GET['callback'];
echo "typeof {$callback_name} === 'function' && {$callback_name}({$result})";
```

![image-20200815191013064](https://cdn.wallleap.cn/img/pic/illustration/20200815191014.png)

- 原生方式实践jsonp

`server.js`

```javascript
//用户名检测是否存在
app.all('/check-username',(request, response) => {
    // response.send('console.log("hello jsonp")');
    const data = {
        exist: 1,
        msg: '用户名已经存在'
    };
    //将数据转化为字符串
    let str = JSON.stringify(data);
    //返回结果
    response.end(`handle(${str})`);
});
```

前端代码：

```html
用户名: <input type="text" id="username">
<p></p>
<script>
  //获取 input 元素
  const input = document.querySelector('input');
  const p = document.querySelector('p');
  //声明 handle 函数
  function handle(data){
    input.style.border = "solid 1px #f00";
    //修改 p 标签的提示文本
    p.innerHTML = data.msg;
  }
  //绑定事件
  input.onblur = function(){
    //获取用户的输入值
    let username = this.value;
    //向服务器端发送请求 检测用户名是否存在
    //1. 创建 script 标签
    const script = document.createElement('script');
    //2. 设置标签的 src 属性
    script.src = 'http://127.0.0.1:8000/check-username';
    //3. 将 script 插入到文档中
    document.body.appendChild(script);
  }
</script>
```

- 封装成一个函数

```javascript
function jsonp (url, params, callback) {
  var funcName = 'jsonp_' + Date.now() + Math.random().toString().substr(2, 5)

  if (typeof params === 'object') {
    var tempArr = []
    for (var key in params) {
      var value = params[key]
      tempArr.push(key + '=' + value)
    }
    params = tempArr.join('&')
  }

  var script = document.createElement('script')
  script.src = url + '?' + params + '&callback=' + funcName
  document.body.appendChild(script)

  window[funcName] = function (data) {
    callback(data)

    delete window[funcName]
    document.body.removeChild(script)
  }
}

jsonp('http://localhost/jsonp/server.php', { id: 123 }, function (res) {
  console.log(res)
})

jsonp('http://localhost/jsonp/server.php', { id: 123 }, function (res) {
  console.log(res)
})
```

- jQuery方式实践jsonp

`server.js`

```javascript
// jQuery jsonp
app.all('/jquery-jsonp-server',(request, response) => {
  // response.send('console.log("hello jsonp")');
  const data = {
    name:'尚硅谷',
    city: ['北京','上海','深圳']
  };
  //将数据转化为字符串
  let str = JSON.stringify(data);
  //接收 callback 参数
  let cb = request.query.callback; // 函数名从前端获取
  //返回结果
  response.end(`${cb}(${str})`);
});
```

前端代码：

```html
<style>
  #result{
    width:300px;
    height:100px;
    border:solid 1px #089;
  }
</style>
<script crossorigin="anonymous" src='https://cdn.bootcss.com/jquery/3.5.0/jquery.min.js'></script>
<button>点击发送 jsonp 请求</button>
<div id="result">

</div>
<script>
  $('button').eq(0).click(function(){
    $.getJSON('http://127.0.0.1:8000/jquery-jsonp-server?callback=?', function(data){
      $('#result').html(`
    名称: ${data.name}<br>
    校区: ${data.city}
   `)
    });
  });
</script>
```

(2)CORS

HTTP访问控制（CORS）<https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS>

Cross Origin Resource Share，跨域资源共享。CORS是官方的跨域解决方案，它的特点是不需要再客户端做任何特殊的操作，完全在服务器中进行处理，支持get和post请求(其他也支持)。跨域资源共享标准新增了一组HTTP首部字段，允许服务器声明哪些源站通过浏览器有权限访问哪些资源。

CORS是通过设置一个响应头来告诉浏览器，这个请求允许跨域，浏览器收到该响应以后就会对响应放行。

`server.js`

```javascript
app.all('/cors-server', (request, response)=>{
  //设置响应头
  response.setHeader("Access-Control-Allow-Origin", "*"); // 允许所有源站发送请求
  response.setHeader("Access-Control-Allow-Headers", '*'); // 允许携带的响应头
  response.setHeader("Access-Control-Allow-Method", '*'); // 允许请求方法
  // response.setHeader("Access-Control-Allow-Origin", "http://127.0.0.1:5500"); // 允许单个
  response.send('hello CORS');
});
```

测试：

```html
<style>
    #result{
        width:200px;
        height:100px;
        border:solid 1px #90b;
    }
</style>
<button>发送请求</button>
<div id="result"></div>
<script>
  const btn = document.querySelector('button');
  btn.onclick = function(){
    //1. 创建对象
    const x = new XMLHttpRequest();
    //2. 初始化设置
    x.open("GET", "http://127.0.0.1:8000/cors-server");
    //3. 发送
    x.send();
    //4. 绑定事件
    x.onreadystatechange = function(){
      if(x.readyState === 4){
        if(x.status >= 200 && x.status < 300){
          //输出响应体
          console.log(x.response);
        }
      }
    }
  }
</script>
```

```php
// 允许远端访问(甚至直接打开文件的方式也可以file://……)
header('Access-Control-Allow-Origin: *') // 允许所有
header('Access-Control-Allow-Origin: http://localhost/index.html') // 允许单个
```

eg:

```php
<?php

$conn = mysqli_connect('localhost', 'root', '123456', 'demo');

$query = mysqli_query($conn, 'select * from users');

while ($row = mysqli_fetch_assoc($query)) {
  $data[] = $row;
}

// 一行代码搞定
// 允许跨域请求
header('Access-Control-Allow-Origin: *');

header('Content-Type: application/json');
echo json_encode($data);
```

客户端

```html
<script src="jquery.js"></script>
<script>
  $.get('http://localhost/cors.php', {}, function (res) {
    console.log(res)
  })
</script>
```

这种方案无序客户端作出任何变化(不用改代码)，只是在被请求的服务端响应的时候**添加一个`Access-Control-Allow-Origin`的响应头**，表示这个资源是否允许指定域请求。

## 六、XMLHttpRequest2.0

> 暂作了解，无需着重看待

更易用，更强大。
