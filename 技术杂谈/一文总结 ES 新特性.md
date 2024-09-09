---
title: 一文总结 ES 新特性
date: 2020-04-28 23:33
updated: 2020-04-28 23:33
cover: //cdn.wallleap.cn/img/pic/cover/202302NoyYdY.jpg
category: 技术杂谈
tags:
  - web
  - 前端
description: 一文总结 ES 新特性
---

总结并列出 ES 5 及之后的新特性

## 一、理解 ES

1. 全称: ECMAScript (/ˈɛkməskrɪpt/)

   - 它是一种由 ECMA 组织（前身为欧洲计算机制造商协会）制定和发布的脚本语言规范
   - 我们学习的 JavaScript 就是 ECMA 的实现

2. JS 包含三个部分：

   - ECMAScript（JS 基础、**核心**部分）

   - 扩展 → 浏览器端
     - BOM（浏览器对象模型）
     - DOM（文档对象模型）

   - 扩展 → 服务器端
     - Node.js

3. ES 的几个重要版本

   - 之前的为 ES 3（ES 4 夭折了，没发布）
   - ES 5：2009 年发布
   - **ES 6(ES 2015)**：2015 年发布，也称为 ECMA 2015——重点（之后的 ES 就以年份命名）
   - ES 7(ES 2016)：2016 年发布，也称为 ECMA 2016

## 二、ES 5 新特性

ES 5 对 JS 进行了修修补补，大概可以分为以下几类：

### 1、严格模式

理解：

- 运行模式分为正常（混杂）模式与严格模式
- 严格模式使得 JavaScript 在更严格的语法条件下运行

目的/作用:

- 使得 Javascript 在更严格的条件下运行
- 消除 Javascript 语法的一些不合理、不严谨之处，减少一些怪异行为
- 消除代码运行的一些不安全之处，保证代码运行的安全

使用：

- 将**全局**或**函数**的**第一条语句**定义为：`"use strict"`
- 如果浏览器不支持，只解析为一条简单的语句，没有任何副作用

语法和行为改变：

- 声明定义变量必须用 `var`（没有隐式的全局变量了，你要创建全局变量必须是显式的）
- 禁止自定义的函数中的 `this` 关键字指向全局对象（`window` 或 `global`），不管是 `fn()` 在全局调用还是 `apply()`、`call()`  默认都不会指向全局对象
- 创建 `eval` 作用域，更安全
- 不准使用 `with`
- `arguments` 只保存原始参数，对形参的赋值不会对 `arguments` 有影响，不准用 `arguments.caller` 和 `arguments.callee`
- 不支持八进制字面量，比如 `var a = 015` 会报错
- 对象字面量或函数形参中，如果有重复的键名就会报错
- 如果一个属性的 `writeable` 是 `false`，给这个属性赋值会报错
- 如果一个属性的 `configurable` 是 `false`，则 `delete` 这个属性会报错

```html
<script>
  'use strict'
  var username = 'luwang'
  // name = 'luwang' 在严格模式下不用 var 声明变量会报错
  console.log(username)

  function Person(name, age) {
    this.name = name
    this.age = age
  }
  new Person('luwang', 23)
  // Person('luwang', 23) //没有 new 会报错

  var str = 'web'
  eval('var str = "HTML"; alert(str)') // HTML
  alert(str) // web 即开启严格模式之后不会污染全局作用域

  var obj = {
    username: 'luwang',
    username: 'luwang'  // 定义重名了
  }
</script>
```

### 2、JSON 序列化和反序列化

- 作用: 用于在 JSON 字符串与 JS 对象/数组相互转换
- `JSON.stringify(obj/arr)` JS 对象（数组）转换为 JSON 数据（字符串）
- `JSON.parse(json)` JSON 字符串转换为 JS 对象（数组）

```html
<script>
  var obj = { username: 'luwang' }
  obj = JSON.stringify(obj)
  console.log(typeof obj)
  obj = JSON.parse(obj)
  console.log(typeof obj)
</script>
```

### 3、Object 扩展

ES 5 给 Object 扩展了一些静态方法

- `Object.keys()`, `Object.create()`, `Object.defineProperty`, `Object.defineProperties`,
`Object.getOwnPropertyDescriptor()`, `Object.getOwnPropertyNames(obj)`,`Object.getPrototypeOf(obj)`
- `Object.seal()`, `Object.freeze()`, `Object.preventExtensions()`, `Object.isSealed()`, `Object.isFrozen()`, `Object.isExtensible()`

常用的两个：

#### create

`Object.create(prototype[, descriptors])`：创建一个新的对象，返回值是新对象

- 作用：使用现有的对象来作为新创建对象的原型

- 为新的对象指定新的属性，并对属性进行描述
  - `value`：指定值
  - `writable`：标识当前属性值是否是可修改的，默认为`false`
  - `configurable`：标识当前属性是否可以被删除，默认为`false`
  - `enumerable`：标识当前属性是否能用for in枚举，默认为`false`

```javascript
var obj = {username: 'luwang', age:23}
var obj1 = {}
obj1 = Object.create(obj, {  // obj的属性为obj1的原型
  sex: {
    value: '男',
    writable: true,  // 默认false
    configurable: true,
    enumerable: true
  }
})
console.log(obj1.sex)
obj1.sex = 'nan'
console.log(obj1.sex)
delete obj1.sex
console.log(obj1)
for(var i in obj1){
  console.log(i)
}
```

#### defineProperties

`Object.defineProperties(object, descriptors)`：为指定对象定义扩展多个属性

- **get 方法**：用来得到当前属性值的回调函数
- **set 方法**：用来监视当前属性值变化的回调函数

```javascript
var obj = { username: 'luwang', age:23 }
var obj1 = {}
var obj2 = { firstName: 'lu', lastName: 'wang' }
Object.defineProperties(obj2, {
  fullName: { // 此方法在原型中
    get: function(){ // 获取扩展属性的值
      console.log('get方法被调用')
      return this.firstName + ' ' + this.lastName
    },
    set: function(data){ // 监听扩展属性，当扩展属性发生变化的时候会自动调用，自动调用后会讲变化的值作为实参注入到set函数
      console.log('set方法被调用，', data)
      var names = data.split(' ') // 根据空格拆分为数组
      this.firstName = names[0]
      this.lastName = names[1]
    }
  }
})
console.log(obj2.fullName) // get会自动调用 
obj2.fullName = 'lu wang'  
console.log(obj2.fullName)
```

惰性求值：点击才给值（什么时候要什么时候给），会再次调用 get 方法

