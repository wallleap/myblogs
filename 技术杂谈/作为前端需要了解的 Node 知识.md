---
title: 作为前端需要了解的 Node 知识
date: 2020-06-14 11:33
updated: 2020-06-14 11:33
cover: //cdn.wallleap.cn/img/pic/cover/202302oHImDg.jpg
category: 技术杂谈
tags:
  - web
  - 前端
description: 作为前端需要了解的 Node 知识
---

Node 知识

## 一、基本知识

### 1、命令行窗口

又称 cmd 窗口、终端、shell

打开方式：

- Win：<kbd>win</kbd> + <kbd>R</kbd>，输入 `cmd`，打开

- mac/linux: 搜索 `terminal` 打开

前面显示的为目前所在的目录

常用的命令

- `dir` / `ls` 列出当前目录下所有文件
- `cd`  目录名 进入到指定的目录
- 目录
  - `.` 表示当前目录
  - `..` 表示上一级目录
- `md 目录名` / `mkdir 目录名` 创建一个文件夹
- `rd 目录名` / `rm -rf 目录名` 删除一个文件夹
- 输入当前目录下的一个文件名（包括后缀）可以打开这个文件

环境变量（Windows 系统中的变量）

- `path`  
- 当我们在命令行窗口打开一个文件，或调用一个程序时，系统会首先在当前目录下寻找文件程序，如果找到了则直接打开，如果没有找到则会依次到环境变量 path 的路径中寻找，知道找到为止，如果没找到则报错
- 所以我们可以将一些经常需要访问的程序和文件的路径添加到 path 中，这样我们就可以在任意位置来访问这些文件和程序了

### 2、进程和线程

#### 进程

- 进程负责为程序的运行提供必备的环境
- 进程就相当于工厂中的车间

#### 线程

- 线程是计算机中的最小的计算单位，线程负责执行进程中的程序
- 线程就相当于工厂中的工人
  - 单线程
    - js 是单线程
  - 多线程

## 二、Node.js 简介

nodejs 是一个能够在服务器端运行 js 的开放源代码、跨平台的 js 运行环境

node 采用 google 开发的 v8 引擎运行 js 代码，使用 event-driven、non-blocking I/O 模型，使其轻量又高效

## 三、node 使用

### 1、安装

~~官网下载安装包，安装即可~~

- ~~macOS 可以使用 brew 安装：`brew install node`~~

推荐使用 nvm 管理 node 版本

1. 下载 nvm 安装包，安装，或者使用包管理器例如 brew 安装：`brew install nvm`（Win 找到官网后下载安装）
2. 安装完成后，打开命令行窗口，输入 `nvm -v`，如果出现版本号，则安装成功
3. 接着输入 `nvm install node`，安装最新版本的 node
4. 多版本管理
   - 使用 `nvm install 版本号` 安装指定版本的 node
   - 可以使用 `nvm ls` 查看已安装的 node 版本
   - 使用 `nvm use 版本号` 切换 node 版本

安装完成后，打开命令行窗口，输入 `node -v`，如果出现版本号，则安装成功

> 安装完成后，会自动安装 npm 包管理器

运行 node，进入 node 命令行窗口，可以直接运行 js 代码

```shell
node
> var i = 0
> console.log(i)
```

还可以直接运行 js 文件

```shell
node hello.js
```

## 四、COMMONJS 规范

### 1、ECMAScript 标准的缺陷

- 没有模块系统
- 标准库较少
- 没有标准接口
- 缺乏管理系统

### 2、模块化 module.js

在 node 中，一个 js 就是一个模块

在 Node 中，每一个 js 文件中的 js 代码都是独立运行在一个函数中，而不是全局作用域，所以一个模块中的变量和函数在其他模块中无法访问

我们可以通过 `exports` 来向外部暴露变量和方法，只需要将要暴露给外部的变量或方法设置为 `exports` 的属性即可

```javascript
exports.x = "我是 module.js中的x"
exports.fn = function(){}
```

在 Node 中有一个全局对象 global，它的作用和网页中 window 类似，在全局中创建的变量都会作为 global 的属性保存，在全局中创建的函数都会作为 global 的方法保存

```javascript
var a = 10;
console.log(global.a);
```

arguments

- arguments.callee 这个属性保存的是当前执行的函数对象

在 node 执行模块中的代码时，它首先会在代码的最顶部添加代码 `function(exports, require, module, __filename, __dirname){`，在代码的最底部，添加代码 `}`

实际上模块中的代码都是包装在一个函数中执行的，并且在函数执行时，同时传递进了 5 个实参（`arguments.length` 查看参数长度）

