---
title: AngularJs 学习笔记
date: 2020-06-04 23:33
updated: 2020-06-04 23:33
cover: //cdn.wallleap.cn/img/pic/cover/202302cmRhbN.jpg
category: 技术杂谈
tags:
  - web
  - 前端
description: AngularJs 学习笔记
---

前端框架之一，个人更喜欢用 Vue 和 React

## 一、Angular 介绍

- 官网：<https://angularjs.org>
- Angular 是 Google 开源的前端 JS 结构化框架
- AngularJS 特性和优点
  - 双向数据绑定
  - 声明式依赖注入
  - 解耦应用逻辑，数据模型和视图
    - 耦合度：两者之间关系密切度
    - 降低耦合度
  - 完善的页面指令
  - 定制表单验证
  - Ajax 封装
- 与 jQuery 比较
  - jQuery
    - JS 函数库
    - 封装简化 DOM 操作
  - Angular
    - JS 结构化框架
    - 主体不再是 DOM，而是页面中的动态数据
- AngularJS 能做什么项目
  - 构建单页面(SPA)Web 应用或 Web APP 应用
    - 单页面应用（SPA）Simple Page Application 特点：
      - 将所有的活动局限于一个页面
      - 当页面中有部分数据发生了变化不会去刷新整个页面，而是局部刷新
      - 利用的 Ajax 技术、路由
  - 应用
    - 微信网页版 <https://wx.qq.com>
    - 知乎周报 <https://zhuanlan.zhihu.com/Weekly>
    - 后台管理应用：阿里云、土豆后台、唯品会……
- 版本学习
  - 1.0 JavaScript
  - ~~2.0 3.0 4.0 TypeScript~~

### 第一个 Angular 程序

使用 jQuery 实现

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>jQuery实现</title>
</head>
<body>
  <input type="text">
  <p>您输入的内容是：<span></span></p>
  <script src="jquery.js"></script>
  <script>
    $(function(){  //document.ready 文档(页面结构)加载完毕 window.onload:整个页面加载完毕，包括图片等资源
      $('input').keyup(function(){
        var value = this.value   // $(this).val()
        $('span').html(value)
      })
    })
  </script>
</body>
</html>
```

使用 AngularJS 实现

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>AngularJS实现</title>
</head>
<body ng-app>
  <input type="text" ng-model="username">
  <p>您输入的内容是：<span>{{username}}</span></p>
  <!-- 引入 NG -->
  <script src="https://cdn.bootcdn.net/ajax/libs/angular.js/1.2.29/angular.js"></script>
</body>
</html>
```

Chrome 调试插件：

> ng-inspector for AngularJS

### Angular 中的知识点

- `ng-app`(指令)：告诉angular核心，它管理当前标签所包含的整个区域，并且会自动创建 $rootScope 根作用域对象（通常放在 body 标签）
- `ng-model`：将当前输入框的值与谁关联(属性名:属性值)，并作为当前作用域对象($rootScope)的属性

- 表达式：通常有一个返回值，可以放在任何需要值的地方，比如函数调用的参数、一个变量名、一个运算等（`{{username}}`）

- 语句：通常表示一个完整的执行单位，一段完整的 js 可执行代码，有的语句也可以用表达式来执行，称为表达式语句

- 区别：语句用分号结尾，有些语句我们没有加分号，例如 `console.log` 虽然没加分号，但也是语句，因为 js 引擎会自动在解析的时候加上分号

- 特例：if 语句，就不用加分号，也可以是完整的语句

## 二、四个重要概念

### 1、双向数据绑定

- 数据绑定：数据从一个地方 A 转移（传递）到另一个地方 B，而且这个操作由框架来完成

