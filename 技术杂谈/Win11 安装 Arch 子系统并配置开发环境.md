---
title: Win11 安装 Arch 子系统并配置开发环境
date: 2022-07-26 19:30
updated: 2022-07-26 19:30
cover: //cdn.wallleap.cn/img/pic/illustrtion/202207261246820.png
category: 技术杂谈
tags:
  - 电脑
  - win
description: Win11 安装 Arch 子系统并配置开发环境
---

最近更新了 win11，重新启用下 Linux 子系统，并设置好基础开发环境。

Win10 启用其子系统 Ubuntu 并安装图形界面可以看这篇文章：<https://myblog.wallleap.cn/#/post/34>

主要是想着 Win11 界面看着也还不错了，`终端` + `oh-my-zsh` / `oh-my-posh` 看着也是非常 nice 的

![命令](https://cdn.wallleap.cn/img/pic/illustrtion/202207111752655.png)

## 1、启用功能

搜索并打开`控制面板`

![打开控制面板](https://cdn.wallleap.cn/img/post/202204281035695.png)

点击`程序`

![程序](https://cdn.wallleap.cn/img/post/202204281036471.png)

点击`启用或关闭 Windows 功能`

![启用功能](https://cdn.wallleap.cn/img/post/202204281038483.png)

把`使用于 Linux 的 Windows 子系统` 和其他有关虚拟平台的勾上（没有 Hyper-V 的把其他的勾选就行），点击确定

![Windows功能](https://cdn.wallleap.cn/img/post/202204281040833.png)

等待一会之后按提示重启电脑就成功开启 WSL 了（如果 BIOS 中有 VT/虚拟 相关的选项，需要进 BIOS 设置为开启状态）

> 为了方便也可以直接在 powershell 中使用命令（管理员身份运行）：
>
> ```powershell
> dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
> dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
> ```

## 2、设置 WSL 2 为默认版

1. 下载升级包：https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi

2. 下载完成后双击安装

3. 在 PowerShell 输入命令：`wsl --set-default-version 2`，将 WSL 2 设置为默认版

## 3、安装 ArchWSL

提供了两种安装方式，我们选择简单点的：

在 [yuk7/ArchWSL - releases](https://github.com/yuk7/ArchWSL/releases/latest)下载 Arch.appx / Arch.zip

解压，双击 Arch.exe 进行安装

提示输入 <kbd>Enter</kbd> 之后可以在终端中找到并打开

![终端中 Arch](https://cdn.wallleap.cn/img/pic/illustrtion/202207111113806.png)

## 4、设置 Root 密码

```sh
[root@PC-NAME]# passwd
在这里输入两次密码
```

## 5、设置默认用户

可以只用 root 用户，但还是建议更改下

参考 ArchWiki 的 [Sudo](https://wiki.archlinux.org/index.php/Sudo#Example_entries) 和 [User and groups](https://wiki.archlinux.org/index.php/Users_and_groups) 页。

```shell
[root@PC-NAME]# echo "%wheel ALL=(ALL) ALL" > /etc/sudoers.d/wheel
# 设置 sudoers 文件

[root@PC-NAME]# useradd -m -G wheel -s /bin/bash {username}
# 添加用户

[root@PC-NAME]# passwd {username}
# 设置默认用户密码

[root@PC-NAME]# exit

>Arch.exe config --default-user {username}
# 设置默认用户
```

把上面的 `{username}` 替换为你自己想创建的用户名，例如 `testuser`

如果默认用户密码被更改 ([issue #7](https://github.com/yuk7/ArchWSL/issues/7)), 请重启电脑或者用以管理员身份打开 CMD 运行下面命令，重启 `LxssManager`

```cmd
net stop lxssmanager && net start lxssmanager
```

## 6、初始化密钥环（keyring）

请执行这些命令以初始化密钥环 keyring（必须执行此步骤才可以使用 Pacman）

```shell
[user@PC-NAME]$ sudo pacman-key --init

[user@PC-NAME]$ sudo pacman-key --populate

[user@PC-NAME]$ sudo pacman -Syy archlinux-keyring
```

## 7、美化终端

首先安装官方源的 zsh

```shell
sudo pacman -S zsh
```

安装 wget 和 git

```shell
sudo pacman -S wget
```

获取 oh-my-zsh 安装脚本

```shell
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh
```

> 如果打死都获取不来，直接把 [tools/install.sh](https://github.com/ohmyzsh/ohmyzsh/blob/master/tools/install.sh) 内容复制，并新建一个 install.sh 文件，粘贴内容进去

给文件运行权限

```shell
chmod +x install.sh
```

运行 shell 文件

```shell
./install.sh
```

设置 zsh 为默认的 shell

```shell
sudo chsh -s /bin/zsh 
```

主题默认是在 `~/.oh-my-zsh/themes/` 目录下，可以选择这里面已经有了的主题

主题预览：[External themes](https://github.com/ohmyzsh/ohmyzsh/wiki/External-themes)

可以尝试自己下载主题，以 `passion` 为例，前往主题仓库：[ChesterYue/ohmyzsh-theme-passion](https://github.com/ChesterYue/ohmyzsh-theme-passion)

下载 passion.zsh-theme 文件，将它复制到主题目录

```zsh
cp passion.zsh-theme ~/.oh-my-zsh/themes/
```

在配置文件中修改主题名为 `passion`

```zsh
vim ~/.zshrc
```

![修改主题](https://cdn.wallleap.cn/img/pic/illustrtion/202207111717945.png)

需要搭配合适的字体才能显示完整，建议使用 FiraCode 字体族

前往 <https://wallleap.lanzoub.com/i43lX08fdnpa> 下载字体，安装时候选择 `FiraCode Nerd Font` 即可

新建一个终端就可以看到主题效果了

下载三个常用的插件：

**历史命令查找**（zsh-history-substring-search）

https://github.com/robbyrussell/oh-my-zsh/tree/master/plugins/history-substring-search

**代码高亮**（zsh-syntax-highlighting）

https://github.com/zsh-users/zsh-syntax-highlighting

**命令提示**（zsh-autosuggestions）

https://github.com/zsh-users/zsh-autosuggestions

之后修改配置文件：

```zsh
vim ~/.zshrc
```

修改一下内容

```config
plugins=(
  git
  zsh-history-substring-search
  zsh-syntax-highlighting
  zsh-autosuggestions
)
```

source 一下，让修改生效

```zsh
source ~/.zshrc
```

文件互通

win 下可以 <kbd>win</kbd>+<kbd>r</kbd> 输入 `\\wsl$` 回车，然后将 Arch 的映射到一个盘符

![映射网络驱动器](https://cdn.wallleap.cn/img/pic/illustrtion/202207120904969.png)

wsl 下可以进入 `/mnt` 目录，win 下的各个盘符都在这底下

![mnt](https://cdn.wallleap.cn/img/pic/illustrtion/202207120900686.png)

## 8、配置开发环境

用的 WSL 已经是 Linux 了，但是不方便复用，可以选择 Docker 配置一个统一的开发环境

### 下载 Docker Desktop

直接前往官网 [Docker Desktop - Docker](https://www.docker.com/products/docker-desktop/) 4.15 版本，下载自己平台的软件

之后安装完成之后，运行软件，设置里找到 Docker Engine，把一下代码复制替换掉方框中的代码

![镜像](https://cdn.wallleap.cn/img/pic/illustrtion/202207261131100.png)

```conf
{
  "registry-mirrors": [
    "https://registry.docker-cn.com",
    "http://hub-mirror.c.163.com",
    "https://docker.mirrors.ustc.edu.cn",
    "https://aa25jngun.mirror.aliyuncs.com"
  ],
  "insecure-registries": [],
  "debug": false,
  "experimental": false,
  "features": {
    "buildkit": true
  },
  "builder": {
    "gc": {
      "enabled": true,
      "defaultKeepStorage": "20GB"
    }
  }
}
```

设置里勾选使用 WSL 2 环境，默认勾选就不需要管

![WSL2](https://cdn.wallleap.cn/img/pic/illustrtion/202207261133741.png)

### 获取镜像

前端开发环境我觉得 [FrankFang](https://github.com/FrankFang) 这个大佬配置的非常好，可以直接使用

仓库地址：[FrankFang/oh-my-env-1 (github.com)](https://github.com/FrankFang/oh-my-env-1)

将上面的文件下载到本地：

```cmd
git clone https://github.com/FrankFang/oh-my-env-1.git oh-my-env
```

运行命令：

```cmd
docker network create network1
```

打开 VSCode

1. 安装 ~~Remote Container 插件~~ 改名了，安装 Dev Container 0.266 版本
2. 打开 oh-my-env 目录
3. 输入 Ctrl + Shift + P，然后输入 Reopen，回车，等待

![reopen in container](https://cdn.wallleap.cn/img/pic/illustrtion/202207261220177.png)

等上一步启动完毕之后，新建终端

![repos](https://cdn.wallleap.cn/img/pic/illustrtion/202207261222995.png)

### 使用说明

- 运行 `nvm use system` 和 `node --version` 得到 node 运行环境
- 运行 `rvm use 3` 和 `ruby --version` 得到 ruby 运行环境
- 一般代码就放在 `~/repos` 目录下
- 需要文件互通，可以在 `oh-my-env` 下新建目录 `temp`，之后将文件复制到这个目录即可

## 参考文档

- [在WSL2中安装ArchLinux](https://zhuanlan.zhihu.com/p/266585727)

- [wsl安装archlinux(Windows10子系统安装archlinux)](https://zhuanlan.zhihu.com/p/417410431)

- [yuk7/ArchWSL](https://github.com/yuk7/ArchWSL/blob/master/i18n/README_zh-cn.md)

- [ArchWSL documentation](https://wsldl-pg.github.io/ArchW-docs/locale/zh-CN/)

- [WSL 的基本命令 | Microsoft Docs](https://docs.microsoft.com/zh-cn/windows/wsl/basic-commands)

- [Arch 终端美化](https://zhuanlan.zhihu.com/p/436313976)

- [Writing ZSH Themes](https://blog.carbonfive.com/writing-zsh-themes-a-quickref/)
