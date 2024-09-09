---
title: 深入学习 JS 高级
date: 2020-04-15 19:33
updated: 2020-04-15 19:33
cover: //cdn.wallleap.cn/img/pic/cover/202302GKk2ms.jpg
category: 技术杂谈
tags:
  - web
  - 前端
description: 深入学习 JS 高级
---

在 JS 基础上深入学习这个语言

- 基础总结

- 函数高级

- 面向对象高级

- 线程机制与事件机制

## 一、基础总结

### 1、数据类型

**分类**

- 基本（值）类型
  - String：任意字符串
  - Number：任意的数字
  - boolean：true/false
  - undefined：undefined
  - null：null
  - symbol：symbol 类型的数据
  - bigint：bigint 类型的数据

- 对象（引用）类型 object
  - Object：任意对象
  - Function：一种特殊的对象（可以执行）
  - Array：一种特殊的对象（数值下标，内部数据是有序的）
  - Date：一种特殊的对象（可以表示日期）
  - RegExp：一种特殊的对象（可以表示正则表达式）
  - Math：数学对象
  - Window：浏览器窗口对象
  - ……

```javascript
var obj = {
  name: 'TOM',
  age: 12
}
function test(){
  var a = 3
}
var arr = [3, 'abc']
arr[1]
```

**判断**

- `typeof`
  - 可以判断：undefined/数值/字符串/布尔值/function
  - 不能判断：null 与 Object、Object与 array

- `instanceof`：判断对象的具体类型

- `===` 可以判断：undefined/null/function
- `isNaN` 判断NaN ……

```javascript
//1. 基本
// typeof返回数据类型的字符串表达
var a
// undefined
console.log(a, typeof a, typeof a==='undefined',a===undefined )  // undefined 'undefined' true true
console.log(undefined==='undefined') // false
// Number Sting Boolean
a = 4
console.log(typeof a==='number') // true
a = "abc123"
console.log(isNaN(a)) // true
a = 'string iiii'
console.log(typeof a==='string') // true
a = true
console.log(typeof a==='boolean') // true
// null
a = null
console.log(typeof a, a===null) // 'object' true

//2. 对象
var b1 = {
 b2: [1, 'abc', console.log],
 b3: function () {
  console.log('b3') // b3
  return function () {
   return 'funb1'
  }
 }
}
// Object Array Function
console.log(b1 instanceof Object, b1 instanceof Array) // true  false
console.log(b1.b2 instanceof Array, b1.b2 instanceof Object) // true true
console.log(b1.b3 instanceof Function, b1.b3 instanceof Object) // true true
console.log(typeof b1.b2) // 'object'
// Function
console.log(typeof b1.b3==='function') // true
console.log(typeof b1.b2[2]==='function') // true

// 细节问题
b1.b2[2](4) // 4
console.log(b1.b3()()) // funb1
/*
b1.b3() ---> b3当前的function
b1.b3()() ---> return的function
*/
```

**实例**

实例：实例对象

类型：类型对象

```javascript
function Person(name, age){ // 构造函数 类型
  this.name = name
  this.age = age
} 
var p = new Person('Tom', 12) // 根据类型创建的实例对象
```

**其他问题**

1、undefined 与 null 的区别?

- undefined 代表定义未赋值
- null 定义并赋值了, 只是值为 null

```javascript
var a
console.log(a)  // undefined
a = null
console.log(a) // null
```

2、什么时候给变量赋值为 null 呢?

- 初始赋值，表明将要赋值为对象
- 结束前，让对象成为垃圾对象（被垃圾回收器回收）

```javascript
//起始
var b = null  // 初始赋值为 null，表明将要赋值为对象
//确定对象就赋值
b = ['luwang', 12]
//最后
b = null // 让 b 指向的对象成为垃圾对象（被垃圾回收器回收）
// b = 2
```

3、严格区别变量类型与数据类型?

- 数据的类型

  - 基本类型
  - 对象类型

- 变量的类型（变量内存值的类型）

  - 基本类型：保存就是基本类型的数据
  - 引用类型：保存的是地址值

```javascript
var c = function () {

}
console.log(typeof c) // 'function'
```

### 2、数据、变量与内存

1、什么是数据?

- 存储在内存中代表特定信息的内容，本质上是 0101...（二进制）

- 数据的特点：可传递，可运算

- 一切皆数据

- 内存中所有操作的目标：数据
  - 算术运算
  - 逻辑运算
  - 赋值
  - 运行函数

2、什么是内存?

- 内存条通电后产生的可储存数据的空间（临时的）

- 内存产生和死亡：内存条(电路版)--->通电--->产生内存空间--->存储数据--->处理数据--->断电--->内存空间和数据都消失

- 一块小内存的2个数据
  - 内部存储的数据
  - 地址值

- 内存分类
  - 栈：全局变量/局部变量
  - 堆：对象

3、什么是变量?

- 可变化的量，由变量名和变量值组成

- 每个变量都对应的一块小内存，变量名用来查找对应的内存，变量值就是内存中保存的数据

4、内存、数据、变量三者之间的关系

- 内存用来存储数据的空间

- 变量是内存的标识

```javascript
var age = 18
console.log(age)

var obj = {name: 'Tom'}
console.log(obj.name)

function fn () {
  var obj = {name: 'Tom'}
}

var a = 3
var b = a + 2
```

5、关于赋值与内存的问题

问题：`var a = xxx`，a 内存中到底保存的是什么?

- xxx是**基本数据**，保存的就是这个**数据**

- xxx是**对象**，保存的是对象的**地址值**

- xxx是一个**变量**，保存的xxx的**内存内容（可能是基本数据，也可能是地址值）**

```javascript
var a = 3
a = function () {

}
var b = 'abc'
a = b
b = {}
a = b
```

