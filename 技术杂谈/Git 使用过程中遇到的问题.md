---
title: Git 使用过程中遇到的问题
date: 2023-02-15 13:18
updated: 2023-02-15 13:18
cover: //cdn.wallleap.cn/img/pic/cover/202302152129387.jpg
category: 技术杂谈
tags:
  - Git
  - fix
description: git pull 未发送所有必需的对象
---

有些问题经常出现，每次都需要重新去搜索，有点浪费时间，因此在这里记录一下

## git pull 未发送所有必需的对象

在 Win 上提交了两次代码，然后到 mac 上运行

```sh
git pull
```

报了如下错误

![](https://cdn.wallleap.cn/img/pic/cover/202302152132544.png)

在 [stackoverflow](https://stackoverflow.com/questions/8788975/bitbucket-git-error-did-not-send-all-necessary-objects) 找到了解决方案

运行下面代码解决

```sh
rm .git/refs/heads/main\ 2
```

> 在正常情况下，当我们执行Git提交（git commit）时，Git会将当前工作目录中的更改创建为一个新的commit对象，并将其加入到版本历史中。但是有时候，当执行Git操作时，会收到一个错误消息：”Git Error: did not send all necessary objects”。

它这个的原因好像挺多的，如果我这个方法不行，可以到上面那个链接看下其他的解决方案