- `exports` 该对象用来将变量或函数暴露到外部

- `require` 函数，用来引入外部的模块

- `module`

  - `module` 代表的是当前模块本身

  - `exports` 就是 `module` 的属性

  - 既可以使用 `exports` 导出，也可以使用 `module.exports` 导出 `module.exports==exports`，`module.exports.a`、`exports.a`

  - 通过 `exports` 只能使用 `.` 的方式来向外暴露内部变量，而 `module.exports` 既可以通过 `.` 的形式，也可以直接复制

    ```javascript
    exports.xxx = xxx
    module.exports.xxx = xxx
    module.exports = {
      name = "swk"
      age = 15000
      sayName = function{
        console.log(name)
      }
    }
    ```

- `__filename` 当前模块的完整路径

- `__dirname` 当前模块所在文件夹的完整路径

在 node 中通过 `require()` 函数来引入外部的模块，`require()` 可以传递一个文件的路径作为参数，node 将会自动根据该路径来引入外部模块，这里的路径如果使用相对路径，必须以 `.` 或 `..` 开头

使用 `require` 引入模块后，该函数会返回一个对象，这个对象代表的是引入的模块

```javascript
var md = require("./module.js");
console.log(md)
```

模块分为两大类

- 核心模块

  - 由 node 引擎提供的模块

- 文件模块

  - 由用户自己创建的模块

### 3、CommonJS 规范

CommonJS 规范的提出，主要是为了弥补当时 JavaScript 没有标准的缺陷

CommonJS 规范为 JS 制定了一个美好的愿景，希望 JS 能够在任何地方运行

CommonJS 规范对模块的定义十分简单

- 模块引用
- 模块定义
- 模块标识
  - 我们使用 `require()` 引入外部模块时，使用的就是模块标识，我们可以通过模块标识来找到指定的模块
  - 核心模块的标识就是模块的名字
  - 文件模块的标识就是文件的路径（绝对、相对），相对路径使用 `./` 或 `../` 开头

## 五、包 Package

### 1、简介

- CommonJS 的包规范允许我们将一组相关的**模块组合到一起**，形成一组完整的工具
- CommonJS 的包规范由包结构和包描述文件两个部分组成
- 包结构：用于组织包中的各种文件
- 包描述文件：描述包的相关信息，以供外部读取分析

### 2、包结构

包实际上就是一个压缩文件，解压以后还原为目录

符合规范的目录，应该包含如下文件：

- **`package.json` 描述文件**

  ```json
  {
    "name": "包名",
    "version": "v1.0.0",
    ...
    "dependencies": {}, // 依赖
    "description": "描述",
    "devDependencies": { // 开发依赖
      ...
    }
  }
  ```

- bin 可执行二进制文件

- lib js 代码

- doc 文档

- test 单元测试

### 3、包描述文件

包描述文件用于表达非代码相关的信息，它是一个 JSON 格式的文件—— `package.json`，位于包的根目录下，是包的重要组成部分

`package.json` 中的字段（JSON 中不能写注释）

- `name`
- `description`
- `version`
- `keywords`
- `maintainers`
- `contributors`
- `bugs`
- `licenses`
- `repositories`
- `dependencies`
- `homepage`
- `os`
- `cpu`
- `engine`
- `builtin`
- `directories`
- `implements`
- `scripts`
- `author`
- `bin`
- `main`
- `devDependencies`

1. 标识
2. 依赖
3. 运行/打包

通过 `npm run` 可以查看当前可执行的脚本命令（`script` 字段），`npm run 脚本名称` 可以执行对应的脚本命令

## 六、NPM(Node Package Manager)

### 1、简介

CommonJS 包规范是理论，NPM 是其中一种实践

对于 Node 而言，NPM 帮助其完成了第三方模块的发布、安装和依赖等。借助 NPM，Node 与第三方模块之间形成了很好的一个生态系统

包管理工具，用于 Node 模块的管理，除了 npm 之外，还有 yarn、cnpm、pnpm 等

现在推荐使用 pnpm 代替 npm，pnpm 是一个快速、零配置的 Node 包管理工具，它使用硬链接和符号链接来降低磁盘空间的使用，它的速度也非常快，它的速度是 npm 的 3~5 倍，yarn 的 2~3 倍

### 2、NPM 命令

