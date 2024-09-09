---
title: 再学 React 之函数组件
date: 2024-04-02 16:54
updated: 2024-04-02 16:54
cover: //cdn.wallleap.cn/img/pic/cover/202302ihq49n.jpg
category: 技术杂谈
tags:
  - web
  - 前端
description: 再学 React 之函数组件
---

之前学 React 的时候，版本还是 16，虽然可以用函数组件，但是用到 state 时只能用 Class 组件。Class 组件比函数组件代码量更多，而且需要写一些冗余的代码。React 16.8 新增了 Hooks API，而且现在[官方文档](https://react.dev/)也推荐写函数组件。

## 创建函数组件

直接定义一个函数，然后 `return` JSX（可以在 [babel](https%3A%2F%2Fbabeljs.io%2Frepl%23%3Fbrowsers%3Ddefaults%252C%20not%20ie%2011%252C%20not%20ie_mob%2011%26build%3D%26builtIns%3Dfalse%26corejs%3D3.21%26spec%3Dfalse%26loose%3Dfalse%26code_lz%3DDwCwTAfIm_GPRmgAcoKjlC_ioB1NAjfoN7lgHpwSA%26debug%3Dfalse%26forceAllTransforms%3Dfalse%26modules%3Dfalse%26shippedProposals%3Dfalse%26circleciRepo%3D%26evaluate%3Dfalse%26fileSize%3Dfalse%26timeTravel%3Dfalse%26sourceType%3Dmodule%26lineWrap%3Dtrue%26presets%3Denv%252Creact%252Cstage-2%26prettier%3Dfalse%26targets%3D%26version%3D7.24.4%26externalPlugins%3D%26assumptions%3D%7B%7D) 在线网址上查看转换的 `render`/`jsx` 函数），这个函数就是一个**函数组件**

```js
function App() {
  return <h2>这是一个函数组件</h2>
}
// 或者箭头函数
const App = () => <h2>这是一个函数组件</h2>
```

使用的时候可以调用它 `App()`，但推荐的方式是组件写成组件形式 `<App />`（JSX 中为了区分 HTML 元素和组件，规定组件以大写字母开头，并且需要闭合）

在一个组件内使用另一个组件的时候，直接导入并使用

`return` 后最好加上 `()` 包裹住 JSX 元素，由于组件只能返回一个元素，如果不想用 `div` 包裹可以使用 `fragment`（简写 `<></>`）

```js
import { createRoot } from "react-dom/client"

const App = () => {
  return (
    <>
      <h1>我是 App 组件</h1>
      <Child />
    </>
  )
}
const Child = () => <h2>我是 Child 组件</h2>

const rootElement = document.getElementById("root")
const root = createRoot(rootElement)

// root.render(App())
root.render(<App />)
```

## props

可以直接在子组件上写属性，然后在接收的时候以参数形式获取

```js
const App = () => {
  const msg = "Hello, "
  return (
    <>
      <h1>我是 App 组件</h1>
      <Child msg={msg} /> {/* JSX 里 JS 内容都写在 `{}` 中 */}
    </>
  )
}
const Child = (props) => <h2>{props.msg}我是 Child 组件</h2>
```

## 转用函数组件的两个问题

- 如何写状态
- 类组件中的生命周期

第一个问题可以通过 `useState` 解决，第二个问题可以用 `useEffect` 等 Hooks 模拟

### useState 状态钩子

用法：

- 传入一个参数作为初始值
- 得到一个数组
  - 第一项为状态变量 `xxx`
  - 第二项为一个函数，传入新的值以“修改”状态，一般命名为 `setXxx`
- 注意点：不能在组件外使用；不能在 `if` 等条件语句中使用

```js
import { useState, StrictMode } from "react"
import { createRoot } from "react-dom/client"

const App = () => {
  const [count, setCount] = useState(0)
  const increment = () => setCount((count) => count + 1)
  return (
    <>
      <h2>{count}</h2>
      <button onClick={increment}>+</button> {/* 所有的属性名都是小驼峰写法，onClick、className */}
    </>
  )
}

const rootElement = document.getElementById("root")
const root = createRoot(rootElement)

root.render(
  <StrictMode>
    <App />
  </StrictMode> // 用于在开发环境下进行严格模式的检查
)
```

### useEffect 副作用钩子模拟生命周期

useEffect 用法：

- 传入两个参数
  - 第一个参数为一个函数，里面写“副作用”（除了计算以外的操作，例如获取后端数据、打印日志、修改 DOM 等），渲染/变化的时候会执行
    - 可以 `return` 一个函数，函数中可以清除之前的“副作用”（例如定时器等），在组件卸载的时候会执行该函数
  - 第二个参数为数组，里面写依赖项（可选）
    - 没有设置第二个参数，则用到的所有变量都依赖（相当于全写在数组中）
    - 设置了空数组，代表没有依赖项，只有在第一次加载进入的时候执行一次，后面组件重新渲染并不会执行
    - 数组中写了的依赖项，当依赖项变化时重新执行

- 返回值为 `undefined`

```js
import { useEffect, useState, StrictMode } from "react"
import { createRoot } from "react-dom/client"

const App = () => {
  const [count, setCount] = useState(0)
  const [childVisible, setChildVisible] = useState(false)
  const increment = () => setCount((count) => count + 1)
  useEffect(() => {
    console.log("依赖项为 count", count) // 每次 count 变化都会执行
  }, [count])
  useEffect(() => {
    console.log("依赖项为所有", count) // 每次渲染都会执行
  })
  useEffect(() => {
    console.log("没有依赖项", count) // 只在首次渲染时执行
  }, [])
  return (
    <>
      <h2>{count}</h2>
      <button onClick={increment}>+</button>
      {childVisible ? (
        <button onClick={() => setChildVisible(false)}>hide</button>
      ) : (
        <button onClick={() => setChildVisible(true)}>show</button>
      )}
      {childVisible && <Child />}
    </>
  )
}

const Child = () => {
  const [m, setM] = useState(0)
  useEffect(() => {
    const timerId = setInterval(() => {
      setM((m) => m + 1)
    }, 1000)
    console.log("子组件依赖项 m", m) // m 变化执行
    return () => {
      console.log("return 的函数中") // 组件卸载执行
      clearInterval(timerId)
    };
  }, [m])
  return <div>我是子组件 {m}</div>
}

const rootElement = document.getElementById("root")
const root = createRoot(rootElement)

root.render(
  <StrictMode>
    <App />
  </StrictMode> // 用于在开发环境下进行严格模式的检查
)
```

总结：

- 第二个参数传入空数组 `[]` 模拟 componentDidMount
- 第二个参数传入依赖项数组或不传模拟 componentDidUpdate
- 第一个参数 `return` 函数模拟 componentWillUnmount
- constructor 不需要模拟，在函数组件执行的时候，就相当于 constructor
- 函数组件的返回值就是 render 的返回值 


## JSX 中技巧

### 条件渲染

直接使用 if-else 或其他判断语句/运算符

```js
let content
if (isLoggedIn) {
  content = <AdminPanel />
} else {
  content = <LoginForm />
}
const [visible, setVisible] = useState(false)
return (
  <>
    {content}
    isLoggedIn ? <AdminPanel /> : <LoginForm />
    visible && <Child />
  </>
)
```

### 列表渲染

JSX 中没办法直接使用 for 进行循环，可以使用数组的 map 方法或者将元素 push 到一个数组中

```js
const products = [
  { title: 'Cabbage', id: 1 },
  { title: 'Garlic', id: 2 },
  { title: 'Apple', id: 3 },
]
const listItems = products.map(product =>
  <li
    key={product.id} // 必须有一个唯一的 key
    style={{ color: product.id % 2 === 0 ? "green" : "blue" }} // JSX 中 style 里面应该是一个对象
  >
    {product.title}
  </li>
)

return <ul>{listItems}</ul>
```

### JSX 注释形式

```js
function MyComponent() {
  return (
    // 在 JSX 周围
    <div>
      {/* JSX 里面 */}
      <Hello // 标签里面
        message="Hello, World!" // 标签里面
      /> 
    </div>
  )
}
```