![image-20200815100153040](https://cdn.wallleap.cn/img/pic/illustration/20200815100154.png)

6、关于引用变量赋值问题

- 2 个引用变量指向同一个对象，通过一个变量修改对象内部数据，另一个变量看到的是修改之后的数据

- 2 个引用变量指向同一个对象，让其中一个引用变量指向另一个对象，另一引用变量依然指向前一个对象

```javascript
var obj1 = {name: 'Tom'}
var obj2 = obj1
obj2.age = 12
console.log(obj1.age)  // 12
function fn (obj) {
  obj.name = 'A'
}
fn(obj1)
console.log(obj2.name) //A

var a = {age: 12}
var b = a
a = {name: 'BOB', age: 13}
b.age = 14
console.log(b.age, a.name, a.age) // 14 Bob 13
function fn2 (obj) {
  obj = {age: 15}
}
fn2(a)
console.log(a.age) // 13
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815101835.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200815102623.png)

7、关于数据传递问题

问题：在 js 调用函数时传递变量参数时，是值传递还是引用传递

- 理解1：都是值（基本/地址值）传递

- 理解2：可能是值传递，也可能是引用传递（地址值）

```javascript
var a = 3
function fn (a) {
  a = a +1
}
fn(a)
console.log(a)  // 3

function fn2 (obj) {
  console.log(obj.name)
}
var obj = {name: 'Tom'}
fn2(obj)  // Tom
```

8、JS 引擎如何管理内存

问题：JS 引擎如何管理内存?

- 内存生命周期
  - 分配小内存空间，得到它的使用权
  - 存储数据，可以反复进行操作
  - 释放小内存空间

- 释放内存
  - 局部变量：函数执行完自动释放
  - 对象：成为垃圾对象==>垃圾回收器回收

```javascript
var a = 3
var obj = {}
obj = undefined

function fn () {
  var b = {}
}

fn() // b是自动释放, b所指向的对象是在后面的某个时刻由垃圾回收器回收
```

### 3、对象

1、什么是对象?

- 多个数据的封装体

- 用来保存多个数据的容器

- 一个对象代表现实中的一个事物

2、为什么要用对象?

- 统一管理多个数据

3、对象的组成

- 属性：属性名（字符串）和属性值（任意）组成

- 方法：一种特别的属性（属性值是函数）

4、如何访问对象内部数据?

- `.属性名`：编码简单，有时不能用

- `['属性名']`：编码麻烦，能通用

```javascript
var p = {
  name: 'Tom',
  age: 12,
  setName: function (name) {
    this.name = name
  },
  setAge: function (age) {
    this.age = age
  }
}

p.setName('Bob')
p['setAge'](23)
console.log(p.name, p['age'])
```

问题：什么时候必须使用 `['属性名']` 的方式?

1. 属性名包含特殊字符： `-`、`空格`

2. 属性名不确定（是变量）

```javascript
var p = {}
//1. 给p对象添加一个属性: content type: text/json
// p.content-type = 'text/json' //不能用
p['content-type'] = 'text/json'
console.log(p['content-type'])

//2. 属性名不确定
var propName = 'myAge'
var value = 18
// p.propName = value //不能用
p[propName] = value
console.log(p[propName])
```

### 4、函数

1、什么是函数?

- 实现特定功能的 n 条语句的封装体

- 只有函数是可以执行的，其它类型的数据不能执行

2、为什么要用函数?

- 提高代码复用

- 便于阅读交流

3、如何定义函数?

- 函数声明

- 表达式

4、如何调用（执行）函数?

- `test()`：**直接调用**
- `obj.test()`：**通过对象调用**
- `new test()`：**new 调用**
- `test.call(obj)`/`test.apply(obj)`：**临时让 test 成为 obj 的方法进行调用**

```javascript
/*
编写程序实现以下功能需求:
  1. 根据年龄输出对应的信息
  2. 如果小于18, 输出: 未成年, 再等等!
  3. 如果大于60, 输出: 算了吧!
  4. 其它, 输出: 刚好!
*/
function showInfo (age) {
  if(age<18) {
    console.log('未成年, 再等等!')
  } else if(age>60) {
    console.log('算了吧!')
  } else {
    console.log('刚好!')
  }
}

showInfo(17)
showInfo(20)
showInfo(65)

function fn1 () { //函数声明
  console.log('fn1()')
}
var fn2 = function () { //表达式
  console.log('fn2()')
}

fn1()
fn2()

var obj = {}
function test2 () {
  this.xxx = 'atguigu'
}
// obj.test2()  不能直接, 根本就没有
test2.call(obj) // obj.test2()   // 可以让一个函数成为指定任意对象的方法进行调用
console.log(obj.xxx)
```

### 5、回调函数

1. 什么函数才是回调函数?
   1) 你定义的
   2) 你没有调
   3) 但最终它执行了（在某个时刻或某个条件下）
2. 常见的回调函数?

   - DOM 事件回调函数 ==> 发生事件的 DOM 元素
   - 定时器回调函数 ===> window
   - ajax 请求回调函数
   - 生命周期回调函数

```html
<button id="btn">测试点击事件</button>
<script type="text/javascript">
  document.getElementById('btn').onclick = function () { // dom事件回调函数
    alert(this.innerHTML)
  }
  //定时器
    // 超时定时器
    // 循环定时器
  setTimeout(function () { // 定时器回调函数
    alert('到点了'+this)
  }, 2000)
  /*var a = 3
  alert(window.a)
  window.b = 4
  alert(b)*/
</script>
```

### 6、IIFE

1、理解

- 全称: Immediately-Invoked Function Expression（立即执行函数）

2、作用

- 隐藏实现
- 不会污染外部（全局）命名空间
- 用它来编码 js 模块

```javascript
(function () { //匿名函数自调用
  var a = 3
  console.log(a + 3)
})()
var a = 4
console.log(a)
;(function () {
  var a = 1
  function test () {
    console.log(++a)
  }
  window.$ = function () { // 向外暴露一个全局函数
    return {
      test: test
    }
  }
})()
$().test() // 1.
```

### 7、函数中的 this

1、this 是什么?

- 任何函数本质上都是通过某个对象来调用的，如果没有直接指定就是 window
- 所有函数内部都有一个变量 this
- 它的值是调用函数的当前对象

2、如何确定 this 的值?

函数调用的时候确定

- `test()`：window
- `p.test()`：p
- `new test()`：新创建的对象
- `p.call(obj)`：obj

箭头函数没有自己的 this，箭头函数中所谓的 this，其实就是外层代码块的 this

```javascript
function Person(color) {
  console.log(this)
  this.color = color;
  this.getColor = function () {
    console.log(this)
    return this.color;
  };
  this.setColor = function (color) {
    console.log(this)
    this.color = color;
  };
}

Person("red"); //this是谁? window

var p = new Person("yello"); //this是谁? p

p.getColor(); //this是谁? p

var obj = {};
p.setColor.call(obj, "black"); //this是谁? obj

var test = p.setColor;
test(); //this是谁? window

function fun1() {
  function fun2() {
    console.log(this);
  }

  fun2(); //this是谁? window
}
fun1();
```

## 二、函数高级

超级重点，两大神兽：**原型和闭包**

### 1、原型和原型链

(1) 原型

函数的 prototype 属性

- 每个函数都有一个 prototype 属性，它默认指向一个 Object 空对象（即称为原型对象）
- 原型对象中有一个属性 constructor，它指向函数对象

![](https://cdn.wallleap.cn/img/pic/illustration/20200815113737.png)

给原型对象添加属性（一般都是方法）

- 作用：函数的所有实例对象自动拥有原型中的属性（方法）

```javascript
// 每个函数都有一个prototype属性, 它默认指向一个Object空对象(即称为: 原型对象)
console.log(Date.prototype, typeof Date.prototype)
function Fun () {//alt + shift +r(重命名rename)

}
console.log(Fun.prototype)  // 默认指向一个Object空对象(没有我们的属性)

// 原型对象中有一个属性constructor, 它指向函数对象
console.log(Date.prototype.constructor===Date)
console.log(Fun.prototype.constructor===Fun)

//给原型对象添加属性(一般是方法) ===>实例对象可以访问
Fun.prototype.test = function () {
  console.log('test()')
}
var fun = new Fun()
fun.test()
```

(2) 显式原型与隐式原型

1. 每个函数 function 都有一个 prototype，即显式原型（属性）
2. 每个实例对象都有一个 `__proto__`，可称为隐式原型（属性）
3. 对象的隐式原型的值为其对应构造函数的显式原型的值
4. 内存结构

总结：

- 函数的 `prototype` 属性：在定义函数时自动添加的，默认值是一个空 Object 对象
- 对象的 `__proto__` 属性：创建对象时自动添加的，默认值为构造函数的 prototype 属性值
- 程序员能直接操作显式原型，但不能直接操作隐式原型（ES6之前）

```javascript
//定义构造函数
function Fn() {   // 内部语句: this.prototype = {}

}
// 1. 每个函数function都有一个prototype，即显式原型属性, 默认指向一个空的Object对象
console.log(Fn.prototype)
// 2. 每个实例对象都有一个__proto__，可称为隐式原型
//创建实例对象
var fn = new Fn()  // 内部语句: this.__proto__ = Fn.prototype
console.log(fn.__proto__)
// 3. 对象的隐式原型的值为其对应构造函数的显式原型的值
console.log(Fn.prototype===fn.__proto__) // true
//给原型添加方法
Fn.prototype.test = function () {
  console.log('test()')
}
//通过实例调用原型的方法
fn.test()
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815115018.png)