- `npm -v` 查看 npm 版本
- `npm version` 查看所有模块版本
- `npm` 帮助说明
- `npm init` 在当前目录下创建 `package.json` 文件，驼峰命名改为 `_` 连接
- `npm search 包名` 搜索包
- `npm install/i 包名` 安装包，将会在当前目录的 `node_modules` 下，直接通过包名引入即可，`var math = require("math")`
- `npm install 包名 -g`  全局安装包，一般都是一些工具
- `npm remove/r 包名`  删除一个模块
- `npm install 包名 --save`  **安装包并将其添加到依赖中**，一般不传 node_modules，太大、不能保证是最新的，有了依赖，传 package.json 直接 `npm install` 可以下载当前项目所依赖的包
- `npm uninstall 包名`  卸载包
- `npm install 文件路径`  从本地安装
- `npm install 包名 -registry=地址`  从镜像源安装包
- `npm config set registry 地址`  设置镜像源

淘宝镜像：<https://npm.taobao.org>

一般不直接设置官方原版 npm 替换为其他源，可以使用 cnpm

```sh
npm install -g cnpm --registry=https://registry.npmmirror.com
```  

注：

- Node 在使用模块名字来引入模块时，它会首先在当前目录的 node_modules 中寻找是否含有该模块，如果有则直接使用
- 如果没有则去上一级目录的 node_modules 中寻找，如果有则直接使用
- 如果没有则再去上一级目录寻找，直到找到为止
- 如果找到磁盘根目录仍没有，则报错

## 七、Buffer（缓冲区）

Buffer 的就结构和数组很像，操作的方法也和数组类似

数组中不能存储二进制的文件，而 buffer 就是专门用来存储**二进制**数据的

使用 buffer 不需要引入模块，直接使用即可

```javascript
var str = "hello"
// 将一个字符串保存到buffer中
var buf = Buffer.from(str)
console.log(buf)
console.log(buf.length,str.length)  // 占用内存的大小,字符串的长度
```

在 buffer 中存储的都是二进制数据，但是在显示的时候都是以 16 进制的形式显示的，buffer 中每一个元素的范围是从 00 到 ff (0~255) 00000000~11111111 8 位(bit) = 1字节(byte)，buffer 中的一个元素占用内存的一个字节

ps：一个汉字 3 字节，一个英文字母 1 字节

buffer 的大小一旦确定，则不能修改，Buffer 实际上是对底层内存的直接操作

- `Buffer.from(str)` 将一个字符串转为 buffer
- `Buffer.alloc(size)` 创建一个指定大小的 buffer
- `Buffer.allocUnsafe(size)` 创建一个指定的大小的 buffer，但是可能包含敏感数据
- `buf.toString()` 将 buffer 里的数据转为字符串

```javascript
// 创建一个指定大小的buffer
var buf = new Buffer(10) // 10个字节的buffer
// buffer构造函数都是不推荐使用的
var buf2 = Buffer.alloc(10)   // 全都是00
buf2[0] = 88
buf2[1] = 255
buf2[2] = 0xaa
buf2[3] = 556
// 1000101100截取后八位
buf2[10] = 15  // 没改变
// 只要数字在控制台或页面中输出一定是10进制
console.log(buf2[2])
console.log(buf2[2].toString(16))  // 可以这样转为16进制显示

var buf3 = Buffer.allocUnsafe(10)  // 创建一个指定大小的buffer，但是buffer中可能含有敏感数据，不全为00
```

<https://nodejs.cn>

## 八、文件系统（File System）

### 1、简介

文件系统简单来说就是通过 Nodejs 来操作系统中的文件

在 Node 中，与文件系统的交互是非常重要的，服务器的本质就是将本地的文件发送给远程的客户端

Node 通过 `fs` 模块来和文件系统进行交互

`fs` 模块提供了一些标准文件访问 API 来打开、读取、写入文件，以及与其交互

要使用文件系统，需要先引入 `fs` 模块，`fs` 是核心模块，直接引入不需要下载；要使用 `fs` 模块，首先需要对其进行加载
  
```js
const fs = require('fs')
```

### 2、同步和异步调用

- `fs` 模块中所有的操作都有两种形式可供选择，同步（`fs.xxx`）和异步（`fs.xxxSync`）

- 同步文件系统会阻塞程序的执行，也就是除非操作完毕，否则不会向下执行代码

- 异步文件系统不会阻塞程序的执行，而是在操作完成时，通过回调函数将结果返回

### 3、同步、异步文件写入

**同步文件的写入**

操作步骤：