![惰性求值](https://cdn.wallleap.cn/img/pic/illustration/1589786198022.png)

- 什么时候调用：
  - get 方法：获取扩展属性值的时候 get 方法自动调用
  - set 方法：监听
- 存储器属性：setter、getter 一个用来存值，一个用来取值

对象本身也有两个方法：

- get propertyName(){}
- set propertyName(){}

```javascript
var obj = {
  firstName: 'lu', 
  lastName: 'wang',
  get fullName(){
    return this.firstName + ' ' + this.lastName
  },
  set fullName(data){
    var names = data.split(' ')
    this.firstName = names[0]
    this.lastName = names[1]
  }
}
console.log(obj)
obj.fullName = 'lu wang'
console.log(obj.fullName)
```

### 4、Array 扩展

`Array.isArray(arr)`：判断一个对象 `arr` 是否是数组

`Array.prototype.indexOf(value)`：得到值在数组中的第一个下标

`Array.prototype.lastIndexOf(value)`：得到值在数组中的最后一个下标

`Array.prototype.forEach(function(item, index, array){}[, asThis])`：遍历数组，返回值是 `undefined`

`Array.prototype.map(function(item, index, array){}[, asThis])`：遍历数组返回一个新的数组（每一项是回调函数的返回值）

`Array.prototype.filter(function(item, index, array){}[, asThis])`：遍历过滤出一个子数组，返回一个由条件为 `true` 的元素组成的新数组

`Array.prototype.reduce(function(accumulator, item, index, array)[, initValue])`：[Array.prototype.reduce](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce) 对数组中的每个元素按序执行一个提供的回调函数，每次执行回调函数会将之前元素的计算结果作为参数传入，最后将其结果汇总为单个返回值

`Array.prototype.reduceRight`：从右到左

`Array.prototype.some(function(){item, index, array}[, asThis])`：数组中是否至少有一个元素符合回调函数给定的条件，有则返回 `true`，没有返回 `false`

`Array.prototype.every(function(item, index, array){}[, asThis])`：判断一个数组内的所有元素是否都能通过指定函数的测试，返回布尔值（回调函数有三个参数，第一个为当前遍历的对象、第二个为当前的下标、第三个为数组本身，方法还接受第二个参数，将作为 `this`）

```javascript
var arr = [2,4,5,1,6,7,4,3,9]
console.log(arr.indexOf(4))
console.log(arr.lastIndexOf(4))
arr.forEach(function(item, index){
  console.log(item, index)
})
var arr1 = arr.map(function(item, index){
  return item + 10
})
console.log(arr, arr1)
arr.filter(function(item, index){
  return item > 3
})
arr.every(function(item) {
  return item > 10
})  // false
```

### 5、Function 扩展

函数新增 `bind` 方法，`Function.prototype.bind(asThis)`，将函数内的 `this` 绑定为 `asThis`，并将函数返回

强制绑定 `this` 使用 `call`/`apply` 和 `bind`

- `this` 的值通过函数调用的时候确定
- 五种函数调用形式
  - `fn`，`this` 是默认值，`undefined` 或 `window`
  - `obj.x.fn()`，`this` 是前面调用的内容 `obj.x`，例如 `btn.addEventListener` 里面 `this` 就是 `btn`
  - `call(asThis, args)` 或 `apply(asThis, [args])`，`this` 就是传的 `asThis`
  - `new fn(args)`，`this` 就是新创建的对象

```javascript
var obj = {username: 'luwang'}
function foo(){
  console.log(this)
}
foo() // this-->window 全局
// call 和 apply 不传参的时候是一样的
foo.call(obj) // this-->{username: 'luwang'} obj 对象
foo.apply(obj) // this-->{username: 'luwang'} obj 对象
// bind 的特点： 绑定完 this 不会立即调用当前的函数，而是将函数返回
// var bar = foo.bind(obj)
// bar()
foo.bind(obj)()

// 传入参数的形式
var obj1 = {age: 23}
function fun(data){
  console.log(this, data)
}
fun(22) // window  22
// call 直接从第二个参数开始，依次传入
fun.call(obj1, 21) // {age: 23} 21
// 第二参数必须是数组，传入放在数组里
fun.apply(obj1, [20]) // {age: 23} 20

// bind 传参的方式同 call 一样
fun.bind(obj1, 18)()
```

> 🔖 面试题：区别 `bind()` 与 `call()` 和 `apply()`

`fn.bind(asThis, args)`：指定函数中的 `this`，并返回函数(不会立即调用)，一般用在回调函数绑定其他对象的 `this`

```javascript
var obj = {username: 'luwang'}
setTimeout(function(){
  console.log(this) // Window
}, 1000)
setTimeout(function(){
  console.log(this) // Window
}.bind(obj), 1000)
```

`fn.call(asThis, args)`：指定函数中的 `this`，并调用函数

`fn.apply(asThis, [args])`：指定函数中的 `this`，并调用函数

总结：三个都可以给 `fn` 指定 `this`，`bind` 不会调用 `fn`，`call` 和 `apply` 都会调用 `fn`，`call` 的其他参数依次以逗号分隔，`apply` 的其他参数以数组形式传递

### 6、Date扩展

- `Date.now()`：得到当前时间值，之前 `new Date()`
- `Date.prototype.toISOString`：新增方法，会返回一个 ISO 格式的字符串（ `YYYY-MM-DDTHH:mm:ss.sssZ`）
- `new Date(string)` 和 `Date.parse(string)` 新增对 ISO 格式的支持

### 7、其他

- 新增 `String.prototype.trim`，去除字串头尾空格
- 尾逗号不报错，即多余的逗号不会报错，如 `{a: 1, b: 2,}`
- 属性名可以使用关键字和保留字了，例如 `{if: 1, else: 2}`
- `NaN`、`Infinity`、`undefined` 都是常量了，不可更改
- `parseInt()` 第二个参数默认为 10
- `/regexp/` 正则字面量每次都会产生一个新的对象

## 三、ES 6 新特性

ES 6 新增了很多特性，让 JS 变得非常好用

### 1、2 个声明变量的新关键字

ES 6 中新增了块作用域，`{}` 包裹的地方就是一个块，ES 5 中没有块级作用域（只有全局和函数作用域）

#### let 关键字

作用：与 var 相似，用于声明一个变量

特点：

- 在块作用域内有效
- 不能重复声明
- 不会预处理，不存在变量提升

应用：

循环遍历加监听

```html
<br/><button>按钮1</button><br/><br/>
<button>按钮2</button><br/><br/>
<button>按钮3</button>
<script>
  var btns = document.getElementsByTagName('button')
  for(var i = 0; i < btns.length; i++){
    var btn = btns[i]
    btn.onclick = function(){
      alert(i)
    }
  }
  /*
  * 一直会显示3
  * 点击事件对应的是回调函数，回调函数又称勾子函数，回调函数会被放到事件队列中，等主线程上的代码执行完毕之后再通过钩子一样的形式，勾出来执行
  * 以前的方式是通过闭包，立即执行函数(自己的作用域)
  */
  for(var i = 0; i < btns.length; i++){
    var btn = btns[i]
    ;(function(i){  // 声明的形参
      btn.onclick = function(){
      alert(i)
    }
    })(i)   // 传的实参
  }
  /*
  * 闭包利用的是函数作用域的特点
  * 因此可以直接使用let
  */
  for(let i = 0; i < btns.length; i++){ // let，在块作用域内有效
    var btn = btns[i]
    btn.onclick = function(){
      alert(i)
    }
  }
</script>
```

> 使用 let 代替 var 是趋势

#### const 关键字

作用：定义一个常量

特点

- 不能修改
- 其他特点同 let

应用

保存不用改变的数据

```javascript
const PI = 3.1415926
```

> let 和 const 声明的变量都是有块级作用域的
>
> let 和 const 声明变量在块作用域内都有暂时性死区，即在声明之前使用该变量会报错

### 2、变量（对象）的解构赋值

理解：

1. 从对象或数组中提取数据，并赋值给多个变量

2. 将包含多个数据的对象/数组一次赋值给多个变量

数据源：对象/数组

目标：`{a, b}`/`[a, b]`

对象的解构赋值：`let {n, a} = {n:'tom', a:12}` 把对象中的值赋值出来（根据属性名 key）

数组的解构赋值：`let[a, b] = [1, 'luwang']` (根据下标)

用途：数组匹配、对象匹配、参数匹配（给多个形参赋值）

```javascript
let obj = {
  username: 'luwang',
  age: 23
}
// let username = obj.username
// let age = obj.age
// console.log(username, age)
// let {username, age} = obj // 对象，因此需要以对象的形式来接收 只需要一个就写一个，不需要按顺序
// console.log(username, age)
let {age} = obj
console.log(age)

// [b, a] = [a, b]
let arr = [1, 3, 5,'abc', true]
// let [a, b, c, d, e] = arr
// console.log(a, b, c, d, e)
// let [a, b] = arr
// console.log(a, b)
let [,,a, b] = arr
console.log(a, b)

function foo({username, age}){ // {username, age} = obj
  console.log(username, age)
}
foo(obj)
```

### 3、各种数据类型的扩展

#### (1) 字符串

**模板字符串**

- 作用：简化字符串的拼接
- 模板字符串必须用两个 "\`" 包裹起来，ESC 下面那个键
- 变量的部分使用 `${xxx}` 定义

```javascript
let obj = {username: 'luwang', age: 23}
/*
* 之前的写法：简单拼串
* 缺点：可能会拼错，效率低。比如，url携带10个参数，动态拼起来
*/
let str = 'My name is ' + obj.username + ', age is '+ obj.age
console.log(str)
/*
* ES6提供的模板字符串
*/
str = `My name is ${obj.username} age is ${obj.age}`
```

字符串支持 Unicode

- `String.fromCodePoint`
- `String.prototype.codePointAt`

新增一些方法

- `String.prototype.includes(str)`：判断是否包含指定的字符串
- `String.prototype.startsWith(str)`：判断是否以指定字符串开头
- `String.prototype.endsWith(str)`：判断是否以指定字符串结尾
- `String.prototype.repeat(count)`：重复指定次数

```javascript
let str = 'asdfghjkklqwrtyuiopzxcvbnm123467890'
console.log(str.includes('t')) // true
console.log(str.includes('abc')) // false
console.log(str.startsWith('a')) // true
console.log(str.endsWith('0')) // true
console.log(str.repeat(2)) // asdfghjkklqwrtyuiopzxcvbnm123467890asdfghjkklqwrtyuiopzxcvbnm123467890
```

#### (2) 数值

二进制与八进制表示法：二进制用 `0b`，八进制用 `0o`

新增方法：

- `Number.EPSILON`：最小精度
- `Number.isFinite(i)`：判断是否是有限大的数字
- `Number.isNaN(i)`：判断是否是NaN
- `Number.isInteger(i)`：判断是否是整数
- `Number.isSafeInteger(i)`
- `Number.parseInt(str)`：将字符串转换为对应的数值
- `Math.acosh`、`Math.hypot`、`Math.imul`、`Math.sign`
- `Math.trunc(i)`：直接去除小数部分

```javascript
console.log(0b1010)
console.log(0o12)
console.log(Number.isFinite(Infinity))
console.log(Number.isNaN(NaN))
console.log(Number.isInteger(123.1))
console.log(Number.isInteger(123.0))
console.log(Number.parseInt('123abc123')) // 123
console.log(Number.parseInt('a123abc123')) // NN
console.log(Math.trunc(123.123)) // 123
```

#### (3) 对象

**简化的对象写法**（短语法）

- 省略同名的属性值
- 省略方法的 function

```JavaScript
let name = 'Tom';
let age = 12;
/* 正常情况 */
let obj = {
  name: name,
  age: age，
  getName: function(){
    retrun this.name
  }
}
console.log(obj)
/* key和value相同，可以省略 */
let person = {
  name,  // 同名的属性可以不写
  age,
  setName (name) { // 可以省略函数的function
    this.name = name
  }
}
```

属性名支持表达式，需要用方括号括起来：

```javascript
const name = ['ha', 'hi', 'ho']
function yes() {
  return 'Yes'
}
const obj = {
  [name+'llo']: 'luwang',
  ['not'+yes()]: 1
}
```

属性简写和解构赋值结合使用：

```javascript
const getUserAction = ({id, name}) => {
  const { data: res } = await axios.get(`http://localhost:3000/user/${id}`)
  res.nickname = name
  return res
}
```

- 在函数的参数中使用对象的解构赋值，可以避免在函数体内部再次对参数对象进行解构赋值（`const {id, name} = user`）
- 函数的参数如果是一个对象的成员，可以使用对象简写方式（`{id: id, name: name}`）
- `{data: res}` 等同于 `{data: data}`，`data` 是一个变量，`res` 是一个新的变量，可以用于解构赋值（获取到等号右边的 `data.data`）

**复制对象**

`Object.assign(target, source1, source2..)`：将源对象的属性复制到目标对象上

```javascript
let obj = {}
let obj1 = {username:'a', age: 20}
let obj2 = {sex: '男'}
// Object.assign(obj, obj1)
// console.log(obj) // {username: "a", age: 20}
Object.assign(obj, obj1, obj2)
console.log(obj) // {username: "a", age: 20, sex: "男"}
```

**判断是否相等**

`Object.is(v1, v2)`：判断2个数据是否完全相等

```javascript
console.log(0 == -0) // true
console.log(NaN == NaN) //false
console.log(Object.is(0, -0)) // false
console.log(Object.is(NaN, NaN)) // true
```

**`__proto__` 属性**

`__proto__` 属性：隐式原型属性。ES 6 中能直接操作`__proto__`属性，但是不推荐使用

```javascript
let obj = {}
let obj1 = {salary: 5000000}
obj.__proto__ = obj1
console.log(obj)
console.log(obj.salary)
```

#### (4) 数组

- `Array.from(v)`：将伪数组对象或可遍历对象转换为真数组
- `Array.of(v1, v2, v3)`：将一系列值转换成数组
- `find(function(value, index, arr){return true})`：找出第一个满足条件返回true的元素
- `findIndex(function(value, index, arr){return true})`：找出第一个满足条件返回 true 的元素下标
- `fill`：填充数组
- `copyWithin`：复制数组中一系列元素到同一数组指定的起始位置
- `entries`：返回一个新的 Array Iterator 对象，该对象包含数组中每个索引的键/值对
- `keys`：返回一个新的 Array Iterator 对象，该对象包含数组中每个索引的键
- `values`：返回一个新的 Array Iterator 对象，该对象包含数组中每个索引的值

```html
<button>測試1</button><br>
<button>測試2</button><br>
<button>測試3</button>
<script>
  let btns = document.getElementsByTagName('button')
  // 偽數組 不能使用forEach(數組的方法)
  Array.from(btns).forEach(function(item, index){
    console.log(item)
  })

  let arr = Array.of(1, 4, 'abc', true)
  console.log(arr)

  let arr2 = [2,3,4,2,5,7,3,6]
  console.log(arr2.find(function(item, index){
    return item > 4
  }))
  console.log(arr2.findIndex(function(item, index){
    return item > 4
  }))