(3) 原型链

原型链

- 访问一个对象的属性时
  - 先在自身属性中查找，找到返回
  - 如果没有，再沿着 `__proto__` 这条链向上查找，找到返回
  - 如果最终没找到，返回 undefined
- 别名：隐式原型链
- 作用：查找对象的属性（方法）

![](https://cdn.wallleap.cn/img/pic/illustration/20200815115136.png)

构造函数/原型/实体对象的关系

```javascript
var o1 = new Object();
var o2 = {};
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815115415.png)

构造函数/原型/实体对象的关系2

```javascript
function Foo(){  }
// var Foo = new Function()
// Function = new Function()
// 所有函数的__proto__都是一样的
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815115508.png)

```javascript
// console.log(Object)
//console.log(Object.prototype)
console.log(Object.prototype.__proto__)
function Fn() {
  this.test1 = function () {
    console.log('test1()')
  }
}
console.log(Fn.prototype)
Fn.prototype.test2 = function () {
  console.log('test2()')
}

var fn = new Fn()

fn.test1()
fn.test2()
console.log(fn.toString())
console.log(fn.test3)
// fn.test3()

/*
1. 函数的显示原型指向的对象默认是空Object实例对象(但Object不满足)
  */
console.log(Fn.prototype instanceof Object) // true
console.log(Object.prototype instanceof Object) // false
console.log(Function.prototype instanceof Object) // true
/*
1. 所有函数都是Function的实例(包含Function)
*/
console.log(Function.__proto__===Function.prototype)
/*
1. Object的原型对象是原型链尽头
  */
console.log(Object.prototype.__proto__) // null

```

原型继承

- 构造函数的实例对象自动拥有构造函数原型对象的属性（方法）
- 利用的就是原型链

原型属性问题

- 读取对象的属性值时：会自动到原型链中查找
- 设置对象的属性值时：不会查找原型链，如果当前对象中没有此属性，直接添加此属性并设置其值
- 方法一般定义在原型中，属性一般通过构造函数定义在对象本身上

```javascript
function Fn() {

}
Fn.prototype.a = 'xxx'
var fn1 = new Fn()
console.log(fn1.a, fn1)

var fn2 = new Fn()
fn2.a = 'yyy'
console.log(fn1.a, fn2.a, fn2)

function Person(name, age) {
  this.name = name
  this.age = age
}
Person.prototype.setName = function (name) {
  this.name = name
}
var p1 = new Person('Tom', 12)
p1.setName('Bob')
console.log(p1)

var p2 = new Person('Jack', 12)
p2.setName('Cat')
console.log(p2)
console.log(p1.__proto__===p2.__proto__) // true
```

(4) 探索 instanceof

instanceof 是如何判断的?

- 表达式：A instanceof B
- 如果 B 函数的显式原型对象在 A 对象的原型链上，返回 true，否则返回 false

Function 是通过 new 自己产生的实例

*案例1*

```javascript
function Foo() {  }
var f1 = new Foo()
console.log(f1 instanceof Foo) // true
console.log(f1 instanceof Object) // true
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815120818.png)

*案例2*

```javascript
console.log(Object instanceof Function) // true
console.log(Object instanceof Object) // true
console.log(Function instanceof Function) // true
console.log(Function instanceof Object) // true

function Foo() {}
console.log(Object instanceof  Foo) // false
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815120915.png)

(5) 面试题

```javascript
/*
测试题1
  */
function A () {

}
A.prototype.n = 1

var b = new A()

A.prototype = {
  n: 2,
  m: 3
}

var c = new A()
console.log(b.n, b.m, c.n, c.m) // 1 undefined 2 3
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815122322.png)

```javascript
/*
  测试题2
  */
function F (){}
Object.prototype.a = function(){
  console.log('a()')
}
Function.prototype.b = function(){
  console.log('b()')
}

