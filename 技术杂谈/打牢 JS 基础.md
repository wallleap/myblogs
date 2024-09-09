---
title: 打牢 JS 基础
date: 2020-04-05 12:33
updated: 2020-04-05 12:33
cover: //cdn.wallleap.cn/img/pic/cover/202302GKk2ms.jpg
category: 技术杂谈
tags:
  - web
  - 前端
description: 打牢 JS 基础
---

JS 是前端三剑客中的“行为”

## 一、JavaScript 简介

### 1、简介

什么是语言

- 计算机就是一个由人来控制的机器，人让它干什么，它就得干什么。
- 我们要学习的语言就是人和计算机交流的工具，人类通过语言来控制、操作计算机。
- 编程语言和我们说的中文、英文本质上没有区别，只是语法比较特殊。
- 语言的发展
  - 纸带机：机器语言
  - 汇编语言：符号语言
  - 现代语言：高级语言

JavaScript起源

- JavaScript 诞生于 1995 年，它的出现主要是用于处理网页中的前端验证
- 所谓的前端验证，就是指检查用户输入的内容是否符合一定的规则
- 比如：用户名的长度，密码的长度，邮箱的格式等

JavaScript简史

- JavaScript 是由**网景**公司发明，起初命名为 LiveScript，后来由于 SUN 公司的介入更名为了 JavaScript
- 1996 年微软公司在其最新的 IE 3 浏览器中引入了自己对 JavaScript 的实现 JScript
- 于是在市面上存在两个版本的  JavaScript，一个网景公司的 JavaScript 和微软的 JScript
- 为了确保不同的浏览器上运行的 JavaScript 标准一致，所以几个公司共同定制了 JS 的标准名命名为 <font color=red>ECMAScript</font>

时间表

| 年份   | 事件                                |
| ------ | ----------------------------------- |
| 1995 年 | 网景公司开发了JavaScript            |
| 1996 年 | 微软发布了和 JavaScript 兼容的 JScript |
| 1997 年 | ECMAScript 第 1 版（ECMA-262）         |
| 1998 年 | ECMAScript 第 2 版                     |
| 1998 年 | DOM Level 1 的制定                    |
| 1998 年 | 新型语言 DHTML 登场                   |
| 1999 年 | ECMAScript 第 3 版                      |
| 2000 年 | DOM Level2 的制定                   |
| 2002 年 | ISO/IEC 16262:2002 的确立            |
| 2004 年 | DOM Level 3 的制定                    |
| 2005 年 | AJAX 登场                            |
| 2009 年 | ECMAScript 第 5 版                      |
| 2009 年 | 新型语言 HTML 5 登场                   |

实现

- ECMAScript 是一个标准，而这个标准需要由各个厂商去实现。
- 不同的浏览器厂商对该标准会有不同的实现。

| 浏览器            | JavaScript 实现方式 |
| ----------------- | ------------------ |
| FireFox           | SpiderMonkey       |
| Internet Explorer | JScript/Chakra     |
| Safari            | JavaScriptCore     |
| Chrome            | v8                 |
| Carakan           | Carakan            |

- 我们已经知道 ECMAScript 是 JavaScript 标准，所以一般情况下这两个词我们认为是一个意思。
- 但是实际上 JavaScript 的含义却要更大一些。
- 在浏览器下一个完整的 JavaScript 实现应该由以下三个部分构成:

![](https://cdn.wallleap.cn/img/pic/illustration/20200812081314.png)

学习内容

- 我们已经知道了一个完整的 JavaScript 实现包含了三个部分：ECMAScript、DOM 和 BOM。
- 由此我们也知道了我们所要学习的内容就是这三部分：
  - ECMAScript
  - DOM
  - BOM

JS 的特点

- 解释型语言
- 类似于 C 和 Java 的语法结构
- 动态语言
- 基于原型的面向对象

### 2、写法

(1) JS 代码需要写到 script 标签中

例如：

```html
<script>
  alert(“Hello”); // 警告框
  document.write(“hahhh”); // 向body中输出一个内容
  console.log(“OK”); // 向控制台输出一个内容
</script>
```

自上而下顺序执行

(2) JS 代码编写位置

写到标签属性中

- 可以将 js 代码编写到标签的 onclick 属性中，当我们点击按钮时，js 代码才会执行

```html
<button onclick="alert('点我干嘛~')">点我一下</button>
```

- 可以将 js 代码写在超链接的 href 属性中，这样当点击超链接时，会执行 js 代码

```html
<a href="javascript:alert('让你点你就点？？');">点我一下</a>
<a href="javascript:;">点我一下</a>
```

- 虽然可以写在标签的属性中，但是他们属于结构和行为耦合，不方便维护，不推荐使用。

写到 script 标签中

```html
<script type="text/javascript">
  alert('我是script标签中的代码')
</script>
```

- 现在默认 script 标签就是 js，因此可以不用写 type 属性

- 写到 js 文件中，再引入

- 可以将 js 代码编写到外部 js 文件中，然后通过 script 标签引入，写到外部文件中可以在不同的页面中同时引用，也可以利用到浏览器的缓存机制 —— 推荐使用的方式

```html
<script src="js/script.js"></script>
```

- script 标签一旦用于引入外部文件了，就不能再编写代码的，即使编写了浏览器也会忽略，如果需要则可以再创建一个新的 script 标签用于编写内部代码

```html
<script src="js/core.js"></script>
<script>
  alert('我是内部代码')
</script>
```

## 二、ECMAScript

是 JS 的核心部分

### 1、注释

```javascript
// 单行注释
/*
  多行注释，注释中的内容不会被执行，但是可以在源代码中查看
*/
```

要养成良好的编写注释的习惯，也可以通过注释来对代码进行一些简单的调试

```js
/**
 * 这是一个注释，说明函数作用
 * @param {类型} a 参数a
 * @param {类型} b 参数b
 * @returns {类型} 返回值
 */
```

### 2、说明

- js 代码中严格区分大小写

- js 中每一条语句以分号（`;`）结尾

  - 如果不写分号，浏览器会自动添加，但是会消耗一些系统资源（也不会很大），而且有些时候，浏览器会加错分号，导致程序出错

对于是否需要加分号，引用下尤雨溪大佬讲的：

> 没有应该不应该，只有你自己喜欢不喜欢。
>
> 至于什么时候加分号。真正会导致上下行解析出问题的 token 有 5 个：括号，方括号，正则开头的斜杠，加号，减号。我还从没见过实际代码中用正则、加号、减号作为行首的情况，所以总结下来就是一句话：
>
> 一行开头是括号或者方括号的时候加上分号就可以了，其他时候全部不需要。

- js 中会忽略多个空格和换行，所以我们可以利用空格和换行对代码进行格式化

### 3、字面量和变量

- 字面量/常量，都是一些不可改变的值，比如：1、2、3、4、5
  - 字面量都是可以直接使用的，但是我们一般都不会直接使用字面量

- 变量
  - 变量可以用来保存字面量，而且变量的值是可以任意改变的，变量更方便我们使用，所以在开发中都是通过变量去保存一个字面量，而很少直接使用字面量

在 js 中使用 `var` 关键字来声明一个变量，为变量赋值

```javascript
var a 
a = 123 
console.log(a)
```

声明和赋值同时进行

```javascript
var b = 789
```

也可以通过变量名对字面量进行描述

```javascript
var age = 23
```

在 JS 中声明变量除了使用 `var` 关键字外，还可以使用 `let` 和 `const`，例如：

```js
let name = 'luwang'
const PI = 3.1415926
const obj = {
  name: 'luwang',
  age: 23
}
```

### 4、标识符

在 js 中所有的可以由我们自主命名的都可以称为标识符

如：变量名、函数名、属性名

命名一个标识符时需要遵守如下的规则：

- 标识符中可以含有字母、数字、`_`、`$`

- 标识符不能以数字开头（有这么一些行业公认的：`$` 开头的一般都是框架或者库、`_` 开头的一般都是私有的、大写字母开头的一般都是类/构造函数）

- 标识符不能是 ES 中的关键字或保留字

    ![](https://cdn.wallleap.cn/img/pic/illustration/20200812084204.png)

- 其他不建议使用的标识符

    ![](https://cdn.wallleap.cn/img/pic/illustration/20200812084252.png)

- 标识符一般都采用驼峰命名法 helloWorld

- js 底层保存标识符时，实际上是采用 Unicode 编码，所以理论上讲，所有的 utf-8 中含有的内容都可以作为标识符

### 5、数据类型

数据类型指的就是字面量的类型

在 js 中一共有八种数据类型

- `String` 字符串

- `Number` 数值

- `Boolean` 布尔值

- `Null` 空值

- `Undefined` 未定义

- `Bigint` 大整数

- `Symbol`

- `Object` 对象

前七种属于**基本数据类型**，`Object` 属于**引用数据类型**

(1) String

- 在 js 中字符串需要使用引号包裹 `var str = ”hello”`
- 使用双引号或单引号都可以，但是不要混着用
- 引号不能嵌套，双引号中不能放双引号，单引号中不能放单引号，但是单/双引号中可以放双/单引号
- 在字符串中，可以使用 `\` 作为转义字符，当表示一些特殊符号时，可以使用 `\` 进行转义 `\”`  `\’`  `\n`  `\t`  `\\`

(2) Number

- 在 js 中所有的数值都是 Number 类型

- 包括整数和浮点数（小数）

- 可以使用运算符 `typeof` 来检查一个变量的类型

```javascript
var a = 1
console.log(typeof a)
console.log(Number.MAX_VALUE)
```

- `Number.MAX_VALUE` 数字的最大值，超过了这个值回返回 `Infinity`，表示正无穷，`-Infinity` 表示负无穷

- `NAN`，表示 Not A Number，是一个特殊的数字

- `Number.MIN_VALUE` 大于 0 的最小值

- 在 js 中整数的运算基本可以保证精确

- <font color=red>浮点数计算，可能得到一个不精确的值</font>，不要进行对精确度要求高的计算（可以先用整数计算，然后再除 10 的整数倍）

(3) Boolean

布尔值只有两个，主要用来做逻辑判断

- true 真

- false 假

(4) Null

`null` 专门用来表示一个为空的对象

(5) undefined

声明了一个变量但是没有赋值时，它的值就是 `undefined`

### 6、强制类型转换

强制类型转换：将一个数据类型转换成其他的数据类型

String Number Boolean

(1) 调用被转换数据类型的 `toString()` 方法

```javascript
var a = 123;
a = a.toString();
```

- 该方法不会影响到原变量，它会将转换的结果返回，所以可以直接用该变量接收

- 但是注意：`null` 和 `undefined` 这两个值没有 `toString()` 方法，如果调用它们的方法，会报错

(2) 调用 `String()` 函数，并将被转换的数值作为参数传递给函数

```javascript
var a = true
a = String(a)
```

- 对于 `Number` 和 `Boolean` 实际上就是调用 `toString()` 方法
- 但是对于 `null` 和 `undefined`，就不会调用 `toString()` 方法，它会将 `null` 直接转换成 `"null"`

(3) 使用 `Number()` 函数

```javascript
var a = true
a = Number(a)
```

- 字符串--->数字
  - 如果是纯数字的字符串，则直接将其转换为数字
  - 如果字符串中有非数字的内容，则转换为 `NaN`
  - 如果字符串是一个空串或者是一个全是空格的字符，转换为 `0`
- 布尔值--->数字
  - `true` 转成 `1`
  - `false` 转成 `0`
- `Null`--->数字 `0`
- `undefined`--->数字 `NaN`

(4) 对字符串，`parseInt()` 把一个字符串转换为一个整数，可取整

可以将字符串中的有效的整数内容取出来，然后转换为 `Number`

```javascript
console.log(parseInt('123a123')) // 123
console.log(parseInt('a123')) // NaN
```

(5) `parseFloat()` 把一个字符串转换为小数

```javascript
var a = parseFloat('123.5px')
console.log(a) // 123.5
```

16进制 `0x10`  8进制 `070` 2进制 `0b10`

```javascript
/* 像'070'这种字符串，有些浏览器会当成八进制解析，有些会当成十进制 */
var a = '070'
/* 可以在 parseInt() 中传递第二个参数，来指定数字的进制 */
console.log(parseInt(a, 8)) // 56
console.log(parseInt(a, 10)) // 70
```

(6) 使用 `Boolean()` 函数将其他数据类型转换为 Boolean

- 数字 ---> 布尔值 除了 `0` 和 `NaN`，其他的都是 `true`
- 字符串 ---> 布尔值 除了空串，其他都是 `true`
- `null` 和 `undefined` 都会转换为 `false`

### 7、运算符

运算符（操作符）通过运算符可以对一个或多个值进行运算

比如：`typeof` 就是一个运算符，可以用来获得一个值的类型，它会将该值的类型以字符串的形式返回

(1) 算术运算符：

- 当对非 Number 类型的值进行运算时，会将这些值转换为 Number 然后再运算
- 任何值和 `NaN` 做运算都得 `NaN`
- `+` 可以对两个值进行加法运算，并将结果返回
  - 如果对两个字符串进行加法运算，则会做拼串，将两个字符串拼接成一个字符串，并返回
  - 任何的值和字符串做加法运算，都会先转换为字符串，然后再和字符串做拼串的操作，我们可以让任意的数据类型 `+””` 使其转换为字符串（隐式转换）
- `-` 可以对两个值进行减法运算，并将结果返回
- `*` 可以对两个值进行乘法运算
- `/` 可以对两个值进行除法运算
- `%` 取模运算（取余数）

(2) 一元运算符 只需要一个操作数

- `+` 正号 正号不会对数字产生任何影响

- `-` 负号 负号可以对数字进行负号的取反

对于非 Number 类型的值，它会先转换为 Number，然后再运算，可以对一个其它的数据类型使用 `+`，将其转换为 Number，它的原理和 `Number()` 函数一样

(3) 自增和自减

自增 `++` 可以使变量在自身的基础上增加1，原变量的值改变

后++（`a++`）前++（`++a`）都会立即使**原变量的值自增1**，但是两个**整体值**不同，后++ 为原值，前++ 为自增后的值，都改变了 a 的值，但是自身的看情况。自减 `--` 类似，只是变为了减一。

```javascript
var a = 5
console.log(a, a++, a, ++a, a) // 5 5 6 7 7
console.log(a, a--, a, --a, a) // 7 7 6 5 5
```

(4) 逻辑运算符 逻辑判断

`!`  **非** 对一个值进行非运算，对布尔值进行取反操作

- 取反 `true` 变 `false`、`false` 变 `true`

- 如果对一个值进行两次取反，它不会变化

- 如果对非布尔值进行运算，则会将其转换为布尔值，然后再取反，所以我们可以利用这个特点，来将一个其他的数据类型转换为布尔值（可以为一个任意数据类型取两次反，来将其转换为布尔值），原理和 `Boolean()` 函数一样

```javascript
var a = true
a=!a
console.log(a) // false
```

`&&` **与** 对符号两侧的值进行与运算并返回结果

- 两个值只要有一个为 `false` 就返回 `false`，只有两个值都为 `true` 时才会返回 `true`

- js 中的与属于**短路的与**，如果第一个值为 `false`，就不会再看第二个值了

```javascript
// 如果两个值都是true则返回true
var result = true && true
console.log(result) // true
// 只要有一个false，就返回false
result = true && false
console.log(result) // false
console.log(false && true) // false
console.log(false && false) // false
// 第一个值为true，会检查第二个值
true && alert('我会弹出来哦')
// 第一个值为false，不会检查第二个值
false && alert('不会弹出来')
```

`||`  **或** 可以对符号两侧的值进行或运算并返回结果

- 两个值中只要有一个 `true` 就返回 `true`，如果两个值都为 `false`，才返回 `false`

- js 中的或属于**短路的或**，如果第一个值为 `true`，就不会看第二个值

```javascript
// 两个都是false，则返回false
console.log(false || false)
// 只要有一个true，就返回true
console.log(true || false)
console.log(false || true)
console.log(true || true)
// 第一个值为false，会检查第二个值
false || alert('123')
// 第一个值为true，则不会检查第二个值
true || alert('123')
```

`&&`、`||` 的非布尔值情况：

- 对于非布尔值进行与或运算时，会先将其转换为布尔值，再运算，并且返回原值

- 与运算：如果第一个值为 `true`，则必然返回第二个值。 如果第一个值为 `false`，则直接返回第一个值

```javascript
// true && true
// 与运算：如果两个值都为 true，则返回后边的
var result = 5 && 6
console.log(result) // 6
// 与运算：如果两个值中有 false，则返回靠前的 false
// false && true
result = 0 && 2
console.log(result) // 0
result = 2 && 0
console.log(result) // 0
// false && false
result = NaN && 0
result = 0 && NaN
console.log(result) // 0
```

或运算：

- 如果第一个值为 `true`，则直接返回回一个值

- 如果第一个值为 `false`，则返回第二个值

```javascript
// true || true , true || false
// 如果第一个值为 true，则直接返回第一个值
console.log(2 || 1) // 2
console.log(2 || NaN) // 2
console.log(2 || 0) // 2
// 如果第一个值为 false，则直接返回第二个值
console.log(NaN || 1) // 1
console.log(NaN || 0) // 0
console.log(0 || NaN) // NaN
```

在实际工作中，一般会用与或代替简单的分支判断，例如

```js
if(a) {
  a = a
} else {
  a = 1
}
// 可以简写成
a = a || 1
if(b) {
  var c = b.name
}
// 可以简写成
c = b && b.name
```

(5) 赋值运算符 `=`

可以将符号右侧的值赋值给符号左侧的变量

复合运算 `+=`、`-=`、`*=`、`/=`、`%=`

```javascript
var a = 10
a += 5 // a = a + 5
a -= 5 // a = a - 5
a *= 2 // a = a * 2
a /= 2 // a = a / 2
a %= 3 // a = a % 3
```

(6) 关系运算符

可以比较两个值之间的大小关系

如果关系成立它会返回 `true`，如果关系不成立则返回 `false`

- `>` 大于号

  - 判断符号左侧的值是否大于右侧的
  - 如果关系成立则返回 `true`，如果关系不成立则返回 `false`

```javascript
var result = 5 > 10 // false
result = 5 > 4 // true
result = 5 > 5 // false
```

- `>=` 大于等于 是否大于或等于
- `<` 小于号
- `<=` 小于等于

非数值的情况

- 对于非数值进行比较时，会将其转换为数字然后再比较

```javascript
console.log(1 > true) // false
console.log(1 >= true) // true
console.log(1 > '0') // true
console.log(10 > null) // true
// 任何值和 NaN 做任何比较都是false
console.log(10 <= "hello") // false
console.log(1000000000 > NaN) // false
console.log(true > false) // true
```

- 如果符号两侧的值都是字符串时，不会将其转换为数字进行比较，而是会分别比较字符串中字符的 Unicode 编码

```javascript
// 比较练歌字符串时，比较的是字符串的字符编码
console.log('a' < 'b') // true
// 比较字符编码时是一位一位进行比较的，如果两位一样则比较下一位，所以可以借用它对英文进行排序
console.log('abc' < 'bcd') // true
// 比较中文时没有意义
console.log("我" > "你") // true
// 如果比较两个字符串型的数字，可能会得到不可预测的结果
console.log('1222222222' < '5') // true
// 因此在比较练歌字符串型的数字时，一定要转型
console.log('1222222222' < +'5') // false
```

(7) 相等运算符

使用 `==` 来做相等运算

- 相等运算符用来比较两个值是否相等，如果相等会返回 `true`，否则返回 `false`

- 如果两个进行比较的值类型不同，则会自动进行类型转换，将其转换为相同的类型，然后再比较

```javascript
console.log(1 == 1) //true
var a=10
console.log(a == 4) //false
console.log("1" == 1) //true
console.log(true == "1") //true
console.log(null == 0) //false
```

- 由于 undefined 衍生自 null，所以这两个值做相等判断时，会返回 true

```javascript
console.log(undefined == null) // true
```

- NaN 不和任何值相等，包括它本身

```javascript
console.log(NaN == "1") // false
console.log(NaN == NaN) // false
```

- 因此需要通过其他方式判断：`isNaN()` 函数就是用来判断一个值是否是 `NaN` 的

```js
var a = 'abc'
a = Number(a)
console.log(a, isNaN(a)) // NaN, true
console.log(isNaN(NaN)) // true
```

使用 `!=` 来做不相等运算

- 不相等运算符用来判断两个值是否不相等，如果不相等会返回 `true`，否则返回 `false`

- 不相等运算符也会对变量进行自动类型转换，如果转换后相等它也会返回 false

使用 `===` 来做全等运算

- 用来判断两个值是否全等，它和相等类似，不同的是他**不会做自动类型转换**，如果两个值的类型不同，直接返回 false

使用 `!==` 来做不全等运算

- 用来判断两个值是否不全等，和不等类似，不同的是它不会做自动类型转换

(8) 条件运算符，也叫三元运算符

`条件表达式?语句1:语句2`

执行的流程：

首先对条件表达式进行求值，如果该值为 `true`，则执行语句1，并返回执行结果；如果该值为 `false`，则执行语句2，并返回执行结果。

非布尔值会先转换为布尔值

```javascript
var a = 30
var b = 20
var c = 10
a > b ? alert('a大') : alert("b大")

// 获取a和b中的较大值
var max = a > b ? a : b
// 获取a、b、c中的最大值
max = max > c ? max : c

// 也可以放到一起，但是不推荐使用，不方便阅读
var max = a > b ? (a > c ? a : c) : (b > c ? b :c)
```

(9) 逗号运算符

使用 `,` 可以分割多个语句，一般可以在声明多个变量时使用

```javascript
// 使用逗号运算符同时声明多个变量
var a, b, c
// 可以同时声明多个变量并赋值
var a = 1, b = 2, c = 3
alert(b)
```

和数学中一样，在 js 中运算符也有优先级，例如先乘除后加减

在 JS 中有一个运算符优先的表，在表中越靠上优先级越高，优先级越高越优先运算，如果优先级一样，则从左往右计算，可以利用 `()` 改变优先级

![运算符的优先级](https://cdn.wallleap.cn/img/pic/illustration/20200812113320.png)

### 8、编码

在字符串中使用转义字符输入 Unicode 编码：`\u四位编码`

```js
console.log('\u2620')
```

在网页中使用 Unicode 编码：`&#编码;` 这里的编码需要的是十进制

```html
<h1 style="font-size: 200px;">&#9760</h1>
```

### 9、语句

- 前面我们说的表达式、运算符等内容可以理解成是一门语言中的单词、短语
- 而**语句**（statement）就是我们这个语言中一句一句完整的话了
- 语句是一个程序的基本单位，js 的程序就是由一条一条语句构成的，每一条语句使用 `;` 结尾
- js 中的语句默认是由上至下顺序执行的，但是我们也可以通过一些流程控制语句来控制语句的执行顺序
- 在 js 中可以使用 `{}` 来为语句进行分组，同一个 `{}` 中的语句我们称为是一组语句，它们要么都执行，要么都不执行，一个 `{}` 中的语句我们也称为一个代码块，在代码块的后边就不用再编写 `;` 了
- js 中的代码块，只具有分组的作用，没有其他的用途，代码块中的内容，在外部是完全可见的（ES 6 之后一个代码块就是一个块作用域）

```javascript
{
  alert('hello')
  console.log('你好')
  document.write("语句")
}
```

流程控制语句

- JS 中的程序是从上到下一行一行执行的
- 通过流程控制语句可以控制程序执行流程，使程序可以根据一定的条件来选择执行
- 语句的分类:
  1. 条件判断语句
  2. 条件分支语句
  3. 循环语句

(1) 条件判断语句

使用条件判断语句可以在执行某个语句之前进行判断，如果条件成立才会执行语句，条件不成立则语句不执行。

if 语句

语法一：

```js
if(条件表达式){
  语句……
}
```

if 语句在执行时，会先对条件表达式进行求值判断，如果条件表达式的值为 `true`，则执行 if 后的语句，如果条件表达式的值为 `false`，则不会执行 if 后的语句。

if 语句只能控制紧随其后的那个语句，如果希望 if 语句可以控制多条语句，可以将这些语句统一放到代码块中。

语法二：

```js
if(条件表达式){
  语句……
}else{
  语句……
}
```

if...else...语句

当该语句执行时，会先对 if 后的条件表达式进行求值判断如果该值为 `true`，则执行 if 后的语句，如果该值为 `false`，则执行 else 后的语句。

语法三：

```js
if(条件表达式){
  语句……
}else if(条件表达式){
  语句……
}else if(条件表达式){
  语句……
}else{
  语句……
}
```

if...else if...else...

当该语句执行时，会从上到下依次对条件表达式进行求值判断，如果值为 `true`，则执行当前语句，如果值为 `false`，则继续向下判断。

补充一个知识点：

`prompt()` 可以弹出一个提示框。该提示框中会带有一个文本框，用户可以在文本恒中输入一段内容，该函数需要一个字符串作为参数，该字符串将会作为提示框的提示文字。用户输入的内容将会作为函数的返回值返回，可以定义一个变量来按收该内容。

```javascript
var score = prompt("请输入成绩：")
// 判断是否合法
if(score > 100 || score < 0 || isNaN(score)){
  alert("请输入0~100的整数")
}
```

(2) 条件分支语句

```js
switch(条件表达式){
  case 表达式:
    语句……
    break;
  case 表达式:
    语句……
    break;
  default:
    语句……
    break;
}
```

switch...case..语句

在执行时会值次将 `case` 后的表达式的值和 switch 后的条件表达式的值进行全等比较。
如果比较结果为 `true`，则从当前 `case` 处开始执行代码。当前 `case` 后的所有的代码都会执行，我们可以在 `case` 的语句后加上一个 `break` 关键字，这样可以确保只会执行当前 `case` 后的语句，而不会执行其他的 `case`。

如果比较结果为 `false`，则继续向下比较。

如果所有的比较结果都为 `false`，则只执行 `default` 后的语句。

switch 语句和 if 语句的功能实际上有重复的，使用 switch 可以实现 if 的功能，同样使用 if 也可以实现 switch 的功能， 所以我们使用时，可以根据自己的习惯选择。

```javascript
/*
switch(parseInt(score/10)){
 case 10:
 case 9:
 case 8:
  console.log("优秀");
  break;
 case 7:
 case 6:
  console.log("合格");
  break;
 default:
  console.log("不合格");
  break;
}
*/
switch(true){
  case score >= 60:
    console.log("合格");
    break;
  default:
    console.log("不合格");
    break;
}
```

(3) 循环语句

通过循环语句可以反复地执行一段代码多次

while 循环

- 语法：

```javascript
while(条件表达式){
  语句……
}
```

- while 语句在执行时，先对条件表达式进行求值判断，如果值为 `true`，则执行循环体，循环体执行完毕以后，继续对表达式进行判断，如果为 `true`，则继续执行循环体，以此类推，如果值为 `false` 则终止循环

```JavaScript
// 像这种条件表达式写死为true的循环，叫做死循环。该循环不会停止，除非浏览器关闭，死循环在开发时慎用。可以使用break来终止循环。
while(true){
  alert(n++)
  if(n == 10){
    break
  }
}
// 创建一个循环，往往需要三个步骤：
// 1、初始化一个变量
var i = 1
// 2、在循环中设置一个条件表达式
while(i < 300){
  // 3、定义一个更新表达式，每次更新初始化变量
  document.write(i++ + "<br />")
}
```

do...while 循环

- 语法：

```js
do{
 语句……
}while(条件表达式)
```

- 执行流程：

do...while 语句在执行时，会先执行循环体，循环体执行完毕以后，再对 while 后的条件表达式进行判断，如果结果为 `true`，则连续执行循环体，执行完毕后继续判断以此类推，如果结果为 `false` 则终止循环

实际上 while 和 do...while 这两个语句功能相似，不同的是 while 是先判断后执行，而 do...while 可以保证循环体至少执行一次，而 while 不能

```javascript
do{
  document.write(i++ + '<br />')
}while(i <= 10)
  
while(true){
  var score = prompt('请输入成绩：')
  if(score >= 0 && score <= 100){
    alert('成绩合法')
    break
 }
  alert('请输入有效的分数！')
}
```

for 循环

for 语句，也是一个循环语句，也称为 for 循环

在 for 循环中，提供了专门的位置用来放三个表达式：

1. 初始化表达式
2. 条件表达式
3. 更新表达式

- 语法：

```js
for(初始化表达式; 条件表达式; 更新表达式){
 语句……
}
```

- 执行流程：

① 执行初始化表达式，初始化变量（初始化表达式只会执行一次）

② 执行条件表达式，判断是否执行循环。

- ​如果为 true，则执行循环 ③

- ​如果为 false，终止循环

④ 执行更新表达式，更新表达式执行完毕继续重复 ③

```javascript
// for循环中的三个部分都可以省略，也可以写在外部
var i = 0
for(; i<10;){
  alert(i++)
}
// 如果在for循环中不写任何的表达式，只写两个分号，即for(;;)，此时是一个死循环
for(var i=100; i<1000; i++){
 var th = parseInt(i/100) 
  var te = parseInt((i-th*100)/10)
  var on = i%10
  // 判断i是否是水仙花数
  if(th*th*th + te*te*te + on*on*on == i)
    console.log(i)
}
```

补充：`break` 和 `continue`

- `break` 关键字可以用来退出 `switch` 或循环语句，不能在 if 语句中使用 `break` 和 `continue`，`break` 关键字会立即终止离他最近的那个循环语句

可以为循环语句创建一个 label，用来标识当前的循环 `label: 循环语句`。使用 break 时，可以在 break 后跟着一个 label，这样 break 将会结束指定的循环，而不是最近的。

```javascript
outer:
for(var i=0; i<5; i++){
  console.log("@外层循环"+i)
  for(var j=0; j<5; j++){
    break outer // 终止外层循环(外层循环都没执行，内层循环自然也执行不了了)
    console.log("@内层循环"+j)
  }
}
```

- continue 关键字可以用来跳过本次循环，通用 continue 也是默认只会对离他最近的循环起作用

```javascript
for(var i=0; i<5; i++){
  if(i==2){
    continue;
  }
  console.log(i) // 0 1 3 4
}

// 当然，也可以用来跳过指定的
outer: for(var i=0; i<5; i++){
  console.log("@外层循环"+i)
  for(var j=0; j<5; j++){
    if(j==1){
      // continue
      continue outer
    }
    console.log("@内层循环"+j)
  }
}
```

测试某段代码的性能：

```javascript
/*
* 在代码执行前，开始计时。console.time("计时器的名字")可以用来开启一个计时器，它需要一个字符串作为参数，这个字符串将会作为计时器的标识
* 在代码结束后终止计时器，console.timeEnd("计时器的名字")用来停止一个计时器，需要一个计时器的名字作为参数
*/
console.time('test')
for(var i=2; i<=10000; i++){
  var flag = true
  for(var j=2; j<i; j++){
    if(i%j == 0){
      flag = false
      // break
    }
    if(flag){
      // console.log(i)
    }
  }
}
console.timeEnd('test')
```

可以通过 `Math.sqrt()` 对一个数进行开方：

```javascript
var result = Math.sqrt(4)
```

### 10、对象

五种基本数据类型：

`String` 字符串、`Number` 数值、`Boolean` 布尔值、`Null` 空值、`Undefined` 未定义

我们以后看到的值只要不是这五种，全都是对象（`Object`）

基本数据类型都是单一的值 "hello"、123、true，值和值之间没有任何的联系

在 js 中表示一个人的信息（name gender age）：

```js
var name = "张三"
var gender = "男"
var age = 18
```

如果使用基本数据类型的数据，我们所创建的变量都是独立的，不能成为一个整体

**对象**属于一种复合的数据类型，在对象中可以保存多个不同数据类型的属性。

对象的分类：

- 内建对象
  - 由 ES 标准中定义的对象，在任何的 ES 的实现中都可以使用
  - 比如：Math、String、Number、Boolean、Function、Object……
- 宿主对象
  - 由 JS 运行环境提供的对象，目前来讲主要指由浏览器提供的对象
  - 比如 BOM、DOM
- 自定义对象
  - 由开发人员自己创建的对象

创建对象：

使用 `new` 关键字调用的函数，是构造函数 constructor，构造函数是专门用来创建对象的函数。使用 `typeof` 检查一个对象时，会返回 object。

```javascript
var obj = new Object()
console.log(obj, typeof(obj))
```

添加属性：

在对象中保存的值称为属性

向对象添加属性，语法：`对象.属性名=属性值` 或 `对象["属性名"]=属性值`

```javascript
// 向obj中添加一个name属性
obj.name = "张三"
// 向obj中添加一个gender属性
obj.gender = "男"
// 向obj中添加一个age属性
obj.age = 18
console.log(obj)
```

读取属性：

读取对象中的属性，语法：`对象.属性名` 或 `对象["属性名"]`

如果读取对象中没有的属性，不会报错，而是会返回 `undefined`

```javascript
console.log(obj.gender)
console.log(obj.hello)
```

修改属性值：

修改对象的属性值，语法：`对象.属性名=新值`

```javascript
obj.name = "tom"
console.log(obj.name)
```

删除属性：

删除对象的属性，语法：`delete 对象.属性名`

```javascript
delete obj.name
console.log(obj.name)
```

属性名：

- 对象的属性名不强制要求遵守标识符的规范，什么乱七八糟的名字都可以取
- 但是我们使用的时候还是尽量按照标识符的规范去做
- 如果想要使用特殊的属性名，不能采用 `.` 的方式来操作，需要使用另一种方式，语法：`对象["属性名"]=属性值`，读取时也需要采用这种方式 `对象["属性名"]`。使用 `[]` 这种形式去操作属性，更加地灵活，在 `[]` 中可以直接传递一个变量，这样变量值是多少就会读取那个属性（变量的时候也只能采用这种方式）。

```js
obj["nihao"] = "你好"
var n = "nihao"
console.log(obj[n])
```

属性值：

- js 对象的属性值，可以是任意的数据类型，甚至也可以是一个对象

```javascript
var obj1 = new Object()
obj1.name = "对象"
obj1.obj2 = new Object()
obj1["2"] = null
obj1["num"] = 12345
var a = u
obj1[a] = undefined
```

`in` 运算符：

- 通过该运算符可以检查一个对象中时候含有指定的属性，如果有则返回 true，没有则返回 false
- 语法：`"属性名" in 对象`

```javascript
console.log("name" in obj1)
console.log("test" in obj1)
```

基本数据类型和引用数据类型：

- 基本数据类型：`String`、`Number`、`Boolean`、`Null`、`Undefined`

- 引用数据类型：`Object`

- 基本数据类型的值直接在栈内存中存储，值与值之间是独立存在，修改一个变量不会影响其他的变量。

```javascript
var a = 123
var b = a
a++
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200812163823.png)

- 对象是保存到堆内存中的，每创建一个新的对象，就会在堆内存中开辟出一个新的空间，而变量保存的是对象的内存地址（对象的引用），如果两个变量保存的是同一个对象引用，当修改其中一个的变量属性时，另一个也会受到影响。

```javascript
var obj = new Object()
obj.name = "张三"
var obj2 = obj
obj.name = "李四"
console.log(obj.name)
console.log(obj2.name)
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200812164416.png)

`new` 会在堆内存中开辟空间

`obj2=null`，这样 obj2 就没有指向 `0x123` 这个地址了

当比较两个基本数据类型的值时，就是比较值。

而比较两个引用数据类型时，它是比较的对象的内存地址，如果两个对象是一模一样的，但是地址不同，它也会返回 false

```javascript
var c = 10
var d = 10
console.log(c == d)

var obj3 = new Object()
var obj4 = new Object()
obj3.name = "张三"
obj4.name = "张三"
console.log(obj3, obj4, obj3==obj4)
```

对象字面量

```javascript
/* 创建一个对象 */
// var obj = new Object()
/* 使用对象字面量来创建一个对象 */
var obj = {}
console.log(typeof obj)
obj.name = "张三"
console.log(obj.name)
```

使用对象字面量，可以在创建对象时，直接指定对象中的属性，语法：`{属性名:属性值,属性名:属性值……}`

```javascript
var obj2 = {name:"张三", age: 18, gender: "男"}
console.log(obj2)
var obj3 = {
  name: "李四",
  age: 23,
  gender: "男"
}
```

对象字面量的属性名可以加引号也可以不加，建议不加，如果要使用一些特殊的名字，则必须加引号。

属性名和属性值是一组一组的名值对结构，名和值之间使用 `:` 连接，多个名值对之间使用 `,` 隔开。

### 11、函数

(1) 函数 function

- 函数也是一个对象
- 函数中可以封装一些功能（代码），在需要时可以执行这些功能（代码）
- 函数中可以保存一些代码在需要的时候再调用
- 使用 `typeof` 检查一个函数对象时，会返回 `function`

```javascript
// 创建一个函数对象
var fun = new Function()
console.log(typeof fun)
```

(2) 创建函数和调用函数

- 在创建一个函数对象的时候，可以将要封装的代码以字符串的形式传递给构造函数
- 封装到函数的代码不会立即执行
- 函数中的代码会在函数调用的时候执行
- 调用函数语法：`函数对象()`
- 当调用函数时，函数中封装的代码会按照顺序执行
- 调用几次就会执行几次

```javascript
var fun = new Function("console.log('这是一个函数哦')")
fun()
fun()
```

我们在实际开发中很少使用构造函数来创建一个函数对象，而是使用其他方式，例如以下两种（事实上学完 ES 6 后这两种方式也很少使用了）

使用函数声明来创建一个函数

语法：

```js
function 函数名([形参1, 形参2...形参N]){
 语句……
}
```

其中`[]`代表可选

```javascript
function fun2(arg){
  console.log("调用了这个" + arg + "函数了~")
}
// console.log(fun2)
fun2("fun2")
```

使用函数表达式来创建一个函数

语法：

```js
var 函数名 = function([形参1, 形参2...形参N]){
 语句……
}
```

例如：

```javascript
var fun3 = function(){
  console.log('fun3')
}
fun3()
```

ES 6 中新增了箭头函数，可以直接使用：

```js
const fun = (p1, p2) => {
  console.log(p1, p2)
}
```

(3) 函数的参数

- 可以在定义函数的时候，在函数的 `()` 中指定一个或多个形参（形式参数），多个形参之间使用 `,` 隔开，声明形参就相当于在函数内部声明了对应的变量，但是并没有赋值。

- 在调用函数的时候，可以在 `()` 中指定实参（实际参数），实参将会赋值给函数中对应的形参。
  - 调用函数时解析器不会检查实参的类型，所以要注意，是否有可能会接收到非法的参数，如果有可能则需要对参数进行类型的检查（函数的实参可以是任意的数据类型）。
  - 调用函数时，解析器也不会检查实参的数量，多余的实参不会被赋值，如果实参的数量少于形参的数量，则没有对应实参的形参将是 `undefined`

```javascript
/*
 * 定义一个用来求两个数和的函数
*/
function sum(a, b){
  console.log(a+b)
}
sum(1,2)
sum(123,456)
```

(4) 返回值

可以使用 return 来设置函数的返回值

语法：`return 值`

return 后的值将会作为函数的执行结果返回，可以定义一个变量来接收该结果

```javascript
function sum(a, b, c){
  var d = a + b + c
  return d
}
var result = sum(4,7,8)
```

在函数中 return 后的语句都不会执行

如果 return 语句后不跟任何值就相当于返回一个 `undefined`，如果函数中不写 return，也是返回 `undefined`

return 后可以跟任意类型的值（返回值可以是任意的类型），可以是一个对象，可以是一个函数……

在函数内部可以再返回声明一个函数，可以这样调用——`fun()()`

总结：使用 `break` 可以退出当前循环，使用 `continue` 跳过当次循环，使用 return 可以结束整个函数。

(5) 立即执行函数（匿名函数）——只想调用一次

函数定义完，立即被调用。

```javascript
(function(){
  alert("我是一个匿名函数~~~");
})()
```

如果不喜欢写分号的，记得上面说过的规则，开头是 `()`、`[]` 需要加上分号：

```javascript
;(function(){
  alert("我是一个匿名函数~~~")
})()
// 或者
!function(){
  alert("我是一个匿名函数~~~")
}()
```

(6) 函数与方法

函数也可以成为对象的属性，如果一个函数作为一个对象的属性保存，那么我们称这个函数时这个对象的**方法(method)**，调用这个函数就说调用对象的方法。

但是它只是名称上的区别，没有其他的区别。

```javascript
var obj = new Object()
obj.name = "张三"
obj.age = 21
obj.sayName = function(){
  console.log(obj.name)
}
// console.log(obj.sayName)
obj.sayName()
```

调用方法：`obj.sayName()`

调用函数：`fun()`

```javascript
var obj2 = {
  name: "李四",
  age: 18,
  sayName: function(){
  console.log(obj2.name) 
 }
}
obj.sayName()
```

> 等学完 ES 6 之后可以总结一下，函数声明、函数赋值、函数调用有多少多方式

### 12、<font color=red>for...in</font>

使用 for...in 语句可以枚举对象中的属性

语法：

```js
for(var 变量 in 对象){

}
```

for...in 语句，对象中有几个属性，循环体就会执行几次，每次执行时，会将对象中的恶一个属性的名字赋值给变量

```javascript
for(var index in obj){
 console.log("属性名："+index)
  console.log("属性值："+obj[index])
}
```

### 13、作用域 scope

作用域指一个变量的作用的范围

在 js 中一共有两种作用域：全局作用域和函数作用域（ES 6 多了块级作用域）

全局作用域

- 直接编写在 script 标签中的 js 代码，都在全局作用域
- 全局作用域在页面打开时创建，页面关闭时销毁。
- 在全局作用域中有一个**全局对象 window**，代表的是一个浏览器的窗口，它由浏览器创建，我们可以直接使用
- 在全局作用域中，创建的变量都会作为 window 对象的属性保存；创建的函数都会作为 window 对象的方法保存

```javascript
var a = 10
console.log(window.a)
function fun(){
  console.log("fun()")
}
window.fun()
```

全局作用域中的变量都是全局变量，在页面的任意的部分都是可以访问到的。

函数作用域

- 调用函数时创建函数作用域，函数执行完毕以后，函数作用域销毁
- 每调用一次函数就会创建一个新的函数作用域，它们之间是相互独立的
- 在函数作用域中可以访问到全局作用域的变量，在全局作用域中无法访问到函数作用域的变量
- 当前函数作用域操作一个变量时，它会现在自身作用域中寻找，如果有就直接使用；如果没有就往上一级作用域中去找，知道找到全局作用域；如果全局作用域中依然没有找到，则会报错 ReferenceError
- 在函数中要访问全局变量可以使用 window 对象
- 在函数作用域中也有声明提前的特性，使用 var 关键字声明的变量，会在函数中所有的代码执行之前声明。函数声明也会在函数中所有的代码执行之前声明
- 在函数中，不使用 var 声明的变量都会成为全局变量
- 定义形参就相当于在函数作用域中声明了变量

### 14、声明提前

变量的声明提前

- 使用 var 关键字声明的变量，会在所有的代码执行之前被声明（即使放在使用的之后）但提前声明并不会同时赋值

```javascript
// 没有var a时
console.log(a) // 报错Uncaught ReferenceError: a is not defined
--------------------------------------------------------------
// 提前声明，相当于在这里 var a
console.log(a) // undefined
var a = 1     // 这里a=1
console.log(a) // 1
```

- 但是如果声明变量时不使用 var 关键字，则变量不会被声明提前

函数的声明提前

- 使用函数声明形式创建的函数 `function 函数(){}`，它会在所有的代码执行之前就被创建

```javascript
fun() // 声明提前，输出fun()
function fun(){
 console.log("fun()")
}
```

- 使用函数表达式创建的函数，不会被声明提前，所以不能在声明前调用

```javascript
var fun2 = function(){
  console.log("我不会被提前声明")
}
```

### 15、this

解析器在调用函数时每次都会向函数内部传递一个隐含的**参数**

这个隐含的参数就是 this，this 指向的是一个对象，这个对象我们称为函数执行的上下文对象，根据**函数的调用方式**的不同，this 会指向不同的对象。

1. 以函数的形式调用，this 永远都是 window
2. 以方法的形式调用，this 就是调用方法的那个对象
3. 当以构造函数的形式调用时，this 就是新创建的那个对象
4. 以 call、apply 调用时，this 就是指定的那个对象（bind 可以指定 this，然后返回一个新的函数）

在后面的学习中将慢慢补全 this 是什么

```javascript
function fun(){
 console.log(this.name)
}
fun()
```

### 16、使用工厂方法创建对象

通过该方法可以大批量的创建对象

```javascript
function createPerson(name, age, gender){
  var obj = new Object()
  obj.name = name
  obj.age = age
  obj.gender = gender
  obj.sayName = function(){
    alert(this.name)
  }
  return obj
}
var zbj = createPerson("猪八戒",1030,"男")
var lcg = createPerson("李长庚",11030,"男")
var ce = createPerson("嫦娥",18,"女")
ce.sayName()
```

使用工厂方法创建的对象，使用的构造函数都是 Object，所以创建的对象都是 Object 这个类型，这就导致我们无法区分出多种不同类型的对象

### 17、<font color=red>构造函数</font>

构造函数就是一个普通的函数，创建方式和普通函数没有区别，不同的是构造函数习惯上首字母大写。

构造函数和普通函数的区别就是调用方法的不同，普通函数时直接调用，而构造函数需要使用 new 关键字调用

```javascript
function Person(){}
var per = new Person()
console.log(per)
```

构造函数的执行流程：

- 立刻创建一个新的对象

- 将新建的对象设置为函数中的 this，在构造函数中可以使用 this 来引用新建的对象

- 逐行执行函数中的代码

- 将新建的对象作为返回值返回

```javascript
function Person(name, age, gender){
  this.name = name
  this.age = age
  this.gender = gender
  this.sayName = function(){
    alert(this.name)
  }
}
var zbj = new Person("猪八戒",1030,"男")
var lcg = new Person("李长庚",11030,"男")
var ce = new Person("嫦娥",18,"女")
console.log(zbj)
console.log(lcg)
console.log(ce)
```

使用同一个构造函数创建的对象，我们称为一类对象，也将一个构造函数称为一个类。我们将通过一个构造函数创建的对象，称为是该类的实例

### 18、instanceof

使用 instanceof 可以检查一个对象是否是一个类的实例

语法：`对象 instanceof 构造函数`

如果是，则返回 true，否则返回 false

```javascript
console.log(lcg instanceof Person) // true
console.log(dog instanceof Person) // false
```

注意：

所有的对象都是 Object 的后代，所以任何对象和 Object 做 instanceof 检查时都会返回 true

```javascript
console.log(dog instanceof Object)
```

缺陷

创建一个 Person 构造函数，在 Person 构造函数中， 为每一个对象都得加了一个 sayName 方法。

目前我们的方法是在构造固数内部创建的，也就是构造函数每执行一次就会创建一个新的 sayName 方法，也就是说实例的 sayName 都是唯一的。

这样就导致了构造函数执行一次就会创建一个新的方法，执行10000次就会创建10000个新的方法，而10000个方法都是一模一样的，这是完全没有必要，完全可以使所有的对象共享同一个方法。

```javascript
function Person(name, age, gender){
  this.name = name
  this.age = age
  this.gender = gender
  // 向对象中添加一个方法
  this.sayName = fun
}
// 将sayName()方法在全局作用域中定义
function fun(){
 alert(this.name)
}
var per = new Person("张三", 21, "男")
var per2 = new Person("李四", 18, "男")
```

将函数定义在全局作用域中，污染了全局作用域的命名空间，而且也不安全

### 19、原型 prototype

我们所创建的每一个函数，解析器都会向函数中添加一个属性 prototype，这个属性对应着一个对象，这个对象就是我们所谓的原型对象

如果函数作为普通函数调用，prototype 没有任何作用

当函数以构造函数的形式调用时，它所创建的对象中都会有一个隐含的属性，指向该构造函数的原型对象，我们可以通过 `__proto__` 来访问该属性

原型对象就相当于一个公共的区域，所有同一个类的实例都可以访问到这个原型对象，我们可以将对象中共有的内容，统一设置到原型对象中

当我们访问对象的一个属性或方法时，它会先在对象自身中寻找，如果有则直接使用，如果没有则会去原型对象中寻找，如果找到则直接使用

```javascript
// 向MyClass的原型中添加属性a
MyClass.prototype.a = 123
// 向mc中添加a属性
mc.a = "我是mc中的a"
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200812192851.png)

mc、mc2、mc3 是通过 MyClass 创建的对象，完整代码如下

```javascript
function MyClass(){
  
}
MyClass.prototype.a = 123
var mc = new MyClass()
var mc2 = new MyClass()
var mc3 = new MyClass()
mc.a = "我是mc中的a"
console.log(mc.a) // 由于mc中自己有a，因此输出自己的 我是mc中的a
console.log(mc2.a)
console.log(mc3.a) // 这两个自己没有a，因此会到原型中去找，找到了则输出 123
```

建议：以后我们创建构造函数时，可以将这些对象共有的属性和方法。 统一添加加到构造函教的原型对象中，这样不用分别为每一个对像添加，也不会影响到到全局作用城，就可以使每个对象都具有这些属性和方法了

```javascript
function Person(name, age, gender){
  // 私有的变量和方法放这里，通过 this 传递
  this.name = name
  this.age = age
  this.gender = gender
}
// 向原型中添加sayName方法
Person.prototype.sayName = function(){
 alert(this.name)
}
```

使用 in 检查对象中是否含有某个属性是，如果对象中没有，但是原型中有，也会返回 true

```javascript
console.log("a" in mc2) // true
```

可以使用对象的 `hasOwnProperty()` 来检查对象自身中是否含有该属性，该方法只有当对象自身中含有属性时，才会返回 true

```javascript
console.log(mc.hasOwnProperty("age")) // false
console.log(mc.hasOwnProperty("a")) // true
console.log(mc.__proto__.__proto__.hasOwnProperty("hasOwnProperty")) // true
```

原型对象也是对象，所以它也有原型，当我们使用一个对象的属性或方法时，会先在自身中寻找，自身中如果有，则直接使用；如果没有则去原型对象中寻找，如果原型对象中有，则使用；如果没有则去原型的原型中寻找，直到找到 Object 对象的原型，Object 对象的原型没有原型，如果在 Object 原型中仍然没有找到，则返回 undefined（原型链）。

![](https://cdn.wallleap.cn/img/pic/illustration/20200812195201.png)

当我们直接在页面中打印一个对象时，实际上输出的是对象的 `toString()` 方法的返回值

```javascript
function Person(name, age, gender){
  this.name = name
  this.age = age
  this.gender = gender
}
var per = new Person("张三", 21, "男")
var result = per.toString()
console.log("result="+result) // result=[object Object]
console.log(per.__proto__.__proto__.hasOwnProperty("toString")) // true
```

如果我么希望在输出对象时不输出 `[object Object]`，可以为对象添加一个 `toString` 方法

```javascript
Person.prototype.toString = function(){
  return "Person[name="+this.name+",age="+this.age+",gender="+this.gender+"]"
}
```

### 20、垃圾回收(GC)

- 就像人生活的时间长了会产生垃圾一样，程序运行过程中也会产生垃圾，这些垃圾积攒过多以后，会导致程序运行的速度过慢，所以我们需要一个垃圾回收的机制，来处理程序运行过程中产生的垃圾
- 当一个对象没有任何的变量或属性对它进行引用，此时我们将永远无法操作该对象，此时这种对象就是一个垃圾，这种对象过多会占用大量的内存空间，导致程序运行变慢，所以这种垃圾必须进行清理
- 在 js 中拥有自动的垃圾回收机制，会自动将这些垃圾对象从内存中销毁，我们不需要也不能进行垃圾回收的操作

![](https://cdn.wallleap.cn/img/pic/illustration/20200812201505.png)

- 因此，我们需要做的只是将不再使用的对象设置为 null 即可

### 21、数组

- 数组（Array）也是一个对象
- 它和普通对象功能类似，也是用来存储一些值的
- 不同的是普通对象是使用字符串作为属性名的，而数组是使用数字来作为索引操作元素的
- 索引：从 0 开始的整数
- 数组的存储性能比普通对象要好，在开发中我们经常使用数组来存储一些数据

![](https://cdn.wallleap.cn/img/pic/illustration/20200812202048.png)

```javascript
/* 创建数组对象 */
var arr = new Array()
console.log(typeof arr) // object
// 使用构造函数创建数组时，可以同时添加元素，将要添加的元素作为构造函数的参数传递，元素之间用逗号隔开
var arr1 = new Array(10,20,30)
console.log(arr1)
/* 向数组中添加元素：数组[索引]=值 */
arr[0] = 10
arr[1] = 20
console.log(arr) // [10, 20]
/* 读取数组中的元素：数组[索引]
 * 如果读取不存在的索引，不会报错，而是返回undefined
*/
console.log(arr[0]) // 10
/* 获取数组的长度，使用length属性来获取
 * 语法：数组.length
 * 对于连续的数组，使用length可以获取到数组的长度(元素的个数)
 * 对于非连续的数组，使用length会获取到数组的最大索引+1  尽量不要创建非连续的数组
*/
console.log(arr.length) // 2
/* 修改length
 * 如果修改的length大于原长度，则多出的部分会空出来
 * 如果修改的length小于原长度，则多出的元素会被删除
*/
arr.length = 10
/* 向数组的最后一个位置添加元素
 * 语法：数组[数组.length] = 值
*/
arr[arr.length] = 30
arr[arr.length] = 40
arr[arr.length] = 50
```

使用字面量来创建数组

```javascript
/* 使用字面量来创建数组
 * 语法：[]
*/
var arr = []
console.log(typeof arr, arr instanceof Array) // object true
/* 使用字面量床架数组时，可以在创建时就指定数组中的元素 */
var arr1 = [1,2,3,4,5,6]
console.log(arr[3])
// 数组中的元素可以是任意的数据类型
arr = ["hello",1,true,null,undefined]
console.log(arr)
// 也可以是对象
var obj = {name:"张三"} 
arr[arr.length] = obj
// 可以是函数
arr = [function(){alert(1)}, function(){alert(2)}]
arr[0]()
// 数组中也可以放数组，如下这种数组称为二维数组
arr = [[1,2,3], [3,4,5], [5,6,7]]
console.log(arr[1])
```

### 22、数组的方法

| 方法                                                                                 | 描述                                                           |
| :----------------------------------------------------------------------------------- | :------------------------------------------------------------- |
| [concat()](https://www.w3school.com.cn/jsref/jsref_concat_array.asp)                 | 连接两个或更多的数组，并返回结果。                             |
| [join()](https://www.w3school.com.cn/jsref/jsref_join.asp)                           | 把数组的所有元素放入一个字符串。元素通过指定的分隔符进行分隔。 |
| [pop()](https://www.w3school.com.cn/jsref/jsref_pop.asp)                             | 删除并返回数组的最后一个元素                                   |
| [push()](https://www.w3school.com.cn/jsref/jsref_push.asp)                           | 向数组的末尾添加一个或更多元素，并返回新的长度。               |
| [reverse()](https://www.w3school.com.cn/jsref/jsref_reverse.asp)                     | 颠倒数组中元素的顺序。                                         |
| [shift()](https://www.w3school.com.cn/jsref/jsref_shift.asp)                         | 删除并返回数组的第一个元素                                     |
| [slice()](https://www.w3school.com.cn/jsref/jsref_slice_array.asp)                   | 从某个已有的数组返回选定的元素                                 |
| [sort()](https://www.w3school.com.cn/jsref/jsref_sort.asp)                           | 对数组的元素进行排序                                           |
| [splice()](https://www.w3school.com.cn/jsref/jsref_splice.asp)                       | 删除元素，并向数组添加新元素。                                 |
| [toSource()](https://www.w3school.com.cn/jsref/jsref_tosource_array.asp)             | 返回该对象的源代码。                                           |
| [toString()](https://www.w3school.com.cn/jsref/jsref_toString_array.asp)             | 把数组转换为字符串，并返回结果。                               |
| [toLocaleString()](https://www.w3school.com.cn/jsref/jsref_toLocaleString_array.asp) | 把数组转换为本地数组，并返回结果。                             |
| [unshift()](https://www.w3school.com.cn/jsref/jsref_unshift.asp)                     | 向数组的开头添加一个或更多元素，并返回新的长度。               |
| [valueOf()](https://www.w3school.com.cn/jsref/jsref_valueof_array.asp)               | 返回数组对象的原始值                                           |

push()

- 该方法可以向数组的末尾添加一个或多个元素，并返回数组的新的长度
- 可以将要添加的元素作为方法的参数传递，这样这些元素将会自动添加到数组的末尾
- 该方法会将数组新的长度作为返回值返回

```javascript
var result = arr.push("HTML", "CSS", "JavaScript")
console.log(arr, result)
```

pop()

- 该方法可以删除数组的最后一个元素，并将被删除的元素作为返回值返回

```javascript
result = arr.pop()
console.log(arr, result)
```

unshift()

- 向数组开头添加一个或多个元素，并返回新的数组长度
- 向前边插入元素以后，其他的元素索引会依次调整

```javascript
console.log(arr)
arr.unshift("HTTP")
console.log(arr)
```

shift()

- 可以删除数组的第一个元素，并将被删除的元素作为返回值返回

```javascript
result = arr.shift()
console.log(arr, result)
```

数组的遍历

for 循环

```javascript
/* 所谓的遍历数组，就是将数组中的元素都取出来
 * arr[0]
 * arr[1]
 * ...
 * arr[lenght-1]
*/
for(var i=0; i<arr.length; i++){
  console.log(arr[i])
}
```

forEach

一般我们都是使用 for 循环去遍历数组，js 中还为我们提供了一个方法，用来遍历数组forEach()

这个方法只支持IE8以上的浏览器，IE8及以下的浏览器均不支持该方法，还是使用for

forEach( ) 方法需要一个函数作为参数

- 像这种函数，由我们创建但是不由我们调用但最后执行了的，我们称为**回调函数**

- 数组中有几个元素函数就会执行几次，每次执行时，浏览器会将遍历到的元素
  以实参的形式传递进来， 我们可以来定义形参，来读取这些内容

- 浏览器会在回调函数中传递三个参数:

  - 第一个参数，就是当前正在遍历的元素
  - 第二个参数，就是当前正在遍历的元素的索引
  - 第三个参数，就是正在遍历的数组

  ```javascript
  arr.forEach(function(value, index, obj){
    console.log(value, index, obj)
  })
  ```

slice()

- 可以用来从数组提取指定元素
- 该方法不会改变元素数组，而是将截取到的元素封装到一个新数组中返回
- 参数，
  1. 数取开始的位置的索引，包含开始索引
  2. 截取結東的位置的索引,不包含结束索引
     - 第二个参数可以省略不写,此时会截取从开始索引往后的所有元素
     - 索引可以传递一个负值， 如果传递一个负值，则从后往前计算，-1——倒数第一个

```javascript
var result = arr.slice(1, 4)
result = arr.slice(3)
result = arr.slice(1, -2)
```

splice()

- 可以用于删除数组中的指定元素
- 使用splice()会影响到原数组，会将指定元素从原数组中删除，并将被删除的元素作为返回值返回
- 参数，
  - 第一个，表示开始位置的索引
  - 第二个，表示删除的数量
  - 第三个及以后，可以传递一些新的元素，这些元素将会自动插入到开始位置索引前边

```javascript
var arr = ["HTTP","HTML","CSS","JavaScript","jQuery","Less"]
var result = arr.splice(3,0,"BootStrap")
```

去除数组中重复的数字

```javascript
for(var i=0; i<arr.length; i++){
  // console.log(i)
  for(var j=i+1; j<arr.length; j++){
    if(arr[i] == arr[j]){
      arr.splice(j,1)
      j--
  }
}
```

concat()

- 可以连接两个或多个数组，并将新的数组返回
- 该方法不会对原数组产生影响

```javascript
var result = arr.concat(arr2)
console.log(result)
result = arr.concat(arr2,arr3,"ES6","模块化","WebPack","AngularJS","React","VUE")
```

join()

- 可以将数组转换为一个字符串
- 该方法不会对原数组产生影响，而是将转换后的字符串作为结果返回
- 在join()中可以指定一个字符串作为参数，这个字符串将会成为数组中元素的连接符

```js
result = arr.join() // 不传，默认用逗号分隔
result = arr.join("") // 想让它们直接连接需要传空串(不是空格)
result = arr.join("-") // 传什么就用什么连接
```

reverse()

- 用来反转数组(前面的元素到后面，后面的元素到前面)
- 该方法会直接修改原数组

```javascript
arr = ["a","b","c","d"]
arr.reverse()
```

sort()

- 可以用来对数组中的元素进行排序
- 也会影响原数组，默认会按照Unicode编码进行排序

```javascript
arr.sort() // 排序
arr.reverse() // 搭配起来进行反向排序
```

- 即使对于纯数字的数组，使用sort( )排序时，也会按照Unicode编码来排序，所以对数字进排序时，可能会得到错误的结果。
- 我们可以自己来指定排序的规则：我们可以在sort( )添加一个回调函数，来指定排序规则，回调函数中需要定义两个形参，浏览器将会分别使用数组中的元素作为实参去调用回调函数，使用哪个元素调用不确定，但是肯定的是在数组中a一定在b前边
- 浏览器会根据回调函数的返回值来决定元素的顺序，
  - 如果返回一个大于0的值，则元素会交换位置
  - 如果返回一个小于0的值，则元素位置不变
  - 如果返回一个0，则认为两个元素相等，也不交换位置
- 如果需要升序排列，则返回a-b，如果需要降序排列，则返回b-a

```javascript
arr.sort(function(a,b){
  /* if(a>b){
    return 1
  }else if(a<b){
    return -1
  }else{
    return 0
  } */
  return a-b
})
```

### 23、函数的方法

call() 和 apply()

- 这两个方法都是函数对象的方法，需要通过函数对象来调用
- 当对函数调用这两个方法时，都会调用函数执行

```javascript
function fun(){
  alert("fun()")
}
fun.apply()
fun.call()
fun()
```

- 在调用 call() 和 apply() 可以将一个对象指定为第一个参数，此时这个对象将会成为函数执行时的 this

```javascript
function fun(){
 alert(this.name)
}
var obj = {
  name: "obj",
  sayName:function(){
    alert(this.name)
  }
}
// fun.call(obj)
fun.apply(obj)
```

- 传递单个参数时没什么不同，但是多个参数：
  - call() 方法可以将实参在对象之后依次传递
  - apply() 方法需要将实参封装到一个数组中统一传递

```javascript
fun.call(obj,2,3)
fun.apply(obj,[2,3])
```

这里 this 又多了一种情况：

> 使用 call() 和 apply() 调用时，this 是指定的那个对象

### 24、arguments

在调用函数时，浏览器每次都会传递进两个隐含的参数：

1. 函数的上下文对象 this

2. 封装实参的对象 arguments

   - arguments 是一个类数组对象，它可以通过索引来操作数据，也可以获取长度

      ```javascript
      function fun(){
        // console.log(arguments instanceof Array) // false
        console.log(Array.isArray(arguments)) // false
      }
      fun()
      ```

   - 在调用函数时，我们所传递的实参都会在 arguments 中保存
   - arguments.length 可以用来获取实参的长度
   - 我们即使不定义形参，也可以通过 arguments 来使用实参，只不过比较麻烦
     - arguments[0] 表示第一个实参
     - arguments[1] 表示第二个实参……
   - 它里边有一个属性叫做 callee，这个属性对应一个函数对象，就是当前正在指向的函数的对象

      ```javascript
      console.log(arguments.callee === fun) // true
      ```

   - 由于是个伪数组（类数组），因此不支持数组的方法，比如 forEach，但是可以通过 Array.from(arguments) 转换成真数组

```javascript
 /*
函数参数可选，可以利用arguments来判断
 arr：数组
 length：长度，可选参数
 callback：回调函数
*/
function(){
  var arr = arguments[0]
  if(arguments.length==2){
    var fun = arguments[1]
    fun()
  }
  if(arguments.length==3){
    var length = arguments[1]
    var fun = arguments[2]
    fun()
  }
}
```

### 25、Date() 对象

- 在 js 中使用 Date 对象来表示一个时间

```javascript
// 创建一个Date对象
var d = new Date()
console.log(d) // Mon Apr 13 2020 09:09:04 GMT+0800 (中国标准时间)
```

> JS 原生 Date 并不好用，因此在工作中一般会使用第三方库如 moment.js、day.js 来处理时间

如果直接使用构造函数创建一个 Date 对象，则会封装为当前代码执行的时间

创建一个指定的时间对象，需要在构造函数中传递一个表示时间的字符串作为参数

日期的格式： `月份/日/年 时:分:秒`

```javascript
var d2 = new Date("4/16/2020 09:09:04") 
console.log(d2) // Thu Apr 16 2020 09:09:04 GMT+0800 (中国标准时间)
```

| 方法                                                                                   | 描述                                                   |
| :------------------------------------------------------------------------------------- | :----------------------------------------------------- |
| [Date()](https://www.w3school.com.cn/jsref/jsref_Date.asp)                             | 返回当日的日期和时间。                                 |
| [getDate()](https://www.w3school.com.cn/jsref/jsref_getDate.asp)                       | 从 Date 对象返回一个月中的某一天 (1 ~ 31)。            |
| [getDay()](https://www.w3school.com.cn/jsref/jsref_getDay.asp)                         | 从 Date 对象返回一周中的某一天 (0 ~ 6)。               |
| [getMonth()](https://www.w3school.com.cn/jsref/jsref_getMonth.asp)                     | 从 Date 对象返回月份 (0 ~ 11)。                        |
| [getFullYear()](https://www.w3school.com.cn/jsref/jsref_getFullYear.asp)               | 从 Date 对象以四位数字返回年份。                       |
| [getYear()](https://www.w3school.com.cn/jsref/jsref_getYear.asp)                       | 请使用 getFullYear() 方法代替。                        |
| [getHours()](https://www.w3school.com.cn/jsref/jsref_getHours.asp)                     | 返回 Date 对象的小时 (0 ~ 23)。                        |
| [getMinutes()](https://www.w3school.com.cn/jsref/jsref_getMinutes.asp)                 | 返回 Date 对象的分钟 (0 ~ 59)。                        |
| [getSeconds()](https://www.w3school.com.cn/jsref/jsref_getSeconds.asp)                 | 返回 Date 对象的秒数 (0 ~ 59)。                        |
| [getMilliseconds()](https://www.w3school.com.cn/jsref/jsref_getMilliseconds.asp)       | 返回 Date 对象的毫秒(0 ~ 999)。                        |
| [getTime()](https://www.w3school.com.cn/jsref/jsref_getTime.asp)                       | 返回 1970 年 1 月 1 日至今的毫秒数。                   |
| [getTimezoneOffset()](https://www.w3school.com.cn/jsref/jsref_getTimezoneOffset.asp)   | 返回本地时间与格林威治标准时间 (GMT) 的分钟差。        |
| [getUTCDate()](https://www.w3school.com.cn/jsref/jsref_getUTCDate.asp)                 | 根据世界时从 Date 对象返回月中的一天 (1 ~ 31)。        |
| [getUTCDay()](https://www.w3school.com.cn/jsref/jsref_getUTCDay.asp)                   | 根据世界时从 Date 对象返回周中的一天 (0 ~ 6)。         |
| [getUTCMonth()](https://www.w3school.com.cn/jsref/jsref_getUTCMonth.asp)               | 根据世界时从 Date 对象返回月份 (0 ~ 11)。              |
| [getUTCFullYear()](https://www.w3school.com.cn/jsref/jsref_getUTCFullYear.asp)         | 根据世界时从 Date 对象返回四位数的年份。               |
| [getUTCHours()](https://www.w3school.com.cn/jsref/jsref_getUTCHours.asp)               | 根据世界时返回 Date 对象的小时 (0 ~ 23)。              |
| [getUTCMinutes()](https://www.w3school.com.cn/jsref/jsref_getUTCMinutes.asp)           | 根据世界时返回 Date 对象的分钟 (0 ~ 59)。              |
| [getUTCSeconds()](https://www.w3school.com.cn/jsref/jsref_getUTCSeconds.asp)           | 根据世界时返回 Date 对象的秒钟 (0 ~ 59)。              |
| [getUTCMilliseconds()](https://www.w3school.com.cn/jsref/jsref_getUTCMilliseconds.asp) | 根据世界时返回 Date 对象的毫秒(0 ~ 999)。              |
| [parse()](https://www.w3school.com.cn/jsref/jsref_parse.asp)                           | 返回1970年1月1日午夜到指定日期（字符串）的毫秒数。     |
| [setDate()](https://www.w3school.com.cn/jsref/jsref_setDate.asp)                       | 设置 Date 对象中月的某一天 (1 ~ 31)。                  |
| [setMonth()](https://www.w3school.com.cn/jsref/jsref_setMonth.asp)                     | 设置 Date 对象中月份 (0 ~ 11)。                        |
| [setFullYear()](https://www.w3school.com.cn/jsref/jsref_setFullYear.asp)               | 设置 Date 对象中的年份（四位数字）。                   |
| [setYear()](https://www.w3school.com.cn/jsref/jsref_setYear.asp)                       | 请使用 setFullYear() 方法代替。                        |
| [setHours()](https://www.w3school.com.cn/jsref/jsref_setHours.asp)                     | 设置 Date 对象中的小时 (0 ~ 23)。                      |
| [setMinutes()](https://www.w3school.com.cn/jsref/jsref_setMinutes.asp)                 | 设置 Date 对象中的分钟 (0 ~ 59)。                      |
| [setSeconds()](https://www.w3school.com.cn/jsref/jsref_setSeconds.asp)                 | 设置 Date 对象中的秒钟 (0 ~ 59)。                      |
| [setMilliseconds()](https://www.w3school.com.cn/jsref/jsref_setMilliseconds.asp)       | 设置 Date 对象中的毫秒 (0 ~ 999)。                     |
| [setTime()](https://www.w3school.com.cn/jsref/jsref_setTime.asp)                       | 以毫秒设置 Date 对象。                                 |
| [setUTCDate()](https://www.w3school.com.cn/jsref/jsref_setUTCDate.asp)                 | 根据世界时设置 Date 对象中月份的一天 (1 ~ 31)。        |
| [setUTCMonth()](https://www.w3school.com.cn/jsref/jsref_setUTCMonth.asp)               | 根据世界时设置 Date 对象中的月份 (0 ~ 11)。            |
| [setUTCFullYear()](https://www.w3school.com.cn/jsref/jsref_setUTCFullYear.asp)         | 根据世界时设置 Date 对象中的年份（四位数字）。         |
| [setUTCHours()](https://www.w3school.com.cn/jsref/jsref_setutchours.asp)               | 根据世界时设置 Date 对象中的小时 (0 ~ 23)。            |
| [setUTCMinutes()](https://www.w3school.com.cn/jsref/jsref_setUTCMinutes.asp)           | 根据世界时设置 Date 对象中的分钟 (0 ~ 59)。            |
| [setUTCSeconds()](https://www.w3school.com.cn/jsref/jsref_setUTCSeconds.asp)           | 根据世界时设置 Date 对象中的秒钟 (0 ~ 59)。            |
| [setUTCMilliseconds()](https://www.w3school.com.cn/jsref/jsref_setUTCMilliseconds.asp) | 根据世界时设置 Date 对象中的毫秒 (0 ~ 999)。           |
| [toSource()](https://www.w3school.com.cn/jsref/jsref_tosource_boolean.asp)             | 返回该对象的源代码。                                   |
| [toString()](https://www.w3school.com.cn/jsref/jsref_toString_date.asp)                | 把 Date 对象转换为字符串。                             |
| [toTimeString()](https://www.w3school.com.cn/jsref/jsref_toTimeString.asp)             | 把 Date 对象的时间部分转换为字符串。                   |
| [toDateString()](https://www.w3school.com.cn/jsref/jsref_toDateString.asp)             | 把 Date 对象的日期部分转换为字符串。                   |
| [toGMTString()](https://www.w3school.com.cn/jsref/jsref_toGMTString.asp)               | 请使用 toUTCString() 方法代替。                        |
| [toUTCString()](https://www.w3school.com.cn/jsref/jsref_toUTCString.asp)               | 根据世界时，把 Date 对象转换为字符串。                 |
| [toLocaleString()](https://www.w3school.com.cn/jsref/jsref_toLocaleString.asp)         | 根据本地时间格式，把 Date 对象转换为字符串。           |
| [toLocaleTimeString()](https://www.w3school.com.cn/jsref/jsref_toLocaleTimeString.asp) | 根据本地时间格式，把 Date 对象的时间部分转换为字符串。 |
| [toLocaleDateString()](https://www.w3school.com.cn/jsref/jsref_toLocaleDateString.asp) | 根据本地时间格式，把 Date 对象的日期部分转换为字符串。 |
| [UTC()](https://www.w3school.com.cn/jsref/jsref_utc.asp)                               | 根据世界时返回 1970 年 1 月 1 日 到指定日期的毫秒数。  |
| [valueOf()](https://www.w3school.com.cn/jsref/jsref_valueOf_date.asp)                  | 返回 Date 对象的原始值。                               |

getTime()

- 获取当前日期对象的时间戳
- 时间戳，指的是从格林威治标准时间的1970年1月1日 0时0分0秒到当前日期所花费的毫秒数(1秒=1000毫秒)

```javascript
var time = d2.getTime()
console.log(time) // 1586999344000
```

- 计算机底层在保存时间时使用的是时间戳，可以利用时间关系进行换算

```javascript
console.log(time/1000/60/60/25/365)
```

- 以前利用过console.time()、console.timeEnd()测试代码的执行性能，现在可以利用Date的函数实现

```javascript
// 获取当前的时间戳
var start  = Date.now()
for(var i=0; i<100; i++){
  console.log(i)
}
var end = Date.now()
console.log("执行了："+(end-start)+"毫秒")
```

### 26、Math 对象

Math 对象用于执行数学任务。

Math 对象并不像 Date 和 String 那样是对象的类，因此没有构造函数 Math()，像 Math.sin() 这样的函数只是函数，不是某个对象的方法。它属于一个工具类，无需创建它，通过把 Math 作为对象使用就可以调用其所有属性和方法。

Math 对象属性

| 属性                                                           | 描述                                              |
| :------------------------------------------------------------- | :------------------------------------------------ |
| [E](https://www.w3school.com.cn/jsref/jsref_e.asp)             | 返回算术常量 e，即自然对数的底数（约等于2.718）。 |
| [LN2](https://www.w3school.com.cn/jsref/jsref_ln2.asp)         | 返回 2 的自然对数（约等于0.693）。                |
| [LN10](https://www.w3school.com.cn/jsref/jsref_ln10.asp)       | 返回 10 的自然对数（约等于2.302）。               |
| [LOG2E](https://www.w3school.com.cn/jsref/jsref_log2e.asp)     | 返回以 2 为底的 e 的对数（约等于 1.414）。        |
| [LOG10E](https://www.w3school.com.cn/jsref/jsref_log10e.asp)   | 返回以 10 为底的 e 的对数（约等于0.434）。        |
| [PI](https://www.w3school.com.cn/jsref/jsref_pi.asp)           | 返回圆周率（约等于3.14159）。                     |
| [SQRT1_2](https://www.w3school.com.cn/jsref/jsref_sqrt1_2.asp) | 返回返回 2 的平方根的倒数（约等于 0.707）。       |
| [SQRT2](https://www.w3school.com.cn/jsref/jsref_sqrt2.asp)     | 返回 2 的平方根（约等于 1.414）。                 |

Math 对象方法

| 方法                                                                    | 描述                                                          |
| :---------------------------------------------------------------------- | :------------------------------------------------------------ |
| [abs(x)](https://www.w3school.com.cn/jsref/jsref_abs.asp)               | 返回数的绝对值。                                              |
| [acos(x)](https://www.w3school.com.cn/jsref/jsref_acos.asp)             | 返回数的反余弦值。                                            |
| [asin(x)](https://www.w3school.com.cn/jsref/jsref_asin.asp)             | 返回数的反正弦值。                                            |
| [atan(x)](https://www.w3school.com.cn/jsref/jsref_atan.asp)             | 以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值。      |
| [atan2(y,x)](https://www.w3school.com.cn/jsref/jsref_atan2.asp)         | 返回从 x 轴到点 (x,y) 的角度（介于 -PI/2 与 PI/2 弧度之间）。 |
| [ceil(x)](https://www.w3school.com.cn/jsref/jsref_ceil.asp)             | 对数进行上舍入。                                              |
| [cos(x)](https://www.w3school.com.cn/jsref/jsref_cos.asp)               | 返回数的余弦。                                                |
| [exp(x)](https://www.w3school.com.cn/jsref/jsref_exp.asp)               | 返回 e 的指数。                                               |
| [floor(x)](https://www.w3school.com.cn/jsref/jsref_floor.asp)           | 对数进行下舍入。                                              |
| [log(x)](https://www.w3school.com.cn/jsref/jsref_log.asp)               | 返回数的自然对数（底为e）。                                   |
| [max(x,y)](https://www.w3school.com.cn/jsref/jsref_max.asp)             | 返回 x 和 y 中的最高值。                                      |
| [min(x,y)](https://www.w3school.com.cn/jsref/jsref_min.asp)             | 返回 x 和 y 中的最低值。                                      |
| [pow(x,y)](https://www.w3school.com.cn/jsref/jsref_pow.asp)             | 返回 x 的 y 次幂。                                            |
| [random()](https://www.w3school.com.cn/jsref/jsref_random.asp)          | 返回 0 ~ 1 之间的随机数。                                     |
| [round(x)](https://www.w3school.com.cn/jsref/jsref_round.asp)           | 把数四舍五入为最接近的整数。                                  |
| [sin(x)](https://www.w3school.com.cn/jsref/jsref_sin.asp)               | 返回数的正弦。                                                |
| [sqrt(x)](https://www.w3school.com.cn/jsref/jsref_sqrt.asp)             | 返回数的平方根。                                              |
| [tan(x)](https://www.w3school.com.cn/jsref/jsref_tan.asp)               | 返回角的正切。                                                |
| [toSource()](https://www.w3school.com.cn/jsref/jsref_tosource_math.asp) | 返回该对象的源代码。                                          |
| [valueOf()](https://www.w3school.com.cn/jsref/jsref_valueof_math.asp)   | 返回 Math 对象的原始值。                                      |

Math.random()

- 可以用来生成一个0~1之间的随机数

`console.log(Math.random())`

- 生成一个0~10的随机数

`Math.random()*10` --> 整数 `Math.round(Math.random()*10)`

- 生成一个0~x之间的随机整数

`Math.round(Math.random()*x)`

- 生成一个x~y之间的随机整数

`Math.round(Math.random()*(y-x)+x)`

Math.max() 可以获取多个数中的最大值

Math.min() 可以获取多个数中的最小值

```javascript
var max = Math.max(10,45,5,30,100,50)
var min = Math.min(10,45,5,30,100,50)
console.log(max,min)
```

Math.pow(x,y) 返回x的y次幂

Math.sqrt(x) 返回x的平方根

````javascript
console.log(Math.pow(2,3)) // 8
console.log(Math.sqrt(2)) // 1.4142135623730951
````

### 27、包装类

基本数据类型：`String`、`Number`、`Boolean`、`Null`、`Undefined`

引用数据类型：`Object`

在 js 中为我们提供了三个包装类，通过这三个包装类可以将基本数据类型的数据转换为对象

- String() 可以将基本数据类型字符串转换为 String 对象
- Number() 可以将基本数据类型的数字转换为 Number 对象
- Boolean() 可以将基本数据类型的布尔值转换为 Boolean 对象

```javascript
var num = new Number(3)
console.log(typeof num) // object
```

但是注意，我们在实际应用中不会使用基本数据类型的对象，如果使用基本数据类型的对象，在做一些比较时可能会带来一些不可预期的结果

方法和属性只能添加给对象，不能添加给基本数据类型

当我们对一些基本数据类型的值去调用属性和方法时，浏览器会临时使用包装类将其转换为对象，然后在调用对象的属性和方法，调用完以后，再将其转换为基本数据类型

### 28、字符串相关

创建一个字符串

```javascript
var str = "Hello JavaScript"
```

在底层字符串是以字符数组的形式保存的 `['H',"e","l","l","o"." ","J","a"]`

```javascript
console.log(str[1])
```

length 属性

- 可以用来获取字符串的长度

```javascript
console.log(str.length)
```

charAt()

- 可以返回字符串中指定位置的字符
- 根据索引获取指定的字符

```javascript
var result = str.charAt(6)
console.log(result) // J
```

charCodeAt()

- 获取指定位置字符的字符编码(Unicode编码)

```javascript
console.log(str.charCodeAt(0)) // 72
```

String.formCharCode()

- 根据字符编码去获取字符

```javascript
result = String.fromCharCode(20045) // 乍
```

concat()

- 可以用来连接两个或多个字符串
- 作用和`+`一样

```javascript
result = str.concat("hello","javascript")
```

indexof()

- 该方法可以检索一个字符串中是否含有指定内容
- 如果字符串中含有该内容，则会返回其第一次出现的索引，如果没有找到指定的内容，则会返回-1
- 可以指定第二个参数，表示开始查找的位置

```javascript
result = str.indexOf("h",1)
```

lastIndexOf()

- 该方法的用法和indexOf()一样，不同的是indexOf是从前往后找，而lastIndexOf是从后往前找
- 也可以指定开始查找的位置

slice()

- 可以从字符串中截取指定的内容
- 不会影响原字符串，而是将截取到的内容返回
- 参数
  - 第一个，开始位置的索引（包括开始位置）
  - 第二个，结束位置的索引（不包括结束位置）
    - 如果省略第二个参数，则会截取到后边所有的
    - 也可以传递一个负数作为参数，负数的话将会从后边计算

```javascript
str = "abcdefghijklmn"
result = str.slice(1)
result = str.slice(1,3)
result = str.slice(3,-3)
```

substring()

- 可以用来截取一个字符串，和 slice() 类似
- 参数：
  - 第一个，开始截取位置的索引（包括开始位置）
  - 第二个：结束位置的索引（不包括结束位置）
  - 不同的是这个方法不能接受负值作为参数。如果传递了一个负值，则默认使用 0
  - 而且他还会自动调整參数的位置，如果第二个参数小于第-一个，则自动交换

```javascript
result = str.substring(0,1);
```

substr()

- 用来截取字符串
- 参数
  - 截取开始位置的索引
  - 截取的长度

```javascript
result = str.substr(3,2)
```

![](https://cdn.wallleap.cn/img/pic/illustration/20200813100827.png)

split()

- 可以将一个字符串拆分为一个数组
- 参数
  - 需要一个字符串作为参数，将会根据这个字符串去拆分为数组
  - 如果传递一个空串作为参数，则会将每个字符都拆分为数组中的一个元素

```javascript
str = "string"
result = str.split("") // ["s", "t", "r", "i", "n", "g"]
str = "abc,bcd,efg,hij"
result = str.split(",") // ["abc", "bcd", "efg", "hij"]
console.log(Array.isArray(result)) // true
```

toUpperCase()

- 将一个字符串转换为大写并返回

```javascript
str = "aBcdefg"
result = str.toUpperCase() // ABCDEFG
```

toLowerCase()

- 将一个字符串转换为小写并返回

```javascript
result = result.toLowerCase() // abcdefg
```

字符串和正则相关方法(正则表达式看下一节)

splite()

- 可以将一个字符串拆分为一个数组
- 方法中可以传递一个正则表达式作为参数，这样方法将会根据正则表达式去拆分字符串

```javascript
// 根据任意字母来将字符串财富
var result = str.split(/[A-z]/)
```

- 这个方法即使不指定全局匹配，也会全部拆分

search()

- 可以搜索字符串中是否含有指定内容
- 如果搜索到指定内容，则会返回第一次出现的索引，如果没有搜索到则返回 -1
- 它可以接受一个正则表达式作为参数，然后会根据正则表达式去检索字符串

```javascript
str = "hello hello aec afc"
// 搜索字符串中是否含有abc或aec或afc
result = str.search(/a[bef]c/)
```

- search() 只会查找第一个，即使设置全局匹配也没用

match()

- 可以根据正则表达式，从一个字符串中将符合条件的内容提取出来
- 默认情况下 match 只会找到第一个符合要求的内容，找到以后就停止检索，我们可以设置正则表达式为全局匹配模式，这样就会匹配到所有的内容了

```javascript
str = "1a2b3c4d5e6f7g8h9i"
result = str.match(/[A-z]/g)
```

- 可以为一个正则表达式设置多个匹配模式，且顺序无所谓

```javascript
result = str.match(/[A-z]/ig)
```

- match() 会将匹配到的内容封装到一个数组中返回，即使只查询到一个结果

replace()

- 可以将字符串中指定内容替换为新的内容
- 参数
  1. 被替换的内容，可以接受一个正则表达式作为参数
  2. 新的内容
- 默认只会替换一个

```javascript
result = str.replace(/a/gi "@_@")
```

### 29、正则表达式

GitHub上有个很好的学习教程 [learn-regex](https://github.com/ziishaned/learn-regex/blob/master/translations/README-cn.md)，[翻译版](https://github.com/cdoco/learn-regex-zh)

- 正则表达式用于定义一些字符串的规则，计算机可以根据正则表达式，来检查一个字符串是否符合规则，将字符串中符合规则的内容提取出来

- 创建正则表达式的对象

  - 语法： `var 变量  = new RegExp("正则表达式","匹配模式")`
  - 使用 typeof 检查正则对象，会返回 object

      ```javascript
      var reg = new RegExp("a")
      var str = "a"
      console.log(typeof reg)
      ```

- 正则表达式的方法 test()

  - 使用这个方法可以检查一个字符串是否符合正则表达式的规则，如果符合则返回 true，否则返回 false

      ```javascript
      var result = reg.test(str)
      console.log(result)
      console.log(reg.test("Abcbc"))
      ```

- 在构造函数中可以传递一个匹配模式作为第二个参数，可以是：

  - i 忽略大小写
  - g 全局匹配模式

- 使用字面量来创建正则表达式，语法：`var 变量 = /正则表达式/匹配模式`

```javascript
// var reg = new RegExp("a","i")
reg = /a/i
console.log(typeof reg)
console.log(reg.test("abc"))
```

使用字面量的方式创建更加简单，使用构造函数创建更加灵活

- 使用 `|` 表示或者的意思

```javascript
// 创建一个正则表达式，检查一个字符串中是否含有a或b
reg = /a|b/
```

- `[]` 里的内容也是或的关系 `[ab]==a|b`
  - `[a-z]` 任意小写字母
  - `[A-Z]` 任意大写字母
  - `[A-z]` 任意字母
  - `[0-9]` 任意数字

```javascript
reg = /[ab]/
// 检查一个字符串中是否含有abc或adc或aec
reg = /a[bde]c/
```

- `[^ ]` 除了

```javascript
reg = /[^ab]/
console.log(reg.test("abc"))
```

- 量词
  - 通过量词可以设置一个内容出现的次数
  - 量词只对它前边的一个内容起作用
- `{n}` 正好出现 n 次
- `{n,m}` 出现 m~n 次
- `{n,}` 出现 n 次以上

```javascript
reg = /a{3}/
console.log(reg.test("aaabc"))
reg = /(ab){3}/
reg = /ab{1,3}c/
reg = /a{2,}/
```

- `+` 至少一个，相当于 `{1,}`
- `*` 0 个或多个，相当于 `{0,}`
- `?` 0 个或 1 个，相当于 `{0,1}`

```javascript
reg = /ab+c/
reg = /ab*c/
reg = /ab?c/
```

- `^` 表示开头
- `$` 表示结尾

```javascript
reg = /^a/
reg = /a$/
```

- 在表达式中同时使用 `^`、`$` 则要求字符串必须完全符合正则表达式

```javascript
reg = /^a$/
console.log(reg.test("a"))
reg = /^a|a$/
```

- `.` 表示任意字符

```javascript
// 在正则表达式中使用\作为转义字符 \.表示.
var reg = /\./
console.log(reg.test("b."))
reg = /\\/
console.log(reg.test("b.\\"))
// 使用构造函数时，由于它的参数是一个字符串，而\是字符串中转义字符，如果要使用\则需要使用\\来代替
reg = new RegExp("\\.")
reg = new RegExp("\\\\")
```

- `\w` 任意字母、数字、下划线(`_`)     `[A-z0-9_]`
- `\W` 除了字母、数字、下划线(`_`)     `[^A-z0-9_]`
- `\d` 任意的数字
- `\D` 除了数字
- `\s` 空格
- `\S` 除了空格
- `\b` 单词边界
- `\B` 除了单词边界

```javascript
reg = /\bchild\b/
console.log(reg.test("child ren"))
```

- 创建一个正则表达式，用来检查一个字符串是否是合法手机号

```javascript
/*
手机号的规则： 1 3 511111111 
1.以1开头
2.第二位3-9任意数字
3.三位以后任意数字9个
^1 [3-9] [0-9]{9}$
*/
var phoneStr = "13511111111"
var phoneReg = /^1[3-9][0-9]{9}$/
```

- 去除首尾的空格

```javascript
// 开头
str = str.replace(/^\s*/, "")
// 结尾
str = str.replace(/\s*$/, "")
// 开头和结尾 /^\s*|\s*$/g
str = str.replace(/^\s*|\s*$/g, "")
```

- 合法电子邮件

```javascript
/*
hello  .host  @  abc .com.cn
任意字母数字下划线  .任意字母数字下划线 @  任意字母数字 .任意字母(2~5位)  .任意字母(2~5位) 
\w{3,}  (\.\w+)*  @  [A-z0-9]+  (\.[A-z]{2,5}){1,2}
*/
var emailReg = /^\w{3,}(\.\w+)*@[A-z0-9]+(\.[A-z]{2,5}){1,2}$/
var email = "abc.hello@163.com"
console.log(emailReg.test(email))
```

## 三、DOM

### 1、什么是 DOM

- 全称 Document Object Model 文档对象模型

- JS 中通过 DOM 来**对 HTML 文档进行操作**。只要了解了 DOM 就可以随心所欲地操作 WEB 页面。

- 文档：表示的就是整个 HTML 网页文档

- 对象：表示将网页中的每一个部分都转换为了一个对象

- 模型：使用模型来表示对象之间的关系，这样方便我们获取对象

- 文档对象模型

![](https://cdn.wallleap.cn/img/pic/illustration/20200813113821.png)

### 2、节点

- 节点 Node，是构成我么网页的最基本的组成部分，网页中的每一个部分都可以称为是一个节点。比如：html 标签、属性、文本、注释、整个文档等都是一个个节点。
- 虽然都是节点，但实际上他们的具体类型是不同的。比如：标签称为元素节点、属性称为属性节点、文本称为文本节点、文档称为文档节点

![](https://cdn.wallleap.cn/img/pic/illustration/20200813114231.png)

- 节点的类型不同，属性和方法也都不尽相同

![](https://cdn.wallleap.cn/img/pic/illustration/20200813115721.png)

### 3、节点分类和 DOM 查询

(1) 节点分类

- 文档节点（document）
  - 文档节点 `document`，代表的是整个 HTML 文档，网页中的所有节点都是它的子节点。
  - document 对象作为 `window` 对象的属性存在的，我们不用获取可以直接使用。
  - 通过该对象我们可以在整个文档访问内查找节对象，并可以通过该对象创建各种节点对象。

- 元素节点(Element)
  - HTML 中的各种标签都是元素节点，这也是我们最常用的一个节点。
  - 浏览器会将页面中所有的标签都转换为一个元素节点，我们可以通过 document 的方法来获取元素节点。
  - 比如: `document.getElementById)` 根据 id 属性值获取-个元素节点对象。
- 文本节点（Text）
  - 文本节点表示的是 HTML 标签以外的文本内容，任意非 HTML 的文本都是文本节点。
  - 它包括可以字面解释的纯文本内容。
  - 文本节点一般是作为元素节点的子节点存在的。
  - 获取文本节点时, 一般先要获取元素节点，再通过元素节点获取文本节点。
  - 例如: `元素节点.firstChild` 获取元素节点的第一个子节点，一般为文本节点
- 属性节点（Attr）
  - 属性节点表示的是标签中的一个一个的属性，这里要注意的是属性节点并非是元素节点的子节点，而是元素节点的一部分。
  - 可以通过元素节点来获取指定的属性节点。
  - 例如: `元素节点.getAttributeNode("属性名")`

(2) 获取元素节点

通过 document 对象调用

- `getElementById()` 通过 id 属性获取一个元素节点对象
- `getElementsByTagName()` 通过标签名获取一组元素节点对象
- `getElementsByName()` 通过 `name` 属性获取一组元素节点对象

```javascript
var btn = document.getElementById("btn")
var lis = document.getElementsTagName("li")
var gender = document.getElementsByName("gender") // <input name="gender" type="radio" value="男" />
```

(3) 获取元素节点的子节点

通过具体的元素节点调用

- `getElementsByTagName()` 方法，返回当前节点的指定标签名后代节点

```javascript
// 查找#city下的所有li节点
var list = city.getElementsByTagName("li")
```

- `childNodes` 属性，表示当前节点的所有子节点

childNodes 属性会获取包括文本节点在内的所有节点，包括 DOM 标签与标签间空白也会当成文本节点

```javascript
// 返回#city的所有子节点
var cns = city.childNodes
```

`children` 属性可以获取当前元素的所有子元素

```javascript
var cns2 = city.children
```

- `firstChild` 属性，表示当前节点的第一个子节点（包括空白文本节点）

```javascript
var phone = document.getElementById("phone")
// 返回#phone的第一个子节点
phone.childNodes[0]
var fir = phone.firstChild
```

`firstElementChild` 获取当前元素的第一个子元素，但是不支持 IE 8 及以下的浏览器

```javascript
fir = phone.firstElementChild
```

- `lastChild` 属性，表示当前节点的最后一个子节点

(4) 获取父节点和兄弟节点

通过具体的节点调用

- `parentNode` 属性，表示当前节点的父节点
- `previousSibling` 属性，表示当前节点的前一个兄弟节点
- `nextSibling` 属性，表示当前节点的后一个兄弟节点

```html
<button id="btn">我是一个按钮</button>
<script type="text/javascript">
  // 浏览器已经为我们提供文档节点对象，这个对象是window属性，可以在页面中直接使用，文档节点代表的是整个网页
  // console.log(document)
  var btn = document.getElementById('btn')
  // 修改按钮的文字
  btn.innerHTML = "I'm Button"
</script>
```

(5) DOM 查询的其他方法

- `querySelector()`  该方法需要一个选择器作为参数，可以根据一个 CSS 选择器来查询一个元素节点对象，IE 8 中也可以使用，总是会返回唯一的一个元素，如果满足条件的元素有多个，那么它只会返回第一个
- `querySelectorAll()`  该方法和 `querySelector()` 用法类似，不同的是它会将符合条件的元素封装到一个数组中返回，即使符合条件的元素之后一个，它也会返回数组
- 获取 body 标签 `document.getElementsByTagName("body")[0]`，其实在 `document` 中有一个属性，它保存的就是 body 的引用`document.body`
- `document.documentElement` 保存的是 html 根标签
- `document.all` 代表页面中所有元素，`document.getElementsByTagName("*")`
- `getElementsByClassName()` 可以根据元素的 class 属性值查询一组元素节点对象，但是该方法不支持 IE 8 及以下的浏览器

```javascript
var btn = document.querySelector("#btn")
var body = document.body
var html = document.documentElement
var all = document.all
var box = document.getElementsByClassName("box")[0]
```

### 3、事件

- 事件，就是文档或浏览器窗口中发生的一些特定的交互瞬间/交互行为。
- JavaScript 与 HTML 之间的交互是通过事件实现的。
- 对于 Web 应用来说，有下面这些代表性的事件：点击某个元素、将鼠标移动至某个元素上方、按下键盘上某个键、关闭窗口等等。
- 可以在事件对应的属性中设置一些 js 代码，这样当事件被触发时，这些代码将会执行。

| 事件句柄                                                               | 此事件发生在何时...                  |
| :--------------------------------------------------------------------- | :----------------------------------- |
| [onabort](https://www.w3school.com.cn/jsref/event_onabort.asp)         | 图像的加载被中断。                   |
| [onblur](https://www.w3school.com.cn/jsref/event_onblur.asp)           | 元素失去焦点。                       |
| [onchange](https://www.w3school.com.cn/jsref/event_onchange.asp)       | 域的内容被改变。                     |
| [onclick](https://www.w3school.com.cn/jsref/event_onclick.asp)         | 当用户点击某个对象时调用的事件句柄。 |
| [ondblclick](https://www.w3school.com.cn/jsref/event_ondblclick.asp)   | 当用户双击某个对象时调用的事件句柄。 |
| [onerror](https://www.w3school.com.cn/jsref/event_onerror.asp)         | 在加载文档或图像时发生错误。         |
| [onfocus](https://www.w3school.com.cn/jsref/event_onfocus.asp)         | 元素获得焦点。                       |
| [onkeydown](https://www.w3school.com.cn/jsref/event_onkeydown.asp)     | 某个键盘按键被按下。                 |
| [onkeypress](https://www.w3school.com.cn/jsref/event_onkeypress.asp)   | 某个键盘按键被按下并松开。           |
| [onkeyup](https://www.w3school.com.cn/jsref/event_onkeyup.asp)         | 某个键盘按键被松开。                 |
| [onload](https://www.w3school.com.cn/jsref/event_onload.asp)           | 一张页面或一幅图像完成加载。         |
| [onmousedown](https://www.w3school.com.cn/jsref/event_onmousedown.asp) | 鼠标按钮被按下。                     |
| [onmousemove](https://www.w3school.com.cn/jsref/event_onmousemove.asp) | 鼠标被移动。                         |
| [onmouseout](https://www.w3school.com.cn/jsref/event_onmouseout.asp)   | 鼠标从某元素移开。                   |
| [onmouseover](https://www.w3school.com.cn/jsref/event_onmouseover.asp) | 鼠标移到某元素之上。                 |
| [onmouseup](https://www.w3school.com.cn/jsref/event_onmouseup.asp)     | 鼠标按键被松开。                     |
| [onreset](https://www.w3school.com.cn/jsref/event_onreset.asp)         | 重置按钮被点击。                     |
| [onresize](https://www.w3school.com.cn/jsref/event_onresize.asp)       | 窗口或框架被重新调整大小。           |
| [onselect](https://www.w3school.com.cn/jsref/event_onselect.asp)       | 文本被选中。                         |
| [onsubmit](https://www.w3school.com.cn/jsref/event_onsubmit.asp)       | 确认按钮被点击。                     |
| [onunload](https://www.w3school.com.cn/jsref/event_onunload.asp)       | 用户退出页面。                       |

```html
<button id="btn" onclick="alert('点我干嘛')">我是一个按钮</button>
```

这种写法结构和行为耦合，不方便维护，不推荐使用

### 4、onclick

可以为按钮的对应事件绑定处理函数的形式来响应事件，这样当事件被触发时，其对应的函数将会被调用

```html
<button id="btn">我是一个按钮</button>
<script>
  // 获取按钮对象
  var btn = document.getElementById('btn')
  // 绑定一个单击事件
  btn.onclick = function(){
    alert('你还点')
  }
</script>
```

像这种单击事件绑定的函数，我们称为单击响应函数

### 4、文档加载 onload

浏览器在加载一个页面时，是按照自上向下的顺序加载的，读取到一行就运行一行，如果将 script 标签写到页面的上边，在代码执行时，页面还没有加载，页面没有加载 DOM 对象也没有加载，会导致无法获取到 DOM 对象

将 js 代码编写到页面的下方就是为了可以在页面加载完毕以后再执行 js 代码

但是，一定要放在上面呢，js 也提供了一个事件

onload 事件会在整个页面加载完成之后才触发

为 window 绑定一个 onload 事件，该事件对应的响应函数将会在页面加载完成之后执行，这样可以确保我们的代码执行时，所有的 DOM 对象已经加载完毕了

```javascript
window.onload = function(){
  var btn = document.getElementById("btn")
  btn.onclick = function(){
    alert("hello")
  }
}
```

在这里来做几个练习呗

1、城市选择

![](https://cdn.wallleap.cn/img/pic/illustration/20200814082611.png)

要求完成右边按钮的功能

```javascript
// 查找#bj节点
btn01.onclick = function(){
  var bj = document.getElementById("bj")
}
// 查找所有li节点
btn02.onclick = function(){
  var lis = document.getElementsByTagName("li")
}
// 查找name为gender的所有节点
btn03.onclick = function(){
  var gNodes = document.getElementsByName("gender")
}
// 查找#city下所有li节点
btn04.onclick = function(){
  var cNodes = document.getElementById("city").getElementsByTagName("li")
}
// 返回#city的所有子节点
btn05.onclick = function(){
  var cAllNodes = document.getElementById("city").childNodes
}
// 返回#phone的第一个子节点
btn06.onclick = function(){
  var firstPNode = document.getElementById("#phone").firstChild
}
// 返回#bj的父节点
btn07.onclick = function(){
  var bParentNode = document.getElementById("bj").parentNode
}
// 返回#android的前一个兄弟节点
btn08.onclick = function(){
  var androidBro = document.getElementById("android").previousSibling
}
// 返回#username的value属性值
btn09.onclick = function(){
  var userNameValue = document.getElementById("username").value
}
// 设置Eusername的value属性值
btn10.onclick = function(){
  document.getElementById('username').value = "用户名"
}
// 返回#bj的文本值
btn11.onclick = function(){
  var bjText = document.getElementById("bj").innerText
}
```

它们的功能相似，可以封装为一个函数(只是提醒一下，这里不一定更方便)

```javascript
function myClick(element, callback){
  document.getElementById(element).onclick = callback
}
myClick("btn04",function(){
  var cNodes = document.getElementById("city").getElementsByTagName("li")
  console.log(cNodes)
})
```

2、轮播图

![](https://cdn.wallleap.cn/img/pic/illustration/20200814095505.png)

```html
<style>
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  img{
    width: 533px;
    height: 300px;
  }
  #wrapper{
    position: relative;
    margin: 50px auto;
    width: 533px;
    height: 300px;
  }
  #wrapper button{
    position: absolute;
    top: 0;
    bottom: 0;
    margin: auto 0;
    width: 60px;
    height: 30px;
    text-align: center;
    line-height: 30px;
    background-color: rgba(0, 0, 0, .3);
    color: white;
    border: none;
    outline: none;
    cursor: pointer;
  }
  #wrapper #prev{
    left: 0;
  }
  #wrapper #next{
    right: 0;
  }
  #wrapper button:hover{
    background-color: rgba(0, 0, 0, .8);
  }
  #wrapper #info{
    width: 533px;
    background-color: rgba(0, 0, 0, .3);
    color: whitesmoke;
    text-align: center;
    position: absolute;
    top: 0;
  }