</script>
```

#### (5) 函数

**Ⅰ、箭头函数**

让函数写法更简便

基本语法：

- 没有参数：`const fn = () => console.log('xxxx')`  箭头前的()不能省略
- 一个参数：`i => i+2`  可以省略
- 大于一个参数：`(i,j) => i+j`  ()不能省略
- 函数体不用大括号：默认返回结果
- 函数体如果有多个语句，需要用 `{}` 包围

使用场景：多用来定义回调函数

特点：

- 简洁
- 箭头函数没有自己的 `this`，箭头函数的 `this` 不是调用的时候决定的，而是在定义的时候所处的对象就是它的 `this`
- 扩展理解：箭头函数的 `this` 看外层是否有函数
  - 箭头外层有函数，`this` 是外层函数的 `this`
  - 箭头外层无函数，`this` 是 `window`

```javascript
let fun = function(){console.log('fun')}
fun()
// 1、没有形参
let fun1 = () => console.log('fun1')
fun1()

// 2、只有一个形参
let fun2 = (a) => console.log(a)
// 可省略() let fun2 = a => console.log(a)
fun2('aaa')

// 3、两个及两个以上的形参
let fun3 = (x,y) => console.log(x, y)
fun3(1, 2)

// I、函数体只有一条语句或表达式，{}可以省略-->会自动返回语句执行的结果或表达式的结果
let foo = (x, y) => x + y
// let foo = (x, y) => {return x + y}
console.log(foo(1, 3))