var f = new F()
f.a() // a()
// f.b() // Uncaught TypeError: f.b is not a function
F.a() // a()
F.b() // b()
console.log(f) // F {}
console.log(Object.prototype) // {a: ƒ, constructor: ƒ, __defineGetter__: ƒ, __defineSetter__: ƒ, hasOwnProperty: ƒ, …}
console.log(Function.prototype) // ƒ () { [native code] }
```

### 2、执行上下文与执行上下文栈

(1) 变量提升与函数提升

变量声明提升

- 通过 **var 定义(声明)的变量**，在定义语句之前就可以访问到
- 值：undefined

函数声明提升

- 通过 **function 声明的函数**，在之前就可以直接调用
- 值：函数定义（对象）

问题：变量提升和函数提升是如何产生的?

- 在 js 中 js 引擎会优先解析 var 变量和 function 定义！在预解析完成后从上到下逐步进行！
- 解析 var 变量时，会把值存储在“执行环境”中，而不会去赋值，值是存储作用！例如：`alert（a）; var a = 2;` 这时会输出 undefined，意思是没有被初始化没有被赋值！这并不是没有被定义、错误了的意思！
- 在解析 function 时会把函数整体定义，这也就解释了为什么在 function 定义函数时为什么可以先调用后声明了！其实表面上看是先调用了，其实在内部机制中第一步实行的是把以 function 方式定义的函数先声明了（预处理）

```javascript
/*
面试题：输出 undefined
*/
var a = 3
function fn () {
  console.log(a)
  var a = 4
}
fn() // undefined

console.log(b) //undefined  变量提升
fn2() //可调用  函数提升 fn2()
// fn3() //不能  变量提升 Uncaught TypeError: fn3 is not a function

var b = 3
function fn2() {
  console.log('fn2()')
}

var fn3 = function () {
  console.log('fn3()')
}
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815122405.png)

(2) 执行上下文

代码分类（位置）

- 全局代码
- 函数（局部）代码

全局执行上下文

- 在执行全局代码前将 window 确定为全局执行上下文
- 对全局数据进行预处理
  - var 定义的全局变量 ==> undefined，添加为 window 的属性
  - function 声明的全局函数 ==> 赋值（fun），添加为 window 的方法
  - this ==> 赋值（window）
- 开始执行全局代码

```javascript
// 全局声明的变量和函数都会在window中：window.a1、window.a2()
console.log(a1, window.a1) // undefined undefined
window.a2() // a2() 
console.log(this) // Window

var a1 = 3 // 在这声明，事实上调到上面声明了，这里赋值(因此上面能访问)
function a2() { // 在这里声明，能够在上面调用
  console.log('a2()')
}
console.log(a1) // 3
```

函数执行上下文

- 在调用函数，准备执行函数体之前，创建对应的函数执行上下文对象（虚拟的，存在于栈中）
- 对局部数据进行预处理
  - 形参变量——>赋值(实参)——>添加为执行上下文的属性
  - arguments==>赋值(实参列表)，添加为执行上下文的属性
  - var 定义的局部变量==>undefined，添加为执行上下文的属性
  - function 声明的函数 ==>赋值(fun)，添加为执行上下文的方法
  - this==>赋值(调用函数的对象)
- 开始执行函数体代码

```js
function fn(a1) {
  console.log(a1) // 2
  console.log(a2) // undefined
  a3() // a3()
  console.log(this) // window
  console.log(arguments) // 伪数组 2, 3

  var a2 = 3
  function a3() {
    console.log('a3()')
  }
}
fn(2, 3)
```

(3) 执行上下文栈

1. 在全局代码执行前，JS 引擎就会创建一个栈来存储管理所有的执行上下文对象
2. 在全局执行上下文（window）确定后，将其添加到栈中（压栈）
3. 在函数执行上下文创建后，将其添加到栈中（压栈）
4. 在当前函数执行完后，将栈顶的对象移除（出栈）
5. 当所有的代码执行完后，栈中只剩下 window

```javascript
var a = 10
var bar = function (x) {
  var b = 5
  foo(x + b)
}
var foo = function (y) {
  var c = 5
  console.log(a + c + y)
}
bar(10)
// bar(10)
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815123328.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200815123402.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200815123416.png)

```javascript
console.log('gb: '+ i)
var i = 1
foo(1)
function foo(i) {
  if (i == 4) {
    return
  }
  console.log('fb:' + i)
  foo(i + 1) //递归调用: 在函数内部调用自己
  console.log('fe:' + i)
}
console.log('ge: ' + i)
/*
1. 依次输出什么?
  gb: undefined
  fb: 1
  fb: 2
  fb: 3
  fe: 3
  fe: 2
  fe: 1
  ge: 1
2. 整个过程中产生了几个执行上下文?  5   */
```

(4) 面试题

测试题 1：先执行变量提升，再执行函数提升（先找 `var` 和 `function xxx(){}`）

```javascript
function a() {}
var a
console.log(typeof a) // function
```

测试题 2：先提出去，window 中有 b，且未赋值

```javascript
if (!(b in window)) {
  var b = 1
}
console.log(b) // undefined
```

测试题 3：针对变量名同名或函数名同名的情况。如果声明了同名的函数其定义会被后者覆盖，声明了同名的变量其值也会被后者覆盖

```javascript
var c = 1
function c(c) {
  console.log(c)
  var c = 3
}
console.log(c) // 1
c(2) // 报错 Uncaught TypeError: c is not a function

// 再看一个
// 声明阶段
function x(){ //函数声明
 //console.log(5)此句会被下句代码覆盖
    console.log(3)
}
var x;//变量声明，因为x已经声明过了，此处不进行声明（忽略）
//执行阶段
console.log(x) // ƒ x(){//函数声明//console.log(5);此句会被下句代码覆盖console.log(3);}
console.log(x()) // 3
x=1 
x=100 //x的值被覆盖
console.log(x) // 100
console.log(x()) // Uncaught TypeError: x is not a function
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815125003.png)

### 3、作用域与作用域链

(1) 作用域

理解：

- 就是一块“地盘”，一个代码段所在的区域
- 它是静态的（相对于上下文对象），在编写代码时就确定了

分类：

- 全局作用域
- 函数作用域
- 没有块作用域（ES 6 有了）

```js
/*  //没块作用域
if(true) {
  var c = 3
}
console.log(c) // 3 有块作用域则报错*/
```

作用：

- 隔离变量，不同作用域下同名变量不会有冲突

例如把如下代码分割

