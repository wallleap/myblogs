---
title: JS 组织代码方式演变——模块化
date: 2020-05-15 19:33
updated: 2020-05-15 19:33
cover: //cdn.wallleap.cn/img/pic/cover/202302GKk2ms.jpg
category: 技术杂谈
tags:
  - web
  - 前端
description: JS 组织代码方式演变——模块化
---

看别人的代码的时候，有些人写的代码一团糟，可是有些人的代码进行合理的分块，看起来很容易阅读理解。

## 1、是什么

* 什么是模块?

  * 将一个复杂的程序依据一定的规则(规范)封装成几个块(文件), 并进行组合在一起
  * 块的内部数据/实现是私有的, 只是向外部暴露一些接口(方法)与外部其它模块通信

* 一个模块的组成

  * 数据--->内部的属性
  * 操作数据的行为--->内部的函数

* 模块化

  * 编码时是按照模块一个一个编码的, 整个项目就是一个模块化的项目
  * 原则
    * 把大程序分割成一个个模块
    * 把大模块分割成一个个小模块
  * 优点
    * 增强代码的可阅读性、可维护性
  * 模块化是现代前端工程化的开端

## 2、模块化的进化过程

代码之间会相互依赖（A 需要 B 中的变量/函数），应该怎样对代码进行组织呢

### （1）通过注释进行组织

* 优点：极简

* 缺点
  * 有些功能可能忘了加注释 → 专人进行代码审查（Code Review）
  * JS 文件会越来越大 → 分成多个 JS 文件

```js
/**
 * 获取元素
 */
getElement(el)
/**
 * 删除元素
 */
removeElement(node)
```

### （2）用函数组织代码

* 编码: 全局变量/函数

* 问题: 污染全局命名空间, 容易引起命名冲突/数据不安全

* 缺点
  * 全局函数名太多了 → 可以使用命名空间
    * 调用关系复杂，难以调整顺序 → 立即执行函数
    * JS 文件会越来越大 → 拆分成多个 JS 文件

```js
function getElement(el) {}
function removeElement(node) {}
/* 在合适的时候调用 */
const red = getElement('.red')
removeElement(red)
```

### （3）用命名空间（namespace） 组织代码

* 编码: 将数据/行为封装到对象中，使用的时候`对象名.方法`

* 解决: 命名冲突(减少了全局变量)

* 问题: 数据不安全(外部可以直接修改模块内部的数据)

* 优点：占用的全局变量少，只有一个 `app`

* 缺点
  * 名字越来越长 → 无解
  * 依赖关系不清晰 → 立即执行函数

```js
var app = app || {}
app.person = () => {}
app.user.sub = () => {}
app.friends = () => {}
app.person()
app.user.sub()
app.friends()
```

### （4）立即执行函数

* IIFE : 立即调用函数表达式--->匿名函数自调用

  * 编码: 将数据和行为封装到一个函数内部, 通过给window添加属性来向外暴露接口
    * 优点
      * 可以有名字，也可以没有名字
      * 可以声明依赖
      * 可以选择导出内容

  * 缺点：无法处理循环依赖 → 无解

```js
// 提前引入依赖
!function user(dom, axios, time) {
  // do something
}(dom, axios, time)  // 直接传入依赖
/* 有名字 */
const personModule = function(dom, axios, time) {
  // do something
  return {
    getPerson,
    updatePerson
  }
}(dom, axios, time)
```

### （5）CommonJS

* Node.js : 服务器端

* 基本语法:

  * 定义暴露模块 : exports

    ```js
    exports.xxx = value
    module.exports = value
    ```

  * 引入模块 : require

    ```js
    var module = require('模块名/模块相对路径')
    ```

* 每个文件都可以当作一个模块

* 引入模块发生在什么时候?

  * Node : 运行时, 动态同步引入

* 优点
  * 用文件当名字，不用全局变量
  * 可以声明依赖
  * 可以选择导出内容
  * 可以循环依赖

* 缺点：不支持异步/浏览器环境 → AMD

### （6）AMD （异步模块定义）

* 浏览器端，模块的加载时异步的

