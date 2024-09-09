---
title: React 教程之从概念到实战
date: 2020-07-12 16:54
updated: 2020-07-12 16:54
cover: //cdn.wallleap.cn/img/pic/cover/202302ihq49n.jpg
category: 技术杂谈
tags:
  - web
  - 前端
description: React 教程之从概念到实战
---

前端三大框架之一，用于构建用户界面的 JavaScript 库

## 一、React 入门

### 1.1 React 的基本认识

React 官网：

- 英文官网：<https://reactjs.org/>

- 中文官网：<https://doc.react-china.org/>

介绍描述：

React 是用于构建用户界面的 JavaScript 框架（只关注于 View）

- JS 库&框架：
  
  - jQuery——函数库（方法、函数包装 DOM 操作）
  
  - React 基本上不操作 DOM——JS 框架

- 构建用户界面：把数据展现出来

- 由**Facebook**开源

React 的特点：

- Declarative（声明式编码）
  - 不需要亲自操作 DOM（申请一块内存，只需要声明一个变量即可），只需要告诉它，我要更新，就会帮你更新，只需要更新数据，界面不需要手动更新（以前需要更新 DOM）

- Component-Based（组件化编码）
  - 简化特别复杂的功能，可以拆分为多个简单的部分（一个小的界面功能就是一个组件），维护也方便

- Learn Once, Write Anywhere（支持客户端与服务器渲染）
  - 一次学习，随处编写：不仅能写 web 应用，还能通过 React Native 打包为 Android、IOS 应用

- 高效

- 单向数据流

React 高效的原因（区域、次数——更新界面效率提高）：

- **虚拟（virtual）DOM**，不总是直接操作 DOM
  - 虚拟 DOM：对象——与组件对应，修改映射到真实的 DOM 上（批量修改、界面重绘**次数少**）

- **DOM Diff 算法**，最小化页面重绘
  - 界面中组件是否更新（更新**区域小**）

### 1.2 React 的基本使用

注意：*此时只是测试语法使用, 并不是真实项目开发使用*

实现效果：将 h1 标签利用 react 放到 test 中