</style>
<div id="wrapper">
  <img src="./img/1.jpg" alt="图片">
  <button id="prev">上一张</button>
  <button id="next">下一张</button>
  <p id="info"></p>
</div>
<script type="text/javascript">
  window.onload = function(){
    /*
     * 点击按钮切换图片
     *  1、找到按钮
     *  2、给按钮添加单击响应事件
     *  3、在单击函数中修改img的src
    */
    var prev = document.getElementById("prev")
    var next = document.getElementById("next")
    var img = document.getElementsByTagName("img")[0]
    var info = document.getElementById("info")
    var imgArr = ["img/1.jpg", "img/2.jpg", "img/3.jpg", "img/4.jpg", "img/5.jpg"]
    var index = 0
    info.innerText = "一共 " +imgArr.length+" 张图片，现在显示的是第 " +(index+1)+" 张"
    // console.log(img)
    prev.onclick = function(){
      // alert("上一张")
      index--
      if(index < 0){
        index = imgArr.length-1
      }
      img.src = imgArr[index]
      // console.log(imgArr[index]);
      info.innerText = "一共 " +imgArr.length+" 张图片，现在显示的是第 " +(index+1)+" 张"
    }
    next.onclick = function(){
      // alert("下一张")
      index++
      if(index > imgArr.length-1){
        index = 0
      }
      img.src = imgArr[index]
      // console.log(imgArr[index]);
      info.innerText = "一共 " +imgArr.length+" 张图片，现在显示的是第 " +(index+1)+" 张"
    }
  }
