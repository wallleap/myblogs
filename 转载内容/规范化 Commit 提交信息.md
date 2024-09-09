---
title: 规范化 Commit 提交信息
date: 2022-07-29 14:30
updated: 2022-07-29 14:30
author: 小康
cover: //cdn.wallleap.cn/img/pic/illustrtion/202207261551425.jpg
category: 技术杂谈
tags:
  - web
  - Git
description: 规范化 Commit 提交信息
---

文章转载自[小康博客](https://www.antmoe.com/)

写此文的目的仅仅是为了在 `commit` 操作时方便快速查找表情符号。因此参考互联网中同类型文章整理此文。

## 使用

在使用命令行提交 `commit` 消息时，可以通过 `:关键字:` 的方式进行使用表情。

```sh
git commit -m ":tada: Initial commit"
```

## 表情列表

使用时可以复制需要的 emoji 代码

|        emoji         |          emoji 代码           |         commit 说明          |
| :------------------: | :---------------------------: | :--------------------------: |
|      🎨 (调色板)      |            `:art:`            |   改进代码结构 / 代码格式    |
|  ⚡️ (闪电) 🐎 (赛马)   |     `:zap:` `:racehorse:`     |           提升性能           |
|       🔥 (火焰)       |           `:fire:`            |        移除代码或文件        |
|       🐛 (bug)        |            `:bug:`            |           修复 bug           |
|      🚑 (急救车)      |         `:ambulance:`         |           重要补丁           |
|       ✨ (火花)       |         `:sparkles:`          |          引入新功能          |
|      📝 (备忘录)      |           `:memo:`            |           撰写文档           |
|       🚀 (火箭)       |          `:rocket:`           |           部署功能           |
|       💄 (口红)       |         `:lipstick:`          |      更新 UI 和样式文件      |
|       🎉 (庆祝)       |           `:tada:`            |           初次提交           |
|    ✅ (白色复选框)    |     `:white_check_mark:`      |           更新测试           |
|        🔒 (锁)        |           `:lock:`            |         修复安全问题         |
|       🍎 (苹果)       |           `:apple:`           |     修复 macOS 下的问题      |
|       🐧 (企鹅)       |          `:penguin:`          |     修复 Linux 下的问题      |
|       🏁 (旗帜)       |      `:checkered_flag:`       |    修复 Windows 下的问题     |
|     🤖（机器人）      |           `:robot:`           |    修复 Android 下的问题     |
|      🍏 (绿苹果)      |        `:green_apple:`        |      修复 iOS 下的问题       |
|       🔖 (书签)       |         `:bookmark:`          |       发行 / 版本标签        |
|      🚨 (警车灯)      |      `:rotating_light:`       |       移除 linter 警告       |
|       🚧 (施工)       |       `:construction:`        |          工作进行中          |
|       👷 (工人)       |    `:construction_worker:`    |       添加 CI 构建系统       |
|       💚 (绿心)       |        `:green_heart:`        |       修复 CI 构建问题       |
|     ⬆️ (上升箭头)     |         `:arrow_up:`          |           升级依赖           |
|     ⬇️ (下降箭头)     |        `:arrow_down:`         |           降级依赖           |
|       📌 (图钉)       |          `:pushpin:`          |    将依赖项固定到特定版本    |
|    📈 (上升趋势图)    | `:chart_with_upwards_trend:`  |      添加分析或跟踪代码      |
|      ♻️ （回收）      |          `:recycle:`          |           重构代码           |
|       🐳 (鲸鱼)       |           `:whale:`           |       Docker 相关工作        |
| 🌐 (带子午线的地球仪) |   `:globe_with_meridians:`    |        国际化与本地化        |
|       ➕ (加号)       |      `:heavy_plus_sign:`      |         增加一个依赖         |
|       ➖ (减号)       |     `:heavy_minus_sign:`      |         减少一个依赖         |
|       🔧 (扳手)       |          `:wrench:`           |         修改配置文件         |
|       🔨 (锤子)       |          `:hammer:`           |           重大重构           |
|       ✏️ (铅笔)       |          `:pencil2:`          |          修复 typo           |
|      💩 (粑粑…)       |          `:hankey:`           |     写了辣鸡代码需要优化     |
|       ⏪ (倒带)       |          `:rewind:`           |           恢复更改           |
|  🔀 (交叉向右的箭头)  | `:twisted_rightwards_arrows:` |           合并分支           |
|       📦 (包裹)       |          `:package:`          |      更新编译的文件或包      |
|      👽 (外星人)      |           `:alien:`           | 由于外部 API 更改而更新代码  |
|       🚚 (货车)       |           `:truck:`           |      移动或者重命名文件      |
|  📄 (正面朝上的页面)  |      `:page_facing_up:`       |      增加或更新许可证书      |
|       💥 (爆炸)       |           `:boom:`            |       引入突破性的变化       |
|       🍱 (铅笔)       |           `:bento:`           |        增加或更新资源        |
|     👌 (OK 手势)      |          `:ok_hand:`          |  由于代码审查更改而更新代码  |
|       ♿️ (轮椅)       |        `:wheelchair:`         |        改善无障碍交互        |
|       💡 (灯泡)       |           `:bulb:`            |        给代码添加注释        |
|       🍻 (啤酒)       |           `:beers:`           |       醉醺醺地写代码…        |
|     💬 (消息气泡)     |      `:speech_balloon:`       |         更新文本文档         |
|    🗃 (卡片文件盒)    |       `:card_file_box:`       |    执行与数据库相关的更改    |
|      🔊 (音量大)      |        `:loud_sound:`         |           增加日志           |
|       🔇 (静音)       |           `:mute:`            |           移除日志           |
|  👥 (轮廓中的半身像)  |    `:busts_in_silhouette:`    |          增加贡献者          |
|     🚸 (孩童通行)     |     `:children_crossing:`     |     优化用户体验、可用性     |
|     🏗 (建筑建造)     |   `:building_construction:`   |           结构变动           |
|      📱 (iPhone)      |          `:iphone:`           |         做响应式设计         |
|      🤡 (小丑脸)      |        `:clown_face:`         | 嘲弄事物（直译，这个没明白） |
|       🥚 (鸡蛋)       |            `:egg:`            |           增加彩蛋           |
|    🙈 (看不见邪恶)    |        `:see_no_evil:`        |     增加或更改 gitignore     |
|   📸 (照相机闪光灯)   |       `:camera_flash:`        |        增加或更新截图        |
|      ⚗️ (蒸馏器)      |          `:alembic:`          |          尝试新东西          |
|      🔍 (放大镜)      |            `:mag:`            |           SEO 优化           |
|    ☸️ (船的方向盘)    |      `:wheel_of_dharma:`      |    关于 Kubernetes 的工作    |
|       🏷 (标签)       |           `:label:`           | 增加类型（FLow、Typescript） |

## 提交预览

### 提交格式

```sh
<emoji 代码><type>(<scope>): <subject>
```

### 参数说明——`<type>`

> 用于说明 `git commit` 的类别，只允许使用下面的标识。
>
> 以下表格来自[阿里技术](https://zhuanlan.zhihu.com/p/182553920?utm_source=org.mozilla.firefox)

|    <span style="width: 7em">标识</span>    |                             含义                             |
| :--------: | :----------------------------------------------------------: |
|   `feat`   |                      新功能（feature）                       |
|  `fix/to`  | 修复 bug，可以是 QA 发现的 BUG，也可以是研发自己发现的 BUG。 `fix`：产生 diff 并自动修复此问题。适合于一次提交直接修复问题 `to`：只产生 diff 不自动修复此问题。适合于多次提交。最终修复问题提交时使用 fix |
|   `docs`   |                    文档（documentation）                     |
|  `style`   |                 格式（不影响代码运行的变动）                 |
| `refactor` |     重构（即不是新增功能，也不是修改 bug 的代码变动）。      |
|   `perf`   |                优化相关，比如提升性能、体验。                |
|   `test`   |                          增加测试。                          |
|  `chore`   |                  构建过程或辅助工具的变动。                  |
|  `revert`  |                      回滚到上一个版本。                      |
|  `merge`   |                          代码合并。                          |
|   `sync`   |                    同步主线或分支的 Bug。                    |

### 参数说明——`<scope>`

scope 用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

例如在 `Angular`，可以是 `$location`, `$browser`, `$compile`, `$rootScope`, `ngHref`, `ngClick`, `ngView` 等。

如果你的修改影响了不止一个 `scope`，你可以使用 `*` 代替。

### 参数说明——`<subject>`

`subject` 是 commit 目的的简短描述，不超过 50 个字符。

建议使用中文（感觉中国人用中文描述问题能更清楚一些）。

结尾不加句号或其他标点符号。

### 示例

```sh
:bug: fix(DAO): 用户查询缺少username属性 
:sparkles: feat(Controller): 用户查询接口开发
```

## 工具

### VScode

vscode 中 `Git-commit-plugin` 插件可以快速生成提交模板。

设置项

- 展示 Emoji

  默认为 `true`。可在设置中修改

- 提交类型

  增加其他的提交类型，需要在 json 中添加。

  ```json
  "GitCommitPlugin.CustomCommitType": [
    {
      "label": "customTypeName",
      "detail": "customTypeDetail"
    }
  ]
  ```

  ![提交](https://cdn.wallleap.cn/img/pic/illustrtion/202207261434920.png)

- subject 最大长度

  subject 的最大长度限制，默认为 20。可在设置中修改。

### 其他

- <https://github.com/typicode/husky>

- <https://commitlint.js.org/#/>

## 文章参考

- [gitmoji](https://gitmoji.carloscuesta.me/)

- [Git 提交时的 emoji 表情使用指南](https://blog.huqing.site/201902/8da9/)

- [git commit 规范指南](https://segmentfault.com/a/1190000009048911)

- [如何规范你的 Git commit？](https://zhuanlan.zhihu.com/p/182553920?utm_source=org.mozilla.firefox)

> 本文转载自：[规范化 Commit 提交信息 | 小康博客 (antmoe.com)](https://www.antmoe.com/posts/40e311db/)