* require.js

  * 基本语法

    * 定义暴露模块: `define([依赖模块名], function(){return 模块对象})`

    * 引入模块: `require(['模块1', '模块2', '模块3'], function(m1, m2){//使用模块对象})`

* 优点
  * 用字符串当名字，不用全局变量
  * 可以声明依赖
  * 可以选择导出内容
  * 可以循环依赖
  * 支持异步
* 缺点
  * 对同步的支持不如 CommonJS → Node 用 CJS，前端用 AMD
  * 没有写入 ECMAScript 文档 → ESM

### （7）ES Modules（ES 模块）

* ES 6 内置了模块化的实现 `<script type="module" src="index.js"></script>`

* 基本语法

  * 定义暴露模块 : `export`

    * 暴露一个对象:

      ```js
      export default 对象
      ```

    * 暴露多个:

      ```js
      export var xxx = value1
      export let yyy = value2
      
      var xxx = value1
      let yyy = value2
      export {xxx, yyy}
      ```

  * 引入使用模块 : `import`

    * default 模块:

      ```js
      import xxx  from '模块路径/模块名'
      ```

    * 其它模块

      ```js
      import {xxx, yyy} from '模块路径/模块名'
      import * as module1 from '模块路径/模块名'
      ```

* 问题: 有些浏览器还不能直接识别 ES 6 模块化的语法  

* 优点
  * 该支持的都支持
  * 支持静态分析（tree-shaking）
  * 支持按需加载（`import()`，是个 promise）
* 缺点
  * 不支持拼接字符串 → 无解
  * 不支持模糊加载 → 使用代码生成技术
  * 不兼容 Node 的 CJS → 使用 `.mjs` 后缀

## 3、模块化演示

### 1、CommonJS 基于服务器端（Node.js）

* 下载安装 Node.js

* 创建目录结构

  * Modules

    * module1.js
    * module2.js
    * module3.js

  * app.js

  * package.json（命令创建 `npm init`，再输入包名）

    ```json
    {
        "name": "conmmonjs_node",
        "version": "1.0.0"
    }
    ```

* 下载第三方模块 `npm install uniq --save`

  * package.json

    ```json
    {
        "name": "conmmonjs_node",
        "version": "1.0.0",
        "dependencies":{
         "uniq": "^1.0.1"
     }
    }
    ```

* 模块化编码

  * module1.js

    ```javascript
    // module.exports = value 暴露一个对象
    module.exports = {
        msg: 'module1',
        foo(){
            console.log(this.msg)
        }
    }
    ```

  * module2.js

    ```javascript
    // 暴露一个函数 module.exports = function(){}
    module.exports = fuction(){
        console.log("module2")
    }
    ```

  * module3.js

    ```javascript
    // exports.xxx = value 分别暴露
    exports.foo = function(){
        console.log('foo() module3')
    }
    exports.bar = function(){
        console.log('bar() module3')
    }
    
    exports.arr = [2, 4, 5, 2, 3, 5, 1]
    ```

  * app.js

    ```javascript
    // 将其他的模块汇集到主模块
    let uniq = require('uniq')
    
    let module1 = require('./modules/module1')
    let module2 = require('./modules/module2')
    let module3 = require('./modules/module3')
    
    module1.foo()
    
    module2()
    
    module3.foo()
    module3.bar()
    
    let result = uniq(module3.arr)
    console.log(result)
    ```

* 通过 node 运行 app.js——`node app.js`

### 2、CommonJS 基于浏览器端应用（Browserify）

* 创建项目结构

  * js

    * dist //打包生成文件的目录
    * src //源码所在的目录
      * module1.js
      * module2.js
      * module3.js
      * app.js //应用主源文件

  * index.html

  * package.json

    ```json
    {
        "name": "browserify-test",
        "version": "1.0.0"
    }
    ```

* 下载 browserify

  * 全局：`npm install browserify -g`

  * 局部：`npm install browserify --save-dev`

    ```json
    {
        "name": "browserify-test",
        "version": "1.0.0",
        "devDependencies":{
            "browserify": "^14.5.0"
        }
    }
    ```