```javascript
var a = 10,
  b = 20
function fn(x) {
  var a = 100,
    c = 300;
  console.log('fn()', a, b, c, x) 
  function bar(x) {
    var a = 1000,
      d = 400
    console.log('bar()', a, b, c, d, x)
  }
  bar(100) // bar() 1000 20 300 400 100
  bar(200) // bar() 1000 20 300 400 200
}
fn(10) // fn() 100 20 300 10
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815125424.png)

(2) 作用域与执行上下文

区别 1：

- 全局作用域之外，每个函数都会创建自己的作用域，作用域在函数定义时就已经确定了，而不是在函数调用时
- 全局执行上下文环境是在全局作用域确定之后，js 代码马上执行之前创建
- 函数执行上下文是在调用函数时，函数体代码执行之前创建

区别 2：

- 作用域是静态的，只要函数定义好了就一直存在，且不会再变化
- 执行上下文是动态的，调用函数时创建，函数调用结束时就会自动释放

联系：

- 执行上下文（对象）是从属于所在的作用域
- 全局上下文环境==>全局作用域
- 函数上下文环境==>对应的函数使用域

还是上面那串代码

![](https://cdn.wallleap.cn/img/pic/illustration/20200815125637.png)

(3) 作用域链

理解：

- 多个上下级关系的作用域形成的链，它的方向是从下向上的（从内到外）
- 查找变量时就是沿着作用域链来查找的

查找一个变量的查找规则：

1. 在当前作用域下的执行上下文中查找对应的属性，如果有直接返回，否则进入 2
2. 在上一级作用域的执行上下文中查找对应的属性，如果有直接返回，否则进入 3
3. 再次执行 2 的相同操作，直到全局作用域，如果还找不到就抛出找不到的异常

```javascript
var a = 1
function fn1() {
  var b = 2
  function fn2() {
    var c = 3
    console.log(c) // 3
    console.log(b) // 2
    console.log(a) // 1
    console.log(d) // Uncaught ReferenceError: d is not defined
  }
  fn2()
}
fn1()
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815125756.png)

(4) 面试题

```javascript
var x = 10;
function fn() {
  console.log(x);
}
function show(f) {
  var x = 20;
  f();
}
show(fn); // 10
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815125904.png)

```javascript
var fn = function () {
  console.log(fn)
}
fn() // f(){console.log(fn)}

var obj = {
  fn2: function () {
    console.log(fn2)
    //console.log(this.fn2) // ƒ () {// console.log(fn2) console.log(this.fn2)}
  }
}
obj.fn2() // Uncaught ReferenceError: fn2 is not defined
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815125936.png)

### 4、闭包

(1) 引入实例

```html
<button>测试1</button>
<button>测试2</button>
<button>测试3</button>
<!--
需求: 点击某个按钮, 提示"点击的是第n个按钮"
-->
<script type="text/javascript">
  var btns = document.getElementsByTagName('button')
  //遍历加监听
  /*// 无论点哪个都是 第4个 ——点击的时候循环已经执行完了
  for (var i = 0,length=btns.length; i < length; i++) {
    var btn = btns[i]
    btn.onclick = function () {
      alert('第'+(i+1)+'个')
    }
  }*/
  /*
  for (var i = 0,length=btns.length; i < length; i++) {
    var btn = btns[i]
    //将btn所对应的下标保存在btn上，利用这中方式可以实现
    btn.index = i
    btn.onclick = function () {
      alert('第'+(this.index+1)+'个')
    }
  }*/

  //利用闭包
  for (var i = 0,length=btns.length; i < length; i++) {
    (function (j) {
      var btn = btns[j]
      btn.onclick = function () {
        alert('第'+(j+1)+'个')
      }
    })(i)
  }
</script>
```

(2) 理解闭包

如何产生闭包?

- 当一个**嵌套的内部（子）函数引用了嵌套的外部（父）函数的变量（函数）**时，就产生了闭包

闭包到底是什么?

- 使用 Chrome 调试查看
- 包含被引用变量（函数）的对象
- 注意：闭包存在于嵌套的内部函数中

***产生闭包的条件?***

- 函数嵌套
- 内部函数引用了外部函数的数据（变量/函数）

```javascript
function fn1 () {
  var a = 2
  var b = 'abc'
  function fn2 () { // 声明函数形式定义函数，会产生闭包
    console.log(a)  // 使用了外部函数的变量
  }
  // fn2()
}
fn1()

function fun1() {
  var a = 3
  var fun2 = function () { // 声明变量形式定义函数，不会产生闭包
    console.log(a)
  }
}
fun1()
```

(3) 常见的闭包

1. 将函数作为另一个函数的返回值
2. 将函数作为实参传递给另一个函数调用

```javascript
// 1. 将函数作为另一个函数的返回值
function fn1() {
  var a = 2
  function fn2() {
    a++
    console.log(a)
  }
  return fn2
}
var f = fn1()
f() // 3
f() // 4
/* f调用的是内部函数，fn1外部函数执行了一次，产生1个闭包 */

// 2. 将函数作为实参传递给另一个函数调用
function showDelay(msg, time) {
  setTimeout(function () {
    alert(msg)
  }, time)
}
showDelay('test', 2000)
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815131913.png)

(4) 闭包的作用

1. 使用函数内部的变量在函数执行完后，仍然存活在内存中（延长了局部变量的生命周期）
2. 让函数外部可以操作（读写）到函数内部的数据（变量/函数）

```javascript
function fn1() {
  var a = 2
  function fn2() {
    a++
    console.log(a)
    // return a
  }
  function fn3() {
    a--
    console.log(a)
  }
  return fn3
}
var f = fn1()
f() // 1
f() // 0
```

(5) 闭包的生命周期

1. 产生：在嵌套内部函数**定义**执行完时就产生了（不是在调用）
2. 死亡：在嵌套的内部函数成为垃圾对象时

```js
function fn1() {
  //此时闭包就已经产生了(函数提升, 内部函数对象已经创建了)
  var a = 2
  function fn2 () {
    a++
    console.log(a)
  }
  return fn2
}
var f = fn1()
f() // 3
f() // 4
f = null // 闭包死亡（包含闭包的函数对象成为垃圾对象）
```

(6) 闭包的应用：自定义 JS 模块

模块：

- 具有特定功能的 js 文件
- 将所有的数据和功能都封装在一个函数内部（私有的）
- 只向外暴露一个包括 n 个方法的对象或函数
- 模块的使用者，只需要通过模块暴露的对象调用方法来实现对应的功能

例如：

文件 `myModule1.js` 就是一个模块

```javascript
function myModule() {
  // 私有数据
  var msg = 'Hello This is Module1'
  // 操作数据的函数
  function doSomething() {
    console.log('doSomething() '+msg.toUpperCase())
  }
  function doOtherthing () {
    console.log('doOtherthing() '+msg.toLowerCase())
  }

  //向外暴露对象（给外部使用的方法）
  return {
    doSomething: doSomething,
    doOtherthing: doOtherthing
  }
}
```

在其他文件中引入

```html
<script type="text/javascript" src="myModule.js"></script>
<script type="text/javascript">
  var module = myModule()
  module.doSomething()
  module.doOtherthing()