1. 打开文件

   - `fs.openSync(path, flags[, mode])`

   - path 要打开文件的路径

   - flags 打开文件要做的操作的类型：r 只读的、w 可写的

   - mode 设置文件的操作权限，一般不传

   - 返回值： 返回一个文件的描述符，可以通过该描述符来对文件进行各种操作

     ```javascript
     var fs = require("fs");
     var fd = fs.openSync("hello.txt", "w");
     // console.log(fd)
     ```

2. 向文件中写入内容

   - `fs.writeSync(fd, string[, position[, encoding]])`

   - fd 文件的描述符，需要传递要写入的文件的描述符

   - string 要写入的内容

   - position 写入的起始位置

   - encoding 写入的编码，默认 utf-8

     ```javascript
     fs.writeSync(fd, "这是写入的内容")
     ```

3. 保存并关闭文件

   - `fs.closeSync(fd)`
   - fd 要关闭的文件的描述符

异步文件写入：

1. 打开 `fs.open(path, flags[, mode], callback)`

   - 用来打开一个文件

   - 异步方法没有返回值，有返回值的都是同步方法。异步调用的方法，结果都是通过回调函数参数返回的。

   - callback 回调函数两个参数(arguments):

     - err 错误对象，如果没有错误则为 null

     - fd 文件的描述符

        ```javascript
        var fs = require("fs")
        var f
        fs.open("hello.txt","w",function(err, fd){
          // console.log('回调函数中的代码')  // callback中的代码会在读取完毕之后执行
          if(!err){
            f = fd
          }else{
            console.log(err)
          }
        })
        console.log("open下的代码") // 能比上面的更早执行
        ```

2. 写入 `fs.write(fd, string[, position[, encoding]], callback)`

   - 用来异步写入一个文件

3. 关闭 `fs.close(fd, callback)`

   - 用来关闭文件

      ```javascript
      var fs = require("fs")
      fs.open("hello.txt","w",function(err, fd){
      if(!err){
        fs.write(fd, "这是异步写入的内容",function(err)    {
        if(!err){
          console.log('写入成功')
        }
        fs.close(fd, function(err){
          if(!err){
            console.log('文件已关闭')
          }
        })
        })
      }else{
        console.log(err)
      }
      })
      ```

### 4、简单文件写入

`fs.writeFile(file, data[, options], callback)`

- file 要操作的文件的路径

- data 要写入的数据

- options 选项，可以对写入进行一些设置，是一个对象{encoding, mode, flag}

  - encoding: 'utf8'
  - mode: '0o666'
  - flag: 'w'   一般用r(只读)、w(可写)、a(追加)

- callback 当写入完成以后执行的函数

    ```javascript
    var fs = require('fs')
    // 路径也可以C:/Users/Shinlo/Desktop/hello.txt
    fs.writeFile("C:\\Users\\Shinlon\\Desktop\\hello.txt", "这是通过writeFile写入的内容", {flag: "a"}, function(err){
      if(!err){
        console.log('写入成功')
      }else{
        console.log(err)
      }
    })
    ```