* 下载第三方模块 `npm install uniq --save`

  * package.json

    ```json
    {
        "name": "browserify-test",
        "version": "1.0.0",
        "devDependencies":{
            "browserify": "^14.5.0"
        },
        "dependencies":{
         "uniq": "^1.0.1"
     }
    }
    ```

* 定义模块代码

  * module1.js

    ```javascript
    module.exports = {
      foo() {
        console.log('moudle1 foo()')
      }
    }
    ```

  * module2.js

    ```javascript
    module.exports = function () {
      console.log('module2()')
    }
    ```

  * module3.js

    ```javascript
    exports.foo = function () {
      console.log('module3 foo()')
    }
    
    exports.bar = function () {
      console.log('module3 bar()')
    }
    ```

  * app.js

    ```javascript
    //引用模块
    let module1 = require('./module1')
    let module2 = require('./module2')
    let module3 = require('./module3')
    
    let uniq = require('uniq')
    
    //使用模块
    module1.foo()
    module2()
    module3.foo()
    module3.bar()
    
    console.log(uniq([1, 3, 1, 4, 3]))
    ```

* 打包处理 js：`browserify js/src/app.js -o js/dist/bundle.js`

* 页面使用引入

  * index.html

    ```html
    <html lang="en">
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>broserify 测试</title>
    </head>
    <body>
    <script src="js/dist/bundle.js"></script>
    </body>
    </html>
    ```

### 3、AMD 规范

#### （1）NoAMD

* 项目结构

  * js
    * alerter.js
    * dataService.js
  * app.js
  * test1.html

* 文件内容

  * dataService.js

    ```javascript
    // 定义一个没有依赖的模块
    (function(win){ // 形参可以和实参的名字相同，这里方便区分
        let name = 'dataservice.js'
        function getName(){
            return name
        }
        win.dataService = {getName}
    })(window) // 实参
    ```

  * alerter.js
  
    ```javascript
    // 定义一个有依赖的模块
    (function(window, dataService){
        let msg = 'alerter.js'
        function showMsg(){
            alert(msg + ',' + dataService.getName())
        }
        window.alerter = {showMsg}
    })(window, dataService) // 依赖dataService
    ```

  * app.js
  
    ```javascript
    (function (alerter){
        alerter.showMsg()
    })(alerter)
    ```
  
  * test1.html
  
    ```html
    <html lang="en">
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Modular Demo: 未使用AMD(require.js)</title>
    </head>
    <body>
    <script src="./js/dataService.js"></script> 
    <script src="./js/alerter.js"></script> 
    <script src="./app.js"></script> // 下面的分别依赖上面的模块
    </body>
    </html>
    ```

#### （2）AMD（require.js）

1. 下载 require.js, 并引入

* 官网: <http://www.requirejs.cn/>
* GitHub: <https://github.com/requirejs/requirejs>
* 将 require.js 导入项目: js/libs/require.js

2. 创建项目结构

* js
  * libs
    * require.js
  * modules
    * alerter.js
    * dataService.js
  * main.js
* index.html

3. 定义require.js的模块代码

* dataService.js

    ```javascript
    // 定义没有依赖的模块
    define(function () {
      let msg = 'dataService.js'
    
      function getMsg() {
        return msg.toUpperCase()
      }
      // 暴露模块
      return {getMsg}
    })
    ```

* alerter.js

    ```javascript
    // 定义有依赖的模块
    define(['dataService', 'jquery'], function (dataService, $) {
      let msg = 'alerter.js'
    
      function showMsg() {
        $('body').css('background', 'gray')
        alert(dataService.getMsg() + ', ' + msg)
      }
    
      return {showMsg}
    })
    ```

4. 应用主(入口) js：main.js

   ```javascript
   (function () {
       //配置
       require.config({
           //基本路径 出发点在根目录下
           baseUrl: "js/",
           //模块标识名与模块路径映射
           paths: {
               "alerter": "modules/alerter",
               "dataService": "modules/dataService",
           }
       })
       //引入使用模块
       require( ['alerter'], function(alerter) {
           alerter.showMsg()
       })
   })()
   ```