// II、函数体不止一条语句或者表达式， {}不可以省略
let foo2 = (x, y) => {
  console.log(x, y)
  return x + y
}
console.log(foo2(3, 5))

// 箭头函数的this
<br/><button id="btn1">按钮1</button><br/><br/>
<button id="btn2">按钮2</button><br/><br/>
<button id="btn3">按钮3</button>
<script>
  let btn1 = document.getElementById('btn1')
  let btn2 = document.getElementById('btn2')
  let btn3 = document.getElementById('btn3')
  btn1.onclick = function(){
    console.log(this) // <button id="btn1">按钮1</button>
  }
  btn2.onclick = () => {
    console.log(this)  // Window
  }
  let obj = {
    name: '箭头函数',
    getName: function(){
      btn3.onclick = () => {
        console.log(this) // {name: "箭头函数", getName: ƒ}
      }
    }
  }
  obj.getName()
  let obj1 = {
    name: '箭头函数',
    getName: () => {
      btn3.onclick = () => {
        console.log(this) // Window
      }
    }
  }
  obj.getName()
</script>
```

**Ⅱ、参数处理**

**3 点运算符/点点点运算符**

第一种用法：在函数中，rest（可变）参数

- 通过形参左侧的 `...` 来表达，取代 `arguments` 的使用
- 比 `arguments` 灵活，只能是最后部分形参参数
  - `arguments` 是伪数组，有 `length`，但是没有数组的一般方法，不能使用 `forEach` 遍历
  - `callee` 是 `arguments` 的一个属性，等于函数本身，递归的时候可以写为：`arguments.callee()`

```javascript
// arguments
function foo(a, b){
  console.log(arguments)
  // arguments.callee() 调用自身，相当于foo(参数)
  /* arguments.forEach(function(item, index){ // 会报错，伪数组并没有数组的一般方法
    console.log(item, index)
  }) */
}
foo(2,5)
```

![参数](https://cdn.wallleap.cn/img/pic/illustration/1590476357564.png)

```javascript
// 点点点运算符
function foo(...value){
  console.log(arguments)
  console.log(value) // 就是一个正常的数组
  value.forEach(function(item, index){
    console.log(item, index)
  })
}
foo(2,5)

function foo(a, ...value){// ...value只能放在最后面
  console.log(arguments)
  // arguments.callee()
  console.log(value) // 使用的时候不用加...
  value.forEach(function(item, index){
    console.log(item, index)
  })
}
foo(2, 3, 5, 7) // 最前面的就是a，value就不包括它了
```

第二种用法——扩展/展开运算符，可以**分解出数组或对象**中的数据

```javascript
let arr = [1, 6]
let arr1 = [2, 3, 4, 5]
arr = [1, ...arr1, 6]
console.log(arr) // (6) [1, 2, 3, 4, 5, 6]  数组
console.log(...arr) // 1 2 3 4 5 6  每项值
```

**Ⅲ、形参的默认值**

- 定义形参时指定其默认的值
- 当不传入参数的时候默认使用形参里的默认值

```javascript
// 定义一个点的坐标的构造函数
function Point(x, y){
  this.x = x
  this.y = y
}
let point = new Point(50, 20)
console.log(point) // Point {x: 50, y: 20}
// 忘记传参
let point1 = new Point()
console.log(point1) // Point {x: undefined, y: undefined}

/* 
* 因此会有需求，在忘记传参的时候使用默认值
* 在形参的位置赋默认值
*/
function Point(x = 0, y = 0){
  this.x = x
  this.y = y
}
let point = new Point(50, 20)
console.log(point) // Point {x: 50, y: 20}
// 忘记传参，使用默认值
let point1 = new Point()
console.log(point1) // Point {x: 0, y: 0}
```

#### (6) 正则表达式

- 正则表达式字面量添加 Unicode 支持（`u` 标记）
- 正则表达式添加 `y` 标记，支持粘滞匹配

### 4、新增数据类型

#### (1) Symbol 类型

前言：ES 5 中对象的属性名都是字符串，容易造成重名，污染环境

概念：ES 6 中添加了一种**原始数据类型 symbol**（已有的数据类型：String、Number、boolean、null、undefined、对象）

特点：

- Symbol 属性对应的值是**唯一**的，解决命名冲突问题
- Symbol 值**不能**与**其他数据**进行**计算**，包括与字符串拼串
- for in、for of 遍历时不会遍历 symbol 属性

使用：

- 调用 Symbol 函数得到 symbol 值
- 传参标识
- 内置 Symbol 值
  - 除了定义自己使用的 Symbol 值以外，ES 6 还提供了 11 个内置的 Symbol 值（查看官方文档）
  - 对象的 Symbol.iterator 属性，指向该对象的默认遍历器方法

```javascript
// 创建symbol属性值
let symbol = Symbol()
console.log(symbol)  // Symbol()
let obj = {username:'kobe', age:39}
// 可以添加symbol属性——但是得用另一种方式
obj.gender = '男'
obj[symbol] = 'hello'
console.log(obj)  // {username: "kobe", age: 39, gender: "男", Symbol(): "hello"}

//let symbol2 = Symbol()
//let symbol3 = Symbol()
// 并不相同，值是唯一的
//console.log(symbol2, symbol3, symbol2 == symbol3)  // Symbol() Symbol() false

// 可以传参，这样就能很明显看出不同了
let symbol2 = Symbol('one')
let symbol3 = Symbol('two')
console.log(symbol2, symbol3, symbol2 == symbol3)  // Symbol(one) Symbol(two) false

// 可以用来定义常量
const Person_key = Symbol('person_key')
console.log(Person_key)  // Symbol(person_key)

