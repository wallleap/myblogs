---
title: 写主题会上瘾，一个简约主题 plain
date: 2024-03-10 10:07
updated: 2024-03-10 19:18
cover: https://cdn.wallleap.cn/img/pic/cover/plain.jpg
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
description: 写主题会上瘾，一个简约主题 plain
---

之前主题 [ethereal](https://github.com/wallleap/ethereal) 用的卡片式风格，展示图片有点多，闲着没事又想重新写一个简约一点的

主页效果如下：

![](https://cdn.wallleap.cn/img/pic/illustration/202403101012197.png)

使用的技术栈&工具：

- [Vite 5](https://vitejs.dev/) + [Vue 3](https://vuejs.org/) + [TS](https://www.typescriptlang.org/) + [Vue Router 4](https://router.vuejs.org/) + [Pinia](https://pinia.vuejs.org/)
- [@antfu/eslint-config](https://www.npmjs.com/package/@antfu/eslint-config)、[Husky](https://www.npmjs.com/package/husky) 和 [lint-staged](https://www.npmjs.com/package/lint-staged)
- [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)（由于太简单就没再使用 axios）
- [Unocss](https://unocss.dev/)
- [MarkdownIt](https://www.npmjs.com/package/markdown-it)、[Highlight.js](https://www.npmjs.com/package/highlight.js)、[Front-matter](https://www.npmjs.com/package/front-matter)
- [不蒜子](https://busuanzi.ibruce.info/)、[Utterance 评论](https://utteranc.es/)

使用的 API： [GitHub API](https://docs.github.com/en/rest)，主要用到的就是 issue 相关

- `/repos/${owner}/${repo}/issues?state=open` 获取到 issue 列表，对获取到的信息进行格式化，用于首页和友链页展示（`page`、`per_page` 参数可设置分页）
- `/repos/${owner}/${repo}/issues?state=closed&labels=About` 特殊页面，将其 close 并设置相应的标签
- `/repos/search/issues?q=${keyword}+repo:${owner}/${repo}+type:issue+state:open` 搜索 issue
- `/repos/${owner}/${repo}/issues/${issue_number}` 获取 issue 详情
- 从获取到的 issue 数据中得到 `comments_url` 请求对应的评论，进行展示
- `/repos/${owner}/${repo}/labels` 获取到所有的标签

TODO 后面需要继续完善的：

- [x] 统计每个页面的访问数，应当还是会使用 [LeanCloud](https://console.leancloud.app/) 进行存储
- [ ] MarkdownIt 自定义输出标签，方便设置样式（例如表格宽度超出问题）
- [ ] 加个后台页面，直接输入 token 就能编写文章，这样可以不登录 GitHub
- [x] 修改 README 文件，添加使用说明
- [x] 添加动画效果及 Loading
- [x] 添加文章目录
- [ ] 添加 manifest

接着记录下后面可能还会遇到的问题和容易忘记的配置或代码

## Vite 配置自定义环境变量前缀

vite 是支持直接使用 `.env` 中的变量的（一般在本地使用 `.env.local`，这样默认 `.gitignore` 忽略就不会上传到仓库中，可以同时给一个 `.env.sample` 样例方便其他人进行配置）

Vite 配置：

```ts
// vite.config.ts
export default defineConfig({
  envPrefix: ['V_'], // 默认前缀是 `VITE_`
})
```

在 `.env` 中的变量就可以在 `index.html` 和 `src` 下的文件中使用

例如 `.env` 中有一个变量 `V_TITLE`，那么可以在 HTML 中使用两个 `%` 包裹

```html
<title>%V_TITLE%</title>
```

在 ts 或 vue 文件中则需要 `import.meta.env.` 获取

```ts
const pageTitle = import.meta.env.V_TITLE
```

有很多环境变量，并且需要用到 TypeScript 智能提示，可以在 `src` 下新建文件 `vite-env.d.ts`

```ts
/// <reference types="vite/client" />

interface ImportMetaEnv {
  readonly V_TITLE: string
  // 更多环境变量...
}

interface ImportMeta {
  readonly env: ImportMetaEnv
}
```

## Vite 中好用的静态资源导入

具体可以看这个章节：[静态资源处理](https://cn.vitejs.dev/guide/assets.html)

记录这个是因为使用到 Highlight.js 的样式，想在暗黑模式下用另一种样式表

最开始的尝试是直接动态引入

```ts
import('./pathto/dark.css').then(css => {})
import('./pathto/light.css').then(css => {})
```

然后发现 `css` 是一个模块，使用 `css.default` 并没有值，并且使用 `import('./pathto/x.css')` 直接将样式引入了，没办法删除之前引入的

后来想到的是使用 `link` 标签设置不同的 URL，`import imgUrl from './img.png'` 可以返回图片的路径（不管开发还是生产构建都会帮你自动解析），但是我在引入本地 `code-dark.css` 的时候发现报错 `The module does not provide an export named 'default'`

故而转用其他方式，例如获取它的字符串

```ts
import darkCode from './pathto/code-dark.css?raw'
```

这样动态生成一个 `style` 标签，将获取到的字符串放到标签下，并且给 `style` 设置一个 `id`，在切换主题的时候就能删除上一个导入的样式了

## 使用 Vite 插件进行 GZip 压缩

使用的插件是：[vbenjs/vite-plugin-compression](https://github.com/vbenjs/vite-plugin-compression)

安装：

```sh
yarn add vite-plugin-compression -D
```

配置：

```ts
// vite.config.ts
import viteCompression from 'vite-plugin-compression';

export default () => {
  return {
    plugins: [
      viteCompression({
        threshold: 1024000 // 大于 1Mb 的文件压缩
      })
    ],
  };
};
```

## Vite 配置 host 让局域网可访问

配置预览选项 `preview` 对本地开发很有效果，常用的有 proxy、cors，这里只配置 host

```ts
export default defineConfig({
  preview: {
    host: true,
  },
})
```

也可以在运行 dev 的时候加上参数 `--host` 或 `--host 0.0.0.0`：

```sh
pnpm dev --host
```

## UnoCSS 配置

配置文件：

```ts
// uno.config.ts
import { defineConfig, presetUno } from 'unocss'

export default defineConfig({
  rules: [
    // 多行文本超出部分省略号 line-n
    [/^line-(\d+)$/, ([, l]) => {
      if (~~l === 1) {
        return {
          'overflow': 'hidden',
          'text-overflow': 'ellipsis',
          'white-space': 'nowrap',
          'width': '100%',
        }
      }
      return {
        'overflow': 'hidden',
        'display': '-webkit-box',
        '-webkit-box-orient': 'vertical',
        '-webkit-line-clamp': l,
      }
    }],
  ],
  theme: {
    colors: {
      primary: 'var(--primary)',  // class="c-primary"
    },
  },
  presets: [
    presetUno({
      dark: { // 默认是 class，即 `.dark`；media 是自动匹配，用起来是 @dark:
        // 但是之前习惯用自定义属性了，所以还是改成这个，使用和 class 一样 dark:
        light: '[data-theme=light]',
        dark: '[data-theme=dark]',
      },
    }),
  ],
})
```

UnoCSS 还有好多不会用的，过几天把文档和 playgroud 过一遍

## 经常忘记的 UnoCSS 写法

列表 style，不选中

```css
.list-none {
  list-style-type: none;
}
.select-none {
  -webkit-user-select: none;
  user-select: none;
}
```

`flex` 对齐 `flex-items-center` 之类能缩写

```css
.items-center {
  align-items: center;
}
.justify-center {
  justify-content: center;
}
.flex-shrink-0 {
  flex-shrink: 0;
}
.flex-wrap {
  flex-wrap: wrap;
}
```

`align` 是 `vertical-align`

```css
.align-super { /* btm mid 等*/
  vertical-align: super;
}
```

圆角

```css
.rounded { /* -full */
  border-radius: 0.25rem;
}
.border-rd { /* border-rounded 可缩写成 rd */
  border-radius: 0.25rem;
}
```

`hover` 用法，

```html
<div class="group hover:b-current"> <!-- 自身 hover:，group 整体 -->
  <h2 class="group-hover:c-primary"></h2>
  <p class="group-hover:text-gray-700"></p>
</div>
```

`transition`

```html
<div class="all:transition-150"><div>
```

`display:none;`

```css
<div class="hidden hover:block"></div>
```

## TS 报第三方包类型缺失

可以在 `src` 下新建文件 `shims.d.ts`

```ts
declare module 'markdown-it-sub' { // 模块名
  export default function () {} // 具体导出什么看导入的内容
}
```

## 简单封装 fetch

由于暂时只有一个请求接口，所以随便封装一下，方便调用

```ts
// utils/fetch.ts
const tempToken: string = import.meta.env.V_GITHUB_TOKEN
// 由于完整的 Token 传到 GitHub 上之后会被检测到失效，因此在中间切断后拼接
const GH_TOKEN = tempToken.split(', ').join('')
const GH_API = 'https://api.github.com'
const ghOpt = {
  method: 'GET',
  headers: {
    Authorization: `Bearer ${GH_TOKEN}`,
  },
}

/*
 * 获取数据（携带 GitHub Token）
 * */
export async function fetchWithToken(url: string, options: RequestInit = { ...ghOpt }) {
  const requestUrl = url.startsWith('http') ? url : `${GH_API}${url}`
  try {
    const response = await fetch(requestUrl, options)
    if (!response.ok)
      throw new Error(`HTTP error! status: ${response.status}`)

    const data = await response.json()
    return data
  }
  catch (error) {
    console.error('Error fetching data:', error)
    return null
  }
}
```

之后使用的时候就简单传路径即可

```ts
const OWNER: string = import.meta.env.V_OWNER
const REPO: string = import.meta.env.V_REPOSITORY

export async function searchPosts({ keyword = '', page = 1, pageSize = 30 }) {
  const res = await fetchWithToken(`/search/issues?q=${keyword}+repo:${OWNER}/${REPO}+type:issue+state:open&page=${page}&per_page=${pageSize}`)
  return res
}
```

## 切换路由后自动跳转顶部

默认是保存查看的位置的

```ts
export default createRouter({
  scrollBehavior() { // to, from, savedPosition
    return { top: 0 }
  },
})
```

附点击平滑回到顶部

```ts
function backTop() {
  window.scrollTo({
    top: 0,
    behavior: 'smooth',
  })
}
```

## RouterLink

`route` 属性传参

```ts
// View A
<router-link :to="{ name: 'post', params: { num: post.num }, query: { title: post.title } }"></router-link>

// View B
import { useRoute } from 'vue-router'
const route = useRoute()
console.log(Number(route.params.num), route.query.title)
```

扩展 RouterLink，能够接收更多 `props`，[扩展 RouterLink](https://router.vuejs.org/zh/guide/advanced/extending-router-link.html)

## 使用 HTML5 web history 模式

```ts
// router.ts
import { createRouter, createWebHistory } from 'vue-router'

export default createRouter({
  history: createWebHistory(),
})
```

这样就没有 hash 模式下的 `#` 了，但是需要服务器端配合，例如配置 Nginx

```nginx
location / {
  try_files $uri $uri/ /index.html;
}
```