4. 页面使用模块：index.html

```html
<script data-main="js/main" src="js/libs/require.js"></script>
```

6. 使用第三方基于 require.js 的框架(jquery)

* 将 jquery 的库文件导入到项目:

  * js/libs/jquery-1.10.1.js

* 在 main.js 中配置 jquery 路径

    ```javascript
    paths: {
        'jquery': 'libs/jquery-1.10.1'  // jQuery定义的返回AMD模块名为小写
    }
    ```

* 在 alerter.js 中使用 jquery

    ```javascript
    define(['dataService', 'jquery'], function (dataService, $) {
        var name = 'xfzhang'
        function showMsg() {
            $('body').css({background : 'red'})
            alert(name + ' '+dataService.getMsg())
        }
        return {showMsg}
    })
    ```

7. 使用第三方不基于 require.js 的框架(angular/angular-messages)

* 将 angular.js 和 angular-messages.js 导入项目

  * js/libs/angular.js
  * js/libs/angular-messages.js

* 在 main.js 中配置

    ```javascript
    (function () {
      require.config({
        //基本路径
        baseUrl: "js/",
        //模块标识名与模块路径映射
        paths: {
          //第三方库
          'jquery' : 'libs/jquery-1.10.1',
          'angular' : 'libs/angular',
          'angular-messages' : 'libs/angular-messages',
          //自定义模块
          "alerter": "modules/alerter",
          "dataService": "modules/dataService"
        },
        /*
         配置不兼容AMD的模块
         exports : 指定导出的模块名
         deps  : 指定所有依赖的模块的数组
         */
        shim: {
          'angular' : {
            exports : 'angular'
          },
          'angular-messages' : {
            exports : 'angular-messages',
            deps : ['angular']
          }
        }
      })
      //引入使用模块
      require( ['alerter', 'angular', 'angular-messages'], function(alerter, angular) {
        alerter.showMsg()
        angular.module('myApp', ['ngMessages'])
        angular.bootstrap(document,["myApp"])
      })
    })()
    ```

* 页面:

    ```html
    <form name="myForm">
      用户名: <input type="text" name="username" ng-model="username" ng-required="true">
      <div style="color: red;" ng-show="myForm.username.$dirty&&myForm.username.$invalid">用户名是必须的</div>
    </form>
    ```

### <font color=lightgray>5、CMD规范</font>

1. 下载 sea.js, 并引入

* 官网: <http://seajs.org/>
* GitHub : <https://github.com/seajs/seajs>
* 将 sea.js 导入项目: js/libs/sea.js

2. 创建项目结构

  ```
|-js
  |-libs
    |-sea.js
  |-modules
    |-module1.js
    |-module2.js
    |-module3.js
    |-module4.js
    |-main.js
|-index.html
  ```

3. 定义sea.js的模块代码

* module1.js

    ```javascript
    // 没有依赖的模块
    define(function (require, exports, module) {
      //内部变量数据
      var data = 'atguigu.com'
      //内部函数
      function show() {
        console.log('module1 show() ' + data)
      }
    
      //向外暴露
      exports.show = show
    })
    ```

* module2.js

    ```javascript
    define(function (require, exports, module) {
      let msg = 'module2'
      function bar(){
          console.log(msg)
      }
        module.exports = bar
      /* module.exports = {
        msg: 'I Will Back'
      } */
    })
    ```

* module3.js

    ```javascript
    define(function(require, exports, module){
        let data = 'module3'
        function fun(){
            console.log(data)
        }
        exports.module3 = {fun}
    })
    /* define(function (require, exports, module) {
      const API_KEY = 'abc123'
      exports.API_KEY = API_KEY
    }) */
    ```