</script>
```

下面这种更好用一点，可以不需要先执行那个函数（IIFE）

`myModule2.js`

```javascript
(function () {
  //私有数据
  var msg = 'Hello This is Module1'
  //操作数据的函数
  function doSomething() {
    console.log('doSomething() '+msg.toUpperCase())
  }
  function doOtherthing () {
    console.log('doOtherthing() '+msg.toLowerCase())
  }

  //向外暴露对象(给外部使用的方法)
  window.myModule2 = {
    doSomething: doSomething,
    doOtherthing: doOtherthing
  }
})()
```

引入使用

```html
<script type="text/javascript" src="myModule2.js"></script>
<script type="text/javascript">
  myModule2.doSomething()
  myModule2.doOtherthing()
</script>
```

压缩代码时，会把变量改为 a、b、c 这种的，因此最好这样做

![](https://cdn.wallleap.cn/img/pic/illustration/20200815132854.png)

(7) 闭包的缺点及解决

缺点：

- 函数执行完后，函数内的局部变量没有释放，占用内存时间会变长
- 容易造成内存泄露

解决：

- 能不用闭包就不用
- 及时释放

```javascript
function fn1() {
  var arr = new Array[100000]
  function fn2() {
    console.log(arr.length)
  }
  return fn2
}
var f = fn1()
f()

f = null //让内部函数成为垃圾对象-->回收闭包
```

补充：内存溢出与内存泄露

- 内存溢出
  - 一种程序运行出现的错误
  - 当程序运行需要的内存超过了剩余的内存时，就会抛出内存溢出的错误
- 内存泄露
  - 占用的内存没有及时释放
  - 内存泄露积累多了就容易导致内存溢出
  - 常见的内存泄露：
    - 意外的全局变量
    - 没有及时清理的计时器或回调函数
    - 闭包

![](https://cdn.wallleap.cn/img/pic/illustration/20200815133732.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200815133741.png)

![](https://cdn.wallleap.cn/img/pic/illustration/20200815133756.png)

(8) 面试题

```javascript
//代码片段一
var name = "The Window"
var object = {
  name : "My Object",
  getNameFunc : function(){
    return function(){
      return this.name
    }
  }
}
alert(object.getNameFunc()())  // the window

//代码片段二
var name2 = "The Window"
var object2 = {
  name2 : "My Object",
  getNameFunc : function(){
    var that = this;
    return function(){
      return that.name2;
    }
  }
}
alert(object2.getNameFunc()()) // my object

// 三
function fun(n,o) {
  console.log(o)
  return {
    fun:function(m){
      return fun(m,n)
    }
  }
}
var a = fun(0)
a.fun(1)
a.fun(2)
a.fun(3)//undefined,0,0,0

var b = fun(0).fun(1).fun(2).fun(3)//undefined,0,1,2

var c = fun(0).fun(1)
c.fun(2)
c.fun(3) // undefined,0,1,1
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815133831.png)

## 三、面向对象高级

### 1、对象创建模式

有如下五种方式：

(1) Object 构造函数模式

- 套路：先创建空 Object 对象，再动态添加属性/方法
- 适用场景：起始时不确定对象内部数据
- 问题：语句太多

```javascript
/*
一个人: name:"Tom", age: 12
  */
// 先创建空Object对象
var p = new Object()
p = {} //此时内部数据是不确定的
// 再动态添加属性/方法
p.name = 'Tom'
p.age = 12
p.setName = function (name) {
  this.name = name
}

//测试
console.log(p.name, p.age)
p.setName('Bob')
console.log(p.name, p.age)
```

(2) 对象字面量模式

- 套路：使用 `{}` 创建对象，同时指定属性/方法
- 适用场景：起始时对象内部数据是确定的
- 问题：如果创建多个对象，有重复代码

```javascript
var p = {
  name: 'Tom',
  age: 12,
  setName: function (name) {
    this.name = name
  }
}

//测试
console.log(p.name, p.age)
p.setName('JACK')
console.log(p.name, p.age)

var p2 = {  //如果创建多个对象代码很重复
  name: 'Bob',
  age: 13,
  setName: function (name) {
    this.name = name
  }
}
```

(3) ~~工厂模式~~

- 套路：通过工厂函数动态创建对象并返回
- 适用场景：需要创建多个对象
- 问题：对象没有一个具体的类型，都是 Object 类型

```javascript
function createPerson(name, age) { //返回一个对象的函数===>工厂函数
  var obj = {
    name: name,
    age: age,
    setName: function (name) {
      this.name = name
    }
  }
  return obj
}

// 创建2个人
var p1 = createPerson('Tom', 12)
var p2 = createPerson('Bob', 13)

// p1/p2 是 Object 类型

function createStudent(name, price) {
  var obj = {
    name: name,
    price: price
  }
  return obj
}
var s = createStudent('张三', 12000)
// s 也是 Object
```

(4) 自定义构造函数模式

- 套路：自定义构造函数，通过 `new` 创建对象
- 适用场景：需要创建多个类型确定的对象
- 问题：每个对象都有相同的数据，浪费内存

```javascript
//定义类型
function Person(name, age) {
  this.name = name
  this.age = age
  this.setName = function (name) {
    this.name = name
  }
}
var p1 = new Person('Tom', 12)
p1.setName('Jack')
console.log(p1.name, p1.age)
console.log(p1 instanceof Person)

function Student (name, price) {
  this.name = name
  this.price = price
}
var s = new Student('Bob', 13000)
console.log(s instanceof Student)

var p2 = new Person('JACK', 23)
console.log(p1, p2)
```

方法两者都有，且相同，不需要单独拥有，可放到原型中(方法一般放到原型中)——>

(5) 构造函数+原型的组合模式