- 双向数据绑定：数据可以从 View（视图层）流向 Model（模型/数据层），也可以从 Model 流向 View

  - 视图（View）：也就是我们的页面（主要是 Angular 指令和表达式）

  - 模型（Model）：作用域对象（当前为 $rootScope），它可以包含一些属性或方法

  - 当改变 View 中的数据，Model 对象的对应属性也会随之改变：ng-model 指令 数据从 View 到 Model

  - 当 Model 域对象的属性发生改变时，页面对应数据随之更新：`{{}}` 表达式  数据从 Model 到 View

  - ng-model 是双向数据绑定，而 `{{}}` 是单向数据绑定（View——页面   Model——内存）

- ng-init：用来初始化当前作用域变量（View-->Model-->View）

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>AngularJS实现</title>
</head>
<body ng-app> <!-- ng-app=""除了接管区域，还会自动生成根作用域($rootScope) -->
  <!--
  <input type="text" ng-model="name">   先传递到Model，再从Model到三个View中的相应位置
  <p>姓名1：{{name}}</p>
  <input type="text" ng-model="name">
  <p>姓名2：{{name}}</p>
  -->
  <script src="https://cdn.bootcdn.net/ajax/libs/angular.js/1.2.29/angular.js"></script>
</body>
</html>
```

显示结果

![测试](https://cdn.wallleap.cn/img/pic/illustration/1589612197548.png)

过程

```html
<body ng-app>
```

`ng-app=""` 除了接管区域，还会自动生成根作用域（$rootScope）

```html
<input type="text" ng-model="name">
```

![过程1](https://cdn.wallleap.cn/img/pic/illustration/1589611921666.png)

```html
<p>姓名1：{{name}}</p>
```

![过程2](https://cdn.wallleap.cn/img/pic/illustration/1589612077497.png)

初始化数据

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>AngularJS实现</title>
</head>
<body ng-app ng-init="name='Tom'"> <!-- ng-init初始化数据 -->
  <input type="text" ng-model="name">
  <p>姓名1：{{name}}</p>
  <input type="text" ng-model="name">
  <p>姓名2：{{name}}</p>
  <script src="https://cdn.bootcdn.net/ajax/libs/angular.js/1.2.29/angular.js"></script>
</body>
</html>
```