</script>
```

3、全选

```html
<form action="" method="post">
  你喜欢的运动是？<label id="control"><input type="checkbox" id="checkAllBox">全选/全不选</label><br>
  <input type="checkbox" name="items" value="足球">足球
  <input type="checkbox" name="items" value="篮球">篮球
  <input type="checkbox" name="items" value="羽毛球">羽毛球
  <input type="checkbox" name="items" value="乒乓球">乒乓球<br>
  <input type="button" id="checkedAllBtn" value="全选">
  <input type="button" id="checkedNoBtn" value="全不选">
  <input type="button" id="checkedRevBtn" value="反选">
  <input type="button" id="sendBtn" value="提交">
</form>
<script>
  window.onload = function(){
    var items = document.getElementsByName("items")
    // 在js中可以直接使用id名
    /* 1、全选 */
    checkedAllBtn.onclick = function(){
      // alert('全选')
      // 设置四个多选框变成选中状态
      for(var i=0; i<items.length; i++){
        // 多选框的checked属性
        items[i].checked = true
      }
      // checkAllBox状态
      checkAllBox.checked = true
    }
    // 2、全不选
    checkedNoBtn.onclick = function(){
      for(var i=0; i<items.length; i++){
        items[i].checked = false
      }
      // checkAllBox状态
      checkAllBox.checked = false
    }
    // 3、反选
    checkedRevBtn.onclick = function(){
      for(var i=0; i<items.length; i++){
        items[i].checked = !items[i].checked
      }
      // checkAllBox状态
      checkAllBox.checked = true
      for(var j=0; j<items.length; j++){
        // 只要有一个不是选中状态，则不是全选
        if(!items[j].checked){
          checkAllBox.checked = false
          // 进入判断就说明已经false了，不需要再执行
          break
        }
      }
    }
    // 4、发送
    sendBtn.onclick = function(){
      for(var i=0; i<items.length; i++){
        if(items[i].checked === true){
          alert(items[i].value)
        }
      }
    }
    // 5、全选/全不选
    checkAllBox.onclick = function(){
      for(var i=0; i<items.length; i++){
        // items[i].checked = checkAllBox.checked
        items[i].checked = this.checked
      }
    }
    // checkAllBox状态
    for(var i=0; i<items.length; i++){
      items[i].onclick = function(){
        checkAllBox.checked = true
        for(var j=0; j<items.length; j++){
          // 只要有一个不是选中状态，则不是全选
          if(!items[j].checked){
            checkAllBox.checked = false
            // 进入判断就说明已经false了，不需要再执行
            break
          }
        }
      }
    }
  }
