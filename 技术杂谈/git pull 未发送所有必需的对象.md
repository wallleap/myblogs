---
title: git pull 未发送所有必需的对象
date: 2023-02-15 13:18
updated: 2023-02-15 13:18
cover: //cdn.wallleap.cn/img/pic/cover/202302152129387.jpg
category: 技术杂谈
tags:
  - Git
  - fix
description: git pull 未发送所有必需的对象
---

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