- 套路：自定义构造函数，属性在函数中初始化，方法添加到原型上
- 适用场景：需要创建多个类型确定的对象

```javascript
function Person(name, age) { //在构造函数中只初始化一般函数
  this.name = name
  this.age = age
}
Person.prototype.setName = function (name) {
  this.name = name
}

var p1 = new Person('Tom', 23)
var p2 = new Person('Jack', 24)
console.log(p1, p2)
```

### 2、继承模式

继承，在 JS 中有三种方式：

(1) 原型链继承

套路：

- 定义父类型构造函数
- 给父类型的原型添加方法
- 定义子类型的构造函数
- 创建父类型的对象赋值给子类型的原型
- 将子类型原型的构造属性设置为子类型
- 给子类型原型添加方法
- 创建子类型的对象：可以调用父类型的方法

关键：

- 子类型的原型为父类型的一个实例对象

```javascript
//父类型
function Supper() {
  this.supProp = 'Supper property'
}
Supper.prototype.showSupperProp = function () {
  console.log(this.supProp)
}

//子类型
function Sub() {
  this.subProp = 'Sub property'
}

// 子类型的原型为父类型的一个实例对象
Sub.prototype = new Supper()
// 让子类型的原型的constructor指向子类型
Sub.prototype.constructor = Sub
Sub.prototype.showSubProp = function () {
  console.log(this.subProp)
}

var sub = new Sub()
sub.showSupperProp()
// sub.toString()
sub.showSubProp()

console.log(sub)  // Sub
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815135207.png)

(2) 借用构造函数继承

套路：

- 定义父类型构造函数
- 定义子类型构造函数
- 在子类型构造函数中调用父类型构造

关键：

- 在子类型构造函数中通过 `call()` 调用父类型构造函数

```javascript
function Person(name, age) {
  this.name = name
  this.age = age
}
function Student(name, age, price) {
  Person.call(this, name, age)  // 相当于: this.Person(name, age)
  /*this.name = name
  this.age = age*/
  this.price = price
}

var s = new Student('Tom', 20, 14000)
console.log(s.name, s.age, s.price)
```

(3) 组合继承

1. 利用原型链实现对父类型对象的方法继承

2. 利用 `super()` 借用父类型构建函数初始化相同属性

```javascript
function Person(name, age) {
  this.name = name
  this.age = age
}
Person.prototype.setName = function (name) {
  this.name = name
}

function Student(name, age, price) {
  Person.call(this, name, age)  // 为了得到属性
  this.price = price
}
Student.prototype = new Person() // 为了能看到父类型的方法
Student.prototype.constructor = Student // 修正 constructor 属性
Student.prototype.setPrice = function (price) {
  this.price = price
}

var s = new Student('Tom', 24, 15000)
s.setName('Bob')
s.setPrice(16000)
console.log(s.name, s.age, s.price)
```

ES 6 中的继承：使用 `class` 类的 `extends` 关键字实现继承

```javascript
class Person {
  constructor(name, age) {
    this.name = name
    this.age = age
  }
  setName(name) {
    this.name = name
  }
}
class Student extends Person {
  constructor(name, age, price) {
    super(name, age)
    this.price = price
  }
  setPrice(price) {
    this.price = price
  }
}

var s = new Student('Tom', 24, 15000)
s.setName('Bob')
s.setPrice(16000)
console.log(s.name, s.age, s.price)
```

## 四、线程机制与事件机制

### 1、进程与线程

(1) 进程（process）

- 程序的一次执行，它占有一片独有的内存空间
- 可以通过 Windows 任务管理器查看进程

(2) 线程（thread）

- 是进程内的一个独立执行单元
- 是程序执行的一个完整流程
- 是 CPU 的最小的调度单元

![线程与进程](https://cdn.wallleap.cn/img/pic/illustration/20200815135743.png)

应用程序必须运行在某个进程的某个线程上

一个进程中至少有一个运行的线程：主线程，进程启动后自动创建

一个进程中也可以同时运行多个线程，我们会说程序是多线程运行的

一个进程内的数据可以供其中的多个线程直接共享

多个进程之间的数据是不能直接共享的

线程池（thread pool）：保存多个线程对象的容器，实现线程对象的反复利用

(3) 相关问题

何为多进程与多线程?

- 多进程运行：一应用程序可以同时启动多个实例运行
- 多线程：在一个进程内，同时有多个线程运行

比较单线程与多线程?

- 多线程
  - 优点
    - 能有效提升 CPU 的利用率
  - 缺点
    - 创建多线程开销
    - 线程间切换开销
    - 死锁与状态同步问题
- 单线程
  - 优点
    - 顺序编程简单易懂
  - 缺点
    - 效率低

JS 是单线程还是多线程?

- jS 是单线程运行的，但使用 H5 中的 Web Workers 可以多线程运行

浏览器运行是单线程还是多线程?

- 都是多线程运行的

浏览器运行是单进程还是多进程?

- 有的是单进程
  - firefox
  - 老版 IE
- 有的是多进程
  - chrome
  - 新版 IE
- 如何查看浏览器是否是多进程运行的呢?
  - 任务管理器-->进程

### 2、浏览器内核

- 支撑浏览器运行的最核心的程序
- 不同的浏览器可能不一样
  - Chrome、Safari：webkit
  - firefox：Gecko
  - IE：Trident
  - 360、搜狗等国内浏览器：Trident + webkit（双核）
- 内核由很多模块组成
  - 主线程
    - js 引擎模块：负责 js 程序的编译与运行
    - html、css文档解析模块：负责页面文本的解析
    - DOM/CSS模块：负责 dom/css 在内存中的相关处理
    - 布局和渲染模块：负责页面的布局和效果的绘制（内存中的对象）
    - ......
  - ​ 分线程
    - 定时器模块：负责定时器的管理
    - DOM事件响应模块：负责事件的管理
    - 网络请求模块：负责 ajax 请求

### 3、定时器引发的思考

定时器真是定时执行的吗?

- 定时器并不能保证真正定时执行（设置了 n 秒，则是 n 秒**之后**执行）

- 一般会延迟一丁点（可以接受），也有可能延迟很长时间（不能接受）

定时器回调函数是在分线程执行的吗?

- 在主线程执行的，js 是单线程的

定时器是如何实现的?

- 事件循环模型

```javascript
document.getElementById('btn').onclick = function () {
  var start = Date.now()
  console.log('启动定时器前...')
  setTimeout(function () {
    console.log('定时器执行了', Date.now()-start)
  }, 200)
  console.log('启动定时器后...')

  // 做一个长时间的工作
  for (var i = 0; i < 1000000000; i++) {

  }
}
```

### 4、JS 是单线程执行的

如何证明 js 执行是单线程的?

- `setTimeout()` 的回调函数是在主线程执行的
- 定时器回调函数只有在运行栈中的代码全部执行完后才有可能执行

为什么 js 要用单线程模式，而不用多线程模式?

- JavaScript 的单线程，与它的用途有关。
- 作为浏览器脚本语言，JavaScript 的主要用途是与用户互动，以及操作 DOM。
- 这决定了它只能是单线程，否则会带来很复杂的同步问题

代码的分类:

- 初始化代码
- 回调代码

js 引擎执行代码的基本流程

- 先执行初始化代码：包含一些特别的代码
  - 回调函数（异步执行）
  - 设置定时器
  - 绑定事件监听
  - 发送 ajax 请求
- 后面在某个时刻才会执行回调代码（回调函数包含的代码）

```javascript
setTimeout(function () {
  console.log('timeout 2222')
  alert('22222222')
}, 2000)
setTimeout(function () {
  console.log('timeout 1111')
  alert('1111111')
}, 1000)
setTimeout(function () {
  console.log('timeout() 00000')
}, 0)
function fn() {
  console.log('fn()')
}
fn()