// 等同于在指定的数据结构上部署了Iterator接口
// 当使用for of去遍历某一个数据结构的时候，首先去找Symbol.itearator，找到了就去遍历，没有找到就不能遍历
let targetData = {
  [Symbol.iterator]: function(){
    let nextIndex = 0
    return{
      next: function(){
        return nextIndex < this.length ? {value: this[nextIndex++], done: false} : {value: undefined, done: true}
      }
    }
  }
}
// 使用三点运算符、解构赋值，默认会去调用Iterator接口
let arr2 = [1,6]
let arr3 = [2,3,4,5]
arr2 = [1,...arr3,6]
console.log(arr2)
let [a,b] = arr2
console.log(a,b)
```

#### (2) Set/Map 容器结构

容器: 能保存多个数据的对象，同时必须具备操作内部数据的方法

任意对象都可以作为容器使用，但有的对象不太适合作为容器使用（如函数）

**Set 的特点**：保存多个 value，value 是不重复 ====>数组元素去重

**Map 的特点**：保存多个 key-value，key 是不重复，value 是可以重复的

API：

- Set 容器：无序不可重复的多个 value 的集合体
  - `Set()`：创建一个空的 Set 容器
  - `Set(arr)`：创建一个 Set 容器，同时将 arr 数组（其中 arr 是一维数组）中的元素添加到 Set 容器中（去重）
  - `add(value)`：向 Set 容器中添加一个 value
  - `delete(value)`：删除 Set 容器中指定的 value
  - `clear()`：清空 Set 容器中的所有元素
  - `has(value)`：判断 Set 容器中是否存在指定的 value
  - `size`：获取 Set 容器中元素的个数
- Map 容器：无序的 key、不重复的多个 key-value 的集合体
  - `Map()`：创建一个空的 Map 容器
  - `Map(arr)`：创建一个 Map 容器，同时将 arr 数组（其中 arr 是二维数组）中的元素添加到 Map 容器中（去重）
  - `set(key, value)`：向 Map 容器中添加一对 key-value
  - `get(key)`：获取 Map 容器中指定 key 对应的 value
  - `delete(key)`：删除 Map 容器中指定的 key-value
  - `clear()`：清空 Map 容器中的所有元素
  - `has(key)`：判断 Map 容器中是否存在指定的 key
  - `size`：获取 Map 容器中元素的个数

```javascript
// let set = new Set()
let set = new Set([1,2,4,5,2,3,6]) // 重复的会去除
console.log(set)
set.add(7)
console.log(set.size, set)
console.log(set.has(8))
console.log(set.has(7))
set.delete(7)
console.log(set.size, set)
set.clear()
console.log(set.size, set)

// let map = new Map()
let map = new Map([['username', 'aaa'], ['age', 35], ['sex', 'female']]) // 二维数组，且只能有两值(一个是key，一个是value)
map.set('other', 'shuoming')
console.log(map.size, map)
map.delete('other')
console.log(map)
console.log(map.has('username'))
map.clear()
console.log(map)
```

#### （3）WeakSet 和 WeakMap 类型

- `WeakSet` 对象是一些对象值的集合。且其与 [`Set`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set) 类似，`WeakSet` 中的每个对象值都只能出现一次。在 `WeakSet` 的集合中，所有对象都是唯一的。
  - `WeakSet` **只能是对象**的集合，而不能像 [`Set`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set) 那样，可以是任何类型的任意值。
  - `WeakSet` 持*弱引用*：集合中对象的引用为*弱*引用。如果没有其他的对 `WeakSet` 中对象的引用，那么这些对象会被当成垃圾回收掉。
- WeakMap 的 key 只能是 `Object` 类型。 [原始数据类型](https://developer.mozilla.org/zh-CN/docs/Glossary/Primitive) 是不能作为 key 的（比如 [`Symbol`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol)）。
  - 原生的 `WeakMap` 持有的是每个键对象的“弱引用”，**`WeakMap` 的 key 是不可枚举的**

#### （4）TypedArray 类型

- 一个 **TypedArray** 对象描述了底层[二进制数据缓冲区](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer)的类数组视图

### 5、class 类

ES6 中新增的语法，用于实现**面向对象编程**

通过 `class` 关键字定义类，实现类的继承

#### (1) 之前实现继承

回顾：原型、构造函数、构造函数+原型——继承

```javascript
function Person(name, age) {
  this.name = name
  this.age = age
}
Person.prototype.showMe = function() {
  console.log(this.name)
}
let person = new Person('kobe', 39)
person.showMe()
console.log(person)
```

![继承](https://cdn.wallleap.cn/img/pic/illustration/1591769869983.png)

#### (2) `class` 定义类

在类中通过 `constructor()` 定义构造方法（相当于构造函数）

```javascript
// 定义一个 Person 类
class Person { // 类声明
// const Person = class { // 类表达式，类表达式的名称是可选的
  // 类的构造方法，只能有一个
  constructor(name, age) { // constructor(){} 里面的参数是生成实例传入的参数
    // 在构造方法中通过 this 给实例对象添加属性
    this.name = name
    this.age = age
  }
  // 在类中定义的方法，都是添加到类的原型对象上的
  showMe(){
    console.log(this.name) // this 指向实例对象，所以可以通过 this 来访问实例对象的属性
  }
}
let person = new Person('kobe', 39)  // new Person() 会自动调用 constructor() 构造方法，创建实例对象，并且将参数传递给 constructor() 构造方法
console.log(person)
person.showName()
```

- 类声明和类表达式的区别
  - 类声明：类声明不可以省略类名，类名是标识符
  - 类表达式：类表达式的类名是可选的，如果有类名，类名是标识符
- constructor() 构造方法
  - 通过 new 关键字调用类时，会自动调用 constructor() 构造方法
  - constructor() 构造方法是类中的**默认方法**，如果类中没有显式定义构造方法，那么类中会有一个隐式的、默认的空的 constructor() 构造方法
  - 通过 constructor() 构造方法可以给实例对象添加属性

![继承](https://cdn.wallleap.cn/img/pic/illustration/1591770059566.png)

#### (3) class 类的继承

- 一般方法：xxx () {}

- 用 extends 来定义子类（实现类的继承）

- 用 super() 来调用父类的构造方法

- 子类方法自定义：将从父类中继承来的方法重新实现一遍（重写从父类继承的一般方法）

```javascript
// 父类
class Person{
  constructor(name, age){
    this.name = name
    this.age = age
  }
  showMe(){
    console.log('调用父类的方法')
    console.log(this.name, this.age)
  }
  add(){
    console.log('父类的一般方法')
  }
}
let person = new Person('kobe', 39)
person.showMe()

// 子类：继承父类
class StarPerson extends Person{
  constructor(name, age, salary){
    // 如果子类中定义了构造方法，那么子类的构造方法中必须调用 super()，否则会报错
    super(name, age) // 调用父类的构造方法，将参数传递给父类的构造方法
    this.salary = salary // 子类自己的属性
  }
  showMe(){
    // 可以通过 super 来调用父类的方法
    super.add() // 调用父类的一般方法
    console.log('子类的重写方法')
    console.log(this.name, this.age, this.salary)
  }
}
let p1 = new StarPerson('wade', 36, 10000000)
console.log(p1)
p1.showMe()
```

- 在一个构造方法中可以使用 `super` 关键字来调用父类的构造方法
- 在派生类中（子类），`super()` 必须要先调用，然后才能使用 `this` 关键字，否则会报错
- `super` 关键字也可以用来调用父类的普通方法
- `extends` 关键字用来实现类的继承，`extends` 后面跟父类的名称（也可以是内建对象）

#### (4) class 类的静态方法

- 通过 static 关键字来定义静态方法

- 静态方法是**通过类来调用**的，不能通过实例对象来调用

- 静态方法中的 this 指向**类本身**

```javascript
// 定义一个 Person 类
class Person{
  constructor(name, age){
    this.name = name
    this.age = age
  }
  showMe(){
    console.log('调用 showMe 方法')
    console.log(this.name, this.age)
  }
  // 静态方法
  static showName(){
    console.log('调用 Person 的静态方法')
    console.log(this) // this 指向类本身
  }
}
let person = new Person('kobe', 39)
person.showMe()
Person.showName() // 通过类来调用静态方法
```

#### (5) class 类的 getter 和 setter 方法

- 通过 get 和 set 关键字来定义 getter 和 setter 方法

- getter 和 setter 方法是**通过实例对象来调用**的

- getter 和 setter 方法中的 this 指向**实例对象**

```javascript
// 定义一个 Person 类
class Person{
  constructor(name, age){
    this.name = name
    this.age = age
  }
  showMe(){
    console.log('调用 showMe 方法')
    console.log(this.name, this.age)
  }
  // 静态方法
  static showName(){
    console.log('调用 Person 的静态方法')
    console.log(this) // this 指向类本身
  }
  // getter 方法
  get info(){
    console.log('调用 getter 方法')
    return this.name + ' ' + this.age
  }
  // setter 方法
  set info(value){
    console.log('调用 setter 方法')
    let arr = value.split(' ')
    this.name = arr[0]
    this.age = arr[1]
  }
}
let person = new Person('kobe', 39)
person.showMe()
Person.showName() // 通过类来调用静态方法
console.log(person.info) // 通过实例对象来调用 getter 方法
person.info = 'wade 36' // 通过实例对象来调用 setter 方法
console.log(person.info)
```

#### (6) class 类的静态属性

- 通过 static 关键字来定义静态属性

- 静态属性是**通过类来调用**的，不能通过实例对象来调用

- 静态属性中的 this 指向**类本身**

```javascript
// 定义一个 Person 类
class Person{
  constructor(name, age){
    this.name = name
    this.age = age
  }
  showMe(){
    console.log('调用 showMe 方法')
    console.log(this.name, this.age)
  }
  // 静态方法
  static showName(){
    console.log('调用 Person 的静态方法')
    console.log(this) // this 指向类本身
  }
  // getter 方法
  get info(){
    console.log('调用 getter 方法')
    return this.name + ' ' + this.age
  }
  // setter 方法
  set info(value){
    console.log('调用 setter 方法')
    let arr = value.split(' ')
    this.name = arr[0]
    this.age = arr[1]
  }
  // 静态属性
  static info = '这是一个静态属性'
}
let person = new Person('kobe', 39)
person.showMe()
Person.showName() // 通过类来调用静态方法
console.log(person.info) // 通过实例对象来调用 getter 方法
person.info = 'wade 36' // 通过实例对象来调用 setter 方法
console.log(person.info)
console.log(Person.info) // 通过类来调用静态属性
```

#### (7) 私有类字段（属性和方法）

- 私有类字段是指类中只能在类的内部访问的字段（属性和方法）

- 私有类字段可以通过在字段名前面添加 `#` 来定义