* module4.js

    ```javascript
    define(function(require, exports, module){
        let msg = 'module4'
        // 同步引入
        let module2 = require('./module2')
        module2()
        // 异步引入
        require.async('./module3', function(module3){
            module3.module3.fun()
        })
        function fun2(){
            console.log(msg)
        }
        exports.fun2 = fun2
    })
    /*define(function (require, exports, module) {
      //引入依赖模块(同步)
      var module2 = require('./module2')
    
      function show() {
        console.log('module4 show() ' + module2.msg)
      }
    
      exports.show = show
      //引入依赖模块(异步)
      require.async('./module3', function (m3) {
        console.log('异步引入依赖模块3  ' + m3.API_KEY)
      })
    })*/
    ```

* main.js : 主(入口)模块

    ```javascript
    define(function (require) {
      let module1 = require('./module1')
      console.log(module1.foo())
      let module4 = require('./module4')
      module4.fun2()
    })
    /*define(function (require) {
      var m1 = require('./module1')
      var m4 = require('./module4')
      m1.show()
      m4.show()
    })*/
    ```

4. index.html:

  ```html
<!--
使用seajs:
  1. 引入sea.js库
  2. 如何定义导出模块 :
    define()
    exports
    module.exports
  3. 如何依赖模块:
    require()
  4. 如何使用模块:
    seajs.use()
-->
<script type="text/javascript" src="js/libs/sea.js"></script>
<script type="text/javascript">
  seajs.use('./js/modules/main')
</script>
  ```

### <font color=red>6、ES6-Babel-Browserify 使用</font>

1. 定义 package.json 文件

  ```json
{
    "name" : "es6-babel-browserify",
    "version" : "1.0.0"
}
  ```

2. 安装 babel-cli, babel-preset-es2015 和 browserify // cli——command line interface

* `npm install babel-cli browserify -g`
* `npm install babel-preset-es2015 --save-dev`
* preset 预设（将es6转换成es5的所有插件打包）

3. 定义 `.babelrc` 文件（babel run control）

   ```bash
   {
    "presets": ["es2015"]
   }
   ```

3. 编码

* js/src/module1.js

    ```JavaScript
    // 暴露模块 分别暴露
    export function foo() {
      console.log('module1 foo()');
    }
    export let bar = function () {
      console.log('module1 bar()');
    }
    export const DATA_ARR = [1, 3, 5, 1]
    ```

* js/src/module2.js

    ```JavaScript
    // 统一暴露——常规暴露
    let data = 'module2 data'
    
    function fun1() {
      console.log('module2 fun1() ' + data);
    }
    
    function fun2() {
      console.log('module2 fun2() ' + data);
    }
    
    export {fun1, fun2}
    ```

* js/src/module3.js

    ```JavaScript
    // 默认暴露：可以暴露任意数据类型，暴露什么数据类型接收到的就是什么数据
    // export default value
    export default() =>{
        console.log('我是默认暴露的箭头函数')
    } // 只能暴露一个default，因此暴露对象
    /* export default {
      name: 'Tom',
      setName: function (name) {
        this.name = name
      }
    } */
    ```

* js/src/app.js

    ```JavaScript
    // 引入其他的模块
    // 语法： import xxx from '路径'
    import {foo, bar} from './module1'
    import {DATA_ARR} from './module1'
    import {fun1, fun2} from './module2'
    
    import module3 from './module3'
    /* import person from './module3' */
    
    // 安装 npm install jquery@1
    import $ from 'jquery'
    
    $('body').css('background', 'red')
    
    foo()
    bar()
    console.log(DATA_ARR);
    fun1()
    fun2()
    
    module3()
    /* person.setName('JACK')
    console.log(person.name); */
    ```

5. 编译

* 使用 Babel 将 ES6 编译为 ES5 代码(但包含CommonJS语法) : `babel js/src -d js/lib`
* 使用 Browserify 编译 js : `browserify js/lib/app.js -o js/lib/bundle.js`

6. 页面中引入测试

  ```html
<script type="text/javascript" src="js/lib/bundle.js"></script>
  ```

7. 引入第三方模块(jQuery)
   1). 下载jQuery模块:

   * `npm install jquery@1 --save` // @后的是版本，1代表`1.x.x`中的最新版本

   2). 在app.js中引入并使用

   ```js
   import $ from 'jquery'
   $('body').css('background', 'red')
   ```
