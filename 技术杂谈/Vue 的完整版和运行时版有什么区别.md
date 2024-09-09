---
title: Vue 的完整版和运行时版有什么区别
date: 2023-06-02 20:13
updated: 2023-06-02 20:13
cover: https://cdn.wallleap.cn/img/pic/cover/vue.jpg
author: Luwang
comments: true
rating: 1
tags:
  - web
  - Vue
category: 技术杂谈
keywords:
  - Vue
  - JS 框架
  - 前端
description: Vue 的完整版和运行时版有什么区别
---

引入 CDN 文件时，Vue 有两个版本，完整版和运行时版，两者有什么区别呢？

在了解这两个版本之前，我们先了解一下 Vue

- 读作 View，意为 MVC 中的 V
- MVC 中的 V 是 Vue 的重点，M 和 C 被简化（是 MV* 框架）
  - Vue 0.x 宣传的是 MVVM
  - 后面的是 MV*

## 官方文档

- 英文：[Vue.js (vuejs.org)](https://v2.vuejs.org/)
- 中文：[Vue.js (vuejs.org)](https://v2.cn.vuejs.org/)

> 渐进式 JavaScript 框架
> The Progressive JavaScript Framework

## 创建 Vue 项目

现在可以直接用 Vite，但是我们在这里先用 Vue Cli 创建

### 使用 [Vue CLI](https://cli.vuejs.org/zh/) 来创建这个项目

- 在终端中使用命令 `npm install -g @vue/cli` 安装 @vue-cli
- 安装完成之后运行 `vue --version` 查看版本
- 运行 `vue create vue-demo` 创建一个项目，进行一些配置选择
  - Manually select features
  - Babel, CSS Pre-processors（使用空格选择，完全选择完之后回车确认）
- 创建完成之后按照提示进入目录，`npm run serve` 进行预览

### 自己从零开始搭建 Vue 项目

- 使用 webpack 或者 rollup

## 两个版本

在官网中[不同版本区别](https://v2.cn.vuejs.org/v2/guide/installation.html#%E5%AF%B9%E4%B8%8D%E5%90%8C%E6%9E%84%E5%BB%BA%E7%89%88%E6%9C%AC%E7%9A%84%E8%A7%A3%E9%87%8A)可以看到除开生产或开发版和模块化，可以分为两个版本**完整版（vue.js）和运行时版本（vue.runtime.js）**

![两个版本](https://cdn.wallleap.cn/img/pic/illustration/202306041331312.png)

- 两个版本
  - 完整版 `vue.js`、`vue.min.js`
    - 从 HTML 得到视图
    - 同时包含编译器（Compiler）和运行时（Runtime）的构建
  - 运行时版本 `vue.runtime.js`
    - 用 JS 构建视图
    - 需要自己写 h 函数（渲染函数）
    - h 也可以交给 vue-loader，把 `.vue` 文件翻译成 h 构建方法，这样做 HTML 就只有一个 `div#app` ，SEO 不友好
- `main.js` 中 `const vm = new Vue({})`
- 编译器负责把模板字符串编译成 JS 渲染函数的代码
- 运行时负责创建 Vue 实例的代码，渲染和修补虚拟 DOM 等。基本上去掉了编译器。

### 用完整版 Vue 实现点击加一

**完整版** Vue 的写法：

在 HTML/模板（`template`）中用到了模板字符串、指令等，需要用到 Compiler（`{{count}}` → `0`、`v-if`、`v-for`  等）

```html
<div id="app">
  {{count}}
  <button @click="add">+1</button>
</div>
<script>
new Vue({
  el: '#app',
  // template: `<div>{{count}}<button v-on:click="add">+1</button></div>` // 或者用这种
 data: {
   count: 0
 },
 methods: {
  add() {
    this.count += 1
  }
 }
})
</script>
```

编译器 → 复杂 → 占用代码体积（用户的）

### 用不完整版 Vue 实现点击加一

**不完整版** Vue 的写法：

纯运行时，不需要用到编译器，可以使用 vue-loader，节省了近 40% 代码体积

```html
<div id="app"></div>
<script>
new Vue({
  el: '#app',
  render(h) {  // h → createElement
    return h('div', [this.count, h('button', {on: {click: this.add}}, '+1')])
  },
  data: {
    count: 0
  },
  methods: {
    add() {
      this.count += 1
    }
  }
})
</script>
```

在 `render` 函数中 `return` 参数 `h`

`h` 用来创建标签，基本用法 `h(标签, 内容)`

### 改写成 Vue 单文件组件

新建 `MyDemo.vue` 文件

```vue
<template>  <!-- 视图放这 -->
  <div class="red">
    {{ count }}
    <button @click="add">+1</button>
  </div>
</template>
<script>  // 除了视图的其他选项
export default {
  data() {  // 单文件组件中 data 必须是函数
    return {
      count: 0
    }
  },
  // 上面的 template 中内容会自动翻译成 render(h){ return h(...) }
  methods: {
    add() {
      this.count += 1
    }
  }
}
</script>
<style scoped> /* 样式写这 */
.red {
  color: red;
}
</style>
```

`main.js` 中引入并挂载

```js
import Vue from 'vue'
import MyDemo from './MyDemo.vue'
// 必须加 ./；加不加 .vue 都可以，但是加了更明确
// console.log(MyDemo)
new Vue({
  el: '#app',
  render: h => h(MyDemo)
})
```

MyDemo 是一个对象，有 methods 对象、beforeCreate、beforeDestroy 数组，data、render 等方法

可以把 `MyDemo.render.toString()` 打印出来就是 render 方法

### 总结

| 对比 | Vue 完整版 | Vue 非完整版 | 评价 |
|---|---|---|---|
| 特点 | 有 Compiler | 没有 Compiler | Compiler 占约 40% 体积 |
| 视图 | 写在 HTML 里或者写在 template 选项 | 写在 render 函数里，用 h 来创建标签 | h 是尤雨溪写好传给 render 的 |
| CDN 引入 | `vue.js` | `vue.runtime.js` | 文件名不同，生产环境后缀为 `.min.js` |
| Webpack 引入 | 需要配置 alias | 默认使用此版本 | 尤雨溪配置的 |
| @vue/cli 引入 | 需要额外配置 | 默认使用此版本 | 尤雨溪、蒋豪群配置的 |

最佳实践：总是使用非完整版，然后配合 vue-loader 和 vue 文件

思路：

1. 保证用户体验，用户下载的 JS 文件体积更小，但只支持 `h` 函数
2. 保证开发体验，开发者可直接在 vue 文件里写 HTML 标签，而不写 `h` 函数
3. 脏活让 loader 做，vue-loader 把 vue 文件里的 HTML 转为 `h` 函数

注意：

- 非完整版中用 template/在 HTML 中写，会报错，只有运行时版本，模版编译器不可用，可以预编译（Vue-loader）或使用包含了编译器的构建版本，**无法将 HTML 编译成视图**
- 完整版中用 h 函数，代码体积会变大，因为 vue.js 有编译  HTML 的功能

> 注：开发版和生产版
>
> - production 生产模式，代码给用户用，尽量优化、压缩、混淆（CDN 文件一般 `.min.js` 结尾）
> - development 开发模式，代码给开发者用，需要边写边预览，尽量方便开发、调试（CDN 文件一般 `.js` 结尾）