</script>
```

反选可以修改下代码，减少一个循环

```javascript
// 3、反选
checkedRevBtn.onclick = function(){
  //将checkedAllBox设置为选中状态
  checkAllBox.checked = true;
  for(var i = 0; i < items.length; i++){
    // 反选
    items[i].checked = !items[i].checked;
    // checkBox状态
    if(!items[i].checked){
      checkAllBox.checked = false;
    }
  }
}
```

上面又用到了 this：

在事件的响应函数中，响应函数是给谁绑定的 this 就是谁

### 5、DOM 对象的其他属性、方法

下面的属性和方法可用于所有 HTML 元素上：

| 属性 / 方法                                                                                                 | 描述                                                            |
| :---------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------- |
| [element.accessKey](https://www.w3school.com.cn/jsref/prop_html_accesskey.asp)                              | 设置或返回元素的快捷键。                                        |
| [element.appendChild()](https://www.w3school.com.cn/jsref/met_node_appendchild.asp)                         | 向元素添加新的子节点，作为最后一个子节点。                      |
| [element.attributes](https://www.w3school.com.cn/jsref/prop_node_attributes.asp)                            | 返回元素属性的 NamedNodeMap。                                   |
| [element.childNodes](https://www.w3school.com.cn/jsref/prop_node_childnodes.asp)                            | 返回元素子节点的 NodeList。                                     |
| [element.className](https://www.w3school.com.cn/jsref/prop_html_classname.asp)                              | 设置或返回元素的 class 属性。                                   |
| element.clientHeight                                                                                        | 返回元素的可见高度。                                            |
| element.clientWidth                                                                                         | 返回元素的可见宽度。                                            |
| [element.cloneNode()](https://www.w3school.com.cn/jsref/met_node_clonenode.asp)                             | 克隆元素。                                                      |
| [element.compareDocumentPosition()](https://www.w3school.com.cn/jsref/met_node_comparedocumentposition.asp) | 比较两个元素的文档位置。                                        |
| [element.contentEditable](https://www.w3school.com.cn/jsref/prop_html_contenteditable.asp)                  | 设置或返回元素的文本方向。                                      |
| [element.dir](https://www.w3school.com.cn/jsref/prop_html_dir.asp)                                          | 设置或返回元素的内容是否可编辑。                                |
| [element.firstChild](https://www.w3school.com.cn/jsref/prop_node_firstchild.asp)                            | 返回元素的首个子。                                              |
| [element.getAttribute()](https://www.w3school.com.cn/jsref/met_element_getattribute.asp)                    | 返回元素节点的指定属性值。                                      |
| [element.getAttributeNode()](https://www.w3school.com.cn/jsref/met_element_getattributenode.asp)            | 返回指定的属性节点。                                            |
| [element.getElementsByTagName()](https://www.w3school.com.cn/jsref/met_element_getelementsbytagname.asp)    | 返回拥有指定标签名的所有子元素的集合。                          |
| element.getFeature()                                                                                        | 返回实现了指定特性的 API 的某个对象。                           |
| element.getUserData()                                                                                       | 返回关联元素上键的对象。                                        |
| [element.hasAttribute()](https://www.w3school.com.cn/jsref/met_element_hasattribute.asp)                    | 如果元素拥有指定属性，则返回true，否则返回 false。              |
| [element.hasAttributes()](https://www.w3school.com.cn/jsref/met_node_hasattributes.asp)                     | 如果元素拥有属性，则返回 true，否则返回 false。                 |
| [element.hasChildNodes()](https://www.w3school.com.cn/jsref/met_node_haschildnodes.asp)                     | 如果元素拥有子节点，则返回 true，否则 false。                   |
| [element.id](https://www.w3school.com.cn/jsref/prop_html_id.asp)                                            | 设置或返回元素的 id。                                           |
| [element.innerHTML](https://www.w3school.com.cn/jsref/prop_html_innerhtml.asp)                              | 设置或返回元素的内容。                                          |
| [element.insertBefore()](https://www.w3school.com.cn/jsref/met_node_insertbefore.asp)                       | 在指定的已有的子节点之前插入新节点。                            |
| [element.isContentEditable](https://www.w3school.com.cn/jsref/prop_html_iscontenteditable.asp)              | 设置或返回元素的内容。                                          |
| [element.isDefaultNamespace()](https://www.w3school.com.cn/jsref/met_node_isdefaultnamespace.asp)           | 如果指定的 namespaceURI 是默认的，则返回 true，否则返回 false。 |
| [element.isEqualNode()](https://www.w3school.com.cn/jsref/met_node_isequalnode.asp)                         | 检查两个元素是否相等。                                          |
| [element.isSameNode()](https://www.w3school.com.cn/jsref/met_node_issamenode.asp)                           | 检查两个元素是否是相同的节点。                                  |
| [element.isSupported()](https://www.w3school.com.cn/jsref/met_node_issupported.asp)                         | 如果元素支持指定特性，则返回 true。                             |
| [element.lang](https://www.w3school.com.cn/jsref/prop_html_lang.asp)                                        | 设置或返回元素的语言代码。                                      |
| [element.lastChild](https://www.w3school.com.cn/jsref/prop_node_lastchild.asp)                              | 返回元素的最后一个子元素。                                      |
| [element.namespaceURI](https://www.w3school.com.cn/jsref/prop_node_namespaceuri.asp)                        | 返回元素的 namespace URI。                                      |
| [element.nextSibling](https://www.w3school.com.cn/jsref/prop_node_nextsibling.asp)                          | 返回位于相同节点树层级的下一个节点。                            |
| [element.nodeName](https://www.w3school.com.cn/jsref/prop_node_nodename.asp)                                | 返回元素的名称。                                                |
| [element.nodeType](https://www.w3school.com.cn/jsref/prop_node_nodetype.asp)                                | 返回元素的节点类型。                                            |
| [element.nodeValue](https://www.w3school.com.cn/jsref/prop_node_nodevalue.asp)                              | 设置或返回元素值。                                              |
| [element.normalize()](https://www.w3school.com.cn/jsref/met_node_normalize.asp)                             | 合并元素中相邻的文本节点，并移除空的文本节点。                  |
| element.offsetHeight                                                                                        | 返回元素的高度。                                                |
| element.offsetWidth                                                                                         | 返回元素的宽度。                                                |
| element.offsetLeft                                                                                          | 返回元素的水平偏移位置。                                        |
| element.offsetParent                                                                                        | 返回元素的偏移容器。                                            |
| element.offsetTop                                                                                           | 返回元素的垂直偏移位置。                                        |
| [element.ownerDocument](https://www.w3school.com.cn/jsref/prop_node_ownerdocument.asp)                      | 返回元素的根元素（文档对象）。                                  |
| [element.parentNode](https://www.w3school.com.cn/jsref/prop_node_parentnode.asp)                            | 返回元素的父节点。                                              |
| [element.previousSibling](https://www.w3school.com.cn/jsref/prop_node_previoussibling.asp)                  | 返回位于相同节点树层级的前一个元素。                            |
| [element.removeAttribute()](https://www.w3school.com.cn/jsref/met_element_removeattribute.asp)              | 从元素中移除指定属性。                                          |
| [element.removeAttributeNode()](https://www.w3school.com.cn/jsref/met_element_removeattributenode.asp)      | 移除指定的属性节点，并返回被移除的节点。                        |
| [element.removeChild()](https://www.w3school.com.cn/jsref/met_node_removechild.asp)                         | 从元素中移除子节点。                                            |
| [element.replaceChild()](https://www.w3school.com.cn/jsref/met_node_replacechild.asp)                       | 替换元素中的子节点。                                            |
| element.scrollHeight                                                                                        | 返回元素的整体高度。                                            |
| element.scrollLeft                                                                                          | 返回元素左边缘与视图之间的距离。                                |
| element.scrollTop                                                                                           | 返回元素上边缘与视图之间的距离。                                |
| element.scrollWidth                                                                                         | 返回元素的整体宽度。                                            |
| [element.setAttribute()](https://www.w3school.com.cn/jsref/met_element_setattribute.asp)                    | 把指定属性设置或更改为指定值。                                  |
| [element.setAttributeNode()](https://www.w3school.com.cn/jsref/met_element_setattributenode.asp)            | 设置或更改指定属性节点。                                        |
| element.setIdAttribute()                                                                                    |                                                                 |
| element.setIdAttributeNode()                                                                                |                                                                 |
| element.setUserData()                                                                                       | 把对象关联到元素上的键。                                        |
| element.style                                                                                               | 设置或返回元素的 style 属性。                                   |
| [element.tabIndex](https://www.w3school.com.cn/jsref/prop_html_tabindex.asp)                                | 设置或返回元素的 tab 键控制次序。                               |
| [element.tagName](https://www.w3school.com.cn/jsref/prop_element_tagname.asp)                               | 返回元素的标签名。                                              |
| [element.textContent](https://www.w3school.com.cn/jsref/prop_node_textcontent.asp)                          | 设置或返回节点及其后代的文本内容。                              |
| [element.title](https://www.w3school.com.cn/jsref/prop_html_title.asp)                                      | 设置或返回元素的 title 属性。                                   |
| element.toString()                                                                                          | 把元素转换为字符串。                                            |
| [nodelist.item()](https://www.w3school.com.cn/jsref/met_nodelist_item.asp)                                  | 返回 NodeList 中位于指定下标的节点。                            |
| [nodelist.length](https://www.w3school.com.cn/jsref/prop_nodelist_length.asp)                               | 返回 NodeList 中的节点数。                                      |

DOM 查询学完了，接着就可以操作对象了（增删改）

增：

`appendChild()` 向父节点添加一个新的子节点，`父元素.appendChild(子节点)`

`insertBefore()` 在指定的子节点前插入新的子节点，`父节点.insertBefore("要插入的子节点","指定的子节点")`

`createElement()` 创建元素节点，需要一个标签名作为参数，将会根据该标签名创建元素节点对象，并将创建好的对象作为返回值返回

`createTextNode()` 创建文本节点，需要一个文本内容作为参数，将会根据该内容创建文本节点，并将新的节点返回

`createAttribute()` 创建属性节点

删：

`removeChild()` 删除子节点，`父节点.removeChild(子节点)`--->**`子节点.parentNode.removeChild(子节点)`**

改：

`replaceChild()` 使用指定的子节点替换已有子节点，`父节点.replaceChild(新节点,旧节点)`

`setAttribute()` 把指定属性设置或修改为指定的值

`innerHTML` 用于获取元素内部的 HTML 代码，对于自结束标签，这个属性没有意义

如果要读取元素节点属性，可以直接使用`元素.属性名`，例如 `元素.id`、`元素.name`、`元素.value`，注意 class 属性不能采用这种方式，读取 class 属性时需要使用 `元素.className`

`innerText` 这个属性可以获取到元素内部的文本内容，和 innerHTML 类似，不同的是它会自动将 html 去除

可以使用 `innerHTML` 完成 DOM 的增删改操作

练习：

1、城市节点修改

![](https://cdn.wallleap.cn/img/pic/illustration/20200814113432.png)

```html
<style>
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  body {
    width: 800px;
    margin-left: auto;
    margin-right: auto;
  }
  button {
    width: 300px;
    margin-bottom: 10px;
  }
  #btnList {
    float:left;
  }
  #total{
    width: 450px;
    float:left;
  }
  ul{
    list-style-type: none;
    margin: 0px;
    padding: 0px;
  }
  .inner li{
    border-style: solid;
    border-width: 1px;
    padding: 5px;
    margin: 5px;
    background-color: #99ff99;
    float:left;
  }
  .inner{
    width:400px;
    border-style: solid;
    border-width: 1px;
    margin-bottom: 10px;
    padding: 10px;
    float: left;
  }
</style>
<div id="total">
  <div class="inner">
    <p>
      你喜欢哪个城市?
    </p>
    <ul id="city">
      <li id="bj">北京</li>
      <li>上海</li>
      <li>东京</li>
      <li>首尔</li>
    </ul>
  </div>
</div>
<div id="btnList">
  <div><button id="btn01">创建一个"广州"节点,添加到#city下</button></div>
  <div><button id="btn02">将"广州"节点插入到#bj前面</button></div>
  <div><button id="btn03">使用"广州"节点替换#bj节点</button></div>
  <div><button id="btn04">删除#bj节点</button></div>
  <div><button id="btn05">读取#city内的HTML代码</button></div>
  <div><button id="btn06">设置#bj内的HTML代码</button></div>
  <div><button id="btn07">将HTML代码"广州"节点,添加到#city下</button></div>
</div>
<script>
  function myClick(element, fun){
    var btn = document.getElementById(element)
    btn.onclick = fun
  }
  // 创建一个"广州"节点,添加到#city下
  myClick("btn01", function(){
    // 创建
    var li = document.createElement("li")
    var gzText = document.createTextNode("广州")
    // 插入
    // li.appendChild(gzText)
    li.innerHTML = "广州"
    city.appendChild(li)
  })
  // 将"广州"节点插入到#bj前面
  myClick("btn02", function(){
    // 创建
    var li = document.createElement("li")
    var gzText = document.createTextNode("广州")
    // 插入
    li.appendChild(gzText)
    city.insertBefore(li,bj)
  })
  // 使用"广州"节点替换#bj节点
  myClick("btn03", function(){
    // 创建
    var li = document.createElement("li")
    var gzText = document.createTextNode("广州")
    // 插入
    li.appendChild(gzText)
    city.replaceChild(li,bj)
  })
  // 删除#bj节点
  myClick("btn04", function(){
    // city.removeChild(bj)
    bj.parentNode.removeChild(bj)
  })
  // 读取#city内的HTML代码
  myClick("btn05", function(){
    alert(city.innerHTML)
  })
  // 设置#bj内的HTML代码
  myClick("btn06", function(){
    bj.innerHTML = "北平"
  })
  // 创建一个"广州"节点,添加到#city下
  myClick("btn07", function(){
    city.innerHTML += "<li>广州</>"
  })
</script>
```

2、员工记录

![](https://cdn.wallleap.cn/img/pic/illustration/20200814112400.png)

HTML 和 CSS 部分

```html
<style>
  #total {
    width: 450px;
    margin-left: auto;
    margin-right: auto;
  }
  ul {
    list-style-type: none;
  }
  li {
    border-style: solid;
    border-width: 1px;
    padding: 5px;
    margin: 5px;
    background-color: #99ff99;
    float: left;
  }
  .inner {
    width: 400px;
    border-style: solid;
    border-width: 1px;
    margin: 10px;
    padding: 10px;
    float: left;
  }
  #employeeTable {
    border-spacing: 1px;
    background-color: black;
    margin: 80px auto 10px auto;
  }
  th,td {
    background-color: white;
  }
  #formDiv {
    width: 250px;
    border-style: solid;
    border-width: 1px;
    margin: 50px auto 10px auto;
    padding: 10px;
  }
  #formDiv input {
    width: 100%;
  }
  .word {
    width: 40px;
  }
  .inp {
    width: 200px;
  }
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
    <!-- <td><a href="javascript:;">Delete</a></td> -->
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
      <td class="word">name: </td>
      <td class="inp">
        <input type="text" name="empName" id="empName" />
      </td>
    </tr>
    <tr>
      <td class="word">email: </td>
      <td class="inp">
        <input type="text" name="email" id="email" />
      </td>
    </tr>
    <tr>
      <td class="word">salary: </td>
      <td class="inp">
        <input type="text" name="salary" id="salary" />
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

取消 a 的默认行为

```javascript
<a href="javascript:;"></a>
a.onclick=function(){
  return false
}
```

其他取消默认行为的方法

```js
// 1. return false
// 2. e.preventDefault()
// 3. e.returnValue = false
```

for 循环会在页面加载完成之后立即执行，而响应函数会在超链接被点击时才执行，等它执行，循环已经结束了

```javascript
var allA = document.getElementsByTagName("a")
for(var i=0; i<allA.length; i++){
  allA[i].onclick = function(){
    alert(i) // 一直是3
    return false
  }
}
```

可以用 this 来解决，添加之后删除，由于绑定删除是之前的，因此需要单独绑定

删除和添加员工

```html
<script>
  /* 删除员工 */
  var allA = document.getElementsByTagName("a")
  for(var i=0; i<allA.length; i++){
    allA[i].onclick = function(){
      var tr = this.parentNode.parentNode
      // var name = tr.getElementsByTagName("td")[0].innerText
      var name = tr.children[0].innerHTML
      // alert("确认删除吗？")
      /* window对象中的方法，找到confirm，这是用于弹出一个带有确认和取消按钮的提示框，字符串(提示文字)作为参数，点击确认返回true，点击取消返回false */
      var flag = confirm("确认删除" +name+ "吗？") // firstChild会找第一个节点，空格也是
      if(flag){
        tr.parentNode.removeChild(tr)
      }
      // 取消默认行为
      return false
    }
  }
  /* 添加员工 */
  addEmpButton.onclick = function(){
    var name = document.getElementById("empName").value
    var email = document.getElementById("email").value
    var salary = document.getElementById("salary").value
    // console.log(name,email,salary)
    /*
    <tr>
      <td>Bob</td>
      <td>bob@tom.com</td>
      <td>10000</td>
      <td><a href="deleteEmp?id=003">Delete</a></td>
    </tr>
    */
    var tr = document.createElement("tr")
    var nameTd = document.createElement("td")
    var emailTd = document.createElement("td")
    var salaryTd = document.createElement("td")
    var aTd = document.createElement("td")
    var a = document.createElement("a")
    // 文本节点
    var nameText = document.createTextNode(name)
    var emailText = document.createTextNode(email)
    var salaryText = document.createTextNode(salary)
    var delText = document.createTextNode("Delete")
    // 将文本插入到td中
    nameTd.appendChild(nameText)
    emailTd.appendChild(emailText)
    salaryTd.appendChild(salaryText)
    a.appendChild(delText)
    a.href = "javascript:;"
    a.onclick = function(){
      var tr = this.parentNode.parentNode
      var name = tr.children[0].innerHTML
      var flag = confirm("确认删除" +name+ "吗？")
      if(flag){
        tr.parentNode.removeChild(tr)
      }
      return false
    }
    aTd.appendChild(a)
    // 将td添加到tr中
    tr.appendChild(nameTd)
    tr.appendChild(emailTd)
    tr.appendChild(salaryTd)
    tr.appendChild(aTd)
    // 插入到table
    // employeeTable.appendChild(tr) // 事实上tr在tbody中
    employeeTable.getElementsByTagName("tbody")[0].appendChild(tr)
  }
</script>
```

由于删除的有相同代码，可以提出来

```javascript
function delA(){
  var tr = this.parentNode.parentNode
  // var name = tr.getElementsByTagName("td")[0].innerText
  var name = tr.children[0].innerHTML
  // alert("确认删除吗？")
  /* window对象中的方法，找到confirm，这是用于弹出一个带有确认和取消按钮的提示框，字符串(提示文字)作为参数，点击确认返回true，点击取消返回false */
  var flag = confirm("确认删除" +name+ "吗？") // firstChild会找第一个节点，空格也是
  if(flag){
    tr.parentNode.removeChild(tr)
  }
  // 取消默认行为
  return false
}
删除员工中
allA[i].onclick = delA
添加员工中
a.onclick = delA
```

增加的使用 appendChild 和 innerHTML 配合更简单一点

```javascript
/* 添加员工 */
addEmpButton.onclick = function(){
  var name = document.getElementById("empName").value
  var email = document.getElementById("email").value
  var salary = document.getElementById("salary").value
  
  var tr = document.createElement("tr")
  tr.innerHTML = "<td>"+name+"</td>"+
                "<td>"+email+"</td>"+
                "<td>"+salary+"</td>"+
                "<td><a href='javascript:;'>Delete</a></td>"
  var a = tr.getElementsByTagName("a")[0]
  a.onclick = delA
  var tbody = employeeTable.getElementsByTagName("tbody")[0]
  tbody.appendChild(tr)
  // tbody.innerHTML += tr // 这样就不太合适了，会影响前面已有的
}
```

### 6、DOM 操作 CSS

通过 js 修改元素的样式

- 语法：`元素.style.样式名=样式值`

- 注意：如果 CSS 的样式名中含有`-`，这种名称在 js 中是不合法的，需要将这种样式名修改为驼峰命名，去掉`-`，然后将`-`后的字母大写

```css
var box1 = document.getElementById("box1")
var btn01 = document.getElementById("btn01")
btn01.onclick = function(){
  // 修改box1的宽度
  box1.style.width = "300px"
  // 修改背景颜色
  box1.style.backgroundColor = "yellow"
}
```

- 通过 style 属性设置的样式都是内联样式，而内联样式有较高的优先级，所以通过 js 修改的样式往往会立即显示；但如果在样式中写了 `!important`，则此时样式会有最高的优先级，即使通过 js 也不能覆盖该样式，此时将会导致 js 修改样式失败，所以在写 CSS 样式的时候尽量不要加 `!important`

js 读取样式

- 语法：`元素.style.样式名`

```javascript
var btn02 = document.getElementById("btn02")
btn02.onclick = function(){
  // 读取box1的样式
  alert(box1.style.height, box1.style.width)
}
```

- 通过 style 属性设置和读取的都是内联样式，无法读取样式表中的样式

js 获取当前显示的样式

- 语法：`元素.currentStyle.样式`
- 它可以用来读取当前元素正在显示的样式，如果当前元素没有设置该样式，则获取它的默认值

```javascript
window.onload = function(){
  btn01.onclick = function(){
    alert(box1.currentStyle.width)
    alert(box1.currentStyle.backgroundColor)
  }
}
```

- currentStyle 只有 IE 浏览器支持，其他的浏览器都不支持

在其他浏览器中可以使用 `getComputedStyle()` 这个方法来获取元素当前的样式，这个方法是 window 的方法，可以直接使用

需要两个参数

- 第一个：要获取样式的元素

- 第二个：可以传递一个伪元素，一般都传 null

这个方法会返回一个对象，对象中封装了当前元素对应的样式

可以通过`对象.样式名`来读取样式，如果获取的样式没有设置，则会获取到真实的值，而不是默认值。比如：没有设置 width，它不会获取到 auto，而是一个长度

这个方法不支持IE8及以下的浏览器

```javascript
// var obj = getComputedStyle(box1, null)
alert(getComputedStyle(box1,null).backgroundColor)
```

通过 currentStyle 和 getComputedStyle() 读取到的样式都是只读的，不能修改，如果要修改必须通过 style 属性