```js
// 定义一个 Person 类
class Person{
  constructor(name, age){
    this.name = name
    this.age = age
  }
  showMe(){
    console.log('调用 showMe 方法')
    console.log(this.name, this.age)
  }
  // 静态方法
  static showName(){
    console.log('调用 Person 的静态方法')
    console.log(this) // this 指向类本身
  }
  // getter 方法
  get info(){
    console.log('调用 getter 方法')
    return this.name + ' ' + this.age
  }
  // setter 方法
  set info(value){
    console.log('调用 setter 方法')
    let arr = value.split(' ')
    this.name = arr[0]
    this.age = arr[1]
  }
  // 静态属性
  static info = '这是一个静态属性'
  // 私有类字段
  #money = 10000000
  #showMoney(){
    console.log('调用私有类方法')
    console.log(this.#money)
  }
}
let person = new Person('kobe', 39)
person.showMe()
Person.showName() // 通过类来调用静态方法
console.log(person.info) // 通过实例对象来调用 getter 方法
person.info = 'wade 36' // 通过实例对象来调用 setter 方法
console.log(person.info)
console.log(Person.info) // 通过类来调用静态属性
console.log(person.money) // undefined
person.showMoney() // 报错
```

### 6、Promise 对象

理解：

- Promise 对象代表了某个将要发生的事件（通常是一个异步操作）
- ES 6 的 Promise 是一个构造函数，用来生成 promise 实例

- 解决**回调地狱**(回调函数的层层嵌套，编码是不断向右扩展，阅读性很差)；有了 promise 对象，可以将异步操作以同步的流程表达出来，避免了层层嵌套的回调函数（回调地狱）

- 能以同步编码的方式实现异步调用

- 在 ES 6 之前原生的 JS 中是没这种实现的，一些第三方框架（jQuery）实现了 Promise

- promise 对象的 3 个状态：

  - pending：待定状态
  - fullfilled：成功状态
  - rejected：失败状态

- 在同一个 Promise 中只能 pending 到 pending、pending 到 fullfilled、pending 到 rejected，不能成功之后又失败或失败之后在成功

- 应用：

  - 使用 promise 实现超时处理
  - 使用 promise 封装处理 Ajax 请求

```js
let request = new XMLHttpRequest()
request.responseType = 'json'
request.open("GET", url)
request.send()
```

#### (1) Promise 的基本使用

ES 6 中定义实现 API（使用 Promise 基本步骤）:

```js
// 1. 创建promise对象
let promise = new Promise((resolve, reject) => { 
  // 初始化 promise 状态为 pending
  // 执行异步操作 
  if(异步操作成功) { // 调用成功的回调
    resolve(result);  // 修改 promise 状态为 fullfilled
  } else { // 调用失败的回调
    reject(errorMsg);   // 修改 promise 的状态为 rejected
  } 
}) 
// 2. 调用 promise 对象的 then()
promise.then(function(
  result => console.log(result), 
  errorMsg => alert(errorMsg)
))
```

例子：

```javascript
// 1、创建 promise 对象
let promise = new Promise((resolve, reject) => {
  // 初始化 promise 状态  pending：初始化
  console.log('11111111')
  // 执行异步操作，通常是发送 Ajax 请求，开启定时器
  setTimeout(() => {
    console.log('3333333')
    // 根据异步任务的返回结果去修改 promise 的状态
    // 异步任务执行成功
    // resolve('哈哈，') // 修改 promise 的状态为 fullfilled：成功
    // 异步任务执行失败
    reject('555, ') // 修改 promise 的状态为 rejsected：失败
  }, 2000)
})
console.log('222222222')
// 2. 调用 promise 对象的 then()
promise
  .then((data) => { // 成功的回调
    console.log(data, '成功了~~~')
  }, (error) => { // 失败的回调
    console.log(error, '失败了……')
})
```

例如：新闻、新闻的评论，只发新闻的内容；在接着根据新闻的 id 拿取这个新闻下的评论

```javascript
// 定义获取新闻的功能函数
function getNews(url){
  let promise = new Promise((resolve, reject) => {
    // 状态：初始化
    // 执行异步任务
    let xmlHttp = new XMLHttpRequest()
    // 绑定监听 readyState
    /* xmlHttp.onreadystatechange = function(){
      if(xmlHttp.readyState === 4 && xmlHttp.status == 200){
        // 请求成功
        console.log(xmlHttp.responseText)
        // 修改状态
        resolve(xmlHttp.responseText) // 修改 promise 的状态为成功
      }else{
        // 请求失败
        reject('暂时没有新闻内容')
      }
    } --> 逻辑有问题*/
    xmlHttp.onreadystatechange = function(){
      if(xmlHttp.readyState === 4){
        if(xmlHttp.status == 200){
          // 请求成功
          // console.log(xmlHttp.responseText)
          // 修改状态
          resolve(xmlHttp.responseText) // 修改promise的状态为成功
        }else{
          // 请求失败
          reject('暂时没有新闻内容')
        }
      }
    }

    // open 设置请求得方式以及 url
    xmlHttp.open('GET', url)
    // 发送
    xmlHttp.send()
  })
  return promise
}
getNews('http://localhost:3000/news?id=2')
  .then((data) => {
    console.log(data)
    // 发送请求获取评论内容准备 url
    let commentsUrl = JSON.parse(data).commentsUrl
    let url = 'http://localhost:3000' + commentsUrl
    // 发送请求
    return getNews(url)
  },(error) => {
    console.log(error)
  })
  .then((data) => {
    console.log(data)
  }, () => {
    
})
```

