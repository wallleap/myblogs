---
title: 写两个简单的 Raycast 脚本
date: 2024-05-06 23:16
updated: 2024-05-06 23:16
cover: //cdn.wallleap.cn/img/pic/cover/raycast.jpg
category: 技术杂谈
tags:
  - 工具
  - 电脑
description: 写两个简单的 Raycast 脚本
---

好早之前就弃用了 Alfred，转用了 Raycast，最主要的一个原因就是后者免费开源。但是换了之后一直用的就是 store 里的脚本，还没自己写过，最近正好有需求，简单记录一下。

## 创建 Node 脚本

第一次创建脚本需要选择一个目录存放，步骤为：进入 Raycast 设置，点击加号，点击 `Add Script Directory`，我设置的目录为 `~/.raycast`

![Add Script Directory](https://cdn.wallleap.cn/img/pic/illustration/202405062323022.png)

接着在这个页面点击 `Create Script Command`，填写信息，看情况是否需要勾选下面两个选项，之后点击 `Create Script` 就创建好了脚本

![填写信息](https://cdn.wallleap.cn/img/pic/illustration/202405062326276.png)

生成好的脚本可以在 `Scripts` 下找到，在搜索的时候，输入标题、别名或包名都可以找到这个脚本

![脚本](https://cdn.wallleap.cn/img/pic/illustration/202405062331128.png)

## 生成随机字符串

根据上述步骤创建一个

- 标题为 `randstring`
- 描述信息为 `生成16位随机字符串`
- 包名为 `randstring`
- 别名为 `rs`
- Mode 为 `Silent`
- 不勾选下面两个选项（不需要确认和参数）

修改生成的 `randstring.js` 写一个生成随机字符串的脚本（可能后面会想要指定长度，这里先不写死 16）

- 先处理异常情况（传参类型不对、值小于等于 0 都返回空字符串）
- 当长度在 1~11 的时候可以直接用 random 生成随机小数，之后将它转成36进制（0~9A~Z），不要前面两位（`0.`），可能会不足11位，需要在末尾补 `0`
- 长度超过 11 的时候，递归小于等于 11 的情况并进行拼接

```js
function randomStr(length) {
  if (typeof length !== 'number' || isNaN(length) || length <= 0)
    return ''
  else if (length <= 11)
    return Math.random().toString(36).slice(2, length + 2).padEnd(length, '0')
  else
    return randomStr(11) + randomStr(length - 11)
}
```

调用这个函数，并且需要直接复制到剪贴板（Node.js 在不使用第三方包情况下可以这样操作）

```js
const { exec } = require('child_process')

// Windows
exec('clip').stdin.end('some text')

// Mac
exec('pbcopy').stdin.end('some text')

// Linux
exec('xclip').stdin.end('some text')
```

所以完整的代码为（不包括脚本自带的描述信息）：

```js
const { exec } = require('child_process')

function randomStr(length) {
  if (typeof length !== 'number' || isNaN(length) || length <= 0)
    return ''
  else if (length <= 11)
    return Math.random().toString(36).slice(2, length + 2).padEnd(length, '0')
  else
    return randomStr(11) + randomStr(length - 11)
}

const rs = randomStr(16)
exec('pbcopy').stdin.end(rs)
console.log(`✅ 复制 ${rs} 成功`)
```

如果后面需要传入长度的话，可以重新创建一条脚本，并勾选 `With Argument`，之后调用的时候传入参数即可 `randomStr(Number(process.argv.slice(2)[0]))`

## 简单翻译脚本

找一个免费的翻译 API：`https://clients5.google.com/translate_a/t?client=dict-chrome-ex&sl=auto&tl=zh-cn&q=English`

通过 Node.js 的 https 模块进行请求

创建脚本

- 标题为 `fanyi`
- 描述信息为 `翻译输入的内容`
- 包名为 `fanyi`
- 别名为 `fy`
- Mode 为 `Compact`
- 勾选 `With Argument`

将下述内容添加到生成的 `fanyi.js` 文件中

```js
const https = require('https')
const querystring = require('querystring')

const translate = (q) => {
  let tl = 'en'
  if (/[a-zA-Z]/.test(q[0])) {
    tl = 'zh-cn'
  }
  // 对参数进行拼接
  const query = querystring.stringify({
    client: "dict-chrome-ex",
    sl: "auto",
    tl,
    q
  })

  const options = {
    hostname: 'clients5.google.com',
    port: 443,
    path: '/translate_a/t?' + query,
    method: 'GET',
  }

  const request = https.request(options, (response) => {
    let chunks = []
    response.on('data', (chunk) => {
      chunks.push(chunk)
    })
    response.on('end', () => {
      const string = Buffer.concat(chunks).toString()
      const object = JSON.parse(string)
      console.log(object[0][0]) // 打印结果
    })
  })
  request.on('error', (e) => {
    console.error(e)
  })
  request.end()
}

translate(process.argv.slice(2)[0])
```

> 注：我对 google 域名进行了代理，不知道正常网络能否正常请求，如果不行的话可以按照这个思路换一个免费 API 试试

使用效果如下：

![使用效果](https://cdn.wallleap.cn/img/pic/illustration/202405071008938.gif)