![过程3](https://cdn.wallleap.cn/img/pic/illustration/1589612507494.png)

### 2、依赖注入

- 依赖对象：完成某个特定的功能需要某个对象才能实现，这个对象就是依赖对象
- 依赖注入：依赖的对象以形参的形式被注入进来使用，这种方式就是依赖注入
- Angular 的 `$scope` 对象就是依赖对象，并且是依赖注入的形式进行使用
- 回调函数的 event 的就是依赖对象
- 回调函数有形参就是依赖注入

eg：数组中每一项加 10

```javascript
var arr = [1,2,3,4,5]
var newArr1 = []
// 命令式
for(var i = 0; i < arr.length; i++){
  var value = arr[i] + 10
  newArr1.push(value)
}
console.log(newArr1)
// 声明式
var newArr2 = arr.map(function(item, index){
  return item + 10
})
console.log(newArr2)
```

## 三、三个重要对象

### 1、作用域与控制器

- 作用域对象
  - 一个 JS 实例对象，ng-app 指令默认会创建一个根作用域对象（$rootScope）
  - 它的属性和方法与页面中的指令或表达式是关联的
- 控制器
  - 用来控制 AngularJS 应用数据的实例对象
  - ng-controller：指定控制器构造函数，Angular 会自动 new 此函数创建控制器对象
  - 同时 Angular 还有创建一个新的域对象 `$scope`，它是 `$rootScope` 的子对象
  - 在控制器函数中声明 `$scope` 形参，Angular 会自动将 `$scope` 传入

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>AngularJS实现</title>
</head>
<body ng-app ng-init="age=12">
  <div ng-controller="MyController">
    <input type="text" placeholder="姓" ng-model="firstName">
    <input type="text" placeholder="名" ng-model="lastName">
    <p>姓名1：{{firstName+'-'+lastName}}</p>
    <p>姓名2：{{getName()}}</p>
    {{age}}
  </div>
  <div>
    {{firstName}}   <!-- 不能显示 -->
  </div>
  <script src="https://cdn.bootcdn.net/ajax/libs/angular.js/1.2.29/angular.js"></script>
  <script>
    function MyController($scope){ // 形参必须是$scope
      // console.log($scope)
      // console.log(this instanceof MyController)
      $scope.firstName = 'lu'
      $scope.lastName = 'wang'
      $scope.getName = function(){
        return $scope.firstName + ' ' + $scope.lastName
        // return this.firstName + ' ' + this.lastName
      }
    }
  </script>
</body>
</html>
```

![作用域](https://cdn.wallleap.cn/img/pic/illustration/1589613477087.png)

### 2、模块和控制器

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>AngularJS实现</title>
</head>
<body ng-app="myApp">   <!--指向模块对象的名字-->
  <div ng-controller="MyController">
    <input type="text" ng-model='empName'>
    <p>员工名字1：{{empName}}</p>
  </div>
  <div ng-controller="MyController2">
    <input type="text" ng-model='empName'>
    <p>员工名字2：{{empName}}</p>
  </div>
  <script src="https://cdn.bootcdn.net/ajax/libs/angular.js/1.5.5/angular.js"></script>
  <script>
    // console.log(angular)
    /* // 创建模块对象
    var myModule = angular.module("myApp", [])
    // 生成作用域对象
    myModule.controller('MyController', function($scope){
      $scope.empName = 'Tom'
    })
    myModule.controller('MyController2', function($scope){
      $scope.empName = 'Jack'
    }) */
    // 优化 链式调用
    /* <angular.module("myApp", [])
          .controller('MyController', function($scope){  // 返回值是模块对象
            $scope.empName = 'Tom'
          })
          .controller('MyController2', function($scope){ // 隐式声明依赖注入
            $scope.empName = 'Jack'
          }) */
      // 但是，由于js代码压缩之后形参会用其他字母abcd代替，会造成angular解析不了，解决方案：
      <angular.module("myApp", [])
          .controller('MyController', ['$scope', function($scope){ // 显式声明依赖注入
            $scope.empName = 'Tom'
          }])
          .controller('MyController2', ['$scope', function($scope){
            $scope.empName = 'Jack'
          }])
  </script>
</body>
</html>
```

## 四、两个页面语法

### 1、表达式

- 使用 Angular 表达式：
  - 语法：`{{expression}}`
  - 作用：显示表达式的结果数据
  - 注意：表达式中引用的变量必须是当前域对象有的属性（包括其原型属性）
- 操作的数据
  - 基本类型数据：`Number` / `String` / `Boolean`
  - `undefined`, `Infinity`, `NaN`, `null` 解析为空串 `""`，不显示任何效果
  - 对象的属性或方法
  - 数组

### 2、常用指令

- Angular 指令
  - Angular 为 HTML 页面扩展的：自定义标签属性或标签
  - 与 Angular 的作用域对象（scope）交互，扩展页面的动态表现力
- 常用指令
  - `ng-app`：指定 AngularJS 应用的根作用域对象
  - `ng-model`：指定表单元素与作用域对象属性的绑定
  - `ng-init`：初始化作用域对象属性的值
  - `ng-click`：指定点击事件的处理函数
  - `ng-controller`：指定控制器构造函数
  - `ng-bind`：指定元素的文本内容与作用域对象属性的绑定
  - `ng-repeat`：指定元素的重复，与作用域对象数组的绑定
  - `ng-show`：指定元素的显示与隐藏，与作用域对象属性的绑定
  - `ng-hide`：指定元素的隐藏与显示，与作用域对象属性的绑定
  - `ng-class`：指定元素的类样式，与作用域对象属性的绑定
  - `ng-style`：指定元素的内联样式，与作用域对象属性的绑定
  - `ng-mouseenter`：指定鼠标进入事件的处理函数
  - `ng-mouseleave`：指定鼠标离开事件的处理函数