- `new Promise()` 创建一个新的 Promise 对象
  - 参数：回调函数（函数中有两个参数，resolve、reject）
  - `resolve()` 将 Promise 对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去
  - `reject()` 将 Promise 对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去
- 创建的 Promise 对象可以调用一些方法
  - `then()`：添加状态改变时的回调函数
  - `catch()`：添加状态改变时的回调函数
  - `finally()`：添加状态改变时的回调函数
  - `all()`：将多个 Promise 实例，包装成一个新的 Promise 实例
  - `race()`：将多个 Promise 实例，包装成一个新的 Promise 实例
  - `resolve()`：将现有对象转为 Promise 对象
  - `reject()`：返回一个新的 Promise 实例，该实例的状态为 rejected

#### (2) Promise 的链式调用

生成的 Promise 对象可以进行链式调用，即 then() 方法返回的是一个新的 Promise 对象，可以继续调用 then() 方法

```javascript
// 1、创建 promise 对象
let promise = new Promise((resolve, reject) => {
  // 初始化 promise 状态  pending：初始化
  console.log('11111111')
  // 执行异步操作，通常是发送 Ajax 请求，开启定时器
  setTimeout(() => {
    console.log('3333333')
    // 根据异步任务的返回结果去修改 promise 的状态
    // 异步任务执行成功
    // resolve('哈哈，') // 修改 promise 的状态为 fullfilled：成功
    // 异步任务执行失败
    reject('555, ') // 修改 promise 的状态为 rejsected：失败
  }, 2000)
})
console.log('222222222')
// 2. 调用 promise 对象的 then()
promise
  .then((data) => { // 成功的回调
    console.log(data, '成功了~~~')
  }, (error) => { // 失败的回调
    console.log(error, '失败了……')
})
```

### 7、Iterator 迭代器

概念：iterator 是一种接口机制，为各种不同的数据结构提供统一的访问机制

作用：

- 为各种数据结构，提供一个统一的、简便的访问接口
- 使得数据机构的成员能够按照某种次序排列
- ES 6 创造了一种新的遍历命令 for...of 循环，Iterator 接口主要供 for...of 消费

工作原理

- 创建一个指针对象（遍历器对象），指向数据结构的起始位置
- 第一次调用 `next` 方法，指针自动指向数据结构的第一个成员
- 接下来不断调用 `next` 方法，指针会一直往后移动，直到指向最后一个成员
- 没调用 `next` 方法返回的是一个包含 value 和 done 的对象 `{value: 当前成员的值, done: 布尔值}`
  - value 表示当前成员的值，done 对应的布尔值表示当前的数据的结构是否遍历结束
  - 当遍历结束的时候返回的 value 值是 undefined，done 值为 false

原生具备 Iterator 接口的数据，可用 for...of 遍历

扩展理解

- 当数据结构上部署了 Symbol.iterator 接口，该数据就是可以用 for of 遍历
- 当使用 for of 去遍历目标数据的时候，该数据会自动去找 Symbol.iterator 属性（Symbol.iterator 属性指向对象的默认遍历器方法）
  - Array
  - arguments
  - set 容器
  - map 容器
  - String
  - ……

for-of 循环：可以遍历任何容器（Set、Map）、数组、对象、伪/类对象、字符串、可迭代的对象

```javascript
let set = new Set([1, 2, 4, 3, 4, 5]) 
for(let i of set){
  console.log(i)
}

// 可以用 Set 给数组去重
let arr = [1,2,4,5,5,6,2]
let arr1 = arr
arr = [] // 保留数组类型
let set = new Set(arr1)
for(let i of set){
  arr.push(i)
}
console.log(arr)
```

例如

```javascript
// 模拟指针对象(遍历器对象)
function myIterator(arr){// Iterator接口
let nextIndex = 0 // 记录指针的位置
  return{
    next: function(){// 遍历器对象
      return nextIndex < arr.length ? {value: arr[nextIndex++], done: false} : {value: undefined, done: true}
    }
  }
}
// 准备一个数据
let arr =[1,4,65,'abc']

let iteratorObj = myIterator(arr)
console.log(iteratorObj.next()) // {value: 1, done: false}
console.log(iteratorObj.next()) // {value: 4, done: false}
console.log(iteratorObj.next()) // {value: 65, done: false}
console.log(iteratorObj.next()) // {value: "abc", done: false}
console.log(iteratorObj.next()) // {value: undefined, done: true}

// 将iterator接口部署到指定的数据类型上，可以使用for of去循环遍历
// 数组、字符串、argument、set容器、map容器
for(let i of arr){
  console.log(i)
}// 1 4 65 abc

let str = 'abcdefg'
for(let i of str){
  console.log(i)
}// a b c d e f g

function fun(){
  for(let i of arguments){
    console.log(i)
  }
}
fun(1,4,5,'abc') // 1 4 5 abc

// let obj = {username:'kobe', age: 39}
// for(let i of obj){
//   console.log(i)
// }// Uncaught TypeError: obj is not iterable 不可迭代
```

### 8、Generator 生成器

概念：

- ES 6 提供的解决异步编程的方案之一
- Generator 函数是一个状态机，内部封装了不同状态的数据
- 用来生成遍历器对象
- 可暂停函数（惰性求值），yield 可暂停，next 方法可启动。每次返回的是 yield 后的表达式结果

特点：

- function 与函数名之间有一个星号

- 内部用 yield 表达式来定义不同的状态

  例如：

```javascript
function* generatorExample(){
    let result = yield 'hello'  // 状态值为hello
    yield 'generator'  // 状态值为generator
}
```

generator 函数返回的是指针对象，而不会执行函数内部逻辑

```javascript
function* generatorExample(){
  console.log('开始执行')
  let result = yield 'hello'  // 状态值为hello
  yield 'generator'  // 状态值为generator
}
generatorExample() // 调用并不会执行函数内部逻辑
```

调用 next 方法函数，内部逻辑开始执行，遇到 yield 表达式停止，返回 `{value: yield后的表达式结果/return后的返回结果(如果没写，返回undefined),done: boolean值(后面还有返回false，没有返回true)}`

```javascript
function* generatorExample(){
  console.log('开始执行')
  let result = yield 'hello'  // 状态值为hello，会执行，停止 测试yield console.log('会执行')
  console.log('下次调用next执行')
  yield 'generator'  // 状态值为generator
  console.log('下次调用next执行')
  return '返回的结果'
}
let MG = generatorExample() // 返回的是指针对象
console.log(MG.next()) // 执行，遇到yield停止
console.log(MG.next('可以拿到这个值')) // 再次调用next，往下执行，可以传参
console.log(MG.next()) // 再次调用next，往下执行，返回true
```

再次调用 next 方法会从上一次停止时的 yield 处开始，直到最后

yield 语句返回结果通常为 undefined，当调用 next 方法时传参内容会作为启动时 yield 语句的返回值

补充：

- 对象的 Symbol.iterator 属性，指向遍历器对象

```javascript
let obj = {username:'kobe', age: 39}
obj[Symbol.iterator] = function* myTest(){
  yield 1
  yield 2
  yield 3
}
for(let i of obj){
  console.log(i)
}
```

例如：

- 发送 ajax 请求获取新闻内容
- 新闻内容获取成功后再次发送请求，获取对应的新闻评论内容
- 新闻内容获取失败则不需要再次发送请求