```javascript
/* 定义一个函数，用来获取指定元素的当前的样式
* 参数：
*  obj 要获取样式的元素
*  name 要获取的样式名
*/
/* function getStyle(obj, name){
 if(window.getComputedStyle){
    // 正常浏览器的方式，具有getComputedStyle()方法
    return getComputedStyle(obj, null)[name]
  }else{
    // IE8的方式，没有getComputedStyle()方法
    return obj.currentStyle[name]
  }
} */
/* // 不建议用下面这个 IE11会优先使用current，虽然都能用
function getStyle(obj, name){
 if(obj.currentStyle){
    return obj.currentStyle[name]
  }else{
    return getComputedStyle(obj, null)[name]
  }
}*/
function getStyle(obj, name){
 return window.getComputedStyle ? getComputedStyle(obj, null)[name] : obj.currentStyle[name]
}
```

clientWidth、clientHeight

这两个属性可以获取元素的可见宽度和高度

这些属性都是不带px的，返回都是一个数字，可以直接进行计算

会获取元素宽度和高度，包括内容区和内边距

这些属性都是只读的，不能修改

```javascript
btn01.onclick = function(){
  alert(box1.clientWidth)
}
```

offsetWidth、offsetHeight

获取元素的整个的宽度和高度，包括内容区、内边距和边框

```javascript
alert(box1.offsetWidth)
```

offsetParent

可以用来获取当前元素的定位父元素

会获取到离当前元素最近的开启了定位的祖先元素，如果所有的祖先元素都没开启定位，则返回body

```javascript
var op = box1.offsetParent
alert(op.id)
```

offsetLeft

当前元素相对于其定位父元素的水平偏移量

offsetTop

当前元素相对于其定位父元素的垂直偏移量

设置了 `overflow:auto;`，高度和长度都太大，会出现滚动条

scrollWidth、scrollHeight

可以获取元素整个滚动区域的宽、高度

```javascript
alert(box4.clientHeight, box4.scrollHeight)
```

scrollLeft

可以获取水平滚动条滚动的距离

scrollTop

可以获取垂直滚动条滚动的距离

```javascript
alert(box4.scrollLeft)
alert(box4.scrollTop)
```

### 7、其他事件

onscroll

该事件会在元素的滚动条滚动时触发

阅读协议：