![React基本使用](https://cdn.wallleap.cn/img/pic/illustration/react1592556203130.png)

相关的库：

- `react.js`：React 的核心库
  - development.js：开发版，开发编写的时候使用
  - production.min.js：生产版，上线的时候使用，压缩过的

- `react-dom.js`：提供操作 DOM 的 React 扩展库

- `babel.min.js`：解析 JSX 语法代码转为纯 JS 语法代码的库，这里不是 ES6 转 ES5（jsx 是 js 扩展语法）

可以到 bootcdn 引用地址，访问链接 <kbd>Ctrl</kbd> + <kbd>S</kbd> 保存到本地

在页面中导入 js

```html
<script type="text/javascript" src="../js/react.development.js"></script>
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<script type="text/javascript" src="../js/babel.min.js"></script>
```

开始编码

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>01_HelloWorld</title>
</head>
<body>
  <div id="test"></div>

  <script type="text/javascript" src="../js/react.development.js"></script>
  <script type="text/javascript" src="../js/react-dom.development.js"></script>
  <script type="text/javascript" src="../js/babel.min.js"></script>
  <script type="text/babel">/*告诉babel.js解析里面的jsx的代码*/
    // 1. 创建虚拟DOM元素对象
    var vDom = <h1>Hello React!</h1>   // jsx，不是字符串，不能加引号
    // 2. 将虚拟DOM渲染到页面真实DOM容器中
    ReactDOM.render(vDom, document.getElementById('test'))  // react-dom.js提供的  render——渲染   将vDom加入到#test中
  </script>
</body>
</html>
```

使用 React 开发者工具调试

[React Developer Tool](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=zh-CN)

### 1.3 React JSX

实现效果：两个 `#test` 分别加入相应内容

![React JSX](https://cdn.wallleap.cn/img/pic/illustration/react1592556978982.png)

代码：

```html
<div id="test1"></div>
<div id="test2"></div>

<script src="../js/react.development.js"></script>
<script src="../js/react-dom.development.js"></script>
<script src="../js/babel.min.js"></script>

<script> // 还没用到jsx语法，不需要babel
  const msg = 'I Like You!'
  const myId = 'Atguigu'

  // 1.创建虚拟DOM
  // var element = React.createElement('h1', {id:'myTitle'},'hello')
  const vDom1 = React.createElement('h2', {id:myId.toLowerCase()},msg.toUpperCase())
  // 2.渲染虚拟DOM
  ReactDOM.render(vDom1, document.getElementById('test1'))
</script>

<script type="text/babel">
  // 1.创建虚拟DOM
  const vDom2 = <h3 id={myId.toUpperCase()}>{msg.toLowerCase()}</h3>  // 变量用{}括起来
  // 2.渲染虚拟DOM
  ReactDOM.render(vDom2, document.getElementById('test2'))
</script>
```

虚拟 DOM

- React 提供了一些 API 来创建一种 **特别** 的一般 js 对象
  - `var element = React.createElement('h1', {id:'myTitle'}, 'hello')`
  - 上面创建的就是一个简单的虚拟 DOM 对象，babel 将会把 jsx 语法转为上述的形式

- 虚拟 DOM 对象最终都会被 React **转换为**真实的 DOM（虚拟 DOM 中的对应真实 DOM 中的标签元素）

- 我们编码时基本只需要操作 react 的虚拟 DOM 相关数据，react 会转换为真实 DOM 变化而更新界面

补充知识：`debugger` 可以在某条 js 代码处添加断点

虚拟 DOM——轻对象，更新虚拟 DOM 页面不重绘

真实 DOM——重对象，更新真实 DOM 页面会发生变化（页面重绘）

JSX

- 全称：JavaScript XML
- react 定义的一种类似于 XML 的**JS 扩展语法**：XML+JS
- 作用：用来创建 react 虚拟 DOM(元素)对象
- 例如：`var ele = <h1>Hello JSX!</h1>`
- 注意1：它不是字符串，也不是 HTML/XML 标签
- 注意2：它最终产生的就是一个 JS 对象
- **标签名任意**：HTML 标签或其它标签
- 标签属性任意：HTML 标签属性或其它
- 基本语法规则
  - **遇到 `<` 开头**的代码, 以**标签**的语法解析：html 同名标签转换为 html 同名元素，其它标签需要特别解析
  - **遇到以 `{` 开头**的代码，以 **JS 语法**解析：标签中的 js 代码必须用 `{}` 包含

babel.js 的作用

- 浏览器不能直接解析 JSX 代码，需要 **babel 转译为纯 JS 的代码**才能运行
- 只要用了 JSX，都要加上 `type="text/babel"`，声明需要 babel 来处理

渲染虚拟 DOM（元素）

- 语法：`ReactDOM.render(virtualDOM, containerDOM)`
- 作用：将虚拟 DOM 元素渲染到页面中的真实容器 DOM 中显示
- 参数说明
  - 参数一：纯 js 或 jsx 创建的虚拟 dom 对象
  - 参数二：用来包含虚拟 DOM 元素的真实 dom 元素对象(一般是一个 div)

建虚拟 DOM 的 2 种方式

- 纯 JS（一般不用） `React.createElement('h1', {id:'myTitle'}, title)`
- **JSX**: `<h1 id='myTitle'>{title}</h1>`

JSX 练习：动态展示列表数据

![JSX](https://cdn.wallleap.cn/img/pic/illustration/react1592558986188.png)

代码：

```html
<h2>前端JS框架列表</h2>
<div id="example1"></div>
<script type="text/javascript" src="../js/react.development.js"></script>
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<script type="text/javascript" src="../js/babel.min.js"></script>
<script type="text/babel">
  /*
    功能: 动态展示列表数据
    - 如何将一个数据的数组，转换为一个标签的数组
      使用数组的map()方法
  */
  // 数据：名称、类型，数组存放
  const names = ['jQuery', 'zepto', 'angular', 'react', 'vue']
  // 1.创建虚拟DOM，有嵌套结构，最好用小括号括起来
  const ul = (
    <ul>
      {
        names.map((name, index) => <li key={index}>{name}</li>)
      }
    </ul>
  )
  // 2.渲染虚拟DOM
  ReactDOM.render(ul, document.getElementById('example1'))
</script>
```

### 1.4 模块与组件和模块化与组件化的理解

模块

- 理解：向外**提供特定功能的** js 程序，一般就是一个 **js 文件**
- 为什么：js 代码更多更复杂
- 作用：复用 js，简化 js 的编写，提高 js 运行效率

有特定功能的 js 文件，内部有数据及对数据的操作

- 数据：变量
- 操作：函数

私有的函数向外暴露

- 暴露一个函数：暴露函数本身
- 暴露多个函数：以对象形式暴露

组件

- 理解：用来**实现特定（局部）功能效果**的**代码**集合（html/css/js）
- 为什么：一个界面的功能更复杂
- 作用：复用编码，简化项目编码，提高运行效率

模块化

- 当应用的 **js 都以模块来编写**的，这个应用就是一个模块化的应用
- 形容项目或编码

组件化

- 当应用是以多组件的方式实现，这个应用就是一个组件化的应用

例如下面 App 组件就是一个组件，它又是由多个组件组成的

- CommentAdd 组件
- CommentList 组件
  - 多个 CommentItem 组件

![component](https://cdn.wallleap.cn/img/pic/illustration/react1592560823655.png)

## 二、React 面向组件编程

面向对象 → 面向模块 → 面向组件

### 2.1 基本理解和使用

实现效果

![组件](https://cdn.wallleap.cn/img/pic/illustration/react1592561100045.png)

组件标签：可以随便取的标签，首字母大写（与 HTML 标签区分开）

自定义组件（Component）：

1. 定义组件（2 种方式）

   - 方式 1：**工厂函数组件（简单组件：没有状态的组件）**——效率高，不需要创建对象

      ```js
      function MyComponent() {
        return <h2>工厂函数组件（简单组件）</h2>
      }
      ```

   - 方式 2：**ES6 类组件（复杂组件）**——需要创建对象，有了状态只能使用这种方式

      ```javascript
      class MyComponent2 extends React.Component {
        render() {
          console.log(this)  // 组件类对象 MyComponent2{...}
          return <h2>ES6类组件（复杂组件）</h2>
        }
      }
      ```

2. 渲染组件标签

    ```JavaScript
    ReactDOM.render(<MyComponent  />, document.getElementById('example1'))
    ReactDOM.render(<MyComponent2  />, document.getElementById('example2'))
    ```

注意

- 组件名必须**首字母大写**
- 虚拟 DOM 元素只能有**一个根元素**
- 虚拟 DOM 元素必须**有结束标签**

`render()` 渲染组件标签的基本流程

1. React 内部会创建组件实例对象
2. 得到包含的虚拟 DOM 并解析为真实 DOM
3. 插入到指定的页面元素内部

### 2.2 组件三大属性 1：`state`

实现效果

![state](https://cdn.wallleap.cn/img/pic/illustration/Like组件.gif)

理解

- `state` 是组件对象最重要的属性，值是对象（可以包含多个数据）
- 组件被称为"状态机"，通过更新组件的 `state` 来更新对应的页面显示（重新渲染组件）

编码操作

1. 初始化状态：

    ```javascript
    constructor (props) {
      super(props)
      this.state = {
        stateProp1: value1,
        stateProp2: value2
      }
    }
    ```

2. 读取某个状态值

    ```javascript
    this.state.statePropertyName
    ```

3. 更新状态-->组件界面更新

    ```javascript
    this.setState({
      stateProp1 : value1,
      stateProp2 : value2
    })
    ```

实现代码

```html
<div id="example"></div>
<script type="text/javascript" src="../js/react.development.js"></script>
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<script type="text/javascript" src="../js/babel.min.js"></script>
<script type="text/babel">
  /*
  需求: 自定义组件, 功能说明如下
    1. 显示h2标题, 初始文本为: 你喜欢我
    2. 点击标题更新为: 我喜欢你
  */
  // 1.定义组件
  class Like extends React.Component {
    constructor(props) {
      super(props)
      // 初始化状态
      this.state = {
        isLikeMe: false
      }

      // 将新增方法中的this强制绑定为组件对象
      this.handleClick = this.handleClick.bind(this) // 也可以不在这里绑定
    }

    handleClick() {
      // console.log(this) // handleClick是新添加方法，内部this默认不是组件对象，而是undefined  render是重写组件类的方法 到上面或下面绑定this
      // 得到状态，并取反
      const isLikeMe = !this.state.isLikeMe
      // 更新状态
      this.setState({isLikeMe}) // isLikeMe: isLikeMe
    }
    render() {
      // 读取状态
      // const isLikeMe = this.state.isLikeMe
      const {isLikeMe} = this.state // 解构赋值
      return <h2 onClick={this.handleClick}>{isLikeMe?'你喜欢我':'我喜欢你'}</h2> // this——组件对象 // this.handleClick.bind(this) —— 在这里绑定也可以
    }
  }
  // 2.渲染组件标签
  ReactDOM.render(<Like />, document.getElementById('example'))
</script>
```

### 2.3 组件三大属性 2：`props`

实现效果

```md
需求：自定义用来显示一个人员信息的组件

1. 姓名必须指定
2. 如果性别没有指定，默认为 男
3. 如果年龄没有指定，默认为 18
```

![props](https://cdn.wallleap.cn/img/pic/illustration/react-4.png)

理解

- 每个组件对象都会有 `props`（properties 的简写）属性
- 组件标签的所有属性都保存在 `props` 中

作用

- 通过标签属性从组件外向组件内传递变化的数据
- 注意：组件内部不要修改 `props` 数据

编码操作

1. 内部读取某个属性值 `this.props.propertyName`
2. 对 `props` 中的属性值进行类型限制和必要性限制

    > 注意：
    >
    > 自 React v15.5 起，`React.PropTypes` 已移入另一个包中。请使用 [`prop-types` 库](https://www.npmjs.com/package/prop-types) 代替。需要先引入该库。
    >
    > 我们提供了一个 [codemod 脚本](https://react.docschina.org/blog/2017/04/07/react-v15.5.0.html#migrating-from-reactproptypes)来做自动转换。

    ```javascript
    Person.propTypes = {
      name: React.PropTypes.string.isRequired,
      age: React.PropTypes.number.isRequired
    }
    ```

3. 扩展属性：将对象的所有属性通过 `props` 传递 `<Person {...person}/>`

4. 默认属性值

    ```javascript
    Person.defaultProps = {
      name: 'Mary'
    }
    ```

5. 组件类的构造函数

    ```javascript
    constructor (props) {
      super(props)
      console.log(props) // 查看所有属性
    }
    ```

代码

```html
<div id="example1"></div>
<div id="example2"></div>
<script type="text/javascript" src="../js/react.development.js"></script>
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<script type="text/javascript" src="../js/prop-types.js"></script> <!-- 验证类型和必要性 -->
<script type="text/javascript" src="../js/babel.min.js"></script>
<script type="text/babel">
  /*
需求: 自定义用来显示一个人员信息的组件, 效果如页面. 说明
  1). 如果性别没有指定, 默认为男
  2). 如果年龄没有指定, 默认为18
  */

  // 1、定义组件
  /*function Person(props){
    return (
      <ul>
        <li>姓名：{props.name}</li>
        <li>性别：{props.sex}</li>
        <li>年龄：{props.age}</li>
      </ul>
    )
  }*/
  class Person extends React.Component{
    render(){
      return (
        <ul>
          <li>姓名：{this.props.name}</li>  // this——组件对象
          <li>性别：{this.props.sex}</li>
          <li>年龄：{this.props.age}</li>
        </ul>
      )
    }
  }
  // 指定属性默认值
  Person.defaultProps = {
    sex: '男',
    age: 18
  }
  // 指定属性值的类型和必要性
  Person.propTypes = {
    name: PropTypes.string.isRequired,
    age: PropTypes.number
  }

  // 2、渲染组件标签
  const p1 = {
    name: 'Tom',
    sex: '女',
    age: 18
  }
  // ReactDOM.render(<Person name={p1.name} sex={p1.sex} age={p1.age}/>, document.getElementById('example1'))
  ReactDOM.render(<Person {...p1}/>, document.getElementById('example1')) // ...作用：1.打包：function fn(...as){} fun(1,2,3) 2.解包：const arr1=[1,2,3] const arr2=[6,...arr1,9] 这里也是在解包
  const p2 = {
    name: 'JACK',
    age: 17
  }
  ReactDOM.render(<Person name={p2.name} age={p2.age}/>, document.getElementById('example2'))
</script>
```

> 🔖 面试题：请区别一下组件的 `props` 和 `state` 属性

- `state`：**组件自身内部可变化的数据**

- `props`：从组件**外部**向组件内部**传递数据**，组件内部**只读**不修改

### 2.4 组件三大属性 3：`refs` 与事件处理

效果

```md
需求：自定义组件，功能说明如下

1. 点击按钮，提示第一个输入框中的值
2. 当第 2 个输入框失去焦点时，提示这个输入框中的值
```

![props_event](https://cdn.wallleap.cn/img/pic/illustration/props_event.gif)

`refs` 属性

- 组件内的标签都可以定义 `ref` 属性来标识自己

  1. `<input type="text" ref={input => this.msgInput = input}/>`

  2. 回调函数在组件初始化渲染完或卸载时自动调用

- 在组件中可以通过 `this.msgInput` 来得到对应的真实 DOM 元素

- 作用：通过 `ref` 获取组件内容特定标签对象，进行读取其相关数据

事件处理

- 通过 `onXxx` 属性指定组件的事件处理函数（注意大小写）

  - React 使用的是自定义（合成）事件, 而不是使用的原生 DOM 事件

  - React 中的事件是通过事件委托方式处理的（委托给组件最外层的元素）

- 通过 `event.target` 得到发生事件的 DOM 元素对象

```js
handleFocus(event) {
  event.target // 返回input对象
}
```

强烈注意

- 组件内置的方法中的 `this` 为组件对象
- 在组件类中自定义的方法中 `this` 为 `null`
- 强制绑定 `this`：通过函数对象的 `bind()` / `apply()` / `call()` 来指定 `this`
- 箭头函数没有 `this`，箭头函数内部的 `this` 是上下文中的 `this`（箭头函数没有自己的 `this`，它的 `this` 是外面的 `this`）

代码

```html
<div id="example"></div>
<script type="text/javascript" src="../js/react.development.js"></script>
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<script type="text/javascript" src="../js/babel.min.js"></script>
<script type="text/babel">
  /*
  需求: 自定义组件, 功能说明如下:
    1. 界面如果页面所示
    2. 点击按钮, 提示第一个输入框中的值
    3. 当第2个输入框失去焦点时, 提示这个输入框中的值
 */
  // 1、定义组件 // React中必须要结束标签
  class MyComponent extends React.Component{
    constructor(props){
      super(props)
      this.showInput = this.showInput.bind(this)
      this.handleBlur = this.handleBlur.bind(this)
    }

    showInput(){
      const input = this.refs.content
      // alert(input.value)
      alert(this.input.value)
    }

    handleBlur(event){
      alert(event.target.value)
    }

    render(){
      return(
        <div>
          <input type="text" ref="content"/>&nbsp;&nbsp;
          <input type="text" ref={input => this.input = input}/>&nbsp;&nbsp;
          <button onClick={this.showInput}>提示输入</button>&nbsp;&nbsp;
          <input type="text" placeholder="失去焦点提示内容" onBlur={this.handleBlur}/>
        </div>
      )
    }
  }

  // 2、渲染组件标签
  ReactDOM.render(<MyComponent/>, document.getElementById('example'))
</script>
```

### 2.5 组件的组合

效果

```md
功能：组件化实现此功能

1. 显示所有 todo 列表
2. 输入文本，点击按钮显示到列表的首位，并清除输入的文本
```

![component组合使用](https://cdn.wallleap.cn/img/pic/illustration/component组合使用.gif)

功能界面的组件化编码流程（无比重要）

1. 拆分组件：拆分界面，抽取组件

2. 实现静态组件：使用组件实现静态页面效果（只有静态界面，没有动态数据和交互）

3. 实现动态组件

   - 实现初始化数据动态显示

   - 实现交互功能(从绑定事件监听开始)

代码

```html
<div id="example"></div>

<script type="text/javascript" src="../js/react.development.js"></script>
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<script type="text/javascript" src="../js/prop-types.js"></script>
<script type="text/javascript" src="../js/babel.min.js"></script>
<script type="text/babel">
  // 静态组件——>动态组件
  /*
  * -名称、类型：todos、数组，Add需要、List需要
  * -数据保存在哪个组件内？
  *   放到App
  *   看数据是某个组件需要(给这个)，还是某些组件需要(给共同的父组件)
  * -需要在子组件中改变父组件的状态
  *    子组件中不能直接改变父组件的状态
  *    状态在哪个组件，更新状态的行为就应该定义在哪个组件，由子组件来调用(通过组件属性传递)
  *    父组件定义函数，传递给子组件，子组件调用
  */
  class App extends React.Component{

    constructor(props){
      super(props)
      // 初始化状态
      this.state = {
        todos: ['吃饭', '睡觉', '敲代码', '打游戏']
      }

      this.addTodo = this.addTodo.bind(this)  // 没定义加上bind
    }

    addTodo(todo){
      // this.state.todos.unshift(todo) // 不能这样做
      const {todos} = this.state
      todos.unshift(todo)
      // 更新状态
      this.setState({todos})
    }

    render(){
      const {todos} = this.state
      return(
        <div>
          <h1>Simple TODO List</h1>
          <Add count={todos.length} addTodo={this.addTodo}/>
          <List todos={todos}/>
        </div>
      )
    //  <List todos={this.state.todos}/> 前面赋值了
    }
  }

  class Add extends React.Component{
    constructor(props){
      super(props)
      this.add = this.add.bind(this)
    }
    add(){
      // 1、读取输入的数据
      const todo = this.todoInput.value.trim()
      // 2、检查合法性
      if(!todo){
        return
      }
      // 3、添加
      this.props.addTodo(todo)
      // 4、清除输入
      this.todoInput.value = ''
    }
    render(){
      return(
        <div>
          <input type="text" ref={input => this.todoInput=input}/>
          <button onClick={this.add}>add #{this.props.count+1}</button>
        </div>
      )
    }
  }
  Add.propTypes = {
    count: PropTypes.number.isRequired,
    addTodo: PropTypes.func.isRequired
  }

  class List extends React.Component{
    render(){
      return(
        <ul>
          {
            this.props.todos.map((todo, index) => <li key={index}>{todo}</li>)
          }
        </ul>
      )
      /*this.props.todos.map((todo, index) => {return <li key={index}>{todo}</li>})*/
      /* 加了大括号需要加return */
    }
  }

  List.protoTypes = {
    todos: PropTypes.array.isRequired
  }


  ReactDOM.render(<App />,document.getElementById('example'))
</script>
```

### 2.6 收集表单数据

效果

```md
需求：自定义包含表单的组件

1. 输入用户名密码后，点击登陆提示输入信息
2. 不提交表单
```

![component表单 (2)](https://cdn.wallleap.cn/img/pic/illustration/component表单.gif)

理解

- 问题：在 react 应用中，如何收集表单输入数据

- 包含表单的组件分类

  - 受控组件：表单项输入数据能自动收集成状态

  - 非受控组件：需要时才手动读取表单输入框中的数据

代码

```html
<div id="example"></div>

<script type="text/javascript" src="../js/react.development.js"></script>
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<script type="text/javascript" src="../js/babel.min.js"></script>
<script type="text/babel">
  /*
  需求: 自定义包含表单的组件
    1. 界面如下所示
    2. 输入用户名密码后, 点击登陆提示输入信息
    3. 不提交表单
  */
  class LoginForm extends React.Component{
    constructor(props){
      super(props)
      // 初始化状态
      this.state  = {
        pwd: ''
      }
      this.handleSubmit = this.handleSubmit.bind(this)
      this.handleChange = this.handleChange.bind(this)
    }

    handleSubmit(event){
      const name = this.nameInput.value // 非受控组件
      const {pwd} = this.state // 受控组件
      alert(`准备提交的用户名为${name}，密码为${pwd}`)
      // 阻止事件的默认行为
      event.preventDefault()
    }
    // 当事件和标签是同一个时，使用event更方便

    handleChange(event){
      // 读取输入的值
      const pwd = event.target.value
      // 更新pwd的状态
      this.setState({pwd})
    }

    render(){
      return(
        <form action="/test" onSubmit={this.handleSubmit}>
          用户名：<input type="text" ref={input => this.nameInput = input}/>
          密码：<input type="password" value={this.state.pwd} onChange={this.handleChange}/>
          <input type="submit" value="登录"/>
        </form>
      )
    }
    // 原生jsonChange事件是在失去焦点时触发，react中是输入则触发
  }
  
  ReactDOM.render(<LoginForm />, document.getElementById('example'))
</script>
```

### 2.7 组件生命周期

效果

```md
需求：自定义组件

1. 让指定的文本做显示/隐藏的渐变动画
2. 切换持续时间为 2s
3. 点击按钮从界面中移除组件界面
```

![component生命周期](https://cdn.wallleap.cn/img/pic/illustration/component生命周期.gif)

理解

- 组件对象从创建到死亡它会经历特定的生命周期阶段

- React 组件对象包含一系列的勾子函数（生命周期回调函数），在生命周期特定时刻回调

- 在定义组件时，可以重写特定的生命周期回调函数，做特定的工作

生命周期流程图

![生命周期流程图](https://cdn.wallleap.cn/img/pic/illustration/reactlife.png)

Mount：挂载，将虚拟标签放到容器（页面）中

render() 渲染

左边初始化过程，这些方法称为声明周期回调函数，或称为生命周期的勾子，这些方法在特定的时刻调用

> 回调函数：你定义的，你没有调用，但是最终执行了；声明式编程，流程设定好，命令式编程 jQuery，每一步自己操作

will 将、did 完成

生命周期详述

- 组件的三个生命周期状态:

  - Mount：插入真实 DOM

  - Update：被重新渲染

  - Unmount：被移出真实 DOM

- React 为每个状态都提供了勾子（hook）函数，可重写

  - `componentWillMount()`

  - `componentDidMount()`

  - `componentWillUpdate()`

  - `componentDidUpdate()`

  - `componentWillUnmount()`

- 生命周期流程:

  1. 第一次初始化渲染显示：`ReactDOM.render()`

     - constructor()：创建对象初始化 state

     - componentWillMount()：将要插入回调

     - render()：用于插入虚拟 DOM 回调

     - componentDidMount()：已经插入回调

  2. 每次更新 state：`this.setSate()`

     - componentWillUpdate()：将要更新回调

     - render()：更新（重新渲染）

     - componentDidUpdate()：已经更新回调

  3. 移除组件：`ReactDOM.unmountComponentAtNode(containerDom)`

     - componentWillUnmount()：组件将要被移除回调

三个阶段，可以都打印一下，看下方法执行的过程（与写的顺序无关，但推荐按阶段的顺序写，更直观）

重要的勾子

- render()：初始化渲染或更新渲染调用

- componentDidMount()：开启监听，发送 ajax 请求

- componentWillUnmount()：做一些收尾工作，如清理定时器

- componentWillReceiveProps()：后面需要时讲

代码

```html
<div id="example"></div>

<script type="text/javascript" src="../js/react.development.js"></script>
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<script type="text/javascript" src="../js/babel.min.js"></script>
<script type="text/babel">
  /*
  需求: 自定义组件
    1. 让指定的文本做显示/隐藏的动画
    2. 切换时间为2S
    3. 点击按钮从界面中移除组件界面
   */
  class Life extends React.Component{
    constructor(props){
      super(props)
      // 初始化状态
      this.state = {
        opacity: 1
      }

      this.distroyComponent = this.distroyComponent.bind(this)
    }

    distroyComponent(){
      ReactDOM.unmountComponentAtNode(document.getElementById('example'))
    }

    // 重写方法
    componentDidMount(){
      // 启动循环定时器
      this.intervalId = setInterval(function () { // 两个函数需要同一个变量，放到上一层共同组件上
        console.log('定时器执行……')
        let {opacity} = this.state
        opacity -= 0.1
        if(opacity<=0){
          opacity = 1
        }
        // 更新状态
        this.setState({opacity})
      }.bind(this), 200) // componentDidMount的this
    }
    componentWillUnmount(){
      // 清理定时器
      clearInterval(this.intervalId)
    }

    render(){ // 一旦改变，就会重新调用;永远写在其他下方，构造器在最上方
      const {opacity} = this.state
      return(
        <div>
          <h2 style={{opacity: opacity}}>{this.props.msg}</h2>
          <button onClick={this.distroyComponent}>不活了</button>
        </div>
      )
    } // style中两个大括号，外面的代表写的是js代码，里面的是对象（样式名：值，也可以写ES6）
  }

  ReactDOM.render(<Life msg="react太难了"/>, document.getElementById('example'))
</script>
```

### 2.8 虚拟 DOM 与 DOM Diff 算法

虚拟 DOM：减少操作真实 DOM 的次数，更新界面次数变少

DOM Diff 算法：计算哪里需要更新，哪里不需要更新，减少更新界面的区域

共同提高更新界面的效率

效果

![component虚拟DOM](https://cdn.wallleap.cn/img/pic/illustration/vDOM.gif)

```html
<div id="example"></div>
<br>

<script type="text/javascript" src="../js/react.development.js"></script>
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<script type="text/javascript" src="../js/babel.min.js"></script>
<script type="text/babel">
  /*
  验证:
  虚拟DOM+DOM Diff算法: 最小化页面重绘
  */

  class HelloWorld extends React.Component {
    constructor(props) {
      super(props)
      this.state = {
        date: new Date()
      }
    }

    componentDidMount () {
      setInterval(() => {
        this.setState({
          date: new Date()
        })
      }, 1000)
    }

    render () {
      console.log('render()')
      return (
        <p>
          Hello, <input type="text" placeholder="Your name here"/>!&nbsp;
          <span>It is {this.state.date.toTimeString()}</span>
        </p>
      )
    }
  }

  ReactDOM.render(
    <HelloWorld/>,
    document.getElementById('example')
  )
</script>
```

只有时间更新，其他不更新

基本原理图

![基本原理](https://cdn.wallleap.cn/img/pic/illustration/react-5.png)

- 初始化：虚拟 DOM 树(div>p>span……)，更新虚拟 DOM 界面不会变——>更新真实 DOM 界面才会变化（更新状态）

- 更新（关键）：调用 setState() 更新状态（会进行对比）——>根据差异更新真实 DOM、重绘页面变化的区域

## 三、react 应用（基于 react 脚手架）

### 3.1 使用 create-react-app 创建 react 应用

react脚手架

- xxx脚手架：用来帮助程序员快速创建一个基于xxx库的模板项目

  - 包含了所有需要的配置

  - 指定好了所有的依赖

  - 可以直接安装/编译/运行一个简单效果

- react 提供了一个用于创建 react 项目的脚手架库：create-react-app

- 项目的整体技术架构为：react + webpack + es6 + eslint

- 使用脚手架开发的项目的特点：模块化、组件化、工程化

创建项目并启动

```sh
npm install -g create-react-app  # 全局下载
create-react-app hello-react
cd hello-react
npm start
```

浏览器访问 <http://localhost:3000>

注：

```sh
npm root -g  # 查看全局下载目录
```

C:\Users\Shinelon\AppData\Roaming\npm\node_modules

react 脚手架项目结构

```md
ReactNews

 |--node_modules---第三方依赖模块文件夹

 |--public

   |-- index.html-----------------主页面

 |--scripts

   |-- build.js-------------------build打包引用配置

   |-- start.js-------------------start运行引用配置

 |--src------------源码文件夹

   |--components-----------------react组件
   
      |-- app.jsx
      
   |--index.css
   
   |--index.js-------------------应用入口js(main.js)

 |--.gitignore------git版本管制忽略的配置

 |--package.json----应用包配置文件 

 |--README.md-------应用描述说明的readme文件
```

`package.json`

- `"dependencies"`：运行时依赖
- `"devDependencies"`：开发时依赖，编译打包时需要，开发时不需要，编译打包时工具包

`public/index.html` 主界面

- 只有一个 `<div id="root"></div>`，依靠组件

`src/index.js` 应用入口

- 引入包(`import * from "*"`)、CSS(`import "*.css"`)
- 渲染组件

`README.md`对项目的说明文件

SPA(Single Page Application)：单应用

`index.html`

```html
<div id="root"></div>
```

`src/components/app.jsx`

```jsx
import React, {Component} from 'react'
import logo from '../logo.svg'

export default class App extends Component {
  render() {
    return(
      <div>
        <img className='logo' src={logo} alt="logo"/>
        <p className="title">react组件</p>
      </div>
    )
  }
}
```

`src/index.js`

```javascript
import React from 'react'
import ReactDOM from 'react-dom'
import App from './components/app'

import './index.css'

ReactDOM.render(<App />, document.getElementById('root'))
```

`src/index.css`

```css
.logo{
  width: 200px;
  height: 200px;
}
.title{
  color: red;
  font-size: 25px;
}
```

本地预览

`cd react_app`

`npm start` 或 `npm run start`

### 3.2 demo：评论管理

效果

![demo_comment](https://cdn.wallleap.cn/img/pic/illustration/demo_comment.gif)

拆分组件

![拆分组件](https://cdn.wallleap.cn/img/pic/illustration/image-20200708170522553.png)

应用组件：App

- state: comments/array

添加评论组件：CommentAdd

- state: username/string, content/string

- props: add/func

评论列表组件：CommentList

- props: comment/object, delete/func, index/number

评论项组件：CommentItem

- props: comments/array, delete/func

实现静态组件

`render(){return}` 中的内容

`src/index.js`

```javascript
import React from 'react'
import ReactDOM from 'react-dom'
import App from './components/app/app'

ReactDOM.render(<App/>, document.getElementById('root'))
```

`src/components/app/app.jsx`

```jsx
import React from 'react'
import CommentAdd from '../comment-add/comment-add'
import CommentList from '../comment-list/comment-list'

export default class App extends React.Component {

  constructor (props) {
    super(props)

    this.state = {
      comments: []
    }

    this.delete = this.delete.bind(this)
  }

  componentDidMount () {
    //模拟异步获取数据
    setTimeout(() => {
      const comments = [
        {
          username: "Tom",
          content: "ReactJS好难啊!",
          id: Date.now()
        },
        {
          username: "JACK",
          content: "ReactJS还不错!",
          id: Date.now() + 1
        }
      ]
      this.setState({
        comments
      })
    }, 1000)
  }

  add = (comment) => {
    let comments = this.state.comments
    comments.unshift(comment)
    this.setState({ comments })
  }

  delete (index) {
    let comments = this.state.comments
    comments.splice(index, 1)
    this.setState({ comments })
  }

  render () {
    return (
      <div>
        <header className="site-header jumbotron">
          <div className="container">
            <div className="row">
              <div className="col-xs-12">
                <h1>请发表对React的评论</h1>
              </div>
            </div>
          </div>
        </header>
        <div className="container">
          <CommentAdd add={this.add}/>
          <CommentList comments={this.state.comments} delete={this.delete}/>
        </div>
      </div>
    )
  }
}

// export default App 可以写到上面
```

`src/components/comment-add/comment-add.jsx`

```jsx
import React from 'react'
import PropTypes from 'prop-types'

class CommentAdd extends React.Component {
  constructor (props) {
    super(props)
    this.state = {
      username: '',
      content: ''
    }
    this.addComment = this.addComment.bind(this)
    this.changeUsername = this.changeUsername.bind(this)
    this.changeContent = this.changeContent.bind(this)
  }

  addComment () {
    // 根据输入的数据创建评论对象
    let { username, content } = this.state
    let comment = { username, content }
    // 添加到comments中, 更新state
    this.props.add(comment)
    // 清除输入的数据
    this.setState({
      username: '',
      content: ''
    })
  }

  changeUsername (event) {
    this.setState({
      username: event.target.value
    })
  }

  changeContent (event) {
    this.setState({
      content: event.target.value
    })
  }

  render () {
    return (
      <div className="col-md-4">
        <form className="form-horizontal">
          <div className="form-group">
            <label>用户名</label>
            <input type="text" className="form-control" placeholder="用户名"
                  value={this.state.username} onChange={this.changeUsername}/>
          </div>
          <div className="form-group">
            <label>评论内容</label>
            <textarea
              className="form-control" rows="6"
              placeholder="评论内容"
              value={this.state.content} onChange={this.changeContent}></textarea>
          </div>
          <div className="form-group">
            <div className="col-sm-offset-2 col-sm-10">
              <button type="button" className="btn btn-default pull-right" onClick={this.addComment}>提交</button>
            </div>
          </div>
        </form>
      </div>
    )
  }
}
CommentAdd.propTypes = {
  add: PropTypes.func.isRequired
}

export default CommentAdd
```

`src/components/comment-list/comment-list.css`

```css
.reply {
  margin-top: 0px;
}
```

`src/components/comment-list/comment-list.jsx`

```jsx
import React from 'react'
import PropTypes from 'prop-types'
import CommentItem from '../comment-item/comment-item'
import './commentList.css'
class CommentList extends React.Component {
  constructor (props) {
    super(props)
  }
  render () {
    let comments = this.props.comments
    let display = comments.length > 0 ? 'none' : 'block'
    return (
      <div className="col-md-8">
        <h3 className="reply">评论回复：</h3>
        <h2 style={{ display: display }}>暂无评论，点击左侧添加评论</h2>
        <ul className="list-group">
          {
            comments.map((comment, index) => {
              console.log(comment)
              return <CommentItem comment={comment} key={index} index={index} delete={this.props.delete}/>
            })
          }
        </ul>
      </div>
    )
  }
}
CommentList.propTypes = {
  comments: PropTypes.array.isRequired,
  delete: PropTypes.func.isRequired
}
export default CommentList
```

`src/components/comment-item/comment-item.css`

```css
li {
  transition: .5s;
  overflow: hidden;
}

.handle {
  width: 40px;
  border: 1px solid #ccc;
  background: #fff;
  position: absolute;
  right: 10px;
  top: 1px;
  text-align: center;
}

.handle a {
  display: block;
  text-decoration: none;
}

.list-group-item .centence {
  padding: 0px 50px;
}

.user {
  font-size: 22px;
}
```

`src/components/comment-item/comment-item.jsx`

```jsx
import React from 'react'
import PropTypes from 'prop-types'
import './commentItem.css'

class CommentItem extends React.Component {
  constructor (props) {
    super(props)
    this.deleteComment = this.deleteComment.bind(this)
  }

  deleteComment () {
    let username = this.props.comment.username
    if (window.confirm(`确定删除${username}的评论吗?`)) {
      this.props.delete(this.props.index)
    }
  }

  render () {
    let comment = this.props.comment
    return (
      <li className="list-group-item">
        <div className="handle">
          <a href="javascript:" onClick={this.deleteComment}>删除</a>
        </div>
        <p className="user"><span >{comment.username}</span><span>说:</span></p>
        <p className="centence">{comment.content}</p>
      </li>
    )
  }
}
CommentItem.propTypes = {
  comment: PropTypes.object.isRequired,
  index: PropTypes.number.isRequired,
  delete: PropTypes.func.isRequired
}

export default CommentItem
```

实现动态组件

动态展示初始化数据

- 初始化状态数据

- 传递属性数据

响应用户操作, 更新组件界面

- 绑定事件监听, 并处理

- 更新 state

## 四、react ajax

### 4.1 理解

前置说明

- React 本身只关注于界面，并不包含发送 ajax 请求的代码

- 前端应用需要通过 ajax 请求与后台进行交互（json 数据）

- react 应用中需要集成第三方 ajax 库（或自己封装）

常用的 ajax 请求库

- jQuery：比较重，如果需要另外引入不建议使用

- **axios**：轻量级，建议使用

  a. 封装 XmlHttpRequest 对象的 ajax

  b. promise 风格

  c. 可以用在浏览器端和 node 服务器端

- fetch：原生函数，但老版本浏览器不支持

  a. 不再使用 XmlHttpRequest 对象提交 ajax 请求

  b. 为了兼容低版本的浏览器，可以引入兼容库 fetch.js

效果

```md
需求：

1. 界面效果如下
2. 根据指定的关键字在 GitHub 上搜索匹配的最受关注的库
3. 显示库名，点击链接查看库

测试接口: https://api.github.com/search/repositories?q=r&sort=stars
```

![ajax](https://cdn.wallleap.cn/img/pic/illustration/ajax.gif)

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>11_ajax</title>
  <style>
    h2{
      text-align: center;
      margin-top: 200px;
    }
  </style>
</head>
<body>
<div id="example"></div>

<script type="text/javascript" src="../js/react.development.js"></script>
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<script type="text/javascript" src="../js/babel.min.js"></script>

<script type="text/javascript" src="https://cdn.bootcdn.net/ajax/libs/axios/0.19.2/axios.js"></script>

<script type="text/babel">
  /*
  需求:
    1. 界面效果如下
    2. 根据指定的关键字在github上搜索匹配的最受关注的库
    3. 显示库名, 点击链接查看库
    4. 测试接口: https://api.github.com/search/repositories?q=r&sort=stars
  */
  class MostStarRepo extends React.Component{
    state = {
      repoName: '',
      repoUrl: ''
    }

    componentDidMount(){
      // 使用axios发送异步的ajax请求
      const url = `https://api.github.com/search/repositories?q=re&sort=stars`
      axios.get(url)
          .then(response => {
            const result = response.data
            // console.log(response)
            // 得到数据
            const {name, html_url} = result.items[0]
            // 更新状态
            this.setState({repoName:name, repoUrl: html_url})
          })
          .catch((error) => {
            alert(error.message)
          })
      // 使用fetch发送异步的ajax请求
      /*fetch(url)
          .then(response => {
            return response.json()
          })
          .then(data => {
            // 得到数据
            const {name, html_url} = data.items[0]
            // 更新状态
            this.setState({repoName:name, repoUrl: html_url})
          })
      */
    }

    render(){
      const {repoName, repoUrl} = this.state
      if(!repoName){
        return(
          <h2>LOADING...</h2>
        )
      }else{
        return(
          <h2>Most star repo is <a href={repoUrl}>{repoName}</a></h2>
        )
      }
      
    }
  }
  ReactDOM.render(<MostStarRepo />, document.getElementById('example'))
</script>
</body>
</html>
```

### 4.2 axios

文档：

https://github.com/axios/axios

相关 API：

GET 请求

```javascript
axios.get('/user?ID=12345')
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });

axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

POST 请求

```javascript
axios.post('/user', {
  firstName: 'Fred',
  lastName: 'Flintstone'
})
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

### 4.3 Fetch

文档

- <https://github.github.io/fetch/>

- <https://segmentfault.com/a/1190000003810652>

相关 API

GET 请求

```javascript
fetch(url).then(function(response) {
    return response.json()
  }).then(function(data) {
    console.log(data)
  }).catch(function(e) {
    console.log(e)
  });
```

POST 请求

```javascript
fetch(url, {
    method: "POST",
    body: JSON.stringify(data),
  }).then(function(data) {
    console.log(data)
  }).catch(function(e) {
    console.log(e)
  })
```

### 4.4 demo：github users

效果

![demo_users](https://cdn.wallleap.cn/img/pic/illustration/demo_users.gif)

拆分组件

![拆分组件](https://cdn.wallleap.cn/img/pic/illustration/image-20200711091558440.png)

```md
App

​       * state: searchName/string

  Search

​      * props: setSearchName/func

  List

​      * props: searchName/string

​      * state: firstView/bool, loading/bool, users/array, errMsg/string
```

编写静态组件、编写动态组件

componentWillReceiveProps(nextProps)：监视接收到新的 props，发送 ajax

使用 axios 库发送 ajax 请求

`public/index.html`

```html
<div id="root"></div>
```

`src/index.js`

```javascript
import React from 'react'
import { render } from 'react-dom'

import App from './components/app'
import './index.css'

render(<App />, document.getElementById('root'))
```

`src/index.css`

```css
.album {
  min-height: 50rem; /* Can be removed; just added for demo purposes */
  padding-top: 3rem;
  padding-bottom: 3rem;
  background-color: #f7f7f7;
}

.card {
  float: left;
  width: 33.333%;
  padding: .75rem;
  margin-bottom: 2rem;
  border: 1px solid #efefef;
  text-align: center;
}

.card > img {
  margin-bottom: .75rem;
  border-radius: 100px;
}

.card-text {
  font-size: 85%;
}
```

`src/components/app.jsx`

```jsx
import React from 'react'
import Search from './search'
import UserList from './user-list'

export default class App extends React.Component {

  state = {
    searchName: ''
  }

  refreshName = (searchName) => this.setState({searchName})

  render() {
    return (
      <div className="container">
        <section className="jumbotron">
          <h3 className="jumbotron-heading">Search Github Users</h3>
          <Search refreshName={this.refreshName}/>
        </section>
        <UserList searchName={this.state.searchName}/>
      </div>
    )
  }
}
```

`src/components/search.jsx`

```jsx
/**
 * 上部的搜索模块
*/
import React, {Component} from 'react'
import PropTypes from 'prop-types'

class Search extends Component {

  static propTypes = {
    refreshName: PropTypes.func.isRequired
  }

  search = () => {
    var name = this.nameInput.value
    this.props.refreshName(name)
  }

  render() {
    return (
      <div>
        <input type="text" placeholder="enter the name you search"
              ref={(input => this.nameInput = input)}/>
        <button onClick={this.search}>Search</button>
      </div>
    )
  }
}

export default Search
```

`src/components/user-list.jsx`

```jsx
/**
 * 下部的用户列表模块
*/
import React from 'react'
import PropTypes from 'prop-types'
import axios from 'axios'
// npm install axios --save 

class UserList extends React.Component {

  static propTypes = {
    searchName: PropTypes.string.isRequired
  }

  state = {
    firstView: true,
    loading: false,
    users: null,
    error: null
  }

  async componentWillReceiveProps(nextProps)  {
    let searchName = nextProps.searchName
    console.log('发送ajax请求', searchName)
    const url = `https://api.github.com/search/users?q=${searchName}`
    this.setState({ firstView: false, loading: true })

    // 使用axios库
    axios.get(url)
      .then((response) => {
        console.log(response)
        this.setState({ loading: false, users: response.data.items })
      })
      .catch((error)=>{
        // debugger
        console.log('error', error.response.data.message, error.message)
        this.setState({ loading: false, error: error.message })
      })

    try {
      const result = await axios.get(url)
      this.setState({ loading: false, users: result.data.items })
    } catch(err) {
      // debugger
      console.log('----', err.message)
    }
  }

  render () {

    if (this.state.firstView) {
      return <h2>Enter name to search</h2>
    } else if (this.state.loading) {
      return <h2>Loading result...</h2>
    } else if (this.state.error) {
      return <h2>{this.state.error}</h2>
    } else {
      return (
        <div className="row">
          {
            this.state.users.map((user) => (
              <div className="card" key={user.html_url}>
                <a href={user.html_url} target="_blank">
                  <img src={user.avatar_url} style={{width: '100px'}} alt='user'/>
                </a>
                <p className="card-text">{user.login}</p>
              </div>
            ))
          }
        </div>
      )
    }
  }
}

export default UserList
```

## 五、几个重要技术总结

### 5.1 组件间通信

#### 5.1.1 方式一：通过 props 传递

- 共同的数据放在父组件上，特有的数据放在自己组件内部（state）

- 通过 props 可以传递一般数据和函数数据，只能一层一层传递

- 一般数据-->父组件传递数据给子组件-->子组件读取数据

- 函数数据-->子组件传递数据给父组件-->子组件调用函数

父组件传到孙组件、兄弟组件之间不能直接通信，经过子组件、服务器传递

#### 5.1.2 方式二：使用消息订阅（subscribe）-发布（publish）机制

工具库: PubSubJS

下载: `npm install pubsub-js --save`

使用:

```javascript
import PubSub from 'pubsub-js' //引入
PubSub.publish('delete', data) //发布消息
// 消息名，消息
PubSub.subscribe('delete', function(msg, data){ }); //订阅
// 消息名，回调函数
```

以上一个用户搜索的 demo 为例，search 和 userlist(main) 之间需要通信，它们是兄弟组件

在这里是通过父组件，利用 props 进行通信

![props-search](https://cdn.wallleap.cn/img/pic/illustration/image-20200714161016458.png)

这是以前的 app.ejs

![app.ejs](https://cdn.wallleap.cn/img/pic/illustration/image-20200714161302225.png)

现在不通过父组件来通信

`src/components/app.ejs`

```ejs
import React from 'react'
import Search from './search'
import UserList from './user-list'

export default class App extends React.Component {

  render() {
    return (
      <div className="container">
        <section className="jumbotron">
          <h3 className="jumbotron-heading">Search Github Users</h3>
          <Search/>
        </section>
        <UserList/>
      </div>
    )
  }

}
```

`src/components/search.ejs`

```ejs
/**
* 上部的搜索模块
*/
import React, {Component} from 'react'
import PropTypes from 'prop-types'
import PubSub from 'pubsub-js' //引入
class Search extends Component {
  search = () => {
    var searchName = this.nameInput.value
    if(searchName){
      // 搜索
      // 发布消息 search
PubSub.publish('search', searchName)
    }
  }
  render() {
    return (
      <div>
        <input type="text" placeholder="enter the name you search"
              ref={(input => this.nameInput = input)}/>
        <input type="submit" value="Search" onClick={this.search} />
      </div>
    )
  }
}
export default Search
```

`src/components/user-list.ejs`

```ejs
/**
* 下部的用户列表模块
*/
import React from 'react'
import PropTypes from 'prop-types'
import axios from 'axios'
import PubSub from 'pubsub-js' //引入
class UserList extends React.Component {
  static propTypes = {
    searchName: PropTypes.string.isRequired
  }
  state = {
    firstView: true,
    loading: false,
    users: null,
    error: null
  }
  componentDidMount(){
    // 订阅消息 search
  PubSub.subscribe('search', (msg, searchName) => { // 指定了新的name，需要请求    
      this.setState({ firstView: false, loading: true })
      // 使用axios库
      const url = `https://api.github.com/search/users?q=${searchName}`
      axios.get(url)
        .then((response) => {
    console.log(response)
          this.setState({ loading: false, users: response.data.items })
        })
        .catch((error)=>{
          // debugger       console.log('error', error.response.data.message, error.message)
          this.setState({ loading: false, error: error.message })
        })
      try {
        const result = axios.get(url)
        this.setState({ loading: false, users: result.data.items })
      } catch(err) {
        // debugger
        console.log('----', err.message)
      }
    })
  }
  render () {
    if (this.state.firstView) {
      return <h2>Enter name to search</h2>
    } else if (this.state.loading) {
      return <h2>Loading result...</h2>
    } else if (this.state.error) {
      return <h2>{this.state.error}</h2>
    } else {
      return (
        <div className="row">
          {         this.state.users.map((user) => (
              <div className="card" key={user.html_url}>
                <a href={user.html_url} target="_blank">
                  <img src={user.avatar_url} style={{width: '100px'}} alt='user'/>
                </a>
                <p className="card-text">{user.login}</p>
              </div>
            ))
          }
        </div>
      )
    }
  }
}
export default UserList
```

再以之前的评论的为例

App.ejs 中有个删除评论的函数，传给了 List 组件(并没有用到)，接着传给 Item

```jsx
delete={this.delete}
```

#### 5.1.3 方式三：redux

redux 是一个状态管理工具，后面专门讲解

### 5.2 事件监听理解

#### 5.2.1 原生 DOM 事件

- 绑定事件监听

  - 事件名（类型）：只有有限的几个，不能随便写

  - 回调函数

- 触发事件

  - 用户操作界面

  - 事件名（类型）

  - 数据

#### 5.2.2 自定义事件（消息机制）

- 绑定事件监听

  - 事件名（类型）：任意

  - 回调函数：通过形参接收数据，在函数体处理事件

- 触发事件（编码）

  - 事件名（类型）：与绑定的事件监听的事件名一致

  - 数据：会自动传递给回调函数

### 5.3 ES 6 常用新语法

- 定义常量/变量：`const/let`

- 解构赋值：`let {a, b} = this.props`、`import {aa} from 'xxx'`

- 对象的简洁表达：`{a, b}`

- 箭头函数：

  - 常用场景

    - 组件的自定义方法：`xxx = () => {}`

    - 参数匿名函数

  - 优点：

    - 简洁

    - 没有自己的 this，使用引用 this 查找的是外部 this

- 扩展(三点)运算符：拆解对象/数组 `(const MyProps = {}, <Xxx {...MyProps}>)`

- 类：`class/extends/constructor/super`

- ES 6 模块化：`export default | import`

## 六、react-router 4

### 6.1 相关理解

#### 6.1.1 react-router 的理解

- react 的一个插件库（依赖/基于 React）

- 专门用来实现一个 SPA 应用

- 基于 react 的项目基本都会用到此库

#### 6.1.2 SPA的理解

- 单页 Web 应用（single page web application, SPA）

- 整个应用只有一个完整的页面

- 点击页面中的链接不会刷新页面，本身也不会向服务器发请求

- 当点击路由链接时，只会做页面的**局部更新**

- 数据都需要通过 **ajax 请求**获取，并在前端**异步展现**

#### 6.1.3 路由的理解

- 什么是路由?

  - 一个路由就是一个**映射关系(key: value)**

  - key 为**路由路径（path）**，value 可能是 function(后台路由)/**component（前台路由）**

- 路由分类

  - 后台路由：node 服务器端路由value 是 function，用来处理客户端提交的请求并返回一个响应数据

  - 前台路由：浏览器端路由，value 是 component，当请求的是路由 path 时，浏览器端前没有发送 http 请求，但界面会更新显示对应的组件

- 后台路由

  - 注册路由：`router.get(path, function(req, res))`

  - 当 node 接收到一个请求时，根据请求路径找到匹配的路由，调用路由中的函数来处理请求，返回响应数据

- 前端路由

  - 注册路由：`<Route path="/about" component={About}>`

  - 当浏览器的 **hash** 变为 `#about` 时，当前路由组件就会变为 About 组件

#### 6.1.4 前端路由的实现

底层实现：

history 库

- 网址：<https://github.com/ReactTraining/history>

- 管理浏览器会话历史（history）的工具库

- 包装的是原生 BOM 中 `window.history` 和 `window.location.hash`

- history API

  - `History.createBrowserHistory()`：得到封装 `window.history` 的管理对象

  - `History.createHashHistory()`：得到封装 `window.location.hash` 的管理对象

  - `history.push()`：添加一个新的历史记录

  - `history.replace()`：用一个新的历史记录替换当前的记录

  - `history.goBack()`：回退到上一个历史记录

  - `history.goForward()`：前进到下一个历史记录

  - `history.listen(function(location){})`：监视历史记录的变化

测试：

![history-方式1](https://cdn.wallleap.cn/img/pic/illustration/history-方式1.gif)

![history-方式2](https://cdn.wallleap.cn/img/pic/illustration/history-方式2.gif)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>history test</title>
</head>
<body>

  <p><input type="text"></p>
  <a href="/test1" onclick="return push('/test1')">test1</a><br><br>
  <button onClick="push('/test2')">push test2</button><br><br>
  <button onClick="back()">回退</button><br><br>
  <button onClick="forward()">前进</button><br><br>
  <button onClick="replace('/test3')">replace test3</button><br><br>

  <script type="text/javascript" src="https://cdn.bootcss.com/history/4.7.2/history.js"></script>
  <script type="text/javascript">
    let history = History.createBrowserHistory() // 方式一
    history = History.createHashHistory() // 方式二
    // console.log(history)

    function push (to) {
      history.push(to)
      return false
    } // 可以返回

    function back() {
      history.goBack()
    }

    function forward() {
      history.goForward()
    }

    function replace (to) {
      history.replace(to)
    } // 不能返回

    history.listen((location) => {
      console.log('请求路由路径变化了', location)
    })
  </script>
</body>
</html>
```

### 6.2 react-router 相关 API

[react_router](https://reactrouter.com/)

![react-router](https://cdn.wallleap.cn/img/pic/illustration/image-20200714181151269.png)

[web](https://reactrouter.com/web/guides/quick-start)

#### 6.2.1 组件

- `<BrowserRouter>`：BrowserRouter 是 react 路由的容器

- `<HashRouter>`：这个是用来兼容老浏览器的

- `<Route>`：Route 的作用就是用来渲染路由匹配的组件。路由渲染有三种方式，每一种方式都可以传递 match,location,history 对象

- `<Redirect>`：路由重定向

- `<Link>`：Link 的作用和 a 标签类似

- `<NavLink>`：NavLink 和 Link 一样最终都是渲染成 a 标签，NavLink 可以给这个 a 标签添加额外的属性

- `<Switch>`：Switch 组件内部可以是 Route 或者 Redirect，只会渲染第一个匹配的元素

#### 6.2.2 其它

- **`history` 对象**：这里的 history 对象是使用 history 插件生成的，<http://www.cnblogs.com/ye-hcj/p/7741742.html> 已经详细讲过了

  - 记住一点，在使用 location 做对比的使用，通过 history 访问的 location 是动态变化的，最好通过 Route 访问 location

- `match`对象：match 对象表示当前的路由地址是怎么跳转过来的

- `withRouter` 函数：当一个非路由组件也想访问到当前路由的 match,location,history 对象，那么 withRouter 将是一个非常好的选择

### 6.3 基本路由使用

![react-router demo](https://cdn.wallleap.cn/img/pic/illustration/react-router%20demo1%20(3).gif)

并没有刷新页面

准备

下载 react-router：`npm install --save react-router@4`

我们只需要web版本：`npm install --save react-router-dom`

由于使用到了 BootStrap，因此在 index.html 中引入 bootstrap.css： `<link rel="stylesheet" href="/css/bootstrap.css">`

`public/index.html`

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta name="theme-color" content="#000000">
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json">
    <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico">
    <title>React-router</title>
    <link rel="stylesheet" href="/css/bootstrap.css">
  </head>
  <body>
    <noscript>
      You need to enable JavaScript to run this app.
    </noscript>
    <div id="root"></div>
  </body>
</html>
```

一般会将路由组件和非路由组件分开写

`pages`/`views` 存放路由组件

`components` 存放其他组件

路由组件：`views/about.jsx`

```jsx
import React,{Component} from 'react'
export default class About extends Component{
  render(){
    return(
      <div>About组件内容</div>
    )
  }
}
```

路由组件：`views/home.jsx`

```jsx
import React, {Component} from 'react'

export default class Home extends Component{
  render(){
    return (
    <div>Home组件内容</div>
    )
  }
}
```

包装 NavLink 组件：`components/my-nav-link.jsx`，由于每个 NavLink 都需要自定义 active 样式（加入属性 activeClassName），因此提出来

```jsx
import React, {Component} from 'react'
import {NavLink} from 'react-router-dom'

export default class MyNavLink extends Component {
  render(){
    // 利用this.props三点运算符接受所有的属性
    return(
      <NavLink {...this.props} activeClassName='activeClass'/>
    )
  }
}
```

应用组件：`components/app.jsx`

```jsx
import React from 'react'
import {NavLink, Route, Switch, Redirect} from 'react-router-dom'
import MyNavLink from './my-nav-link'
import About from '../views/about'
import Home from '../views/home'

export default class App extends React.Component {

  render() {
    return (
      <div>
        <div className="row">
          <div className="col-xs-offset-2 col-xs-8">
            <div className="page-header">
              <h2>React Router Demo</h2>
            </div>
          </div>
        </div>

        <div className="row">
          <div className="col-xs-2 col-xs-offset-2">
            <div className="list-group">
              {/*导航路由链接，不能使用a标签，to指向的path*/}
              <MyNavLink className="list-group-item" to='/about'>About</MyNavLink>
              <MyNavLink className="list-group-item" to='/home'>Home</MyNavLink>
            </div>
          </div>
          <div className="col-xs-6">
            <div className="panel">
              <div className="panel-body">
                {/*可切换的路由组件，使用switch只有匹配才显示，route的path对应上方的to、component对应路由组件，Redirect自动重定向到about、默认到about组件*/}
                <Switch>
                  <Route path='/about' component={About}/>
                  <Route path='/home' component={Home}/>
                  <Redirect to='/about'/>
                </Switch>
              </div>
            </div>
          </div>
        </div>
      </div>
    )
  }
}
```

自定义样式：`index.css`

```css
activeClass {
  color: red !important;
}
```

入口JS：`index.js`

```javascript
import React from 'react'
//import ReactDOM from 'react-dom'
import {render} from 'react-dom'
import {BrowserRouter, HashRouter} from 'react-router-dom'
import App from './components/app'

import './index.css'

// ReactDOM.render(
render(
  (
    <BrowserRouter>
      <App/>
    </BrowserRouter>
    /* 组件需要用路由器组件包含起来，两者任选一个 */
    /*<HashRouter>
      <App />
    </HashRouter>*/
  ),
  document.getElementById('root')
)
```

总结：如何编写路由效果？

1. 编写路由组件
2. 在父路由组件中指定
   - 路由连接：`<NavLink></NavLink>`
   - 路由：`<Route></Route>`

### 6.4 嵌套路由使用

嵌套路由——路由组件中的路由

![react-router demo2](https://cdn.wallleap.cn/img/pic/illustration/react-router-demo2.gif)

二级路由组件：`views/news.jsx`

```jsx
import React from 'react'

export default class News extends React.Component {
  state = {
    newsArr: ['news001', 'news002', 'news003']
  }

  render () {
    return (
      <div>
        <ul>
          {
            this.state.newsArr.map((news, index) => <li key={index}>{news}</li>)
          }
        </ul>
      </div>
    )
  }
}
```

二级路由组件：`views/message.jsx`

```jsx
import React from 'react'
import {Link, Route} from 'react-router-dom'

export default class Message extends React.Component {
  state = {
    messages: []
  }

  componentDidMount () {
    // 模拟发送ajax请求
    setTimeout(() => {
      const data = [
        {id: 1, title: 'Message001'},
        {id: 3, title: 'Message003'},
        {id: 6, title: 'Message006'},
      ]
      this.setState({
        messages: data
      })
    }, 1000)
  }

  render () {
    const path = this.props.match.path

    return (
      <div>
        <ul>
          {
            this.state.messages.map((m, index) => {
              return (
                <li key={index}>
                  <a href='???'>{m.title}</a>
                </li>
              )
            })
          }
        </ul>
      </div>
    )
  }
}
```

一级路由组件：`views/home.jsx`

```jsx
import React, {Component} from 'react'
import {Switch, Route, Redirect} from 'react-router-dom'
import MyNavLink from '../components/my-nav-link'
import News from './news'
import Message from './message'

export default class Home extends Component{
  render(){
    return (
      <div>
        <h2>Home组件内容</h2>
        <div>
          <ul className="nav nav-tabs">
            <li>
              <MyNavLink to='/home/news'>News</MyNavLink>
            </li>
            <li>
              <MyNavLink to="/home/message">Message</MyNavLink>
            </li>
          </ul>
          <Switch>
            <Route path='/home/news' component={News} />
            <Route path='/home/message' component={Message} />
            <Redirect to='/home/news'/>
          </Switch>
        </div>
      </div>
    )
  }
}
```

### 6.5 向路由组件传递参数数据

传递的是 id 值

![react-router demo3 (2)](https://cdn.wallleap.cn/img/pic/illustration/react-router-demo3.gif)

三级路由组件：`views/message-detail.jsx`

```jsx
import React from 'react'

const messageDetails = [
  {id: 1, title: 'Message001', content: '中国，你是最棒的'},
  {id: 3, title: 'Message003', content: '对的，没错，非常赞成楼上'},
  {id: 6, title: 'Message006', content: '我也赞成'},
]

// 函数的组件
export default function MessageDetail(props) {

  const id = props.match.params.id
  const md = messageDetails.find(md => md.id===id*1)

  return (
    <ul>
      <li>ID: {md.id}</li>
      <li>TITLE: {md.title}</li>
      <li>CONTENT: {md.content}</li>
    </ul>
  )
}
```

二级路由组件：`views/message.jsx`

```jsx
import React from 'react'
import {Link, Route} from 'react-router-dom'
import MessageDetail from "./message-detail"

export default class Message extends React.Component {
  state = {
    messages: []
  }

  componentDidMount () {
    // 模拟发送ajax请求
    setTimeout(() => {
      const data = [
        {id: 1, title: 'Message001'},
        {id: 3, title: 'Message003'},
        {id: 6, title: 'Message006'},
      ]
      this.setState({
        messages: data
      })
    }, 1000)
  }

  render () {
    const path = this.props.match.path

    return (
      <div>
        <ul>
          {
            this.state.messages.map((m, index) => {
              return (
                <li key={index}>
                  <Link to={`${path}/${m.id}`}>{m.title}</Link>
                </li>
              )
            })
          }
        </ul>
        <Route path={`${path}/:id`} component={MessageDetail}></Route>
      </div>
    )
  }
}
```

路由链接与非路由链接：是否发了请求（路由连接不发）

- `<NavLink to=''></NavLink>`
- `<Link to=''></Link>`
- `<a href=''></a>`

### 6.6 多种路由跳转方式

前面讲的路由切换都是通过点击链接的方式切换的，不是链接也能够

![react-router demo4](https://cdn.wallleap.cn/img/pic/illustration/react-router-demo4.gif)

二级路由：`views/message.jsx`

```jsx
import React from 'react'
import {Link, Route} from 'react-router-dom'
import MessageDetail from "./message-detail"

export default class Message extends React.Component {
  state = {
    messages: []
  }

  componentDidMount () {
    // 模拟发送ajax请求
    setTimeout(() => {
      const data = [
        {id: 1, title: 'Message001'},
        {id: 3, title: 'Message003'},
        {id: 6, title: 'Message006'},
      ]
      this.setState({
        messages: data
      })
    }, 1000)
  }

  // props中有history属性，它由push等方法
  ShowDetail = (id) => {
    this.props.history.push(`/home/message/${id}`)
  }

  ShowDetail2 = (id) => {
    this.props.history.replace(`/home/message/${id}`)
  }

  back = () => {
    this.props.history.goBack()
  }

  forward = () => {
    this.props.history.goForward()
  }

  render () {
    const path = this.props.match.path

    return (
      <div>
        <ul>
          {
            this.state.messages.map((m, index) => {
              return (
                <li key={index}>
                  <Link to={`${path}/${m.id}`}>{m.title}</Link>
                  &nbsp;&nbsp;&nbsp;
                  <button onClick={() => this.ShowDetail(m.id)}>查看详情(push)</button>&nbsp;
                  <button onClick={() => this.ShowDetail2(m.id)}>查看详情(replace)</button>
                </li>
              )
            })
          }
        </ul>
        <p>
          <button onClick={this.back}>返回</button>&nbsp;
          <button onClick={this.forward}>前进</button>&nbsp;
        </p>
        <hr/>
        <Route path={`${path}/:id`} component={MessageDetail}></Route>
        {/*<Route path={`home/message/meassagedetail/:id`} component={MessageDetail}></Route>*/}
      </div>
    )
  }
}
```

总结：

- 路由器标签
  - `<BrowserRouter>`：BrowserRouter 是 react 路由的容器
  - `<HashRouter>`：多了一个 `#` 号

- 路由
  - `<Route>`：Route 的作用就是用来渲染路由匹配的组件。路由渲染有三种方式，每一种方式都可以传递 match,location,history 对象

- `<Redirect>`：路由重定向

- 链接
  - `<Link>`：Link的作用和a标签类似
  - `<NavLink>`：可以添加其他属性，例如 activeClassName
- `<Switch>`：Switch 组件内部可以是 Route 或者 Redirect，只会渲染第一个匹配的元素

- `this.props.`
  - `match`
    - `params`
  - `history`
    - `push()`
    - `replace()`
    - `goback()`
    - `goforward()`

## 七、react-ui

### 7.1 最流行的开源 React UI 组件库

#### 7.1.1 material-ui（国外）

- 官网：<http://www.material-ui.com/#/>

- GitHub：<https://github.com/callemall/material-ui>

#### 7.1.2 ant-design（国内蚂蚁金服）

- PC 官网：<https://ant.design/index-cn>

- 移动官网：<https://mobile.ant.design/index-cn>

- Github：<https://github.com/ant-design/ant-design/>

- Github：<https://github.com/ant-design/ant-design-mobile/>

### 7.2 ant-design-mobile 使用入门

![antd-mobile](https://cdn.wallleap.cn/img/pic/illustration/antd-mobile.gif)

使用 create-react-app 创建 react 应用

```bash
npm install create-react-app -g
create-react-app antm-demo
cd antm-demo
npm start
```

搭建 antd-mobile 的基本开发环境

下载 `npm install antd-mobile --save`

`src/components/App.jsx`

```jsx
import React, {Component} from 'react'
import {Button, Toast} from 'antd-mobile'
export default class App extends Component {
  handleClick = () => {
    Toast.info('提交成功', 2)
  }

  render() {
    return (
        <div>
          <Button type="primary" onClick={this.handleClick}>提交</Button>
        </div>   
      )
  }
  /* type值不同样式不同 */
}
```

`src/index.js`

```javascript
import React from 'react';
import {render} from 'react-dom'
import App from "./components/App"
// 引入整体css
import 'antd-mobile/dist/antd-mobile.css'

render(<App />, document.getElementById('root'))
```

`index.html`

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no" />
    <meta name="theme-color" content="#000000">
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json">
    <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico">
    <title>React ant design mobile</title>
    <script src="https://as.alipayobjects.com/g/component/fastclick/1.0.6/fastclick.js"></script>
    <script>
      if ('addEventListener' in document) {
        document.addEventListener('DOMContentLoaded', function() {
          FastClick.attach(document.body);
        }, false);
      }
      if(!window.Promise) {
        document.writeln('<script src="https://as.alipayobjects.com/g/component/es6-promise/3.2.2/es6-promise.min.js"'+'>'+'<'+'/'+'script>');
      }
    </script>
  </head>
  <body>
    <noscript>
      You need to enable JavaScript to run this app.
    </noscript>
    <div id="root"></div>
  </body>
</html>
```

实现按需打包(组件 js/css)

下载依赖包

```bash
yarn add react-app-rewired --dev
yarn add babel-plugin-import --dev
```

修改默认配置：`package.json`

```json
{
  "name": "react_ui",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "antd-mobile": "^2.1.3",
    "react": "^16.2.0",
    "react-dom": "^16.2.0"
  },
  "devDependencies": {
    "babel-plugin-import": "^1.6.3",
    "react-app-rewired": "^1.4.0",
    "react-scripts": "1.0.17"
  },
  "scripts": {
    "start": "react-app-rewired start",
    "build": "react-app-rewired build",
    "test": "react-app-rewired test --env=jsdom"
  }
}
```

`config-overrides.js`

```javascript
const {injectBabelPlugin} = require('react-app-rewired');
module.exports = function override(config, env) {
  config = injectBabelPlugin(['import', {libraryName: 'antd-mobile', style: 'css'}], config);
  return config;
};
```

编码

```jsx
// import 'antd-mobile/dist/antd-mobile.css'
// import Button from 'antd-mobile/lib/button'
// import Toast from 'antd-mobile/lib/toast' 
import {Button, Toast} from 'antd-mobile'
```

## 八、redux

### 8.1 redux 理解

学习文档

- 英文文档: <https://redux.js.org/>

- 中文文档: <http://www.redux.org.cn/>

- Github: <https://github.com/reactjs/redux>

redux 是什么?

- redux 是一个独立专门用于做**状态管理**的 **JS 库**（不是 react 插件库）

- 它可以用在 react、angular、vue 等项目中，但基本与 react 配合使用

- 作用：**集中式管理** react 应用中多个组件共享的状态

redux 工作流程

![redux](https://cdn.wallleap.cn/img/pic/illustration/image-20200715104120743.png)

什么情况下需要使用 redux

- 总体原则：能不用就不用, 如果不用比较吃力才考虑使用

- 某个组件的状态，需要共享

- 某个状态需要在任何地方都可以拿到

- 一个组件需要改变全局状态

- 一个组件需要改变另一个组件的状态

### 8.2 redux 的核心 API

#### 8.2.1 `createStore()`

作用：创建包含指定 reducer 的 store 对象

编码:

```js
import {createStore} from 'redux'
import counter from './reducers/counter'
const store = createStore(counter)
```

#### 8.2.2 `store`对象

作用：redux 库最核心的管理对象

它内部维护着：

- `state`

- `reducer`

核心方法：

- `getState()`

- `dispatch(action)`

- `subscribe(listener)`

编码:

```js
store.getState()
store.dispatch({type:'INCREMENT', number})
store.subscribe(render)
```

#### 8.2.3 `applyMiddleware()`

作用：应用上基于 redux 的中间件（插件库）

编码：

```js
import {createStore, applyMiddleware} from 'redux'
import thunk from 'redux-thunk' // redux异步中间件
const store = createStore(
counter,
applyMiddleware(thunk) // 应用上异步中间件
)
```

#### 8.2.4 `combineReducers()`

作用：合并多个 reducer 函数

编码：

```js
export default combineReducers({
  user,
  chatUser,
  chat
})
```

### 8.3 redux的三个核心概念

#### 8.3.1 `action`

标识要执行行为的对象

包含 2 个方面的属性

- type：标识属性，值为字符串，唯一，必要属性

- xxx：数据属性，值类型任意，可选属性

例子：

```js
const action = {
  type: 'INCREMENT',
  data: 2
}
```

- Action Creator（创建 Action 的工厂函数）

```js
const increment = (number) => ({type: 'INCREMENT', data: number})
```

#### 8.3.2 `reducer`

根据老的 state 和 action，产生新的 state 的纯函数

样例

```js
export default function counter(state = 0, action) {
  switch (action.type) {
    case 'INCREMENT':
      return state + action.data
    case 'DECREMENT':
      return state - action.data
    default:
      return state
  }
}
```

注意

- 返回一个新的状态

- 不要修改原来的状态

#### 8.3.3 `store`

将 state、action 与 reducer 联系在一起的对象

如何得到此对象?

```js
import {createStore} from 'redux'
import reducer from './reducers'
const store = createStore(reducer)
```

此对象的功能?

- getState()：得到 state

- dispatch(action)：分发 action，触发 reducer 调用，产生新的 state

- subscribe(listener)：注册监听，当产生了新的 state 时，自动调用

### 8.4 使用 redux 编写应用

效果

![redux](https://cdn.wallleap.cn/img/pic/illustration/redux.gif)

使用 react 实现

![app.jsx](https://cdn.wallleap.cn/img/pic/illustration/image-20200715112226383.png)

![index.js](https://cdn.wallleap.cn/img/pic/illustration/image-20200715112313127.png)

下载依赖包

```sh
npm install --save redux
```

`src/redux/action-types.js`

```javascript
/*
Action对象的type常量名称模块
*/
export const INCREMENT = 'increment'
export const DECREMENT = 'decrement'
```

`src/redux/actions.js`

```javascript
/*
action creator模块
*/
import {INCREMENT, DECREMENT} from './action-types'

export const increment = number => ({type: INCREMENT, number})
export const decrement = number => ({type: DECREMENT, number})
```

`src/redux/reducers.js`

```javascript
/*
包含n个reducer函数的模块
根据老的state和指定action, 处理返回一个新的state
*/
import {INCREMENT, DECREMENT} from './action-types'

export function counter(state = 0, action) {
  console.log('counter', state, action)
  switch (action.type) {
    case INCREMENT:
      return state + action.number
    case DECREMENT:
      return state - action.number
    default:
      return state
  }
}
```

`src/components/app.jsx`

```jsx
/*
应用组件
*/
import React, {Component} from 'react'
import PropTypes from 'prop-types'
import * as actions from '../redux/actions'
import { INCREMENT } from '../redux/action-types'

export default class App extends Component {
  static propTypes = {
    store: PropTypes.object.isRequired,
  }

  increment = () => {
    // 1.得到选择增加数量
    const number = this.refs.numSelect.value * 1
    // 2.调用store的方法更新状态
    this.props.store.dispatch(actions.increment(number))
  }

  decrement = () => {
    // 1.得到选择减小数量
    const number = this.refs.numSelect.value * 1
    // 2.调用store的方法更新状态
    this.props.store.dispatch(actions.decrement(number))
  }

  incrementIfOdd = () => {
    // 1.得到选择增加数量
    const number = this.refs.numSelect.value * 1
    // 2.得到原本的count状态
    let count = this.props.store.getState()
    // 判断，满足条件猜更新状态
    if (count % 2 === 1) {
      // 调用store的方法更新状态
      this.props.store.dispatch(actions.increment(number))
    }
  }

  incrementAsync = () => {
    // 1.得到选择增加数量
    const number = this.refs.numSelect.value * 1
    // 2.启动延时定时器，模拟异步
    setTimeout(() => {
      // 3.调用store的方法更新状态
      this.props.store.dispatch(actions.increment(number))
    }, 1000)
  }

  render() {
    const count = this.props.store.getState()
    return (
      <div>
        <p>
          click {count} times {' '}
        </p>
        <select ref="numSelect">
          <option value="1">1</option>
          <option value="2">2</option>
          <option value="3">3</option>
        </select>{' '}
        <button onClick={this.increment}>+</button>
        {' '}
        <button onClick={this.decrement}>-</button>
        {' '}
        <button onClick={this.incrementIfOdd}>increment if odd</button>
        {' '}
        <button onClick={this.incrementAsync}>increment async</button>
      </div>
    )
  }
}
```

`src/index.js`

```javascript
import React from 'react'
import ReactDOM from 'react-dom'
import {createStore} from 'redux'

import App from './components/app'
import {counter} from './redux/reducers'

// 根据counter函数创建store对象
const store = createStore(counter) // 内部会第一次调用reduer函数，得到初始state

// 定义渲染根组件标签的函数
const render = () => {
  ReactDOM.render(
    <App store={store}/>,
    document.getElementById('root')
  )
}
// 初始化渲染
render()

// 注册(订阅)监听, 一旦状态发生改变, 自动重新渲染
store.subscribe(render)
```

也可以把 `index.js` 中 `store` 提取出来

`src/redux/store.js`

```javascript
import {createStore} from 'redux'
import {counter} from './reducers'
// 根据counter函数创建store对象
const store = createStore(counter)  // // 内部会第一次调用reduer函数，得到初始state

export default store
```

`src/index.js`

```javascript
import React from 'react'
import ReactDOM from 'react-dom'

import App from './components/app'
import store from './redux/store'

// 定义渲染根组件标签的函数
const render = () => {
  ReactDOM.render(
    <App store={store}/>,
    document.getElementById('root')
  )
}
// 初始化渲染
render()

// 注册(订阅)监听, 一旦状态发生改变, 自动重新渲染
store.subscribe(render)
```

问题

- redux 与 react 组件的代码耦合度太高（大多数地方用到 store）

- 编码不够简洁

### 8.5 react-redux

#### 8.5.1 理解

- 一个 **react 插件库**

- 专门用来简化 react 应用中使用 redux

#### 8.5.2 React-Redux 将所有组件分成两大类

- UI 组件

  - 只负责 UI 的呈现，不带有任何业务逻辑

  - 通过 props 接收数据（一般数据和函数）

  - 不使用任何 Redux 的 API

  - 一般保存在 `components` 文件夹下

- 容器组件

  - 负责管理数据和业务逻辑，不负责 UI 的呈现

  - 使用 Redux 的 API

  - 一般保存在 `containers` 文件夹下

#### 8.5.3 相关API

`Provider`

让所有组件都可以得到state数据

```js
<Provider store={store}>
   <App />
</Provider>
```

`connect()`

用于包装 UI 组件生成容器组件

```js
import { connect } from 'react-redux'
connect(
   mapStateToprops,
   mapDispatchToProps
)(Counter)
```

`mapStateToprops()`

将外部的数据（即 state 对象）转换为 UI 组件的标签属性

```js
const mapStateToprops = function (state) {
  return {
   value: state
  }
}
```

`mapDispatchToProps()`

将分发 action 的函数转换为 UI 组件的标签属性

简洁语法可以直接指定为 actions 对象或包含多个 action 方法的对象

#### 8.5.4 使用 react-redux

下载依赖包

```sh
npm install --save react-redux
```

`redux/action-types.js`

不变

`redux/actions.js`

不变

`redux/reducers.js`

不变

`components/counter.jsx`

```jsx
/*
UI组件: 不包含任何redux API
*/
import React from 'react'
import PropTypes from 'prop-types'

export default class Counter extends React.Component {

  static propTypes = {
    count: PropTypes.number.isRequired,
    increment: PropTypes.func.isRequired,
    decrement: PropTypes.func.isRequired
  }

  increment = () => {
    const number = this.refs.numSelect.value * 1
    this.props.increment(number)
  }

  decrement = () => {
    const number = this.refs.numSelect.value * 1
    this.props.decrement(number)
  }

  incrementIfOdd = () => {
    const number = this.refs.numSelect.value * 1
    let count = this.props.count
    if (count % 2 === 1) {
      this.props.increment(number)
    }
  }

  incrementAsync = () => {
    const number = this.refs.numSelect.value * 1
    setTimeout(() => {
      this.props.increment(number)
    }, 1000)
  }

  render() {
    return (
      <div>
        <p>
          click {this.props.count} times {' '}
        </p>
        <select ref="numSelect">
          <option value="1">1</option>
          <option value="2">2</option>
          <option value="3">3</option>
        </select>{' '}
        <button onClick={this.increment}>+</button>
        {' '}
        <button onClick={this.decrement}>-</button>
        {' '}
        <button onClick={this.incrementIfOdd}>increment if odd</button>
        {' '}
        <button onClick={this.incrementAsync}>increment async</button>
      </div>
    )
  }
}
```

`containers/app.jsx`

```jsx
/*
包含Counter组件的容器组件
*/
import React from 'react'
// 引入连接函数
import {connect} from 'react-redux'
// 引入action函数
import {increment, decrement} from '../redux/actions'

import Counter from '../components/counter'

// 向外暴露连接App组件的包装组件
export default connect(
  state => ({count: state}),
  {increment, decrement}
)(Counter)
```

`store.js`

不变

`index.js`

```javascript
import React from 'react'
import ReactDOM from 'react-dom'
import {Provider} from 'react-redux'

import App from './containers/app'
import store from './redux/store'

// 定义渲染根组件标签的函数
ReactDOM.render(
  (
    <Provider store={store}>
      <App/>
    </Provider>
  ),
  document.getElementById('root')
)
```

问题

- redux 默认是不能进行异步处理的（前面的都是 react 实现的）

- 应用中又需要在 redux 中执行异步任务（ajax、定时器等）

### 8.6 redux 异步编程

下载 redux 插件（异步中间件）

```sh
npm install --save redux-thunk
```

`redux/store.js`

```javascript
import React from 'react'
import {createStore, applyMiddleware} from 'redux'
import thunk from 'redux-thunk'
import {composeWithDevTools} from 'redux-devtools-extension'

import reducers from './reducers'

// 根据counter函数创建store对象
export default createStore(
  reducers,
  applyMiddleware(thunk) // 应用上异步中间件
)
```

`index.js`

```javascript
import React from 'react'
import ReactDOM from 'react-dom'
import {Provider} from 'react-redux'

import App from './containers/app'
import store from './redux/store'

// 定义渲染根组件标签的函数
ReactDOM.render(
  (
    <Provider store={store}>
      <App/>
    </Provider>
  ),
  document.getElementById('root')
)
```

`redux/actions.js`

```jsx
/*
action creator模块
*/
import {
  INCREMENT,
  DECREMENT
} from './action-types'

export const increment = number => ({type: INCREMENT, number})

export const decrement = number => ({type: DECREMENT, number})

// 异步action creator(返回一个函数)
export const incrementAsync = number => {
  return dispatch => { // 要在这返回一个函数，得在store中应用上异步中间件
    // 异步的代码
    setTimeout(() => {
      // 1s之后才分发一个增加的action
      dispatch(increment(number))
    }, 1000)
  }
}
```

同步的 action 都返回一个对象

异步的 action 返回的是一个函数

`components/counter.jsx`

```jsx
/*
包含Counter组件的容器组件
*/
import React from 'react'
import PropTypes from 'prop-types'

export default class Counter extends React.Component {

  static propTypes = {
    count: PropTypes.number.isRequired,
    increment: PropTypes.func.isRequired,
    decrement: PropTypes.func.isRequired
  }

  increment = () => {
    const number = this.refs.numSelect.value*1
    this.props.increment(number)
  }

  decrement = () => {
    const number = this.refs.numSelect.value*1
    this.props.decrement(number)
  }

  incrementIfOdd = () => {
    const number = this.refs.numSelect.value*1
    let count = this.props.count
    if(count%2===1) {
      this.props.increment(number)
    }
  }

  // Async
  incrementAsync = () => {
    const number = this.refs.numSelect.value*1
    this.props.incrementAsync(number)
  }

  render () {
    return (
      <div>
        <p>
          click {this.props.count} times {' '}
        </p>
        <select ref="numSelect">
          <option value="1">1</option>
          <option value="2">2</option>
          <option value="3">3</option>
        </select>{' '}
        <button onClick={this.increment}>+</button>{' '}
        <button onClick={this.decrement}>-</button>{' '}
        <button onClick={this.incrementIfOdd}>increment if odd</button>{' '}
        <button onClick={this.incrementAsync}>increment async</button>
      </div>
    )
  }
}
```

`containers/app.jsx`

```jsx
/*
包含Counter组件的容器组件
*/
import React from 'react'
// 引入连接函数
import {connect} from 'react-redux'
// 引入action函数
import {increment, decrement, incrementAsync} from '../redux/actions'
import Counter from '../components/counter'

// 向外暴露连接App组件的包装组件
export default connect(
  state => ({count: state.counter}),
  {increment, decrement, incrementAsync}
)(Counter)
```

`redux/action-types.js`

```javascript
export const INCREMENT = 'increment'
export const DECREMENT = 'decrement'
```

### 8.7 使用上 redux 调试工具

安装 Chrome 浏览器插件

[Redux DevTools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?utm_source=chrome-ntp-icon)

下载工具依赖包

```sh
npm install --save-dev redux-devtools-extension
```

编码

```javascript
import { composeWithDevTools } from 'redux-devtools-extension'
const store = createStore(counter, composeWithDevTools(applyMiddleware(thunk)))
```

### 8.8 Redux 版评论

需求

使用 react_redux 和中间件实现异步评论功能

安装

```bash
……
npm install --save react-redux
npm install --save redux-thunk
npm install --save-dev redux-devtools-extension
```

目录结构

```md
> - REACT_REDUX
>   - public
>     - css
>       - bootstrap.css
>     - index.html
>   - src
>     - components
>       - app
>         - app.jsx
>       - comment-add
>         - comment-add.jsx
>       - comment-item
>         - comment-item.jsx
>         - comment-item.css
>       - comment-list
>         - comment-list.jsx
>         - comment-list.css
>     - redux
>       - action-types.js
>       - actions.js
>       - reducers.js
>       - store.js
>     - index.js
```

文件内容

`public/index.html`

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta name="theme-color" content="#000000">
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json">
    <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico">
    <title>React App</title>
    <link rel="stylesheet" href="/css/bootstrap.css">
  </head>
  <body>
    <noscript>
      You need to enable JavaScript to run this app.
    </noscript>
    <div id="root"></div>
  </body>
</html>
```

`src/index.js`

```javascript
import React from 'react'
import ReactDOM from 'react-dom'
import {Provider} from 'react-redux'

import App from './components/app/app'
import store from './redux/store'

// 定义渲染根组件标签的函数
ReactDOM.render(
  (
    <Provider store={store}>
      <App/>
    </Provider>
  ),
  document.getElementById('root')
)
```

`src/components/app/app.jsx`

```jsx
import React from 'react'
import {connect} from 'react-redux'
import CommentAdd from '../comment-add/comment-add'
import CommentList from '../comment-list/comment-list'
import {getComments} from '../../redux/actions'

class App extends React.Component {

  componentDidMount() {
    //模拟异步获取数据
    this.props.getComments()
  }

  render() {
    return (
      <div>
        <header className="site-header jumbotron">
          <div className="container">
            <div className="row">
              <div className="col-xs-12">
                <h1>请发表对React的评论</h1>
              </div>
            </div>
          </div>
        </header>
        <div className="container">
          <CommentAdd/>
          <CommentList/>
        </div>
      </div>
    )
  }
}

export default connect(
  null,
  {getComments}
)(App)
```

`src/components/comment-add/comment-add.jsx`

```jsx
import React from 'react'
import PropTypes from 'prop-types'
import {connect} from 'react-redux'
import {addComment} from '../../redux/actions'
class CommentAdd extends React.Component {
  constructor (props) {
    super(props)
    this.state = {
      username: '',
      content: ''
    }
    this.addComment = this.addComment.bind(this)
    this.changeUsername = this.changeUsername.bind(this)
    this.changeContent = this.changeContent.bind(this)
  }
  addComment () {
    // 根据输入的数据创建评论对象
    let { username, content } = this.state
    let comment = { username, content }
    // 添加到comments中, 更新state
    this.props.addComment(comment)
    // 清除输入的数据
    this.setState({
      username: '',
      content: ''
    })
  }
  changeUsername (event) {
    this.setState({
      username: event.target.value
    })
  }
  changeContent (event) {
    this.setState({
      content: event.target.value
    })
  }
  render () {
    return (
      <div className="col-md-4">
        <form className="form-horizontal">
          <div className="form-group">
            <label>用户名</label>
            <input type="text" className="form-control" placeholder="用户名"
                  value={this.state.username} onChange={this.changeUsername}/>
          </div>
          <div className="form-group">
            <label>评论内容</label>
            <textarea
             className="form-control" rows="6" placeholder="评论内容"
              value={this.state.content} onChange={this.changeContent}></textarea>
          </div>
          <div className="form-group">
            <div className="col-sm-offset-2 col-sm-10">
              <button type="button" className="btn btn-default pull-right" onClick={this.addComment}>提交</button>
            </div>
          </div>
        </form>
      </div>
    )
  }
}
CommentAdd.propTypes = {
  addComment: PropTypes.func.isRequired
}
export default connect(
  null,
  {addComment}
)(CommentAdd)
```

`src/components/comment-item/comment-item.jsx`

```jsx
import React from 'react'
import PropTypes from 'prop-types'
import {connect} from 'react-redux'
import './commentItem.css'
import {deleteComment} from '../../redux/actions'
class CommentItem extends React.Component {
  constructor(props) {
    super(props)
  }
  deleteComment = () => {
    let username = this.props.comment.username
    if (window.confirm(`确定删除${username}的评论吗?`)) {
      this.props.deleteComment(this.props.index)
    }
  }
  render() {
    let comment = this.props.comment
    return (
      <li className="list-group-item">
        <div className="handle">
          <a href="javascript:" onClick={this.deleteComment}>删除</a>
        </div>
        <p className="user"><span>{comment.username}</span><span>说:</span></p>
        <p className="centence">{comment.content}</p>
      </li>
    )
  }
}
CommentItem.propTypes = {
  comment: PropTypes.object.isRequired,
  index: PropTypes.number.isRequired,
  deleteComment: PropTypes.func.isRequired
}
export default connect(
  null,
  {deleteComment}
)(CommentItem)

```

`src/components/comment-item/comment-item.css`

```css
li {
  transition: .5s;
  overflow: hidden;
}
.handle {
  width: 40px;
  border: 1px solid #ccc;
  background: #fff;
  position: absolute;
  right: 10px;
  top: 1px;
  text-align: center;
}
.handle a {
  display: block;
  text-decoration: none;
}
.list-group-item .centence {
  padding: 0px 50px;
}
.user {
  font-size: 22px;
}
```

`src/components/comment-list/comment-list.jsx`

```jsx
import React from 'react'
import PropTypes from 'prop-types'
import {connect} from 'react-redux'
import CommentItem from '../comment-item/comment-item'
import './commentList.css'
class CommentList extends React.Component {
  render () {
    let comments = this.props.comments
    let display = comments.length > 0 ? 'none' : 'block'
    return (
      <div className="col-md-8">
        <h3 className="reply">评论回复：</h3>
        <h2 style=双大括号 display: display 双大括号>暂无评论，点击左侧添加评论！！！</h2>
        <ul className="list-group">
          {
            comments.map((comment, index) => {
              console.log(comment)
              return <CommentItem comment={comment} key={index} index={index}/>
            })
          }
        </ul>
      </div>
    )
  }
}
CommentList.propTypes = {
  comments: PropTypes.array.isRequired,
}
export default connect(
  state => ({comments: state.comments})
)(CommentList)
```

`src/components/comment-list/comment-list.css`

```css
.reply {
  margin-top: 0px;
}
```

`redux/action-types.js`

```javascript
export const ADD_COMMENT = 'ADD_COMMENT'
export const DELETE_COMMENT = 'DELETE_COMMENT'
export const RECEIVE_COMMENTS = 'RECEIVE_COMMENTS'
```

`redux/actions.js`

```javascript
import {
  ADD_COMMENT,
  DELETE_COMMENT,
  RECEIVE_COMMENTS
} from './action-types'
export const addComment = (comment) => ({type: ADD_COMMENT, data: comment})
export const deleteComment = (index) => ({type: DELETE_COMMENT, data: index})
const receiveComments = (comments) => ({type: RECEIVE_COMMENTS, data: comments})
export const getComments = () => {
  return dispatch => {
    setTimeout(() => {
      const comments = [
        {
          username: "Tom",
          content: "ReactJS好难啊!",
          id: Date.now()
        },
        {
          username: "JACK",
          content: "ReactJS还不错!",
          id: Date.now() + 1
        }
      ]
      dispatch(receiveComments(comments))
    }, 1000)
  }
}
```

`redux/reducers.js`

```javascript
import {combineReducers} from 'redux'
import {
  ADD_COMMENT,
  DELETE_COMMENT,
  RECEIVE_COMMENTS
} from './action-types'
const initComments = []
function comments(state = initComments, action) {
  switch (action.type) {
    case ADD_COMMENT:
      return [...state, action.data]
    case DELETE_COMMENT:
      return state.filter((c, index) => index !== action.data)
    case RECEIVE_COMMENTS:
      return action.data
    default:
      return state
  }
}
export default combineReducers({
  comments
})
```

`redux/store.js`

```javascript
import React from 'react'
import {createStore, applyMiddleware} from 'redux'
import thunk from 'redux-thunk'
import {composeWithDevTools} from 'redux-devtools-extension'
import reducers from './reducers'
// 根据counter函数创建store对象
export default createStore(
  reducers,
  composeWithDevTools(applyMiddleware(thunk)) // 应用上异步中间件
)
```

### 8.9 相关重要知识：纯函数和高阶函数

#### 8.9.1 纯函数

- 一类特别的函数：只要是同样的输入，必定得到同样的输出

  - 必须遵守以下一些约束

    - 不得改写参数

    - 不能调用系统 I/O 的 API

    - 能调用 `Date.now()` 或者 `Math.random()` 等不纯的方法

- reducer函数必须是一个纯函数

#### 8.9.2 高阶函数

- 理解：一类特别的函数

  - 情况 1：参数是函数（回调函数）

  - 情况 2：返回是函数（新的函数）

- 常见的高阶函数：

  - 定时器设置函数：setTimeout()/setInterval()

  - 数组的 map()/filter()/reduce()/find()/bind()

  - react-redux 中的 connect 函数

- 作用：能实现更加动态，更加可扩展的功能
