---
title: Git 命令总结
date: 2020-06-10 11:20
updated: 2020-06-10 11:20
cover: //cdn.wallleap.cn/img/pic/cover/202302xrceGw.jpg
category: 技术杂谈
tags:
  - web
  - 前端
description: Git 命令总结
---

使用 Git 进行代码版本管理

## 版本控制

### 集中式（svn）

SVN 因为每次存的都是差异，需要的硬盘空间会相对的小一点，可是回滚的速度会很慢

- 优点：
  - 代码存放在单一的服务器上，便于项目的管理
- 缺点：
  - 服务器宕机：员工写的代码得不到保障
  - 服务器炸了：整个项目的历史记录都会丢失

### 分布式（git）

Git 每次存的都是项目的完整快照，需要的硬盘空间会相对大一点 (Git 团队对代码做了极致的压缩，最终需要的实际空间比 SVN 多不了太多，可是 Git 的回滚速度极快)

- 优点：完全的分布式
- 缺点：学习起来比 SVN 陡峭

## Git 底层命令

![常用命令](https://cdn.wallleap.cn/img/pic/illustration/git.webp)

### 底层命令

git 对象

- `git hash-object -w fileUrl`：生成一个 `key(hash 值):val(压缩后的文件内容)` 键值对存到 `.git/objects`

tree 对象

- `git update-index --add --cacheinfo 100644 hash test.txt`：往暂存区添加一条记录（让 git 对象 对应 上文件名）存到 `.git/index`

- `git write-tree`：生成树对象存到 `.git/objects`

commit 对象

- `echo 'first commit' | git commit-tree treehash`：生成一个提交对象存到 `.git/objects`

对以上对象的查询

- `git cat-file -p hash`：拿对应对象的内容

- `git cat-file -t hash`：拿对应对象的类型

### 查看暂存区

```sh
git ls-files -s        
```

## Git 高层命令

### 安装

前往官网下载安装包安装，或者使用包管理器进行安装，例如 Mac 上的 Homebrew：

```sh
brew install git
```

安装完成后，可以使用以下命令查看版本：

```sh
git --version
```

### 初始化配置

使用以下命令配置全局用户名和邮箱：

```sh
git config --global user.name "用户名"
git config --global user.email "damu@example.com"
```

只需要配置当前目录的用户名和邮箱，将 `--global` 参数去掉即可，或者把 `--global` 改成 `--local`：

```sh
git config --local user.name "用户名"
git config --local user.email "邮箱"
```

使用以下命令查看配置：

```sh
git config --list
```

### 初始化仓库

在项目目录下使用以下命令初始化仓库：

```sh
git init
```

### C（新增）

在工作目录中新增文件

新建文件之后

可以使用 `git status` 查看当前文件状态

使用 `git add <file>` 将文件添加到暂存区（`<file>` 是需要添加的文件 `.` 代表所有）

使用 `git commit -m "msg"` 将文件提交到版本库（`msg` 为提交的信息）

```sh
git status
git add .
git commit -m "msg"
```

### U（修改）

在工作目录中修改文件

之后添加并提交修改的文件

```sh
git status
git add ./
git commit -m "msg"     
```

### D（删除 & 重命名）

```sh
git rm 要删除的文件  # 把文件从暂存区和工作目录中删除
git mv 老文件 新文件  # 重命名文件
git status
git commit -m "msg"
```

### R（查询）

- `git status`：查看工作目录中文件的状态【已跟踪(已提交 已暂存 已修改)、未跟踪】

- `git diff`：查看未暂存的修改，即工作目录中当前文件和暂存区中最新版本之间的差异

- `git diff --cache`：查看已暂存的修改，即暂存区中最新版本和上一次提交的版本之间的差异

- `git log --oneline`：查看提交历史

- `git log --oneline --decorate --graph --all`：查看整个项目的提交历史

- `git log -p`：查看每次提交的内容差异

- `git log -p -2`：查看最近两次提交的内容差异

- `git log --stat`：查看每次提交的简略信息

### 分支

分支的本质其实就是一个提交对象！

HEAD：是一个指针

它默认指向 master 分支，切换分支时其实就是让 HEAD 指向不同的分支

每次有新的提交时 HEAD 都会带着当前指向的分支一起往前移动

- `git log --oneline --decorate --graph --all`：查看整个项目的分支图  

- `git branch`：查看分支列表

- `git branch -v`：查看分支指向的最新的提交

- `git branch name`：在当前提交对象上创建新的分支

- `git branch name commitHash`：在指定的提交对象上创建新的分支

- `git checkout name`：切换分支

- `git checkout -b name`：创建&切换分支

- `git branch -d name`：删除空的分支、删除已经被合并的分支，会有提示

- `git branch -D name`：强制删除分支，不会有提示

- `git merge name`：合并分支

  - 快进合并 --> 不会产生冲突
  - 典型合并 --> 有机会产生冲突
  - 解决冲突 --> 打开冲突的文件 进行修改 add commit

- `git branch --merged`：查看合并到当前分支的分支列表

  - 一旦出现在这个列表中就应该删除

- `git branch --no-merged`：查看没有合并到当前分支的分支列表
  
  - 一旦出现在这个列表中就应该观察一下是否需要合并

- `git rebase name`：变基

### git 分支的注意点

在切换的时候，一定要保证当前分支是干净的！

允许切换分支:

- 分支上所有的内容处于【已提交状态】
- (避免)分支上的内容是初始化创建处于未跟踪状态
- (避免)分支上的内容是初始化创建第一次处于已暂存状态

不允许切分支:

- 分支上所有的内容处于【已修改状态】或【第二次以后的已暂存状态】

在分支上的工作做到一半时，如果有切换分支的需求, 我们应该将现有的工作存储起来

- `git stash`：会将当前分支上的工作推到一个栈中

分支切换 → 进行其他工作 → 完成其他工作后 → 切回原分支

- `git stash apply`：将栈顶的工作内容还原，但不让任何内容出栈
- `git stash drop`：取出栈顶的工作内容后，就应该将其删除（出栈）
- `git stash pop`：`git stash apply` +  `git stash drop`
- `git stash list`：查看存储

### 后悔药

撤销工作目录的修改

```sh
git checkout -- filename
```

撤销暂存区的修改

```sh
git reset HEAD filename
```

撤销提交

```sh
git commit --amend
```

### reset 三部曲

- `git reset --soft commithash`    ---> 用 commithash 的内容重置 HEAD 内容

- `git reset [--mixed] commithash` ---> 用 commithash 的内容重置 HEAD 内容、重置暂存区

- `git reset --hard commithash`    ---> 用 commithash 的内容重置 HEAD 内容、重置暂存区、重置工作目录

### 路径 reset

所有的路径 reset 都要省略第一步！

第一步是重置 HEAD 内容

我们知道 HEAD 本质指向一个分支，分支的本质是一个提交对象

提交对象指向一个树对象，树对象又很有可能指向多个 git 对象，一个 git 对象代表一个文件！

HEAD 可以代表一系列文件的状态！

用 commithash 中 filename 的内容重置暂存区

```sh
git reset [--mixed] commithash filename
```

### checkout 深入理解

`git checkout name` 跟 `git reset --hard commithash` 特别像

- 共同点
  - 都需要重置 HEAD 暂存区工作目录

- 区别
  - checkout 对工作目录是安全的
  - reset --hard 是强制覆盖
  - checkout 动 HEAD 时不会带着分支走而是切换分支
  - reset --hard 时是带着分支走

- checkout + 路径
  - `git checkout commithash filename`
    - 重置暂存区
    - 重置工作目录
  - `git checkout -- filename`
    - 重置工作目录  

### gitignore

`.gitignore` 文件中的内容会被 git 忽略

语法：

- `#` 表示注释
- `*` 表示任意多个字符
- `?` 表示一个字符
- `!` 表示取反
- `dir/` 表示目录
- `/` 表示根目录

例如：

```gitignore
# 忽略所有的 .a 文件
*.a
# 但是 lib.a 除外
!lib.a
# 忽略目录 build 下的所有文件
build/
# 忽略 doc 目录下的所有 .txt 文件
doc/*.txt
# 忽略指定文件 .ignore
.ignore
```

## 使用 eslint 约束提交信息

### eslint

JS 代码的检查工具

下载:

```sh
npm i eslint -D
```

使用:

生成配置文件

```sh
npx eslint --init
```

检查 js 文件

```sh
npx eslint 目录名
```

命中的规则:

- 字符串必须使用单引号
- 语句结尾不能有分号
- 文件的最后必须要有换行

### eslint 结合 git

husky：哈士奇，为 Git 仓库设置钩子程序

使用：

在仓库初始化完毕之后，再去安装哈士奇

在 `package.json` 文件写配置

```json
"husky": {
  "hooks": {
    "pre-commit": "npm run lint"   
    // 在 git commit 之前一定要通过 npm run lint 的检查
    // 只有 npm run lint 不报错时 commit 才能真正的运行
  }
}
```

## 远程协作

### 三个必须懂得概念

- 本地分支
- 远程跟踪分支（remote/分支名）
- 远程分支

### 远程协作的基本流程

1. 项目经理创建一个空的远程仓库
2. 项目经理创建一个待推送的本地仓库
3. 为远程仓库配别名  配置用户名 邮箱
4. 在本地仓库中初始化代码 提交代码
5. 推送
6. 邀请成员
7. 成员克隆远程仓库
8. 成员做出修改
9. 成员推送自己的修改
10. 项目经理拉取成员的修改

### 做跟踪

克隆才仓库时会自动为 master 做跟踪

本地没有分支

```sh
git checkout --track 远程跟踪分支(remote/分支名)
```

本地已经创建了分支

```sh
git branch -u 远程跟踪分支(remote/分支名)
```

### 生成公钥

```sh
ssh-keygen -t rsa -C "邮箱"  # 默认生成的公钥是 id_rsa.pub，在 ~/.ssh/ 目录下
# 还可以生成指定名称的公钥
ssh-keygen -t rsa -C "邮箱" -f ~/.ssh/指定名称.pub
```

### 远程仓库

添加远程仓库

```sh
git remote add origin 远程仓库地址
```

查看远程仓库

```sh
git remote -v
```

删除远程仓库

```sh
git remote rm 远程仓库名
```

### 推送

```sh
git push  # 推送当前分支
git push origin 分支名  # 推送指定分支
git push origin 本地分支名:远程分支名  # 推送指定分支
git push -f  # 强制推送
```

### 拉取

```sh
git fetch  # 拉取远程仓库的所有分支
git pull  # 拉取远程仓库的当前分支
git pull origin 分支名  # 拉取远程仓库的指定分支
git pull origin 本地分支名:远程分支名  # 拉取远程仓库的指定分支
git pull origin 本地分支名:远程分支名 -f  # 强制拉取
```

### pull request

让第三方人员参与到项目中 fork

fork 之后的仓库是独立的，提交的代码不会影响到原仓库，但是可以通过 pull request 来向原仓库提交代码，原仓库的项目经理可以选择是否接受这个 pull request

### 使用频率最高的五个命令

```sh
git status
git add
git commit
git push
git pull
```