![](https://cdn.wallleap.cn/img/pic/illustration/20200814143326.png)

```html
<style type="text/css">
  #info{
    width: 300px;
    height: 500px;
    background-color: #bfa;
    overflow: auto;
  }
</style>
<h3>欢迎亲爱的用户注册</h3>
<p id="info">
  Lorem ipsum, dolor sit amet consectetur adipisicing elit. Amet, doloremque. Ea tempora consequuntur mollitia corrupti. Commodi iusto ducimus deleniti, ratione quam, harum fugit autem omnis nihil dolorem fuga, sequi eligendi excepturi expedita tenetur accusamus! In eaque voluptate inventore commodi a? Unde provident tempore, dolorem deserunt numquam reiciendis eum vero. Aut ipsum, dolorem doloribus nemo molestiae exercitationem deserunt amet quod voluptatibus expedita ex architecto, cum culpa fuga dolore. Ratione perspiciatis soluta, facilis temporibus, error laudantium nostrum facere doloremque natus sint cum esse incidunt officiis eum officia velit ab illo perferendis distinctio enim voluptas tempore? Reiciendis, itaque cupiditate? Totam mollitia tenetur labore neque possimus vero porro modi iure atque reiciendis fugit iste, omnis, magnam rem animi adipisci tempore repellendus iusto fugiat voluptatum consequuntur excepturi. Similique vel praesentium quo quam at. Veniam, neque nostrum, minima ex assumenda perferendis aliquam cum, molestiae culpa repellat explicabo? Sapiente, placeat eligendi voluptas velit beatae accusantium minus culpa reprehenderit similique, corporis eum neque tempore expedita iure, adipisci molestias. Quidem, sapiente temporibus deserunt nobis architecto incidunt ipsam. Provident distinctio accusamus quaerat inventore ex, omnis excepturi temporibus quod alias possimus maxime nesciunt odio aperiam error quia? Neque rem eos a perferendis repellat repudiandae reprehenderit reiciendis molestiae ullam! Nihil, illum odio!
</p>
<!-- 如果为表单项添加disabled="disabled" 则表单项将变成不可用的状态 -->
<input type="checkbox" disabled="disabled" />我已仔细阅读协议，一定遵守
<input type="submit" value="注册" disabled="disabled" />
<script type="text/javascript">
  window.onload = function(){
    /*
      * 当垂直滚动条滚动到底时使表单项可用
      */
    //获取id为info的p元素
    var info = document.getElementById("info")
    //获取两个表单项
    var inputs = document.getElementsByTagName("input")
    //为info绑定一个滚动条滚动的事件
    info.onscroll = function(){
      //检查垂直滚动条是否滚动到底
      if(info.scrollHeight - info.scrollTop == info.clientHeight){
        //滚动条滚动到底，使表单项可用
        /*
          * disabled属性可以设置一个元素是否禁用，
          *  如果设置为true，则元素禁用
          *  如果设置为false，则元素可用
          */
        inputs[0].disabled = false
        inputs[0].onclick = function(){ // 只有到底了才能能点复选框，点了复选框才能点按钮
          if(inputs[0].checked){
            inputs[1].disabled = false
          }
        }
      }
    }
  }
</script>
```

onmousemove

该事件会在鼠标在元素中移动时被触发

事件对象：当事件的响应函数被触发时，浏览器每次都会将一个事件对象作为实参传递进响应函数，在事件对象中封装了当前事件相关的一切信息。比如，鼠标坐标、键盘哪个按键被按下、鼠标滚轮滚动的方向……

```html
<style>
  #areaDiv{
    position: relative;
    width: 100vw;
    height: 100vh;
    background-color: rgba(0,0,0,.2);
  }
  #showMsg{
    position: absolute;
    width: 160px;
    height: 20px;
    line-height: 20px;
    text-align: left;
    background-color: rgba(0,0,0,.5);
    left: 0;
    top: 0;
  }
</style>
<div id="areaDiv"></div>
<div id="showMsg"></div>
<script>
  /* 当鼠标在areaDiv中移动时，在showMsg中来显示鼠标的坐标 */
  areaDiv.onmousemove = function(event){
    /*
     * clientX可以获取鼠标指针的水平坐标
     * clientY可以获取鼠标指针的垂直坐标
    */
    var x = event.clientX
    var y = event.clientY
    showMsg.innerHTML = "(x = " + x + ", y = " + y +")"
    showMsg.style.left = x + 10 + "px"
    showMsg.style.top = y + 10 + "px"
  }
</script>
```

在IE8中，响应函数被触发时，浏览器不会传递事件对象，在IE8及以下的浏览器中，是将事件对象作为window对象的属性保存的

```javascript
/*var x = window.event.clientX
var y = window.event.clientY*/
/*if(!event){
  event = window.event
}*/
envent = event || window.event
```

上面也涉及到了跟随鼠标的，下面来详细说一下

```html
<style type="text/css">
  #box1{
    width: 100px;
    height: 100px;
    background-color: red;
    position: absolute;
  }
</style>
<script type="text/javascript">
  window.onload = function(){
    /*
     * 使div可以跟随鼠标移动
     */
    //绑定鼠标移动事件
    document.onmousemove = function(event){  
      //解决兼容问题
      event = event || window.event
      //获取滚动条滚动的距离
      /*
       * chrome认为浏览器的滚动条是body的，可以通过body.scrollTop来获取
       * 火狐等浏览器认为浏览器的滚动条是html的，
       */
      var st = document.body.scrollTop || document.documentElement.scrollTop
      var sl = document.body.scrollLeft || document.documentElement.scrollLeft
      //var st = document.documentElement.scrollTop;
      //获取到鼠标的坐标
      /*
       * clientX和clientY
       *  用于获取鼠标在当前的可见窗口的坐标
       * div的偏移量，是相对于整个页面的
       * 
       * pageX和pageY可以获取鼠标相对于当前页面的坐标
       *  但是这个两个属性在IE8中不支持，所以如果需要兼容IE8，则不要使用
       */
      var left = event.clientX
      var　top = event.clientY
      
      //设置div的偏移量
      box1.style.left = left + sl + "px"
      box1.style.top = top + st + "px"
    };    
  };
</script>
<body style="height: 1000px;width: 2000px;">
  <div id="box1"></div>
</body>
```

ontouchstart

该事件会在手指触摸到屏幕时被触发

ontouchmove

该事件会在手指在屏幕上移动时被触发

ontouchend

该事件会在手指离开屏幕时被触发

```html
<style type="text/css">
  #box1{
    width: 100px;
    height: 100px;
    background-color: red;
    position: absolute;
  }
</style>
<script type="text/javascript">
  window.onload = function(){
    /*
     * 使div可以跟随鼠标移动
     */
    //绑定鼠标移动事件
    document.ontouchmove = function(event){  
      //解决兼容问题
      event = event || window.event
      //获取滚动条滚动的距离
      /*
       * chrome认为浏览器的滚动条是body的，可以通过body.scrollTop来获取
       * 火狐等浏览器认为浏览器的滚动条是html的，
       */
      var st = document.body.scrollTop || document.documentElement.scrollTop
      var sl = document.body.scrollLeft || document.documentElement.scrollLeft
      //var st = document.documentElement.scrollTop;
      //获取到鼠标的坐标
      /*
       * clientX和clientY
       *  用于获取鼠标在当前的可见窗口的坐标
       * div的偏移量，是相对于整个页面的
       * 
       * pageX和pageY可以获取鼠标相对于当前页面的坐标
       *  但是这个两个属性在IE8中不支持，所以如果需要兼容IE8，则不要使用
       */
      var left = event.clientX
      var　top = event.clientY
      
      //设置div的偏移量
      box1.style.left = left + sl + "px"
      box1.style.top = top + st + "px"
    };    
  };
</script>
```

### 8、事件的冒泡（Bubble）

![](https://cdn.wallleap.cn/img/pic/illustration/20200814152101.png)

所谓的冒泡指的就是事件的向上传导，当后代元素上的事件被触发时，其祖先元素的相同事件也会被触发

```javascript
// body>#box1>span#s1
s1.onclick = function(){
  alert("我是span的单击响应函数")
}
box1.onclick = function(){
  alert("我是div的单击响应函数")
}
document.body.onclick = function(){
  alert("我是body的单击响应函数")
}
```

点一下 span，span、div、body 的单击响应函数都会被触发

在开发中大部分情况冒泡都是有用的，如果不希望发生事件冒泡可以通过事件对象来取消冒泡

```javascript
s1.onclick = function(e){
  event = e || window.event
  alert("我是span的单击响应函数")
  // 取消冒泡，可以将事件对象的cancelBubble设置为true，即可取消冒泡
  event.cancelBubble = true
}
box1.onclick = function(e){
  e = e || window.event
  alert("我是div的单击响应函数")
  e.cancelBubble = true
}
```

### 9、事件的委派

```html
<script type="text/javascript">
  window.onload = function(){
    var u1 = document.getElementById("u1")
    //点击按钮以后添加超链接
    var btn01 = document.getElementById("btn01")
    btn01.onclick = function(){
      //创建一个li
      var li = document.createElement("li")
      li.innerHTML = "<a href='javascript:;' class='link'>新建的超链接</a>";
      //将li添加到ul中
      u1.appendChild(li)
    }
    /*
      * 为每一个超链接都绑定一个单击响应函数
      * 这里我们为每一个超链接都绑定了一个单击响应函数，这种操作比较麻烦，而且这些操作只能为已有的超链接设置事件，而新添加的超链接必须重新绑定
      */
    //获取所有的a
    var allA = document.getElementsByTagName("a")
      //遍历
      for(var i=0 ; i<allA.length ; i++){
        allA[i].onclick = function(){
          alert("我是a的单击响应函数！！！")
      }
    }
  }
</script>
<button id="btn01">添加超链接</button>
<ul id="u1" style="background-color: #bfa;">
  <li>
    <p>我是p元素</p>
  </li>
  <li><a href="javascript:;" class="link">超链接一</a></li>
  <li><a href="javascript:;" class="link">超链接二</a></li>
  <li><a href="javascript:;" class="link">超链接三</a></li>
</ul>
```

事件的委派

指将事件统一绑定给元素的共同的祖先元素，这样当后代元素上的事件触发时，会一直冒泡到祖先元素，从而通过祖先元素的响应函数来处理事件。

事件委派是利用了冒泡，通过委派可以减少事件绑定的次数，提高程序的性能

```javascript
/*
* 我们希望，只绑定一次事件，即可应用到多个的元素上，即使元素是后添加的
* 我们可以尝试将其绑定给元素的共同的祖先元素
*/
//为ul绑定一个单击响应函数
u1.onclick = function(event){
  event = event || window.event
  /*
   * target
   *  - event中的target表示的触发事件的对象
  */
  //alert(event.target);
  //如果触发事件的对象是我们期望的元素，则执行否则不执行
  if(event.target.className == "link"){
    alert("我是ul的单击响应函数")
  }  
}
```

### 10、事件的绑定

使用 `对象.事件 = 函数` 的形式绑定响应函数，它只能同时为一个元素的一个事件绑定一个响应函数，能绑定多个，如果绑定了多个，则后边会覆盖掉前边的

```javascript
/*
* 点击按钮以后弹出一个内容
*/
//获取按钮对象
var btn01 = document.getElementById("btn01")
//为btn01绑定一个单击响应函数
btn01.onclick = function(){
  alert(1)
}
//为btn01绑定第二个响应函数
btn01.onclick = function(){
  alert(2)
}
```

**`addEventListener()`**

- 通过这个方法也可以为元素绑定响应函数

- 参数：

1. 事件的字符串，不要 on

2. 回调函数，当事件触发时该函数会被调用

3. 是否在捕获阶段触发事件，需要一个布尔值，一般都传 false

使用 addEventListener() 可以同时为一个元素的相同事件同时绑定多个响应函数，这样当事件被触发时，响应函数将会按照函数的绑定顺序执行

这个方法不支持 IE 8 及以下的浏览器

```javascript
btn01.addEventListener("click",function(){
  alert(1);
},false);
btn01.addEventListener("click",function(){
  alert(2);
},false);
btn01.addEventListener("click",function(){
  alert(3);
},false);
```

`attachEvent()`

- 在 IE 8 中可以使用 attachEvent() 来绑定事件

- 参数：
  1. 事件的字符串，要 on
  2. 回调函数

- 这个方法也可以同时为一个事件绑定多个处理函数，不同的是它是后绑定先执行，执行顺序和 addEventListener() 相反（顺序实在有要求可以反着写）

```javascript
btn01.attachEvent("onclick",function(){
  alert(1)
})
btn01.attachEvent("onclick",function(){
  alert(2)
})
btn01.attachEvent("onclick",function(){
  alert(3)
})
btn01.addEventListener("click",function(){
  alert(this)
},false)
btn01.attachEvent("onclick",function(){
  alert(this)
})
```

定义一个函数，用来为指定元素绑定响应函数

- addEventListener() 中的 this，是绑定事件的对象

- attachEvent() 中的 this，是 window

需要统一两个方法 this

```javascript
 /*
  ** 参数：
  **  obj 要绑定事件的对象
  **  eventStr 事件的字符串(不要on)
  **  callback 回调函数
  **/
function bind(obj , eventStr , callback){
  if(obj.addEventListener){
    //大部分浏览器兼容的方式
    obj.addEventListener(eventStr , callback , false)
  }else{
    /*
      * this是谁由调用方式决定
      * callback.call(obj)
      */
    //IE8及以下
    obj.attachEvent("on"+eventStr , function(){
      //在匿名函数中调用回调函数
      callback.call(obj)
    })
  }
}
// 借助function由浏览器调用变成自己调用，就能使用call
// 传入实参
bind(btn01 , "click" , function(){
  alert(this);
})
```

### 11、事件的传播

关于事件的传播网景公司和微软公司有不同的理解

- 微软公司认为事件应该是由内向外传播，也就是当事件触发时，应该先触发当前元素上的事件，然后再向元素的祖先元素上传播，也就是说事件应该在冒泡阶段执行
- 网景公司认为事件应该是由外向内传播的，也就是当前事件触发时，应该先触发当前元素的最外层的祖先元素的事件，然后再向内传播给后代元素

![事件传播](https://cdn.wallleap.cn/img/pic/illustration/20200814155622.png)

W3C综合了两个公司的方案，将事件传播分为了三个阶段：

1. 捕获阶段——在捕获阶段时从最外层的祖先元素，向目标元素进行事件的捕获，但是默认此时不会触发事件
2. 目标阶段——事件捕获到目标元素，捕获结果开始在目标元素上触发事件
3. 冒泡阶段——事件从目标元素向它的祖先元素传递，一次触发祖先元素上的事件

![W3C事件传播](https://cdn.wallleap.cn/img/pic/illustration/20200814160425.png)

如果希望在捕获阶段就触发事件，可以在 addEventListener() 的第三个参数设置为 true，一般情况下我们不会希望在捕获阶段触发事件，所以这个参数一般都是 false

```javascript
obj.addEventListener(eventStr,callback,true)
```

IE 8 及以下的浏览器中没有捕获阶段

### 12、鼠标事件

onmousedown、onmousemove、onmouseup

拖拽

还记得 H5 新添加的那个拖拽 API 嘛，那个非常好用的对吧，可是在 H5 还没出来的时候咋实现的呢

```html
<style>
  #box1{
    width: 100px;
    height: 100px;
    background-color: red;
    position: absolute;
  }
  #box2{
    width: 100px;
    height: 100px;
    background-color: yellow;
    position: absolute;
    left: 200px;
    top: 200px;
  }
</style>
<div id="box1"></div>
<div id="box2"></div>
<script type="text/javascript">
  window.onload = function(){
    /*
    * 拖拽box1元素
    *  - 拖拽的流程
    *   1.当鼠标在被拖拽元素上按下时，开始拖拽  onmousedown
    *   2.当鼠标移动时被拖拽元素跟随鼠标移动 onmousemove
    *   3.当鼠标松开时，被拖拽元素固定在当前位置 onmouseup
    */
    //获取box1
    var box1 = document.getElementById("box1")
    //为box1绑定一个鼠标按下事件
    //当鼠标在被拖拽元素上按下时，开始拖拽  onmousedown
    box1.onmousedown = function(event){
      event = event || window.event
      //div的偏移量 鼠标.clentX - 元素.offsetLeft
      //div的偏移量 鼠标.clentY - 元素.offsetTop
      var ol = event.clientX - box1.offsetLeft
      var ot = event.clientY - box1.offsetTop
      //为document绑定一个onmousemove事件
      document.onmousemove = function(event){
        event = event || window.event
        //当鼠标移动时被拖拽元素跟随鼠标移动 onmousemove
        //获取鼠标的坐标
        var left = event.clientX - ol
        var top = event.clientY - ot
        //修改box1的位置
        box1.style.left = left+"px"
        box1.style.top = top+"px"
      }
      //为document绑定一个鼠标松开事件
      document.onmouseup = function(){
        //当鼠标松开时，被拖拽元素固定在当前位置 onmouseup
        //取消document的onmousemove事件(移到同样是`position: absolute`的另一个盒子上时，会被另一个覆盖，松开鼠标会触发另一个盒子的onmouseup，因此需要给document绑定)
        document.onmousemove = null
        //取消document的onmouseup事件
        document.onmouseup = null
      }
    }
  }
</script>
```

onmouseup 使用过了直接就不需要了，可以直接取消，这样 onmouseup 就变成一次性事件了。

点击 box 光标会变到鼠标左上角，需要求出 box 的偏移量，在按下时求出，移动时减去这个偏移量就是鼠标所处的位置了（如果有滚动条还要进行处理）

```javascript
box1.onmousedown = function(event){
 /* 设置box1捕获所有鼠标按下的事件
  * setCapture()
  *  - 当调用一个元素的setCapture()方法后，这个元素将会把下一次所有的鼠标按下相关的事件捕获到自己身上
  *  - 只有IE支持，但是在火狐中调用时不会报错，
  *   而如果使用chrome调用，会报错
  */
  // 只需要设置一次，不需要一直捕获，在up中释放
  // 做判断，有就用(IE)，没有就不用
 /*if(box1.setCapture){
  box1.setCapture()
 }*/
 box1.setCapture && box1.setCapture()
 event = event || window.event
 //div的偏移量 鼠标.clentX - 元素.offsetLeft
 //div的偏移量 鼠标.clentY - 元素.offsetTop
 var ol = event.clientX - box1.offsetLeft
 var ot = event.clientY - box1.offsetTop
 //为document绑定一个onmousemove事件
 document.onmousemove = function(event){
  event = event || window.event
  //当鼠标移动时被拖拽元素跟随鼠标移动 onmousemove
  //获取鼠标的坐标
  var left = event.clientX - ol
  var top = event.clientY - ot
  //修改box1的位置
  box1.style.left = left+"px"
  box1.style.top = top+"px"
 }
 //为document绑定一个鼠标松开事件
 document.onmouseup = function(){
  //当鼠标松开时，被拖拽元素固定在当前位置 onmouseup
  //取消document的onmousemove事件
  document.onmousemove = null
  //取消document的onmouseup事件
  document.onmouseup = null
  //当鼠标松开时，取消对事件的捕获
  box1.releaseCapture && box1.releaseCapture()
 }
 /*
  * 当我们拖拽一个网页中的内容时，浏览器会默认去搜索引擎中搜索内容，
  *  此时会导致拖拽功能的异常，这个是浏览器提供的默认行为，
  *  如果不希望发生这个行为，则可以通过return false来取消默认行为
  * 但是这招对IE8不起作用(IE8用capture，其他用这个)
  */
 return false
}
```

封装

```javascript
/*
* 提取一个专门用来设置拖拽的函数
* 参数：开启拖拽的元素
*/
function drag(obj){
//当鼠标在被拖拽元素上按下时，开始拖拽  onmousedown
obj.onmousedown = function(event){
 obj.setCapture && obj.setCapture()
 event = event || window.event
 var ol = event.clientX - obj.offsetLeft
 var ot = event.clientY - obj.offsetTop
 //为document绑定一个onmousemove事件
 document.onmousemove = function(event){
  event = event || window.event
  var left = event.clientX - ol
  var top = event.clientY - ot
  obj.style.left = left+"px"
  obj.style.top = top+"px"
  
 }
 //为document绑定一个鼠标松开事件
 document.onmouseup = function(){
  //当鼠标松开时，被拖拽元素固定在当前位置 onmouseup
  //取消document的onmousemove事件
  document.onmousemove = null
  //取消document的onmouseup事件
  document.onmouseup = null
  //当鼠标松开时，取消对事件的捕获
  obj.releaseCapture && obj.releaseCapture()
 }
 return false
}

var box1 = document.getElementById("box1")
var box2 = document.getElementById("box2")
var img1 = document.getElementById("img1")
//开启box1的拖拽
drag(box1)
//开启box2的
drag(box2)
drag(img1)  // <img src="img/an.jpg" id="img1" style="position: absolute;"/>
```

鼠标滚轮事件

onmousewheel（火狐用 DOMMouseScroll）

```javascript
<style type="text/css">
  #box1{
    width: 100px;
    height: 100px;
    background-color: red;
  }
</style>
<script type="text/javascript">
  window.onload = function(){
    //获取id为box1的div
    var box1 = document.getElementById("box1")
    //为box1绑定一个鼠标滚轮滚动的事件
    /*
      * onmousewheel鼠标滚轮滚动的事件，会在滚轮滚动时触发，
      *  但是火狐不支持该属性
      * 在火狐中需要使用 DOMMouseScroll 来绑定滚动事件
      *  注意该事件需要通过addEventListener()函数来绑定
      */
    box1.onmousewheel = function(event){
      event = event || window.event;
      //event.wheelDelta 可以获取鼠标滚轮滚动的方向
      //向上滚 120   向下滚 -120
      //wheelDelta这个值我们不看大小，只看正负
      //alert(event.wheelDelta); 
      //wheelDelta这个属性火狐中不支持
      //在火狐中使用event.detail来获取滚动的方向
      //向上滚 -3  向下滚 3
      //alert(event.detail);
      /*
        * 当鼠标滚轮向下滚动时，box1变长
        *  当滚轮向上滚动时，box1变短
        */
      //判断鼠标滚轮滚动的方向
      if(event.wheelDelta > 0 || event.detail < 0){
        //向上滚，box1变短
        box1.style.height = box1.clientHeight - 10 + "px"
      }else{
        //向下滚，box1变长
        box1.style.height = box1.clientHeight + 10 + "px"
      /*
        * 使用addEventListener()方法绑定响应函数，取消默认行为时不能使用return false
        * 需要使用event来取消默认行为event.preventDefault();
        * 但是IE8不支持event.preventDefault();这个玩意，如果直接调用会报错
        */
      event.preventDefault && event.preventDefault()
      /*
        * 当滚轮滚动时，如果浏览器有滚动条，滚动条会随之滚动，
        * 这是浏览器的默认行为，如果不希望发生，则可以取消默认行为
        */
      return false
    }
    //为火狐绑定滚轮事件
    bind(box1,"DOMMouseScroll",box1.onmousewheel)
  }
  function bind(obj , eventStr , callback){
    if(obj.addEventListener){
      //大部分浏览器兼容的方式
      obj.addEventListener(eventStr , callback , false);
    }else{
      /*
        * this是谁由调用方式决定
        * callback.call(obj)
        */
      //IE8及以下
      obj.attachEvent("on"+eventStr , function(){
        //在匿名函数中调用回调函数
        callback.call(obj)
      })
    }
  }
</script>
<body style="height: 2000px;">
<div id="box1"></div>
</body>
```

### 13、键盘事件

onkeydown

- 按键被按下

- 对于 onkeydown 来说如果一直按着某个按键不松手，则事件会一直触发

- 当 onkeydown 连续触发时，第一次和第二次之间会间隔稍微长一点，其他的会非常的快，这种设计是为了防止误操作的发生。

onkeyup
  
- 按键被松开

- 键盘事件一般都会绑定给一些可以获取到焦点的对象或者是 document

可以通过 keyCode 来获取按键的编码

通过它可以判断哪个按键被按下

除了keyCode，事件对象中还提供了几个属性

`altKey` `ctrlKey` `shiftKey`，这个三个用来判断 alt ctrl 和 shift 是否被按下，如果按下则返回 true，否则返回 false

```javascript
window.onload = function(){
  document.onkeydown = function(event){
    event = event || window.event
    /*
  * 可以通过keyCode来获取按键的编码，通过它可以判断哪个按键被按下
  * 除了keyCode，事件对象中还提供了几个属性 altKey、 ctrlKey、shiftKey
  */
    //console.log(event.keyCode)
    //判断一个y是否被按下
    //判断y和ctrl是否同时被按下
    if(event.keyCode === 89 && event.ctrlKey){
      console.log("ctrl和y都被按下了")
    }
  }
  /*document.onkeyup = function(){
   console.log("按键松开了")
 }*/
  //获取input
  var input = document.getElementsByTagName("input")[0] // <input type="text" />
  input.onkeydown = function(event){  
    event = event || window.event
    //console.log(event.keyCode)
    //数字 48 - 57
    //使文本框中不能输入数字
    if(event.keyCode >= 48 && event.keyCode <= 57){
      //在文本框中输入内容，属于onkeydown的默认行为
      //如果在onkeydown中取消了默认行为，则输入的内容，不会出现在文本框中
      return false
    }
  }
}
```

通过按键移动盒子

```html
<style type="text/css">
 #box1{
  width: 100px;
  height: 100px;
  background-color: red;
  position: absolute;
 }
</style>
<script type="text/javascript">
 //使div可以根据不同的方向键向不同的方向移动
 /*
  * 按左键，div向左移
  * 按右键，div向右移
  * ……
  */
 window.onload = function(){
  //为document绑定一个按键按下的事件
  document.onkeydown = function(event){
   event = event || window.event
   //定义一个变量，来表示移动的速度
   var speed = 10
   //当用户按了ctrl以后，速度加快
   if(event.ctrlKey){
    speed = 500
   }
   
   /*
    * 37 左
    * 38 上
    * 39 右
    * 40 下
    */
   switch(event.keyCode){
    case 37
     //alert("向左"); left值减小
     box1.style.left = box1.offsetLeft - speed + "px"
     break
    case 39:
     //alert("向右");
     box1.style.left = box1.offsetLeft + speed + "px"
     break
    case 38:
     //alert("向上");
     box1.style.top = box1.offsetTop - speed + "px"
     break
    case 40:
     //alert("向下");
     box1.style.top = box1.offsetTop + speed + "px"
     break
   }
  }
 }
</script>
<div id="box1"></div>
```

还存在问题：会有卡顿

总结：

JS 中事件可以分为以下几种

- 鼠标事件
  - 点击 click、双击 dblclick、右击 contextmenu
  - 鼠标移入 mouseenter、鼠标移动 mousemove、鼠标移出 mouseleave
  - 拖动 drag、拖动开始 dragstart、拖动结束 dragend
- 键盘事件
  - 按下 keydown、松开 keyup
  - 按键被按下 keypress
- 表单事件
  - 输入 input
  - 获得焦点 focus、失去焦点 blur
  - 提交表单 submit
  - 选择选项 change
  - 重置 reset
  - 选中文本 select
  - 失去选中文本 deselect
  - 复制 copy、剪切 cut、粘贴 paste
  - 撤销 undo、重做 redo
- 窗口事件
  - 加载 load
  - 关闭 unload
  - 改变大小 resize
  - 滚动 scroll
  - 错误 error
- 滚动条事件
  - 滚动 scroll
- BOM事件
- 打印事件
  - 打印 print
- 移动端事件
  - 触摸事件
    - touchstart
    - touchmove
    - touchend
    - touchcancel
- 自定义事件

涉及概念

- 事件对象
- 事件流
- 事件委托
- 事件兼容
- 事件监听
- 事件冒泡
- 事件捕获
- 事件阻止
- 事件取消
- 事件绑定
- 事件解绑

## 四、BOM

BOM (浏览器对象模型)可以使我们通过 js 来操作浏览器

在 BOM 中为我们提供了一组对象，用来完成对浏览器的操作

BOM 对象：

- window——代表的是整个浏览器窗口，同时也是网页中的全局对象
- navigator——代表的是当前浏览器的信息，通过该对象可以识别不同的浏览器
- location——代表当前浏览器的地址栏信息，通过 Location 可以获取地址栏信息，或者操作浏览器跳转网页
- history——代表浏览器的历史记录，可以通过该对象来操作浏览器的而历史记录（由于隐私原因，该对象不能获取到具体的历史记录，只能操作浏览器向前或向后翻页，而且该操作只在当次访问时有效）
- screen——代表用户的屏幕信息，通过该对象可以获取到用户的显示器的相关信息

这些 BOM 对象在浏览器中都是作为 window 对象的属性保存的，可以通过 window 对象来使用，也可以直接使用

```javascript
console.log(window)
// console.log(navigator)
console.log(window.navigator)
console.log(location)
console.log(screen)
```

### 1、Navigator

- 代表的当前浏览器的信息，通过该对象可以来识别不同的浏览器
- 由于历史原因，Navigator 对象中的大部分属性已经不能帮助我们识别浏览器了

| 属性                                                                              | 描述                                           |
| :-------------------------------------------------------------------------------- | :--------------------------------------------- |
| [appCodeName](https://www.w3school.com.cn/jsref/prop_nav_appcodename.asp)         | 返回浏览器的代码名。                           |
| [appMinorVersion](https://www.w3school.com.cn/jsref/prop_nav_appminorversion.asp) | 返回浏览器的次级版本。                         |
| [appName](https://www.w3school.com.cn/jsref/prop_nav_appname.asp)                 | 返回浏览器的名称。                             |
| [appVersion](https://www.w3school.com.cn/jsref/prop_nav_appversion.asp)           | 返回浏览器的平台和版本信息。                   |
| [browserLanguage](https://www.w3school.com.cn/jsref/prop_nav_browserlanguage.asp) | 返回当前浏览器的语言。                         |
| [cookieEnabled](https://www.w3school.com.cn/jsref/prop_nav_cookieenabled.asp)     | 返回指明浏览器中是否启用 cookie 的布尔值。     |
| [cpuClass](https://www.w3school.com.cn/jsref/prop_nav_cpuclass.asp)               | 返回浏览器系统的 CPU 等级。                    |
| [onLine](https://www.w3school.com.cn/jsref/prop_nav_online.asp)                   | 返回指明系统是否处于脱机模式的布尔值。         |
| [platform](https://www.w3school.com.cn/jsref/prop_nav_platform.asp)               | 返回运行浏览器的操作系统平台。                 |
| [systemLanguage](https://www.w3school.com.cn/jsref/prop_nav_systemlanguage.asp)   | 返回 OS 使用的默认语言。                       |
| [userAgent](https://www.w3school.com.cn/jsref/prop_nav_useragent.asp)             | 返回由客户机发送服务器的 user-agent 头部的值。 |
| [userLanguage](https://www.w3school.com.cn/jsref/prop_nav_userlanguage.asp)       | 返回 OS 的自然语言设置。                       |

| 方法                                                                         | 描述                                         |
| :--------------------------------------------------------------------------- | :------------------------------------------- |
| [javaEnabled()](https://www.w3school.com.cn/jsref/met_nav_javaenabled.asp)   | 规定浏览器是否启用 Java。                    |
| [taintEnabled()](https://www.w3school.com.cn/jsref/met_nav_taintenabled.asp) | 规定浏览器是否启用数据污点 (data tainting)。 |

```javascript
alert(navigator.appName)
```

一般我们只会使用 userAgent 来判断浏览器的信息，userAgent 是一个字符串，这个字符串中包含有用来描述浏览器信息的内容，不同的浏览器会有不同的 userAgent

```javascript
console.log(navigator.userAgent)
火狐的userAgent：
"Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:78.0) Gecko/20100101 Firefox/78.0"
Chrome的userAgent：
"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36"
IE11
"Mozilla/5.0 (Windows NT 10.0; WOW64; Trident/7.0; .NET4.0C; .NET4.0E; .NET CLR 2.0.50727; .NET CLR 3.0.30729; .NET CLR 3.5.30729; Tablet PC 2.0; rv:11.0) like Gecko"
IE10
"Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 10.0; WOW64; Trident/7.0; .NET4.0C; .NET4.0E; .NET CLR 2.0.50727; .NET CLR 3.0.30729; .NET CLR 3.5.30729; Tablet PC 2.0)"
IE9
"Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 10.0; WOW64; Trident/7.0; .NET4.0C; .NET4.0E; .NET CLR 2.0.50727; .NET CLR 3.0.30729; .NET CLR 3.5.30729; Tablet PC 2.0)"
IE8
"Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 10.0; WOW64; Trident/7.0; .NET4.0C; .NET4.0E; .NET CLR 2.0.50727; .NET CLR 3.0.30729; .NET CLR 3.5.30729; Tablet PC 2.0)"
```

根据 UA 来判断

```javascript
var ua = navigator.userAgent
console.log(ua)
if(/firefox/i.test(ua)){
  alert("你是火狐")
}else if(/chrome/i.test(ua)){
  alert("你是Chrome")
}else if(/msie/i.test(ua)){
  alert("woc，你是IE")
}
```

如果通过 userAgent 不能判断，还可以通过一些浏览器中特有的对象，来判断浏览器的信息

比如：`ActiveXObject`

```javascript
if("ActiveXObject" in window){
 alert("你是IE，我已经抓住你了~~~");
}else{
 alert("你不是IE~~~");
}

/*alert("ActiveXObject" in window);*/

if(/firefox/i.test(ua)){
  alert("你是火狐")
}else if(/chrome/i.test(ua)){
  alert("你是Chrome")
}else if(/msie/i.test(ua)){
  alert("woc，你是IE")
} else if("ActiveXObject" in window){
 alert("你是IE11，还好");
}
```

### 2、History

History 对象可以用来操作浏览器向前或向后翻页

| 属性                                                            | 描述                              |
| :-------------------------------------------------------------- | :-------------------------------- |
| [length](https://www.w3school.com.cn/jsref/prop_his_length.asp) | 返回浏览器历史列表中的 URL 数量。 |

| 方法                                                               | 描述                                |
| :----------------------------------------------------------------- | :---------------------------------- |
| [back()](https://www.w3school.com.cn/jsref/met_his_back.asp)       | 加载 history 列表中的前一个 URL。   |
| [forward()](https://www.w3school.com.cn/jsref/met_his_forward.asp) | 加载 history 列表中的下一个 URL。   |
| [go()](https://www.w3school.com.cn/jsref/met_his_go.asp)           | 加载 history 列表中的某个具体页面。 |

```javascript
// length属性可以获取到当前访问的链接数量
alert(history.length)
// back()可以用来回退到上一个页面，作用和浏览器的回退按钮一样
history.back()
// forward()可以跳转到下一个页面，作用和浏览器的前进按钮一样
history.forward()
/*
 go()可以用来跳转到指定的页面，需要一个整数作为参数
 * 1：表示向前跳转一个页面，相当于forward()
 * 2：表示向前跳转两个页面
 * -1：表示向后跳转一个页面
 * -2：表示向后跳转 两个页面
*/
history.go(-2)
```

### 3、Location

如果直接打印 location，则可以获取到地址栏中的信息(当前页面的完整路径)

```js
alert(location)
```

如果直接将 location 属性修改为一个完整的路径或相对路径，则我们的页面会自动跳转到该路径，并且会生成响应的历史记录

```js
location = "http://www.baidu.com"
location = "./index.html"
```

| 属性                                                                | 描述                                          |
| :------------------------------------------------------------------ | :-------------------------------------------- |
| [hash](https://www.w3school.com.cn/jsref/prop_loc_hash.asp)         | 设置或返回从井号 (#) 开始的 URL（锚）。       |
| [host](https://www.w3school.com.cn/jsref/prop_loc_host.asp)         | 设置或返回主机名和当前 URL 的端口号。         |
| [hostname](https://www.w3school.com.cn/jsref/prop_loc_hostname.asp) | 设置或返回当前 URL 的主机名。                 |
| [href](https://www.w3school.com.cn/jsref/prop_loc_href.asp)         | 设置或返回完整的 URL。                        |
| [pathname](https://www.w3school.com.cn/jsref/prop_loc_pathname.asp) | 设置或返回当前 URL 的路径部分。               |
| [port](https://www.w3school.com.cn/jsref/prop_loc_port.asp)         | 设置或返回当前 URL 的端口号。                 |
| [protocol](https://www.w3school.com.cn/jsref/prop_loc_protocol.asp) | 设置或返回当前 URL 的协议。                   |
| [search](https://www.w3school.com.cn/jsref/prop_loc_search.asp)     | 设置或返回从问号 (?) 开始的 URL（查询部分）。 |

| 属性                                                               | 描述                     |
| :----------------------------------------------------------------- | :----------------------- |
| [assign()](https://www.w3school.com.cn/jsref/met_loc_assign.asp)   | 加载新的文档。           |
| [reload()](https://www.w3school.com.cn/jsref/met_loc_reload.asp)   | 重新加载当前文档。       |
| [replace()](https://www.w3school.com.cn/jsref/met_loc_replace.asp) | 用新的文档替换当前文档。 |

```javascript
// assign()用来跳转到其他的页面，作用和直接修改location一样
location.assign("http://www.baidu.com");

/*
 * reload()
 *  - 用于重新加载当前页面，作用和刷新按钮一样
 *  - 如果在方法中传递一个true，作为参数，则会强制清空缓存刷新页面
 */
location.reload(true);

/*
 * replace()
 *  - 可以使用一个新的页面替换当前页面，调用完毕也会跳转页面
 *   不会生成历史记录，不能使用回退按钮回退
 */
location.replace("index.html");
```

### 4、Screen

| 属性                                                                                           | 描述                                         |
| :--------------------------------------------------------------------------------------------- | :------------------------------------------- |
| [availHeight](https://www.w3school.com.cn/jsref/prop_screen_availheight.asp)                   | 返回显示屏幕的高度 (除 Windows 任务栏之外)。 |
| [availWidth](https://www.w3school.com.cn/jsref/prop_screen_availwidth.asp)                     | 返回显示屏幕的宽度 (除 Windows 任务栏之外)。 |
| [bufferDepth](https://www.w3school.com.cn/jsref/prop_screen_bufferdepth.asp)                   | 设置或返回调色板的比特深度。                 |
| [colorDepth](https://www.w3school.com.cn/jsref/prop_screen_colordepth.asp)                     | 返回目标设备或缓冲器上的调色板的比特深度。   |
| [deviceXDPI](https://www.w3school.com.cn/jsref/prop_screen_devicexdpi.asp)                     | 返回显示屏幕的每英寸水平点数。               |
| [deviceYDPI](https://www.w3school.com.cn/jsref/prop_screen_deviceydpi.asp)                     | 返回显示屏幕的每英寸垂直点数。               |
| [fontSmoothingEnabled](https://www.w3school.com.cn/jsref/prop_screen_fontsmoothingenabled.asp) | 返回用户是否在显示控制面板中启用了字体平滑。 |
| [height](https://www.w3school.com.cn/jsref/prop_screen_height.asp)                             | 返回显示屏幕的高度。                         |
| [logicalXDPI](https://www.w3school.com.cn/jsref/prop_screen_logicalxdpi.asp)                   | 返回显示屏幕每英寸的水平方向的常规点数。     |
| [logicalYDPI](https://www.w3school.com.cn/jsref/prop_screen_logicalydpi.asp)                   | 返回显示屏幕每英寸的垂直方向的常规点数。     |
| [pixelDepth](https://www.w3school.com.cn/jsref/prop_screen_pixeldepth.asp)                     | 返回显示屏幕的颜色分辨率（比特每像素）。     |
| [updateInterval](https://www.w3school.com.cn/jsref/prop_screen_updateinterval.asp)             | 设置或返回屏幕的刷新率。                     |
| [width](https://www.w3school.com.cn/jsref/prop_screen_width.asp)                               | 返回显示器屏幕的宽度。                       |

### 5、Window

| 属性                                                                                 | 描述                                                                                                                                                       |
| :----------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [closed](https://www.w3school.com.cn/jsref/prop_win_closed.asp)                      | 返回窗口是否已被关闭。                                                                                                                                     |
| [defaultStatus](https://www.w3school.com.cn/jsref/prop_win_defaultstatus.asp)        | 设置或返回窗口状态栏中的默认文本。                                                                                                                         |
| [document](https://www.w3school.com.cn/jsref/dom_obj_document.asp)                   | 对 Document 对象的只读引用。请参阅 [Document 对象](https://www.w3school.com.cn/jsref/dom_obj_document.asp)。                                               |
| [history](https://www.w3school.com.cn/jsref/dom_obj_history.asp)                     | 对 History 对象的只读引用。请参数 [History 对象](https://www.w3school.com.cn/jsref/dom_obj_history.asp)。                                                  |
| [innerheight](https://www.w3school.com.cn/jsref/prop_win_innerheight_innerwidth.asp) | 返回窗口的文档显示区的高度。                                                                                                                               |
| [innerwidth](https://www.w3school.com.cn/jsref/prop_win_innerheight_innerwidth.asp)  | 返回窗口的文档显示区的宽度。                                                                                                                               |
| length                                                                               | 设置或返回窗口中的框架数量。                                                                                                                               |
| [location](https://www.w3school.com.cn/jsref/dom_obj_location.asp)                   | 用于窗口或框架的 Location 对象。请参阅 [Location 对象](https://www.w3school.com.cn/jsref/dom_obj_location.asp)。                                           |
| [name](https://www.w3school.com.cn/jsref/prop_win_name.asp)                          | 设置或返回窗口的名称。                                                                                                                                     |
| [Navigator](https://www.w3school.com.cn/jsref/dom_obj_navigator.asp)                 | 对 Navigator 对象的只读引用。请参数 [Navigator 对象](https://www.w3school.com.cn/jsref/dom_obj_navigator.asp)。                                            |
| [opener](https://www.w3school.com.cn/jsref/prop_win_opener.asp)                      | 返回对创建此窗口的窗口的引用。                                                                                                                             |
| [outerheight](https://www.w3school.com.cn/jsref/prop_win_outerheight.asp)            | 返回窗口的外部高度。                                                                                                                                       |
| [outerwidth](https://www.w3school.com.cn/jsref/prop_win_outerwidth.asp)              | 返回窗口的外部宽度。                                                                                                                                       |
| pageXOffset                                                                          | 设置或返回当前页面相对于窗口显示区左上角的 X 位置。                                                                                                        |
| pageYOffset                                                                          | 设置或返回当前页面相对于窗口显示区左上角的 Y 位置。                                                                                                        |
| parent                                                                               | 返回父窗口。                                                                                                                                               |
| [Screen](https://www.w3school.com.cn/jsref/dom_obj_screen.asp)                       | 对 Screen 对象的只读引用。请参数 [Screen 对象](https://www.w3school.com.cn/jsref/dom_obj_screen.asp)。                                                     |
| [self](https://www.w3school.com.cn/jsref/prop_win_self.asp)                          | 返回对当前窗口的引用。等价于 Window 属性。                                                                                                                 |
| [status](https://www.w3school.com.cn/jsref/prop_win_status.asp)                      | 设置窗口状态栏的文本。                                                                                                                                     |
| [top](https://www.w3school.com.cn/jsref/prop_win_top.asp)                            | 返回最顶层的先辈窗口。                                                                                                                                     |
| window                                                                               | window 属性等价于 self 属性，它包含了对窗口自身的引用。                                                                                                    |
| screenLef/tscreenTop/screenX/screenY                                                 | 只读整数。声明了窗口的左上角在屏幕上的的 x 坐标和 y 坐标。IE、Safari 和 Opera 支持 screenLeft 和 screenTop，而 Firefox 和 Safari 支持 screenX 和 screenY。 |

| 方法                                                                           | 描述                                               |
| :----------------------------------------------------------------------------- | :------------------------------------------------- |
| [alert()](https://www.w3school.com.cn/jsref/met_win_alert.asp)                 | 显示带有一段消息和一个确认按钮的警告框。           |
| [blur()](https://www.w3school.com.cn/jsref/met_win_blur.asp)                   | 把键盘焦点从顶层窗口移开。                         |
| [clearInterval()](https://www.w3school.com.cn/jsref/met_win_clearinterval.asp) | 取消由 setInterval() 设置的 timeout。              |
| [clearTimeout()](https://www.w3school.com.cn/jsref/met_win_cleartimeout.asp)   | 取消由 setTimeout() 方法设置的 timeout。           |
| [close()](https://www.w3school.com.cn/jsref/met_win_close.asp)                 | 关闭浏览器窗口。                                   |
| [confirm()](https://www.w3school.com.cn/jsref/met_win_confirm.asp)             | 显示带有一段消息以及确认按钮和取消按钮的对话框。   |
| [createPopup()](https://www.w3school.com.cn/jsref/met_win_createpopup.asp)     | 创建一个 pop-up 窗口。                             |
| [focus()](https://www.w3school.com.cn/jsref/met_win_focus.asp)                 | 把键盘焦点给予一个窗口。                           |
| [moveBy()](https://www.w3school.com.cn/jsref/met_win_moveby.asp)               | 可相对窗口的当前坐标把它移动指定的像素。           |
| [moveTo()](https://www.w3school.com.cn/jsref/met_win_moveto.asp)               | 把窗口的左上角移动到一个指定的坐标。               |
| [open()](https://www.w3school.com.cn/jsref/met_win_open.asp)                   | 打开一个新的浏览器窗口或查找一个已命名的窗口。     |
| [print()](https://www.w3school.com.cn/jsref/met_win_print.asp)                 | 打印当前窗口的内容。                               |
| [prompt()](https://www.w3school.com.cn/jsref/met_win_prompt.asp)               | 显示可提示用户输入的对话框。                       |
| [resizeBy()](https://www.w3school.com.cn/jsref/met_win_resizeby.asp)           | 按照指定的像素调整窗口的大小。                     |
| [resizeTo()](https://www.w3school.com.cn/jsref/met_win_resizeto.asp)           | 把窗口的大小调整到指定的宽度和高度。               |
| [scrollBy()](https://www.w3school.com.cn/jsref/met_win_scrollby.asp)           | 按照指定的像素值来滚动内容。                       |
| [scrollTo()](https://www.w3school.com.cn/jsref/met_win_scrollto.asp)           | 把内容滚动到指定的坐标。                           |
| [setInterval()](https://www.w3school.com.cn/jsref/met_win_setinterval.asp)     | 按照指定的周期（以毫秒计）来调用函数或计算表达式。 |
| [setTimeout()](https://www.w3school.com.cn/jsref/met_win_settimeout.asp)       | 在指定的毫秒数后调用函数或计算表达式。             |

定时器：

**循环定时器**

js 的程序执行速度是非常快的，如果洗完过一段程序，可以每隔一段事件执行一次，可以使用定时调用

`setInterval()` 定时调用

可以将一个函数，每隔一段事件执行一次

参数有两个：

第一个是回调函数，该函数会每隔一段时间调用一次

第二个是每次调用间隔的时间，单位是毫秒

返回值：

返回一个 Number 类型的数据，这个数字用来作为定时器的唯一标识

`clearInterval()` 可以用来关闭一个定时器，方法中需要一个定时器的标识作为参数，这样将关闭标识对应的定时器

**延时定时器**

`setTimeout()` 延时调用，延时调用一个函数不马上执行，而是隔一段时间以后在执行，而且只会执行一次

延时调用和定时调用的区别，定时调用会执行多次，而延时调用只会执行一次

延时调用和定时调用实际上是可以互相代替的，在开发中可以根据自己需要去选择

1、count 自动增加

```html
<h1 id="count"></h1>
<script>
 /*// 执行太快
  for(var i=0 ; i<10000 ; i++){
      count.innerHTML = i
      alert("hello")
  }*/
  var num = 1
  var timer = setInterval(function(){
    count.innerHTML = num++
  if(num == 11){
   //关闭定时器
   clearInterval(timer)
  }   
 },1000)  
 //console.log(timer)
</script>
```

2、自动切换图片

```html
<script type="text/javascript">
  window.onload = function(){
    /*
      * 使图片可以自动切换
      */
    //获取img标签
    var img = document.getElementById("img")
    //创建一个数组来保存图片的路径
    var imgArr = ["img/1.jpg","img/2.jpg","img/3.jpg","img/4.jpg","img/5.jpg"]
    //创建一个变量，用来保存当前图片的索引
    var index = 0
    //定义一个变量，用来保存定时器的标识
    var timer
    //为btn01绑定一个单击响应函数
    var startBtn = document.getElementById("startBtn")
    startBtn.onclick = function(){
      /*
        * 目前，我们每点击一次按钮，就会开启一个定时器，
        *  点击多次就会开启多个定时器，这就导致图片的切换速度过快，
        *  并且我们只能关闭最后一次开启的定时器
        */
      //在开启定时器之前，需要将当前元素上的其他定时器关闭
      clearInterval(timer)
      /*
        * 开启一个定时器，来自动切换图片
        */
      timer = setInterval(function(){
        //使索引自增
        index++
        //判断索引是否超过最大索引
        /*if(index >= imgArr.length){
          //则将index设置为0
          index = 0;
        }*/
        index %= imgArr.length
        //修改img的src属性
        img.src = imgArr[index]
      },1000)
    }
    //为stopBtn绑定一个单击响应函数
    var stopBtn = document.getElementById("stopBtn")
    stopBtn.onclick = function(){
      //点击按钮以后，停止图片的自动切换，关闭定时器
      /*
        * clearInterval()可以接收任意参数，
        *  如果参数是一个有效的定时器的标识，则停止对应的定时器
        *  如果参数不是一个有效的标识，则什么也不做
        */
      clearInterval(timer)
    }
  }
</script>
<img id="img" src="img/1.jpg"/>
<br /><br />
<button id="startBtn">开始</button>
<button id="stopBtn">停止</button>
```

3、解决按键移动 box 卡顿问题

```html
<style type="text/css">
  #box1{
    width: 100px;
    height: 100px;
    background-color: red;
    position: absolute;
  }
</style>
<script type="text/javascript">
  //使div可以根据不同的方向键向不同的方向移动
  /*
    * 按左键，div向左移
    * 按右键，div向右移
    * 。。。
    */
  window.onload = function(){ 
    //定义一个变量，来表示移动的速度
    var speed = 10
    //创建一个变量表示方向
    //通过修改dir来影响移动的方向
    var dir = 0
    //开启一个定时器，来控制div的移动
    setInterval(function(){
      /*
        * 37 左
        * 38 上
        * 39 右
        * 40 下
        */
      switch(dir){
        case 37:
          //alert("向左"); left值减小
          box1.style.left = box1.offsetLeft - speed + "px"
          break
        case 39:
          //alert("向右");
          box1.style.left = box1.offsetLeft + speed + "px"
          break
        case 38:
          //alert("向上");
          box1.style.top = box1.offsetTop - speed + "px"
          break
        case 40:
          //alert("向下");
          box1.style.top = box1.offsetTop + speed + "px"
          break
      }
    },30)
    //为document绑定一个按键按下的事件
    document.onkeydown = function(event){
      event = event || window.event
      //当用户按了ctrl以后，速度加快
      if(event.ctrlKey){
        speed = 500
      }else{
        speed = 10
      }
      //使dir等于按键的值
      dir = event.keyCode
    };
    //当按键松开时，div不再移动
    document.onkeyup = function(){
      //设置方向为0
      dir = 0
    }  
  }
</script>
<div id="box1"></div>
```

延时调用

```javascript
/*setInterval(function(){
 console.log(num++);
},3000);*/
var timer = setTimeout(function(){
 console.log(num++)
},3000)
//使用clearTimeout()来关闭一个延时调用
clearTimeout(timer);
```

44、盒子移动

```html
<style type="text/css"> 
  *{
    margin: 0;
    padding: 0;
  } 
  #box1{
    width: 100px;
    height: 100px;
    margin-top: 50px;
    background-color: red;
    position: absolute;
    left: 0;
  }
</style>
<script type="text/javascript">
  window.onload = function(){
    //获取box1
    var box1 = document.getElementById("box1")
    //获取btn01
    var btn01 = document.getElementById("btn01")
    //定义一个变量，用来保存定时器的标识
    var timer
    //点击按钮以后，使box1向右移动（left值增大）
    btn01.onclick = function(){
      //关闭上一个定时器
      clearInterval(timer)
      //开启一个定时器，用来执行动画效果
      timer = setInterval(function(){
        //获取box1的原来的left值
        var oldValue = parseInt(getStyle(box1,"left"))
        //在旧值的基础上增加
        var newValue = oldValue + 1
        //判断newValue是否大于800
        if(newValue > 800){
          newValue = 800
        }
        //将新值设置给box1
        box1.style.left = newValue + "px"
        //当元素移动到800px时，使其停止执行动画
        if(newValue == 800){
          //达到目标，关闭定时器
          clearInterval(timer)
        }
      },30)
    }
  }
  /*
    * 定义一个函数，用来获取指定元素的当前的样式
    * 参数：
    *   obj 要获取样式的元素
    *   name 要获取的样式名
    */
  function getStyle(obj , name){
    if(window.getComputedStyle){
      //正常浏览器的方式，具有getComputedStyle()方法
      return getComputedStyle(obj , null)[name]
    }else{
      //IE8的方式，没有getComputedStyle()方法
      return obj.currentStyle[name]
    }
  }
</script>
<button id="btn01">点击按钮以后box1向右移动</button>
<div id="box1"></div>
<div style="width: 0; height: 1000px; border-left:1px black solid; position: absolute; left: 800px;top:0;"></div>
```

5、封装一个移动函数

```html
<script type="text/javascript">
  window.onload = function(){
    //获取box1
    var box1 = document.getElementById("box1")
    //获取btn01
    var btn01 = document.getElementById("btn01")
    //获取btn02
    var btn02 = document.getElementById("btn02")
    //点击按钮以后，使box1向右移动（left值增大）
    btn01.onclick = function(){
      move(box1 , 800 , 10)
    }
    //点击按钮以后，使box1向左移动（left值减小）
    btn02.onclick = function(){
      move(box1 , 0 , 10)
    }
  }
  //定义一个变量，用来保存定时器的标识
  var timer
  //尝试创建一个可以执行简单动画的函数
  /*
    * 参数：
    *  obj:要执行动画的对象
    *  target:执行动画的目标位置
    *  speed:移动的速度(正数向右移动，负数向左移动)
    */
  function move(obj , target ,speed){
    //关闭上一个定时器
    clearInterval(timer)
    //获取元素目前的位置
    var current = parseInt(getStyle(obj,"left"))
    //判断速度的正负值
    //如果从0 向 800移动，则speed为正
    //如果从800向0移动，则speed为负
    if(current > target){
      //此时速度应为负值
      speed = -speed
    }
    //开启一个定时器，用来执行动画效果
    timer = setInterval(function(){
      //获取box1的原来的left值
      var oldValue = parseInt(getStyle(obj,"left"))
      //在旧值的基础上增加
      var newValue = oldValue + speed
      //判断newValue是否大于800
      //从800 向 0移动
      //向左移动时，需要判断newValue是否小于target
      //向右移动时，需要判断newValue是否大于target
      if((speed < 0 && newValue < target) || (speed > 0 && newValue > target)){
        newValue = target
      }
      //将新值设置给box1
      obj.style.left = newValue + "px"
      //当元素移动到0px时，使其停止执行动画
      if(newValue == target){
        //达到目标，关闭定时器
        clearInterval(timer)
      }
    },30)
  }
  /*
    * 定义一个函数，用来获取指定元素的当前的样式
    * 参数：
    *   obj 要获取样式的元素
    *   name 要获取的样式名
    */
  function getStyle(obj , name){
    if(window.getComputedStyle){
      //正常浏览器的方式，具有getComputedStyle()方法
      return getComputedStyle(obj , null)[name]
    }else{
      //IE8的方式，没有getComputedStyle()方法
      return obj.currentStyle[name]
    }
  }
</script>
<button id="btn01">点击按钮以后box1向右移动</button>
<button id="btn02">点击按钮以后box1向左移动</button>
<div id="box1"></div>
<div style="width: 0; height: 1000px; border-left:1px black solid; position: absolute; left: 800px;top:0;"></div>
```

封装 move.js

```javascript
//尝试创建一个可以执行简单动画的函数
/*
 * 参数：
 *  obj:要执行动画的对象
 *  attr:要执行动画的样式，比如：left top width height
 *  target:执行动画的目标位置
 *  speed:移动的速度(正数向右移动，负数向左移动)
 *  callback:回调函数，这个函数将会在动画执行完毕以后执行
 */
function move(obj, attr, target, speed, callback) {
 //关闭上一个定时器
 clearInterval(obj.timer)
 //获取元素目前的位置
 var current = parseInt(getStyle(obj, attr))
 //判断速度的正负值
 //如果从0 向 800移动，则speed为正
 //如果从800向0移动，则speed为负
 if(current > target) {
  //此时速度应为负值
  speed = -speed
 }
 //开启一个定时器，用来执行动画效果
 //向执行动画的对象中添加一个timer属性，用来保存它自己的定时器的标识
 obj.timer = setInterval(function() {
  //获取box1的原来的left值
  var oldValue = parseInt(getStyle(obj, attr))
  //在旧值的基础上增加
  var newValue = oldValue + speed
  //判断newValue是否大于800
  //从800 向 0移动
  //向左移动时，需要判断newValue是否小于target
  //向右移动时，需要判断newValue是否大于target
  if((speed < 0 && newValue < target) || (speed > 0 && newValue > target)) {
   newValue = target
  }
  //将新值设置给box1
  obj.style[attr] = newValue + "px"
  //当元素移动到0px时，使其停止执行动画
  if(newValue == target) {
   //达到目标，关闭定时器
   clearInterval(obj.timer)
   //动画执行完毕，调用回调函数
   callback && callback()
  }

 }, 30)
}

/*
 * 定义一个函数，用来获取指定元素的当前的样式
 * 参数：
 *   obj 要获取样式的元素
 *   name 要获取的样式名
 */
function getStyle(obj, name) {
 if(window.getComputedStyle) {
  //正常浏览器的方式，具有getComputedStyle()方法
  return getComputedStyle(obj, null)[name]
 } else {
  //IE8的方式，没有getComputedStyle()方法
  return obj.currentStyle[name]
 }
}
```

调用

```html
<style type="text/css">
  *{
    margin: 0;
    padding: 0;
  }  
  #box1{
    margin-top: 50px;
    width: 100px;
    height: 100px;
    background-color: red;
    position: absolute;
    left: 0;
  }
  #box2{
    width: 100px;
    height: 100px;
    background-color: yellow;
    position: absolute;
    left: 0;
    top: 200px;
  }
</style>
<script type="text/javascript" src="js/move.js"></script>
<script type="text/javascript">
  window.onload = function(){
    //点击按钮以后，使box1向右移动（left值增大）
    btn01.onclick = function(){
      move(box1 ,"left", 800 , 20)
    }
    //点击按钮以后，使box1向左移动（left值减小）
    btn02.onclick = function(){
      move(box1 ,"left", 0 , 10)
    }
    //获取btn03
    var btn03 = document.getElementById("btn03")
    btn03.onclick = function(){
      move(box2 , "left",800 , 10)
    }
    //测试按钮
    var btn04 = document.getElementById("btn04");
    btn04.onclick = function(){
      //move(box2 ,"width", 800 , 10);
      //move(box2 ,"top", 800 , 10);
      //move(box2 ,"height", 800 , 10);
      move(box2 , "width" , 800 , 10 , function(){
        move(box2 , "height" , 400 , 10 , function(){
          move(box2 , "top" , 0 , 10 , function(){
            move(box2 , "width" , 100 , 10 , function(){
          
            })
          })
        })
      })
    }
  }
</script>
<button id="btn01">点击按钮以后box1向右移动</button>
<button id="btn02">点击按钮以后box1向左移动</button>
<button id="btn03">点击按钮以后box2向右移动</button>
<button id="btn04">测试按钮</button>
<div id="box1"></div>
<div id="box2"></div>
<div style="width: 0; height: 1000px; border-left:1px black solid; position: absolute; left: 800px;top:0;"></div>
```

6、轮播图

```html
<style>
*{
 margin: 0;
 padding: 0;
}

/*
 * 设置outer的样式
 */
#outer{
 /*设置宽和高*/
 width: 520px;
 height: 333px;
 /*居中*/
 margin: 50px auto;
 /*设置背景颜色*/
 background-color: greenyellow;
 /*设置padding*/
 padding: 10px 0;
 /*开启相对定位*/
 position: relative;
 /*裁剪溢出的内容*/
 overflow: hidden;
}

/*设置imgList*/
#imgList{
 /*去除项目符号*/
 list-style: none;
 /*设置ul的宽度*/
 /*width: 2600px;*/
 /*开启绝对定位*/
 position: absolute;
 /*设置偏移量*/
 /*
  * 每向左移动520px，就会显示到下一张图片
  */
 left: 0px;
}

/*设置图片中的li*/
#imgList li{
 /*设置浮动*/
 float: left;
 /*设置左右外边距*/
 margin: 0 10px;
}

/*设置导航按钮*/
#navDiv{
 /*开启绝对定位*/
 position: absolute;
 /*设置位置*/
 bottom: 15px;
 /*设置left值
   outer宽度  520
   navDiv宽度 25*5 = 125
    520 - 125 = 395/2 = 197.5
  * */
 /*left: 197px;*/
}

#navDiv a{
 /*设置超链接浮动*/
 float: left;
 /*设置超链接的宽和高*/
 width: 15px;
 height: 15px;
 /*设置背景颜色*/
 background-color: red;
 /*设置左右外边距*/
 margin: 0 5px;
 /*设置透明*/
 opacity: 0.5;
 /*兼容IE8透明*/
 filter: alpha(opacity=50);
}

/*设置鼠标移入的效果*/
#navDiv a:hover{
 background-color: black;
}
</style>
<!-- 创建一个外部的div，来作为大的容器 -->
<div id="outer">
 <!-- 创建一个ul，用于放置图片 -->
 <ul id="imgList">
  <li><img src="img/1.jpg"/></li>
  <li><img src="img/2.jpg"/></li>
  <li><img src="img/3.jpg"/></li>
  <li><img src="img/4.jpg"/></li>
  <li><img src="img/5.jpg"/></li>
    <!-- 由于需要流畅衔接，故在最后加一张 -->
    <li><img src="img/1.jpg"/></li>
 </ul>
 <!--创建导航按钮-->
 <div id="navDiv">
  <a href="javascript:;"></a>
  <a href="javascript:;"></a>
  <a href="javascript:;"></a>
  <a href="javascript:;"></a>
  <a href="javascript:;"></a>
 </div>
</div>
```

js

```html
  <!--引用工具-->
  <script type="text/javascript" src="js/move.js"></script>
  <script type="text/javascript">
   window.onload = function(){
    //获取imgList
    var imgList = document.getElementById("imgList");
    //获取页面中所有的img标签
    var imgArr = document.getElementsByTagName("img");
    //设置imgList的宽度
    imgList.style.width = 520*imgArr.length+"px";
    
    /*设置导航按钮居中*/
    //获取navDiv
    var navDiv = document.getElementById("navDiv");
    //获取outer
    var outer = document.getElementById("outer");
    //设置navDiv的left值
    navDiv.style.left = (outer.offsetWidth - navDiv.offsetWidth)/2 + "px";
    
    //默认显示图片的索引
    var index = 0;
    //获取所有的a
    var allA = document.getElementsByTagName("a");
    //设置默认选中的效果
    allA[index].style.backgroundColor = "black";
    
    /*
      点击超链接切换到指定的图片
       点击第一个超链接，显示第一个图片
       点击第二个超链接，显示第二个图片
     * */
    
    //为所有的超链接都绑定单击响应函数
    for(var i=0; i<allA.length ; i++){
     
     //为每一个超链接都添加一个num属性
     allA[i].num = i;
     
     //为超链接绑定单击响应函数
     allA[i].onclick = function(){
      
      //关闭自动切换的定时器
      clearInterval(timer);
      //获取点击超链接的索引,并将其设置为index
      index = this.num;
      
      //切换图片
      /*
       * 第一张  0 0
       * 第二张  1 -520
       * 第三张  2 -1040
       */
      //imgList.style.left = -520*index + "px";
      //设置选中的a
      setA();
      
      //使用move函数来切换图片
      move(imgList , "left" , -520*index , 20 , function(){
       //动画执行完毕，开启自动切换
       autoChange();
      });
      
     };
    }
    
    
    //开启自动切换图片
    autoChange();
    
    
    //创建一个方法用来设置选中的a
    function setA(){
     
     //判断当前索引是否是最后一张图片
     if(index >= imgArr.length - 1){
      //则将index设置为0
      index = 0;
      
      //此时显示的最后一张图片，而最后一张图片和第一张是一摸一样
      //通过CSS将最后一张切换成第一张
      imgList.style.left = 0;
     }
     
     //遍历所有a，并将它们的背景颜色设置为红色
     for(var i=0 ; i<allA.length ; i++){
      allA[i].style.backgroundColor = "";
     }
     
     //将选中的a设置为黑色
     allA[index].style.backgroundColor = "black";
    };
    
    //定义一个自动切换的定时器的标识
    var timer;
    //创建一个函数，用来开启自动切换图片
    function autoChange(){
     
     //开启一个定时器，用来定时去切换图片
     timer = setInterval(function(){
      
      //使索引自增
      index++;
      
      //判断index的值
      index %= imgArr.length;
      
      //执行动画，切换图片
      move(imgList , "left" , -520*index , 20 , function(){
       //修改导航按钮
       setA();
      });
      
     },3000);
     
    }
    
    
   };
   
  </script>

```

类的操作实现样式修改

我们可以通过修改元素的 class 属性来间接地修改样式，这样一来，我们只需要修改一次，即可同时修改多个样式，浏览器只需要重新渲染页面一次，性能比较好，并且这种方式，可以使表现和行为进一步地分离

```javascript
box.className = "b2" // 修改类名为b2
box.className += "b3"  // 在原有类的基础上加
```

定义函数，用来对一个元素中 class 进行操作

```javascript
/* 添加添加指定的class属性值
参数：
obj: 要添加class属性的元素
cn: 要添加的class值
*/
/*function addClass(obj, cn){
  obj.className += " "+cn
}
addClass(box, "b2")
*/
// 有了就不需要添加了
function addClass(obj, cn){
  if(!hasClass(obj, cn)){
    obj.className += " "+cn
  }
}
/*
判断一个元素中是否含有指定的class属性值，如果有则返回true，没有则返回false
*/
function hasClass(obj, cn){
 var reg = new RegExp("\\b" +cn+ "\\b")
  return reg.test(obj.className)
}
/*
删除一个元素中的指定的class属性
*/
function removeClass(obj, cn){
  var reg = new RegExp("\\b" +cn+ "\\b")
  obj.className = obj.className.replace(reg, "")
}
/*
toggleClass用来切换一个类，如果有，则删除；没有则添加
*/
function toggleClass(obj, cn){
  if(hasClass(obj, cn)){
    removeClass(obj, cn)
  }else{
    addClass(obj, cn)
  }
}
```

二级菜单

```html
<style type="text/css">
 * {
  margin: 0;
  padding: 0;
  list-style-type: none;
 }
 a,img {
  border: 0;
  text-decoration: none;
 }
 body {
  font: 12px/180% Arial, Helvetica, sans-serif, "新宋体";
 }
 div.sdmenu {
  width: 150px;
  margin: 0 auto;
  font-family: Arial, sans-serif;
  font-size: 12px;
  padding-bottom: 10px;
  background: url(bottom.gif) no-repeat right bottom;
  color: #fff;
 }
 div.sdmenu div {
  background: url(title.gif) repeat-x;
  overflow: hidden;
 }
 div.sdmenu div:first-child {
  background: url(toptitle.gif) no-repeat;
 }
 div.sdmenu div.collapsed {
  height: 25px;
 }
 div.sdmenu div span {
  display: block;
  height: 15px;
  line-height: 15px;
  overflow: hidden;
  padding: 5px 25px;
  font-weight: bold;
  color: white;
  background: url(expanded.gif) no-repeat 10px center;
  cursor: pointer;
  border-bottom: 1px solid #ddd;
 }
 div.sdmenu div.collapsed span {
  background-image: url(collapsed.gif);
 }
 div.sdmenu div a {
  padding: 5px 10px;
  background: #eee;
  display: block;
  border-bottom: 1px solid #ddd;
  color: #066;
 }
 div.sdmenu div a.current {
  background: #ccc;
 }
 div.sdmenu div a:hover {
  background: #066 url(linkarrow.gif) no-repeat right center;
  color: #fff;
  text-decoration: none;
 }
</style>
<div id="my_menu" class="sdmenu">
 <div>
  <span class="menuSpan">在线工具</span>
  <a href="javascript:;">图像优化</a>
  <a href="javascript:;">收藏夹图标生成器</a>
  <a href="javascript:;">邮件</a>
  <a href="javascript:;">htaccess密码</a>
  <a href="javascript:;">梯度图像</a>
  <a href="javascript:;">按钮生成器</a>
 </div>
 <div class="collapsed">
  <span class="menuSpan">支持我们</span>
  <a href="javascript:;">推荐我们</a>
  <a href="javascript:;">链接我们</a>
  <a href="javascript:;">网络资源</a>
 </div>
 <div class="collapsed">
  <span class="menuSpan">合作伙伴</span>
  <a href="javascript:;">JavaScript工具包</a>
  <a href="javascript:;">CSS驱动</a>
  <a href="javascript:;">CodingForums</a>
  <a href="javascript:;">CSS例子</a>
 </div>
 <div class="collapsed">
  <span class="menuSpan">测试电流</span>
  <a href="javascript:;">Test</a>
  <a href="javascript:;">2</a>
  <a href="javascript:;">Lorem</a>
  <a href="javascript:;">Lorem ipsum dolor sit amet</a>
 </div>
</div>
```

使这个菜单在点击时能够把二级菜单展示出来，点击另一个 span，关掉该项打开点击的项

![](https://cdn.wallleap.cn/img/pic/illustration/20200815084147.png)

```html
<script type="text/javascript" src="js/move.js"></script>
<script type="text/javascript" src="js/class.js"></script>
<script type="text/javascript">
 window.onload = function(){
  /*
   * 我们的每一个菜单都是一个div
   *  当div具有collapsed这个类时，div就是折叠的状态
   *  当div没有这个类是，div就是展开的状态
   */
  /*
   * 点击菜单，切换菜单的显示状态
   */
  //获取所有的class为menuSpan的元素
  var menuSpan = document.querySelectorAll(".menuSpan");
  //定义一个变量，来保存当前打开的菜单
  var openDiv = menuSpan[0].parentNode
  //为span绑定单击响应函数
  for(var i=0 ; i<menuSpan.length ; i++){
   menuSpan[i].onclick = function(){
    //this代表我当前点击的span
    //获取当前span的父元素
    var parentDiv = this.parentNode
    //切换菜单的显示状态
    toggleMenu(parentDiv)
    //判断openDiv和parentDiv是否相同
    if(openDiv != parentDiv  && !hasClass(openDiv , "collapsed")){
     //打开菜单以后，应该关闭之前打开的菜单
     //为了可以统一处理动画过渡效果，我们希望在这将addClass改为toggleClass
     //addClass(openDiv , "collapsed")
     //此处toggleClass()不需要有移除的功能
     //toggleClass(openDiv , "collapsed")
     //切换菜单的显示状态
     toggleMenu(openDiv)
    }
    //修改openDiv为当前打开的菜单
    openDiv = parentDiv
   }
  }
  /*
   * 用来切换菜单折叠和显示状态
   */
  function toggleMenu(obj){
   //在切换类之前，获取元素的高度
   var begin = obj.offsetHeight
   //切换parentDiv的显示
   toggleClass(obj , "collapsed")
   //在切换类之后获取一个高度
   var end = obj.offsetHeight
   //动画效果就是将高度从begin向end过渡
   //将元素的高度重置为begin
   obj.style.height = begin + "px"
   //执行动画，从bengin向end过渡
   move(obj,"height",end,10,function(){
    //动画执行完毕，内联样式已经没有存在的意义了，删除之
    obj.style.height = ""
   })
  }
 }
</script>
```

新的 class 操作：

```js
classList.add("className") //添加类
classList.remove("className") //删除类
classList.toggle("className") //切换类
classList.contains("className") //判断是否包含类
```

## 五、JSON

JSON

- JS 中的对象只有 JS 自己认识，其他的语言都不认识
- JSON 就是一个特殊格式的字符串，这个字符串可以被任意的语言所识别，并且可以转换为任意语言中的对象，JSON 在开发中主要用来数据的交互
- JavaScript Object Notation JS 对象表示法
- JSON 借鉴了部分 JS 的语法，实现了 number、boolean、string、array、object、null 的表示
- JSON 和 JS 对象的格式一样，只不过 JSON 字符串中的属性名必须加双引号，其他的和 JS 语法一致
- JSON 分类：

 1. 对象 `{}`
 2. 数组 `[]`

- JSON中允许的值：

 1. 字符串
 2. 数值
 3. 布尔值
 4. null
 5. 对象
 6. 数组

```javascript
//创建一个对象
var arr = '[1,2,3,"hello",true,null]'
var obj2 = '{"arr":[1,2,3]}'
var arr2 ='[{"name":"孙悟空","age":18,"gender":"男"},{"name":"孙悟空","age":18,"gender":"男"}]'
```

将 JSON 字符串转换为 JS 中的对象

- 在 JS 中，为我们提供了一个工具类，就叫 JSON
- 这个对象可以帮助我们将一个 JSON 转换为 JS 对象，也可以将一个 JS 对象转换为 JSON

JSON ---> JS对象

- `JSON.parse()`
- 可以将以 JSON 字符串转换为 js 对象
- 它需要一个 JSON 字符串作为参数，会将该字符串转换为 JS 对象并返回

```javascript
var json = '{"name":"孙悟空","age":18,"gender":"男"}'
var o = JSON.parse(json)
var o2 = JSON.parse(arr)
console.log(o.gender)
console.log(o2[1])
```

JS对象 ---> JSON

- `JSON.stringify()`
- 可以将一个 JS 对象转换为 JSON 字符串
- 需要一个 js 对象作为参数，会返回一个 JSON 字符串

```javascript
var obj3 = {name:"猪八戒" , age:28 , gender:"男"}
var str = JSON.stringify(obj3)
console.log(str)
```

JSON 这个对象在 IE 7 及以下的浏览器中不支持，所以在这些浏览器中调用时会报错

如果需要兼容 IE 7 及以下的 JSON 操作，则可以通过引入一个外部的 js 文件来处理

```html
<script src="https://cdn.bootcdn.net/ajax/libs/json2/20110223/json2.js"></script>
```

`eval()`

- 这个函数可以用来执行一段字符串形式的 JS 代码，并将执行结果返回
- 如果使用 eval() 执行的字符串中含有 {}，它会将 {} 当成是代码块
- 如果不希望将其当成代码块解析，则需要在字符串前后各加一个()
- eval() 这个函数的功能很强大，可以直接执行一个字符串中的 js 代码
- 但是在开发中尽量不要使用，首先它的执行性能比较差，然后它还具有安全隐患

```javascript
var str = '{"name":"孙悟空","age":18,"gender":"男"}'
var obj = eval("("+str+")")
console.log(obj)
```