```javascript
// 要比使用Promise更好
function getNews(url){
  $.get(url, function(data){ // 前面引入了jQuery
    console.log(data)
    let url = 'http://localhost:3000' + data.commentsUrl
    SX.next(url) // 放在这里也可以往下移，并且这里参数传输更方便
  })
}
function* sendXml(){
  let url = yield getNews('http://localhost:3000/news?id=3') // 如果这里出错，后面评论也不会再执行了
  yield getNews(url)
}
// 获取遍历器对象
let SX = sendXml()
SX.next()
```

### 9、模块

#### 导入

- 静态的 **`import`** 语句用于导入由另一个模块导出的绑定
- 在浏览器中，`import` 语句只能在声明了 `type="module"` 的 `script` 的标签中使用
- 还有一个类似函数的动态 `import()`，它不需要依赖 `type="module"` 的 script 标签

语法：

```js
/* 默认导出的导入 */
import defaultExport from "module-name";

/* 导入全部，设置别名 */
import * as name from "module-name";

/* 导入对象中单个或多个 */
import { export } from "module-name";
import { export as alias } from "module-name";
import { export1 , export2 } from "module-name";
import { foo , bar } from "module-name/path/to/specific/un-exported/file";
import { export1 , export2 as alias2 , [...] } from "module-name";

/* 导入默认导出的和对象的 */
import defaultExport, { export [ , [...] ] } from "module-name";
import defaultExport, * as name from "module-name";

/* 可以导入其他文件 */
import "module-name";

/* 动态导入 */
var promise = import("module-name");//这是一个处于第三阶段的提案。
```

#### 导出

在创建 JavaScript 模块时，**`export`** 语句用于从模块中导出实时绑定的函数、对象或原始值，以便其他程序可以通过 [`import`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/import) 语句使用它们

```js
// 导出单个特性
export let name1, name2, …, nameN; // 也可以用 var, const
export let name1 = …, name2 = …, …, nameN;
export function FunctionName(){...}
export class ClassName {...}

// 导出列表
export { name1, name2, …, nameN };

// 重命名导出
export { variable1 as name1, variable2 as name2, …, nameN };

// 解构导出并重命名
export const { name1, name2: bar } = o;

// 默认导出
export default expression;
export default function (…) { … } // also class, function*
export default function name1(…) { … } // also class, function*
export { name1 as default, … };

// 导出模块合集
export * from …; // does not set the default export
export * as name1 from …; // Draft ECMAScript® 2O21
export { name1, name2, …, nameN } from …;
export { import1 as name1, import2 as name2, …, nameN } from …;
export { default } from …;
```

### 10、其他

- 元编程
  - [代理（Proxy）](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy)
  - [反射（Reflect）](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect)

- 尾调用优化

## 五、ES 2016

新增了两个新特性

### 1、指数操作

指数运算符(幂): `**`

```javascript
console.log(3 ** 3)  // 27 （3 的 3 次方）
```

### 2、数组新方法

`Array.prototype.includes(value)`: 判断数组中是否包含指定 value

```javascript
let arr = [1,2,3,'abc']
console.log(arr.includes('a'))  // false
```

## 六、ES 2017

### 1、async/await 函数

概念：真正意义上去解决异步回调的问题，同步流程表达异步操作

本质：Generator 的语法

语法：

```javascript
async function foo(){
  await 异步操作;
  await 异步操作;
}
```

特点：

- 不需要像 Generator 去调用 next 方法，遇到 await 等待，当前的异步操作完成就往下执行
- **返回的总是 Promise 对象**，可以用 then 方法进行下一步操作
- async 取代 Generator 函数的 `*`，await 取代 Generator 的 yield
- 语义上更为明确，使用简单，暂时没有任何副作用

```javascript
// async基本使用
async function foo(){
  return new Promise(resolve => {
    // setTimeout(function(){
    //   resolve()
    // }, 2000)
    // 可以写成下方这种
    setTimeout(resolve, 2000)
  })
}
async function test(){
  console.log('开始执行', new Date().toTimeString())
  await foo()
  console.log('执行完毕', new Date().toTimeString())
}
test()

// async 里 await 返回值
function test2(){
  return 'xxx'
}
async function asyncPrint(){
  /* let result = await test2()
  console.log(result) // 普通函数没有返回值
  */
  /*
  let result = await Promise.resolve()
  console.log(result) // Promise对象成功状态返回undefined
  */
  let result = await Promise.resolve('promise')
  console.log(result) // Promise对象成功状态传参返回参数 promise
  result = await Promise.reject('失败了……')
  console.log(result) // 失败状态，返回出错，且能将参数返回 Uncaught (in promise) 失败了……
}
asyncPrint()
```

获取新闻内容案例

```javascript
// async 比 generator 又更简单
async function getNews(url){
  return new Promise((resolve, reject) => {
    $.ajax({ // 前面已经引入jQuery
      method: 'GET',
      url,  // 这是ES6中简写
      /* success: function(data){
        resolve()
      },
      error: function(error){
        reject() 
      }*/
      // 简写
      success: data => resolve(data),
      error: error => reject(error)
    })
  })
}
async function sendXml(){
  let result = await getNews('http://localhost:3000/news?id=7')
  console.log(result) // {id: "7", title: "news title1...", content: "news content1...", commentsUrl: "/comments?newsId=7"}
  result = await getNews('http://localhost:3000' + result.commentsUrl)
  console.log(result)
}
sendXml()
```

改进一下，由于这种写法 error 并不会显示错误信息

```html
<script src="./jquery-3.1.0.min.js"></script>
<script>
  async function getNews(url){
    return new Promise((resolve, reject) => {
      $.ajax({
        method: 'GET',
        url,
        success: data => resolve(data),
        // error: error => reject(error)
        error: error => resolve(false) // 不用reject，而是返回false
      })
    })
  }
  async function sendXml(){
    let result = await getNews('http://localhost:30010/news?id=7')
    console.log(result) // {id: "7", title: "news title1...", content: "news content1...", commentsUrl: "/comments?newsId=7"}
    if(!result){ // 出错就弹窗
      alert('暂时没有新闻……')
    }
    result = await getNews('http://localhost:3000' + result.commentsUrl)
    console.log(result)
  }
  sendXml()
</script>
```

给个模板

```javascript
const onError = reason => {
  handleError(reason)  // 具体操作
  throw reason
}
async function fetchSome() {
  showLoading()  // Loading 处理
  const response = await axios.get('/xxx')  // 成功的
    .catch(onError)  // 失败的
    .finally(hideLoading)  // 处理 Loading
  /* doSomething */
  console.log(response)
}
fetchSome()
```

### 2、对象

- `Object.values`：返回对象的所有值
- `Object.entries`：返回对象的所有键值对

### 3、字符串填充

`padStart()`、`padEnd()` 分别可以在字符串位数不足的时候向头部和尾部进行填充内容

第一个参数是总位数，第二个参数为位数不足时填充的内容

例如：

```js
let str = 1
str.padStart(2, '0')  // 01
str.padEnd(4, '*')  // 1***
```

### 4、参数可以有多余的逗号

```js
function f(p1, p2, p3,) {}
```

### 5、其他

- `getOwnPropertyDescriptors`：获取对象的所有属性，包括不可枚举的属性
- 共享内存和原子操作

## 后续好用的新特性

### 问号

**可选链**：`?.`

```javascript
let a = user && user.name && user.name.firstName
let a = user?.name?.firstName
```

**双问号**：`??`

```javascript
let a = a || b  // 有个问题，0 是 false
let a = a ?? b  // undefined、null
```

两个结合使用

```javascript
let a = user?.name ?? 'default' // 如果 user.name 存在就取 user.name，否则取 'default'
```

由于现在开发都会用到 Babel 转译代码，所以可以放心使用这些新特性