![模式](https://cdn.wallleap.cn/img/pic/illustration/1588844894085.png)

`fs.writeFileSync(file, data[, options])`

同步简单写入

### 5、流式文件写入

同步、异步、简单文件的写入都不适合大文件的写入，性能较差，容易导致内存溢出

流式文件写入：

`fs.createWriteStream(path[, options])`

- 可以用来创建一个可写流
- path 文件路径
- options 配置的参数

```javascript
var fs = require("fs")
var ws = fs.createWriteStream("hello.txt")
// 可以通过监听流的open和close事件来监听流的打开和关闭
// ws.on("open", function{  // on绑定一个长期有效的事件
ws.once("open", function{   // once绑定一次性的事件，在触发一次之后事件自动失效
  console.log("流打开了")
})
ws.once("close", function{
  console.log("流关闭了")
})
// 通过ws向文件中输出内容
ws.write("通过可写流写入文件的内容1")
ws.write("通过可写流写入文件的内容2")
ws.write("通过可写流写入文件的内容3")
// 只要流还存在就可以接着写入
// 关闭流
// ws.close()    // 这个在传入的方向断开流，文件没到管子里
ws.end()  // 在传出的这一方断开流，数据已经在管子里了
```

### 6、文件的读取

同步文件读取、异步文件读取、简单文件读取

`fs.readFile(path[, options], callback)`

`fs.readFileSync(path[, options])`

- path 要读取的文件的路径
- options 读取的选项
- callback 回调函数，通过回调函数将读取到的内容返回
  - err 错误对象
  - data 读取到的数据，会返回一个Buffer

```javascript
var fs = require("fs")
var path="C:/Users/Shinlon/a.mp3"
fs.readFile("hello.txt", function(err, data) {
  if(!err) {
    console.log(data)  // buffer通用性更高
    // console.log(data.toString())文本可以，其他不行
    fswriteFile("hello.mp3", data, function(err) {
      if(!err) {
        console.log("文件写入成功")
      }
    })
  }
})
```

流式文件读取

- 流式文件读取也适用于一些比较大的文件，可以分多次将文件读取到内存中
- `fs.createReadStream(path[, options])`

```javascript
var fs = require("fs")
// 创建一个可读流
var rs = fs.createReadStream("an.jpg")
// 监听流的开启和关闭
rs.once("open", function() {
  console.log("可读流打开了")
})
rs.once("close", function() {
  console.log("可读流关闭了")
})
// 读取一个可读流中的数据，必须要为可读流绑定一个 data 事件，data 事件绑定完毕，它会自动开始读取数据
rs.on("data", function(data) {
  console.log(data) // 参数就是数据  data.length 最大 65536 字节
})
```

可读流、可写流复制一个大文件

```javascript
var fs = require("fs")
var rs = fs.createReadStream("an.jpg")
var ws = fs.createWriteStream("an.jpg")
rs.once("open", function() {
  console.log("可读流打开了")
})
rs.once("close", function() {
  console.log("可读流关闭了")
  // 数据读取完毕，关闭可写流
  ws.end()
})
ws.once("open", function() {
  console.log("可写流打开了")
})
ws.once("close", function() {
  console.log("可写流关闭了")
})
rs.on("data", function(data) {
  ws.write(data)
})
```

简单的方式

```javascript
var fs = require("fs")
var rs = fs.createReadStream("an.jpg")
var ws = fs.createWriteStream("an.jpg")
rs.once("open", function() {
  console.log("可读流打开了")
})
rs.once("close", function() {
  console.log("可读流关闭了")
})
ws.once("open", function() {
  console.log("可写流打开了")
})
ws.once("close", function() {
  console.log("可写流关闭了")
})
// pipe()可以将可读流中的内容直接输出到可写流中
rs.pipe(ws)
```

### 7、fs 的其他方法

验证路径是否存在

- ~~fs.exists(path, callback)~~
- `fs.exitsSync(path)`

```js
var fs = require("fs")
var isExists = fs.exitsSync("a.mp3")
// console.log(isExists)
```

获取文件信息

- `fs.stat(path, callback)`获取文件的状态，会返回一个对象，这个对象中保存了当前对象状态的相关信息
- `fs.statSync(path)`

```js
fs.stat("a.mp3", function(err, stat) {
  console.log(stat)
})
```

stat 参数的一些属性、方法

- size 大小
- ……

删除文件

- `fs.unlink(path, callback)`
- `fs.unlinkSync(path)`

```js
fs.unlinkSync("hello.txt")
```

列出文件

- `fs.readdir(path[, options], callback)`读取一个目录的目录结构
- `fs.readdirSync(path[, options])`
  - files 是一个字符串数组，每一个元素就是一个文件夹或文件的名字

```js
fs.readdir(".", function(err, files) {
  if(!err){
    console.log(files)
  }
})
```

截断文件

- `fs.truncate(path, len, callback)` 将文件修改为指定的大小
- `fs.truncateSync(path, len)`

```js
fs.truncateSync("hello.txt", 3)
```

建立目录

- `fs.mkdir(path[,mode], callback)`
- `fs.mkdirSync(path[, mode])`

```js
fs.mkdirSync("hello")
```

删除目录

- `fs.rmdir(path, callback)`
- `fs.rmdirSync(path)`

```js
fs.rmdirSync("hello")
```

重命名文件和目录

- `fs.rename(oldPath, newPath, callback)`
- `fs.renameSync(oldPath, newPath)`
  - oldPath 旧的路径
  - newPath 新的路径
  - callback 回调函数

```js
fs.rename("a.mp3", "new.mp3", function(err) {
  if(!err){
    console.log("success")
  }
})
```

监视文件更改写入

- `fs.watchFile(filename[, options], listener)`
  - filename 要监视的文件的名字
  - options 配置选项
  - listener 回调函数，当文件发生变化时，回调函数会执行
    - curr 当前文件的状态
    - prev 修改前文件的状态
    - 这两个对象都是stats对象

```js
fs.watchFile("hello.txt", function {
  console.log(prev.size)
  console.log(curr.size)
})
```

时间间隔，配置选项中

```js
fs.watchFile("hello.txt", { interval: 1000 }, function {
  console.log(prev.size)
  console.log(curr.size)
})
```