console.log('alert()之前')
alert('------') // 暂停当前主线程的执行，同时暂停计时，点击确定后，恢复程序执行和计时
console.log('alert()之后')
```

### 5、浏览器的事件循环（轮询）模型

(1) 模型原理图

![](https://cdn.wallleap.cn/img/pic/illustration/20200815141019.png)

所有代码分类

- 初始化执行代码（同步代码）：包含绑定 dom 事件监听，设置定时器，发送 ajax 请求的代码
- 回调执行代码（异步代码）：处理回调逻辑

js 引擎执行代码的基本流程：

- 初始化代码===>回调代码

模型的 2 个重要组成部分：

- 事件（定时器/DOM 事件/Ajax）管理模块
- 回调队列

模型的运转流程

- 执行初始化代码，将事件回调函数交给对应模块管理
- 当事件发生时，管理模块会将回调函数及其数据添加到回调列队中
- 只有当初始化代码执行完后（可能要一定时间），才会遍历读取回调队列中的回调函数执行

```javascript
function fn1() {
  console.log('fn1()')
}
fn1()
document.getElementById('btn').onclick = function () {
  console.log('点击了btn')
}
setTimeout(function () {
  console.log('定时器执行了')
}, 2000)
function fn2() {
  console.log('fn2()')
}
fn2()
```

(2) 相关重要概念

执行栈 execution stack

- 所有的代码都是在此空间中执行的

浏览器内核 browser core

- js引擎模块(在主线程处理)

- 其它模块(在主/分线程处理)

![运行原理图](https://cdn.wallleap.cn/img/pic/illustration/20200815141526.png)

- 任务队列 task queue

- 消息队列 message queue

- 事件队列 event queue

上面这三个在同一个 callback queue

事件轮询 event loop

- 从任务队列中循环取出回调函数放入执行栈中处理（一个接一个）

事件驱动模型 event-driven interaction model

请求响应模型 request-response model

### 6、H5 Web Workers（多线程）

(1) 介绍

- Web Workers 是 HTML5 提供的一个 javascript 多线程解决方案
- 我们可以将一些大计算量的代码交由 web Worker 运行而不冻结用户界面
- 但是子线程完全受主线程控制，且不得操作DOM。所以，这个新标准并没有改变 JavaScript 单线程的本质

(2) 相关API

- `Worker`：构造函数，加载分线程执行的 js 文件
- `Worker.prototype.onmessage`：用于接收另一个线程的回调函数
- `Worker.prototype.postMessage`：向另一个线程发送消息

(3) 使用

创建在分线程执行的 js 文件

```javascript
var onmessage =function (event){ // 不能用函数声明
  console.log('onMessage()22')
  var upper = event.data.toUpperCase() // 通过 event.data 获得发送来的数据
  postMessage( upper ) // 将获取到的数据发送会主线程
}
```

在主线程中的 js 中发消息并设置回调

```javascript
// 创建一个Worker对象并向它传递将在新线程中执行的脚本的URL
var worker = new Worker("worker.js")
//接收 worker 传过来的数据函数
worker.onmessage = function (event) {     
  console.log(event.data)          
};
// 向 worker 发送数据
worker.postMessage("hello world")  
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200815143823.png)

(4) 应用练习

直接在主线程

```javascript
<input type="text" placeholder="数值" id="number">
<button id="btn">计算</button>
<script type="text/javascript">
// 1 1 2 3 5 8    f(n) = f(n-1) + f(n-2)
function fibonacci(n) {
  return n<=2 ? 1 : fibonacci(n-1) + fibonacci(n-2)  //递归调用
}
// console.log(fibonacci(7))
var input = document.getElementById('number')
document.getElementById('btn').onclick = function () {
  var number = input.value
  var result = fibonacci(number)
  alert(result)
}
</script>
```

使用Worker在分线程

- 主线程

```javascript
var input = document.getElementById('number')
document.getElementById('btn').onclick = function () {
  var number = input.value

  //创建一个Worker对象
  var worker = new Worker('worker.js')
  // 绑定接收消息的监听
  worker.onmessage = function (event) {
    console.log('主线程接收分线程返回的数据: '+event.data)
    alert(event.data)
  }

  // 向分线程发送消息
  worker.postMessage(number)
  console.log('主线程向分线程发送数据: '+number)
}
// console.log(this) // window
```

- 分线程 worker.js

```javascript
function fibonacci(n) {
  return n<=2 ? 1 : fibonacci(n-1) + fibonacci(n-2)  //递归调用
}

console.log(this)
this.onmessage = function (event) {
  var number = event.data
  console.log('分线程接收到主线程发送的数据: '+number)
  //计算
  var result = fibonacci(number)
  postMessage(result)
  console.log('分线程向主线程返回数据: '+result)
  // alert(result)  alert是window的方法, 在分线程不能调用
  // 分线程中的全局对象不再是window, 所以在分线程中不可能更新界面
}
```

(5) 不足

- worker 内代码不能操作 DOM（更新 UI）
- 不能跨域加载 JS
- 不是每个浏览器都支持这个新特性
