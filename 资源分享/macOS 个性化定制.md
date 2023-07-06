---
title: macOS个性化定制
date: 2023-05-29 20:13
updated: 2023-05-29 20:13
cover: //cdn.wallleap.cn/img/post/1.jpg
author: Luwang
comments: true
aliases:
  - macOS 个性化定制
rating: 1
tags:
  - 电脑
  - macOS
category: 资源分享
keywords:
  - 关键词1
  - 关键词2
  - 关键词3
description: macOS 个性化设置和软件分享
---

六年 macOS 使用经验，推荐好用的软件和一些配置，并提供资源备份（以目前最新版 macOS Ventura 13.0 为例）

用了好久的黑苹果，但是那电脑已经有点 hold 不住了，所以干脆换了 MacBook Pro，由于 M2 相比于 M1 提升并没有很大，而且最新的实在太贵了，所以直接在苹果官网找的[官翻机](https://www.apple.com.cn/shop/refurbished/mac/macbook-pro)。

最后选中的是 14 英寸 MacBook Pro Apple M1 Pro 芯片（配备 10 核中央处理器和 16核图形处理器）- 银色，32 GB 内存 + 1 T 存储空间

![mbp](https://cdn.wallleap.cn/img/pic/illustration/202305291740275.png)

文章结构是先推荐，然后有总结，总结中有可以直接到 Homebrew 或 App store 下载的命令或链接，最后是个人习惯分享

不能在以上渠道下载的先放出网盘链接：



## 系统设置

### 允许安装任意来源的 APP

在终端输入以下命令：

```zsh
sudo spctl --master-disable
```

会要求输入密码，直接输入你的电脑登录密码即可（*输入的时候不会在终端中显示 输入完直接回车*）

之后到设置-安全性与隐私中查看是否是勾选的“任何来源”，如果不是，可以点击左下的锁，输入密码之后再选择“任何来源”

![允许任何来源](https://cdn.wallleap.cn/img/pic/illustrtion/20221009005904.png)

如果之后打开 app 还是报错

![](https://cdn.wallleap.cn/img/pic/illustrtion/202211272032523.png)

可以再到这个界面看下有没有提示，如果有，请选择【仍要打开】

![](https://cdn.wallleap.cn/img/pic/illustrtion/202211272033851.png)

如果还不行，可能需要**绕过苹果的公证 Gatekeeper**

终端输入以下命令，并且将需要打开的应用拖到终端中，再回车

注：安装的软件都在这个目录下，如果是通过镜像安装的话一般会让你拖动到这个目录，只有 `.app` 文件也需要你自己手动拖动到这个目录下（通过 App store 和 `brew` 安装的软件也会自动到这个目录下），所以直接到这里找到打不开的软件

![](https://cdn.wallleap.cn/img/pic/illustration/202306032244553.png)

输入后

```sh
sudo xattr -rd com.apple.quarantine
```

再拖到终端中

就类似这样的：

![](https://cdn.wallleap.cn/img/pic/illustrtion/202212151818586.png)

如果还是显示出现问题，那么就需要关闭 SIP 了

进入恢复模式（关机状态长按开机键）→ 状态栏实用工具-终端 → 输入命令 `csrutil disable` 回车 → 按提示输入 `y` 回车 → 输入密码回车（密码在输入过程中看不到）→ 重启

还有一种报错，`无法打开“xxx”，因为“安全策略”已设为“宽松安全性”。`，在“恢复” App 中，选取“实用工具”>“启动安全性实用工具”，选择“降低安全性”

> 也可以直接看这个 <https://zhuanlan.zhihu.com/p/474801204>

### 安装 Xcode Command Line Tools

完整的 Xcode 占用空间太大，而且也不一定使用，Command Line Tools 是在 Xcode 中的一款工具，macOS 下不少开发工具都会依赖这个，手动安装一下，后面安装其他工具可以省下不少麻烦：

```zsh
xcode-select --install
```

### 安装 HomeBrew

好用的软件包管理器，官网为：[Homebrew](https://brew.sh/)（可以直接到官网首页搜索框搜软件，之后直接复制到终端运行）

由于国内直接运行安装命令会报错，所以需要先配置好代理（自行解决），或者使用镜像（自己搜索教程）

之后到命令行执行（端口号 `10809`、`10808` 改成自己设定的 http socks5 代理端口）

```sh
export https_proxy=http://127.0.0.1:10809 http_proxy=http://127.0.0.1:10809 all_proxy=socks5://127.0.0.1:10808
```

之后再执行安装命令

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

如果前面安装顺利，之后弹出提示的话，可以按照它给出的提示，运行命令（*这里没有演示*）

查看有哪些指令可以使用

```sh
# 使用帮助
brew help
# 列出指令
brew commands
```

![](https://cdn.wallleap.cn/img/pic/illustrtion/202212271440509.png)

下面是一些常用的 `brew` 命令：

1. `brew install <package>`：安装一个软件包，如果是 CASK 则需要加上 `--cask`（先使用 `search` 命令和 `info` 命令查看软件包或去官网直接搜）
2. `brew uninstall <package>`：卸载一个软件包
3. `brew upgrade`：升级所有已安装的软件包
4. `brew outdated`：查看已安装的软件包中哪些需要更新
5. `brew update`：更新 `Homebrew` 本身和软件包的信息
6. `brew list`：列出所有已安装的软件包
7. `brew info <package>`：查看软件包的详细信息
8. `brew search <keyword>`：搜索软件包
9. `brew cleanup`：清理旧版本的软件包、缓存和日志文件
10. `brew doctor`：检查 `Homebrew` 是否正常工作

### 修改启动台图标行和列数

启动台里面也可以设置应用的列和宽，使用如下命令即可：

```zsh
# 设置列数为 9  
defaults write com.apple.dock springboard-columns -int 9  

# 设置行数为 6  
defaults write com.apple.dock springboard-rows -int 6  

# 重启 Dock 生效  
killall Dock
```

![启动台](https://cdn.wallleap.cn/img/pic/illustrtion/20221009005905.png)

恢复默认启动台：

```zsh
# 恢复默认的列数和行数  
defaults write com.apple.dock springboard-rows Default  
defaults write com.apple.dock springboard-columns Default  

# 重启 Dock 生效  
killall Dock
```

### 鼠标滚动方向

~~个人习惯了 Win 的方式，把自然的选项去掉~~

把自然去掉的话触控板方向也会变，所以我一般使用 Mos 这个软件来修改

![](https://cdn.wallleap.cn/img/pic/illustration/202305041029589.png)

安装：

```zsh
brew install --cask mos
```

右击状态栏图标，在偏好设置中设置

![设置 mos](https://cdn.wallleap.cn/img/pic/illustration/202305291801410.png)

在例外中默认是黑名单模式，加上不需要平滑或反转的应用

![例外](https://cdn.wallleap.cn/img/pic/illustration/202305291803342.png)

### 程序坞

- 默认的 Dock 栏效果：
  - 呆呆傻傻，没有动画，显示最近使用的应用程序（关掉了还会占位置）
  - ![默认的程序坞](https://cdn.wallleap.cn/img/pic/illustrtion/20221009005907.png)
  - 可以先记住恢复默认 Dock 的命令：`defaults delete com.apple.dock; killall Dock`
- 系统设置-程序坞与菜单栏，设置图标大小和动画（长按拖动分割线可以快速调整图标大小、按住 shift 键长按分割线上下左右拖动快速调整位于屏幕上的位置、右键分割线可以快速设置隐藏等）
  - ![分割线](https://cdn.wallleap.cn/img/pic/illustrtion/20221009005908.png)
  - ![程序坞与菜单栏](https://cdn.wallleap.cn/img/pic/illustrtion/20221009005909.png)
- 添加和删除图标：
  - 添加需要的图标：拖动应用/文件夹到程序坞进行添加（文件夹可以放到分割线右侧），或者右击正在运行的应用图标，在选项中选择在程序坞保留
  - 去除无用的图标：不需要的时候长按图标往上拖，出现移除时之后松手就能删除，或者右键需要删除的图标选择从程序坞中移除
- 添加空白占位图标，右键选择从程序坞中移除可以删掉

    ```zsh
    # 添加空白图标
    defaults write com.apple.dock persistent-apps -array-add '{"tile-type"="spacer-tile";}'
    # 重启 Dock 生效
    killall Dock
    ```

    ![添加空白分割](https://cdn.wallleap.cn/img/pic/illustrtion/20221009005910.png)

- 按住 Alt 键再右击应用图标可以强制退出应用程序

### 菜单栏

- 按住 Command 键拖动图标可以移动图标在菜单栏中的位置
- 系统设置里可以设置是否在菜单栏显示，一般在底部

  - ![蓝牙设置](https://cdn.wallleap.cn/img/pic/illustrtion/20221009005911.png)

- 后面软件部分推荐一款可以点击隐藏图标的应用

### 访达

- 菜单栏-访达-偏好设置（大部分 app 的首选项设置快捷键都是 <kbd>Command</kbd> + <kbd>,</kbd>）

  - ![偏好设置](https://cdn.wallleap.cn/img/pic/illustrtion/20221009005912.jpeg)

  - 边栏大小设置在系统设置-通用中
  - 设置显示隐藏文件：在终端输入 `defaults write com.apple.Finder AppleShowAllFiles true; killall Finder`，或者在访达中使用快捷键 <kbd>⌘</kbd> + <kbd>Shift</kbd> + <kbd>.</kbd> 控制隐藏文件的显示或隐藏
- 工具栏设置，右击工具栏选择自定工具栏，根据自己喜好添加删除排序

  - ![工具栏](https://cdn.wallleap.cn/img/pic/illustrtion/20221009005913.png)
- 显示，菜单栏-显示
- ![显示](https://cdn.wallleap.cn/img/pic/illustrtion/20221009005914.jpeg)
- 常用操作：

  - 排序：空白处右键-排序方式-名称/时间/大小

  - 放大/缩小文件图标：<kbd>Command</kbd> + <kbd>+</kbd>/<kbd>-</kbd>

  - 返回上一层：<kbd>Command</kbd> + <kbd>↑</kbd>，下键为下一层

  - 列表视图下，<kbd>option</kbd> + <kbd>↑</kbd>/<kbd>↓</kbd>，快速到达第一个/最后一个文件

  - 按住 <kbd>option</kbd> 键，拖动访达窗口大小，下次打开大小仍保留

  - 空格键快速查看文件

## 软件推荐

推荐到软件官网下载或者到使用 Homebrew 下载

推荐一个应用分享站：[精品MAC应用分享 (xclient.info)](https://xclient.info/)

付费软件，我一般到这上面购买：[麦软网](https://www.mairuan.com/)、[数码荔枝)](https://lizhi.shop/)

M1 可以直接安装移动端 APP，对于 App Store 中没有的移动端 APP，可以到网上找下砸壳了的 IPA 文件，然后到这个网站中安装：<https://appdb.to/my/devices>

### 菜单栏增强——iStat Menus/iStatistica、Bartender/Dozer、MenubarX

前两者是可以在菜单栏显示系统状态

![](https://cdn.wallleap.cn/img/pic/illustrtion/202211272019218.png)

后两者个人仅用于解决状态栏图标过多的问题（隐藏不需要的图标）

如果你和我一样只需要隐藏图标的话可以只使用 Dozer（刘海屏这个就不好用了），安装之后简单设置就可以使用：

- 首先点击这个圆点
- 然后按住 <kbd>Command</kbd> 键同时拖动状态栏的图标移动到两个点的左边
- 再次点击圆点就可以隐藏两个圆点左边的图标了
- 如果需要彻底将图标从状态栏移除，可以开启 `Enable 'remove' Dozer icon`，之后将图标移到小圆点的左边即可，需要恢复的时候，按住 <kbd>Option</kbd> 再点击 Dozer 在状态栏的图标就能显示移除的图标
- 最主要的是显示隐藏图标的时候只会显示 Dozer 的名字，状态栏基本可以看到所有的图标了

![](https://cdn.wallleap.cn/img/pic/illustrtion/202211272024131.png)

演示：

![](https://cdn.wallleap.cn/img/pic/illustrtion/202211272155291.gif)

MenubarX 可以直接在菜单栏中打开一个小的浏览器，可以修改各种 UA（某些时候非常方便）

### 访达增强——超级右键、MacZip

使用习惯了 win 下的右键新建文件的功能，mac 下没有还是很不适应的，【超级右键】这个软件就很好地解决了这个烦恼

![](https://cdn.wallleap.cn/img/pic/illustrtion/202212271552937.png)

mac 自带的解压功能并不强，还是需要其他的软件辅助，个人使用过 Bandzip、Dr. Unarchiver、eZip 等，它们都很好用，但大多都需要付费，最后保留下来的是 MacZip 这款免费且强大的解压缩软件

界面很简洁，解压、压缩、加密等功能都有

![](https://cdn.wallleap.cn/img/pic/illustrtion/202212271557631.png)

### 窗口——AltTab、Magnet/Rectangle

<kbd>Alt</kbd> + <kbd>Tab</kbd> win 下面切换窗口最常用的方式

![](https://cdn.wallleap.cn/img/pic/illustrtion/202212271559065.png)

Magnet/Rectangle 便捷管理窗口，可以快捷键快速分屏，拖动对齐窗口，拖动到屏幕边缘快速分屏等，前者付费、后者开源免费

![](https://cdn.wallleap.cn/img/pic/illustrtion/202212271608711.png)

### 输入法——鼠须管、自动切换输入法

之前有写过 Rime 的文章，可以去看下：[个人输入法调教之 Rime](https://myblog.wallleap.cn/#/post/93)

个人是把系统自带的中文输入法删除了，只留下了 ABC 和鼠须管

![输入法只留 ABC 和鼠须管](https://cdn.wallleap.cn/img/pic/illustration/202305291816704.png)

使用 mac 最烦恼的一件事就是它会自动切换回默认的输入法，如果有多个输入法，一不小心就不知道正在用的是哪个了

自动切换输入法可以设定规则，我把常用的软件都设置成了自动切换到“鼠须管”，并且在写代码或者经常使用快捷键的软件中**强制英文符号**，这样用起来就很顺手了

### 启动器——Alfred、Raycast

用来代替系统的“聚焦”搜索

把系统的快捷键去掉

![](https://cdn.wallleap.cn/img/pic/illustration/202305291834332.png)

然后把软件的快捷键设置为 <kbd>⌘</kbd> + <kbd>Space</kbd>

Alfred 之前用的和谐版，现在直接用免费的 Raycast 了

这两个软件不仅用于搜索，他们的剪贴板和 flow /插件也很好用

可以去 [Raycast - Store](https://www.raycast.com/store) 找好用的扩展插件

### 截图——ishot、snipaste、shottr

单纯的截图系统自带的已经够用了，但是它的快捷键不太好按，因此我改成了自己喜欢的

修改快捷键的方式：

设置中找到【键盘】，再找到【键盘快捷键】，【截屏】中修改快捷键

由于我只想记一个快捷键，所以只改了一个功能全一点的，用的是 <kbd>Option</kbd> + <kbd>Shift</kbd> + <kbd>Q</kbd>

![](https://cdn.wallleap.cn/img/pic/illustrtion/202212271622706.png)
Snipaste 最开始看中的是它的贴图功能，取色功能也常用，但是它检测窗口好像总是会有问题，并且免费版功能有点不够了

iShot 功能就非常全面了，支持截屏、标注、贴图、长截图等，基本上把我需要的功能都包含了（现在是有些功能会有水印了？）

![](https://cdn.wallleap.cn/img/pic/illustrtion/202212271630460.png)

Shottr 也开始收费了

### 磁盘/文件传输——Tuxera NTFS、Android File Transfer

前者用于 NTFS 格式外置磁盘，后者用于 Android 手机文件传输

### 看图——Xee^3/pictureview

个人喜欢的看图方式是在文件管理器里看缩略图，需要放大看的双击打开，能方便切换下一张，方便缩放，界面看着舒适

win 下之前使用2345看图王绿色版非常符合，后面找到[蓝山看图王](https://www.lanshan.com/pic/)也不错

mac 暂时还没找到一款符合我期望的看图软件，勉强使用的是 ~~Xee^3~~ pictureview，基本能用，就是叉掉图片之后软件不能自动关闭，会一直留在 Dock 栏

### 音视频

- Ever Play 用于播放 Onedrive/百度网盘中的音乐（移动端）
- YesPlayMusic 在线播放多平台音乐
- QQ音乐，版权更多一点，缺点是不充豪华绿挺多音乐只能试听（尝试使用安卓端的一些 APP 下载音乐本地播放）
- 抖音、片多多、微光都是移动端 APP，一般摸鱼的时候看
- IINA/Infuse 播放视频

### 时间管理——滴答清单、Microsoft TODO

滴答清单合理安排大任务、小任务

TODO 用来安排每天的任务

### 编辑器——CotEditor、VS Code

CotEditor 我用来替换系统自带的文本编辑器，缺点也是关掉之后还会在 Dock 栏

VS Code 就用于编写代码

### API 工具——Apifox、Apipost

个人感觉 Apifox 更好用点

### 终端——iTerm2、warp

iTerm2 的文章有很多，可以配置得很好看

Warp 更轻量，而且支持 AI

### 代码片段——SnippetsLab、Cacher

SnippetsLab 用于本地代码片段收集

Cacher 可以多平台使用，能和 Gist 双向同步，但是 web 端访问有点慢，还是需要下客户端

### Docker Desktop 替代品 —— OrbStack

再也不用下载 Docker Desktop 了

### 笔记/知识管理——备忘录、Typora、Obsidian、Notion

临时的想法和任务基本使用的是系统自带的备忘录，如果用的苹果全家桶，记录之后同步很方便

一般记笔记现在都用 Markdown，Typora 简洁还好用

Obsidian 用来进行知识库搭建，他的双链和关系图谱很好用

Notion 用来记录一些需要联网同步的，之后还是需要誊抄到 Obsidian 中

### 图床——uPic、PicGo

个人使用的是腾讯云的 COS + CDN，下载客户端之后存储桶能一次性下载，迁移起来挺方便的

uPic 支持的图床种类很多，使用也方便，但是 Obsidian 和 Typora 都支持 PicGo，所以一直使用的都是 PicGo

### 设计、剪辑、建模等

PS、AI、Figma、MasterGo

Pr、Final Cut Pro、剪映

白板工具——fabrie

Spline、C4D、Blender

iFonts 之类的字体软件

### 素材收集——Billfish、Eagle

Billfish 用于浏览器素材收集

Eagle 用来整理，已入正

### 浏览器

Chrome、Edge、Arc、Tor Browser

浏览器插件太多，想单独一个文章列出

### 下载——NDM

需要搭配浏览器插件使用，我一般就用这个，其他需要的时候再搜索安装使用

### 防火墙/网络限制

TripMode——之前就用的这个，但是 M1 好像用不了

后来用的 Lulu

### SSH 工具——Termius

这个工具很好用，iPad 上也有

### 思维导图——MindNode、XMind ZEN、iThoughtsX

前两个中第一个不需要怎么配置、第二个模板很多

iThoughtsX 可以直接用 markdown 语法，非常推荐

### 办公——365、系统自带、WPS

之前注册了一个 A5 帐号，365 一直都是免费使用的，但是个人文字处理需求没那么强，所以基本没怎么用

### PDF——PDF Exper/PDF Reader Pro

很好用的 PDF 阅读/处理软件，需要找和谐版

### 阅读——X-Reader/NeatReader、CAJ 云阅读、微信读书

最常用的是 NeatReader、微信读书

NeatReader 基本全平台都有客户端，阅读体验非常不错，已经入了永久了

M1 可以直接下载 iPad 软件，微信读书可以直接购买图书，所以这个也直接下载使用了

### 翻译软件——Bob/TTime/Easydict、欧陆词典 Eudic

Bob 社区版是免费的，可以自定义配置

Easydict 完全免费，而且不需要配置，可以直接使用

### 网盘/同步——iCloud、Onedrive、百度网盘

iCloud 苹果全家桶必备，已经用上了土区的 2T 套餐，正好亲戚加起来凑满家庭共享人数

Onedrive 主要用来同步一些大点的文件或素材

百度网盘用于分享或备份，阿里云盘和其他网盘都使用了，但是还是感觉没百度网盘好用，反正刚好几个人一起用，就直接在优惠的时候开了四年 SVIP

### 远程控制

- 向日葵远程控制：这个全平台可使用，但是在 iPad 上操作的话不支持鼠标映射（toDesk 支持，但是副屏切换收费）
- raylink 远程控制：还不是很完善，但是看它功能计划，好像会升级需要的功能

### 邮件——系统自带邮件、网易邮箱大师、Spark Desktop

网易邮箱大师挺好用的，就是有些邮箱经常要重新登录

Spark Desktop UI 非常好看

### AI 客户端——chatbox/chatX、macGPT

- chatbox 在 win 和 mac 下都有，且能自定义更多功能
- chatX 有内置免费额度，也可以改成 API 模式
- macGPT 只有 mac 版，只有 openai 的且不能自定义域名（对网络要求比较高），但是它支持直接在任何输入框中用快捷方式使用它（在写文档或代码的时候很方便）

我一般两个都用，正常情况下都需要 fq，需要把自己的 key 和 API 域名都填入自己的

key 的话不想自己注册的，可以到网上低成本（超过 ￥3 就自己注册吧）购入一个帐号，有免费的额度，一般会直接给 key

因为 openai 的域名已经被墙了，每次 fc 都不太现实，可以到网上找下教程【使用 Cloudflare Workers 让 OpenAI API 绕过 GFW】

### 录屏等

用 OBS 录屏或者推流直播，用这个就够了

KeyCastr、显示按键，可以用来录制教程的时候屏显按键

[KeyCastr替代品和类似软件 — Altapps.net](https://zh.altapps.net/soft/keycastr)

## 参考文章

<https://www.sqlsec.com/2019/12/macos.html>

## 总结：安装命令和安装包

ClashX Pro 直接到这里下载：[App Center](https://install.appcenter.ms/users/clashx/apps/clashx-pro/distribution_groups/public)

修改配置文件和订阅，添加好别名

打开配置文件夹，修改默认配置文件 `config.yaml`，重点修改（添加）下列代码（个人习惯使用下面端口）

```yaml
# (HTTP and SOCKS5 in one port)
mixed-port: 10807
socks-port: 10808
port: 10809
```

一般机场都会提供 ClashX 的订阅，如果没有可以转换后一键导入到 Clash：[Subscription Converter](https://sub-web.opo.repl.co/)

修改 `~/.zshrc` 或 `~/.bashrc`，添加下面两条，然后 `source ~/.zshrc` 或 `~/.bashrc`

```sh
alias fq="export https_proxy=http://127.0.0.1:10807 http_proxy=http://127.0.0.1:10807 all_proxy=socks5://127.0.0.1:10807; echo setted"
alias fqexit="unset https_proxy http_proxy all_proxy; echo disabled"
```



### 安装 App 和 Cli 工具

安装 HomeBrew 并用他安装 App 和 Cli 工具

App 可以在 [homebrew-cask — Homebrew Formulae](https://formulae.brew.sh/cask/) 里找有没有，Cli 工具可以在 [homebrew-core — Homebrew Formulae](https://formulae.brew.sh/formula/) 找有没有

或者直接使用 `brew search appname` 然后使用 `brew info appname` 看是不是自己要的那个软件

```sh
# 先开代理，不然会很慢（依赖第一步）
fq

# 安装 HomeBrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 用 HomeBrew 安装 App
brew install bigwig-club/brew/upic --cask
brew install --cask \
	airserver \ 
  alfred \
  alt-tab \
  android-file-transfer \
  apifox \
  arc \ 
  aria2gui \ 
  baidunetdisk \ 
  battery-buddy \ 
  bitwarden \ 
  blender \ 
  bob \ 
  cacher \ 
  chatbox \ 
  dash \ 
  dingtalk \ 
  discord \ 
  downie \ 
  eagle \  
  easydict \ 
  eudic \ 
  espanso \  
  feishu \ 
  figma \  
  firefox \ 
  franz \ 
  free-download-manager \ 
  fork \ 
  google-chrome  \  
  gas-mask \  
  handbrake \  
  handshaker \ 
  iina \  
  imageoptim \ 
  iterm2 \  
  jetbrains-toolbox \ 
	kap \ 
  karabiner-elements \  
  keepingyouawake \  
  keyboardholder \ 
  keycastr \  
  licecap \  
  lyricsx \ 
  maczip \ 
  mailmaster \ 
  menubarx \
  miaoyan \
  microsoft-edge \ 
  microsoft-remote-desktop \  
  middleclick \ 
  motrix \ 
  mos \ 
  neat-reader \ 
  neteasemusic \ 
  notion \ 
  obs \  
  obsidian \ 
  onedrive \ 
  orbstack \ 
  oss-browser \ 
  permute \ 
  picgo \ 
  pictureview \ 
  qq \ 
  qqmusic \ 
  raycast \  
  rectangle \
  shottr \ 
  simplenote \ 
  sip \ 
  snipaste \ 
  sourcetree \  
  sunlogincontrol \ 
  telegram \  
  tencent-lemon \ 
  termius \ 
  thor \  
  tinypng4mac \ 
  tor-browser \ 
  tuxera-ntfs \ 
  usr-sse2-rdm \  
  videofusion \  
  visual-studio-code \  
  warp \ 
  wechat \
  yesplaymusic \ 
  yuque \ 
  zerotier-one

# 安装 Cli 工具，以下是我的（以字母排序，方便你查找）
brew install \  
  autojump \  
  bat \  
  cmatrix \  
  commitzen \  
  deno \  
  diff-so-fancy \  
  fd \  
  ffmpeg \  
  fzf \  
  gh \  
  git \  
  httpie \  
  hub \  
  hyperfine \  
  imagemagick \  
  jq \  
  lazygit \  
  macvim \ 
  mkcert \  
  neovim \ 
  nvm \  
  paper \
  pnpm \  
  thefuck \ 
  the_silver_searcher \  
  tig \  
  tldr \  
  tree \  
  ugit \  
  wget
```

2、用 SetApp 安装额外 App。

- Bartender
- CleanMyMac X
- CleanShot X
- DevUtils
- Downie
- Focus
- Sip
- RapidAPI
- Paste
- Yoink

3、用 Mac App Store 安装额外 App。

- Bob
- Tot
- RunCat
- Infuse

4、通过其他渠道安装额外 App。

- [Flomo x Pake](https://github.com/tw93/Pake)
- [Flux](https://justgetflux.com/)
- Reeder（国区没有）
- PDF Expert
- [uPic](https://github.com/gee1k/uPic)
- [ChatGPT x Tauri](https://github.com/lencx/ChatGPT)
- [Microsoft 365](https://apps.apple.com/cn/app-bundle/microsoft-365/id1450038993?mt=12)
- [以方·iFonts字体助手](https://ifonts.com/client)
- [Neat Download Manager](https://www.neatdownloadmanager.com/index.php/en/)



## 配置 App

> 按这个顺序会比较好。

1、Karabiner-Elements

参考 [Karabiner-Element 配置 F19 键 - HackMD](https://hackmd.io/@UXqYDTxCTie91Shvsppqyw/rk4u9i-pG?type=view) 。在 [Karabiner-Elements complex\_modifications rules](https://pqrs.org/osx/karabiner/complex_modifications/) 搜「Change caps\_lock key」，import 后只保留一条和 F19 相关的，然后在命令行里编辑「~/.config/karabiner/karabiner.json」，把刚才那条规则的「caps\_lock」换成「right\_command」（两处）。这样你就把基本不会用到的「右⌘」废物利用变成了「F19」键，然后你的快捷键组合会多很多。

如果你仔细看配置，会发现「F19」是由四个键「⌘⇧⌃⌥」组成的，在一些 App 的快捷键配置里你会看到四个键，不要奇怪，这也是他。

2、Alfred

做几个配置。1）开启 Powerpack，2）修改快捷键为刚才配的「F19」，3）把老电脑的 Alfred 配置复制到 ~/Documents/SoftwareConfiguration/Alfred 下，然后在「Advanced」里修改配置目录指向他，你的 Workflow 就全回来了，4）「Features > Web Bookmarks」里记得把「Google Chrome Bookmarks」选上，这样就可以用 Alfred 模糊搜 Chrome 书签，用于快速打开网站。

3、iTerm2 和 zsh

先配置 iTerm2，这是[效果图](https://img.alicdn.com/imgextra/i1/O1CN01PPttEm1mCx3bddVjX_!!6000000004919-2-tps-2374-1532.png)。1）Appearance 里，General 的 Theme 选「Minimal」，Pane 里不要「Show per-pane title bar with split panes」，Dimming 里选上第一和第三个，2）Profiles 里，Working Directory 里选「Reuse previous session's directory」。

安装 zsh 和 [starship](https://starship.rs/)，starship 是 rust 写的 prompt 工具，极快。

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
omz update
source ~/.zshrc
# starship 是 rust 写的 prompt 工具，极快
brew install starship
echo 'eval "$(starship init zsh)"' >> ~/.zshrc
```

安装 zsh 的插件，我个人用到了 zsh-autosuggestions、zsh-completions 和 fast-syntax-highlighting。

```
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-completions ${ZSH_CUSTOM:-${ZSH:-~/.oh-my-zsh}/custom}/plugins/zsh-completions
git clone https://github.com/zdharma-continuum/fast-syntax-highlighting.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/fast-syntax-highlighting
```

配置 ~/.zshrc，我的配置如下（略做删减）。这里有些 alias 是以 `,` 开头的，因为这样你敲 `,` 然后按「Tab」就可以[看到所有自己定义的命令](https://img.alicdn.com/imgextra/i3/O1CN01XUDvg01ZHRwduLZSo_!!6000000003169-0-tps-1422-194.jpg)了。为啥有些没有加 `,` ？历史原因… 因为其他都用习惯了就不改了。

```
# Disable brew auto update
export HOMEBREW_NO_AUTO_UPDATE=1
export ZSH="$HOME/.oh-my-zsh"

plugins=(
  # 不会 git 插件，因为和我的 alias 设置冲突
  # git
  zsh-completions
  zsh-autosuggestions
  fast-syntax-highlighting
)

# Alias
alias ,ms="%PATH/TO/MY/SCRIPT%"
alias ,ip="ipconfig getifaddr en0"
alias ,sshconfig="vim ~/.ssh/config"
alias ,gitconfig="vim ~/.gitconfig"
alias b=",ms branch"
alias umi="/Users/%MY_USERNAME%/Documents/Code/github.com/umijs/umi/packages/umi/bin/umi.js"
# chore
alias br="bun run"
alias c='code .'
alias i='webstorm .'
alias cdtmp='cd `mktemp -d /tmp/sorrycc-XXXXXX`'
alias pi="echo 'Pinging Baidu' && ping www.baidu.com"
alias ip="ipconfig getifaddr en0 && ipconfig getifaddr en1"
alias cip="curl cip.cc"
alias qr='qrcode-terminal'
alias ee="stree"
alias hosts="vi /etc/hosts"
## system
alias showFiles="defaults write com.apple.finder AppleShowAllFiles YES && killall Finder"
alias hideFiles="defaults write com.apple.finder AppleShowAllFiles NO && killall Finder"
# cd
alias ..='cd ../'
alias ...='cd ../../'
alias ..l.='cd ../../ && ll'
alias ....='cd ../../../'
alias ~="cd ~"
alias -- -="cd -"
alias ll='ls -alhG'
alias ls='ls -G'
# git
alias git=hub
alias gp="git push"
alias gt="git status -sb"
alias ga="git add ."
alias gc="git commit -av"
alias gcr="git checkout master && git fetch && git rebase"
alias gclean="git reset --hard && git clean -df"
alias grebase="git fetch && git rebase -i"

## timelapse
## ref: https://www.reddit.com/r/mac/comments/wshn4/another_way_to_timelapse_record_your_mac_screen/
function record() {
  cd ~/screencapture/jpg;
  RES_WIDTH=$(/usr/sbin/system_profiler SPDisplaysDataType | grep Resolution);
  RES_WIDTH=(${RES_WIDTH:22:4});
  RES_WIDTH=$((RES_WIDTH/2));
  while :
  NOW=$(date +"%y%m%d%H%M%S");
  do screencapture -C -t jpg -x ~/screencapture/jpg/$NOW.jpg;
    sleep 7 & pid=$!
    NOW=$(date +"%y%m%d%H%M%S");
    wait $pid
  done
}
function movie() {
  NOW=$(date +"%y%m%d%H%M%S");
  cd ~/screencapture/jpg;
  cnt=0
  rm -rf .DS_Store;
  for file in *
    do
      if [ -f "$file" ] ; then
      ext=${file##*.}
      printf -v pad "%05d" "$cnt"
      mv "$file" "${pad}.${ext}"
      cnt=$(( $cnt + 1 ))
    fi
  done;
  rm -rf 00000.jpg;
  for pic in *.jpg;
    do convert $pic -resize 50% $pic;
  done;
  ffmpeg -r 24 -i %05d.jpg -b 20000k ~/screencapture/mov/$USER-$NOW.mov;
  rm -rf ./*.jpg;
}

function pfd() {
  osascript 2> /dev/null <<EOF
  tell application "Finder"
    return POSIX path of (target of window 1 as alias)
  end tell
EOF
}
function mcd {
  mkdir $1 && cd $1;
}
function cdf() {
  cd "$(pfd)"
}
function ,touch {
  mkdir -p "$(dirname "$1")" && touch "$1"
}
function ,take() {
  mkdir -p "$(dirname "$1")" && touch "$1" && take "$(dirname "$1")"
}

# load zsh-completions
autoload -U compinit && compinit

# use nvm
source /opt/homebrew/opt/nvm/nvm.sh

# autojump
source /opt/homebrew/etc/profile.d/autojump.sh

# use starship theme (needs to be at the end)
eval "$(starship init zsh)"

# 必须在 plugins 之后
source $ZSH/oh-my-zsh.sh

# bun completions
[ -s "/Users/chencheng/.bun/_bun" ] && source "/Users/chencheng/.bun/_bun"

# bun
export BUN_INSTALL="$HOME/.bun"
export PATH="$BUN_INSTALL/bin:$PATH"

# pnpm
export PNPM_HOME="/Users/chencheng/Library/pnpm"
export PATH="$PNPM_HOME:$PATH"
```

4、SSH

```
mkdir ~/.ssh
# file name 用 github，passphrase 随意
ssh-keygen -t ed25519 -C "github"
# 编辑配置，内容如下
touch ~/.ssh/config
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/github
# 添加到系统 keychain
ssh-add --apple-use-keychain ~/.ssh/github
# 添加 public key 到 github
gh auth login
gh ssh-key add ~/.ssh/github.pub -t github
```

5、额外的命令行工具：Bun 和 Projj

安装 Bun。我主要是用他的 run 命令，极快，上面也有别名 `br`，比如执行比如 `br dev` 即 `npm run dev`。

```
curl -fsSL https://bun.sh/install | bash
```

安装 PROJJ，我用他来管理 Code 下的仓库，按「domain/group/repo」这样组织，找起来会比较容易。

```
pnpm i projj projj-hooks -g
projj init
```

然后编辑 ~/.projj/config.json，我的配置如下（记得把 name 和邮箱改成自己的）。

```
{
  "base": [
    "/Users/%YOUR_USERNAME%/Documents/Code"
  ],
  "hooks": {
    "postadd": "projj_git_config_user"
  },
  "postadd": {
    "github.com": {
      "name": "sorrycc",
      "email": "sorrycc@gmail.com"
    }
  },
  "alias": {
    "github://": "https://github.com/"
  }
}
```

然后就可以愉快地用 PROJJ 添加项目了，比如。

```
projj add git@github.com:umijs/umi.git
```

6、Espanso

我在 ~/Documents/SoftwareConfiguration/Espanso 下建了个 base.yml，内容如下（已删除个人敏感信息），并软链到 Espanso 原来的配置文件夹里。

```
matches:
  # misc
  - trigger: ";>>"
    replace: ➡
  - trigger: ";vv"
    replace: ⬇
  - trigger: ";^^"
    replace: ⬆
  - trigger: ";<<"
    replace: ⬅
  # life
  - trigger: ";mobi"
    replace: 我的手机号
  - trigger: ";mail"
    replace: 我的邮箱
  - trigger: ";addr"
    replace: 我的家庭住址
  - trigger: ";officeAddr"
    replace: 公司地址
  # faq
  - trigger: ";chongt"
    replace: 冲突了，merge 下 master。
  # code
  - trigger: ";log"
    replace: console.log($|$)
  - trigger: ";delay"
    replace: const delay = (ms) => new Promise((res) => setTimeout(res, ms));
  # mac symbols
  - trigger: ":cmd"
    replace: "⌘"
  - trigger: ":shift"
    replace: "⇧"
  - trigger: ":ctrl"
    replace: "⌃"
  - trigger: ":alt"
    replace: "⌥"
  - trigger: ":opt"
    replace: "⌥"
  - trigger: ":left"
    replace: "←"
  - trigger: ":right"
    replace: "→"
  - trigger: ":up"
    replace: "↑"
  - trigger: ":down"
    replace: "↓"
  - trigger: ":caps_lock"
    replace: "⇪"
  - trigger: ":esc"
    replace: "⎋"
  - trigger: ":eject"
    replace: "⏏"
  - trigger: ":return"
    replace: "↵"
  - trigger: ":enter"
    replace: "⌅"
  - trigger: ":tab"
    replace: "⇥"
  - trigger: ":backtab"
    replace: "⇤"
  - trigger: ":pgup"
    replace: "⇞"
  - trigger: ":pgdown"
    replace: "⇟"
  - trigger: ":home"
    replace: "↖"
  - trigger: ":end"
    replace: "↘"
  - trigger: ":space"
    replace: "␣"
  - trigger: ":del"
    replace: "⌫"
  - trigger: ":fdel"
    replace: "⌦"  
```

7、Thor

让你可以一键启动、显示或隐藏某个 App，对我来说是效率神器。但有时太快也不好，会让你无意间地快速切过去，比如钉钉、Reeder 和 Telegram 我后来就把他们去掉了。

我的配置见[图](https://img.alicdn.com/imgextra/i3/O1CN01PWmDZN24797TUfPbL_!!6000000007343-0-tps-594-1918.jpg)，快捷键供参考。

8、安装字体

编程字体我用 [Monolisa](https://www.monolisa.dev/)，之前还用过 [Source Code Pro](https://github.com/adobe-fonts/source-code-pro)、[Dank Mono](https://dank.sh/) 和 [Operator Mono](https://www.typography.com/fonts/operator/overview)。此外我还安装了[霞鹜文楷](https://github.com/lxgw/LxgwWenKai)和阿里普惠体，霞鹜文楷我用在了语雀等文档站和 Obsidian 里。

9、WebStorm

简单几步配置即可。1）安装 Github Copilot 和 Inspection Lens 插件，2）配置 Color Schema 为「Intellij Light」，3）配置 Font 为 MonoLisa，同时 Size 为 20，大点对眼睛好，哈哈。

10、VSCode

辅助编辑器，施工中。

目前包含的插件如下。

```
dbaeumer.vscode-eslint
esbenp.prettier-vscode
GitHub.copilot
isudox.vscode-jetbrains-keybindings
kettanaito.nako
styled-components.vscode-styled-components
unifiedjs.vscode-mdx
usernamehw.errorlens
```

主题是 [Nako - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=kettanaito.nako)。

配置如下。

```
。
```

11、Git

先配 name 和 email。

```
git config --global user.name "Your Name"
git config --global user.email "you@your-domain.com"
```

再执行这两条命令。

```
git config --global --add push.default current
git config --global --add push.autoSetupRemote true
```

你会收获两个好处。1）不需要「git push origin xxx」，只要「git push」，2）再也不会遇到「no upstream branch」的报错，也不需要「git push --set-upstream origin test && git push」。因为我们执行 git push 的大部分场景都是 push 到同名的 remote branch。来源是 [Auto setup remote branch and never again see an error about the missing upstream | pawelgrzybek.com](https://pawelgrzybek.com/auto-setup-remote-branch-and-never-again-see-an-error-about-the-missing-upstream/)。

再修改 ~/.gitignore\_global，加入和你 IDE 相关的 ignore 配置。我会把 .idea 加进去，这是和你相关的专有配置，如果给其他用 VSCode 的作者的项目提交时，都加上 .idea 的 .gitignore 配置，其实并不太礼貌。反之，VSCode 或其他编辑器工具的用户也要加上自己的。

```
*~
.DS_Store
.idea
```

12、NVM 和 Node

```
nvm install 18
node -v
```

13、Eagle

Eagle 的库我保存在 ~/Documents/SoftwareConfiguration/Eagle 下。

14、Focus

要稍微做下配置。1）添加 Block App，我加了钉钉、Reeder，2）Block Website 里我把内置的全删了，留了[这些](https://img.alicdn.com/imgextra/i3/O1CN017Pt2Y827DxrmBSPh4_!!6000000007764-2-tps-1448-1408.png)，3）Block App 的配置要选「强制退出」，「隐藏」的模式在 Mac 13.2 下有问题，不会生效或者表现奇怪。

15、Bob。

我的快捷键是「F19+A」划词翻译，「F19+S」截图翻译。插件装了 [bob-plugin-deeplx](https://github.com/clubxdev/bob-plugin-deeplx) 和 [bobplugin-google-translate](https://github.com/roojay520/bobplugin-google-translate)。文本翻译我加了 Deepl X、有道、阿里、金山词霸，文本识别我用腾讯 OCR。

16、Rectangle。

删了所有快捷键，只保留两个。「F19+C」居中，「F19+M」放最大。

17、uPic

用了自定义图床，略。

18、Paste

我的快捷键是「⌘⌥C」。配置里选上「Always paste as Plain Text」，去掉「Enable sound effects」。

19、Reeder

两个改动。在 Shortcuts 配置里，把「Mark All as Read…」的快捷键改成「⇧A」，然后去掉「Ask before marking all as read」。

20、Google Chrome

登录 Google 账号后所有东西就都同步过来了，除了 Tampermonkey 的自定义脚本。但简单 Google 后也找到了办法，我参考 [extract\_tampermonkey\_script.py · GitHub](https://gist.github.com/derjanb/9f6c10168e63c3dc3cf0) 把 `/Users/%YOUR_USERNAME%/Library/Application\ Support/Google/Chrome/Default/Local\ Extension\ Settings/dhdgffkkebhmkfjojejmpbldmpobfkfo` 这个文件夹下的内容复制到新电脑后就能用了。

21、Telegram

登录时死活登不上，开了代理才行。

22、Obsidian

我先试了用 Obsidian Sync 直接同步出本地文档库，但发现只包含文档，不包含插件。于是改成先用 git clone 完整仓库，再关联到 Obsidian Sync 的远程文档库。用 Git 做同步时有个要注意的是，.obsidian 目录下的 workspace 相关的 3 个文件不要提交，否则会很容易冲突。

23、SourceTree

配置中「Git」Tab 下选「Use System Git」，否则会报找不到 git 的错误。

24、iA Writer

把所有 Markdown 文件[改成用 iA Writer 打开](https://img.alicdn.com/imgextra/i1/O1CN01YZ2Osn1qtmYrCS9tw_!!6000000005554-2-tps-502-752.png)，因为 iA Writer 又轻又好看。然后我在「系统设置 > Keyboard > Keyboard Shortcuts > App Shortcuts」中增加了一些针对 IA Writer 的快捷键配置。

- Show Preview「⌘P」
- Hide Preview「⌘P」
- Move Line Up「⌘⇧↑」
- Move Line Down「⌘⇧↓」
- Strikethrough「⌘⇧R」

25、Shottr

快捷键里把所有都删了，只保留两个。Area screenshot 用「F19 + 7」，Scrolling screenshot 用「F19 + 8」。

26、Sip

Show Picker 的快捷键是「F19 + 2」。

27、CleanShotX

Capture Area 的快捷键是「F19 + 6」。

## 系统设置

1、General。1）Default Web Browser 用「Google Chrome」，2）Language & Region 里，把 First day of week 改成「Monday」，这样你的日历就会[从周一开始](https://img.alicdn.com/imgextra/i2/O1CN014aouuQ1HfZisiosbo_!!6000000000785-0-tps-2456-1572.jpg)了。

2、Siri。直接禁掉。

3、Trackpad。Scroll direction：Natural 去掉。

4、Keyboard。1）Keyboard 里把 Key Repeat 调到「Fast」，把 Delay Util Repeat 调到「Short」，需要一点时间适应，适应后会感受到光标快速移动带来的效率提升，2）Text 里 use `"` for double quotes，use `'` for single quotes，然后把其他都禁掉，不需要系统帮忙改，基本都是帮倒忙的，3）Shortcuts 里，Mission Control 用「⌥A」,Application windows 用「⌥S」，Show Desktop 用「⌥D」，Input Sources 的 Select Previous 用 「⌘Space」，Screenshots 里 Save picture of selected area as a file 用「F19 + 3」，Copy picture of selected area to the clipboard 用「F19 + 4」，4）输入法删除默认的拼音改用搜狗拼音，登录后可以在不同电脑之间同步词库，搜狗输入法的皮肤我用的[Matrix 矩阵](https://github.com/xiaochunjimmy/Sogou-Input-Skin)。

5、Spotlight。只开 Applications、Bookmarks & History、Documents、Folders、System Preferences。

6、Mission Control。把 Hot Corners 里的全部关掉，不需要，因为有 Thor 了，可以更快切除应用。

7、Sharing。只留「AirPlay Receiver」即可，同时可以改下 computer name。

8、Security & Privacy。把「Use Apple Watch to unlock」打开。

9、Notification。不必要的全关掉，我只开了 Calendar、Find By、Reminders 和 Wallet。

10、Touch ID and Password。开启用 Apple Watch 解锁。

11、执行 `defaults write -g NSWindowShouldDragOnGesture -bool true`，然后就可以按住「⌘+⌃」然后鼠标点击任意地方拖动窗口了。来源 [Moving a macOS window by clicking anywhere on it (like on Linux) · mmazzarolo.com](https://mmazzarolo.com/blog/2022-04-16-drag-window-by-clicking-anywhere-on-macos/)，但是在 MacOS 13 下似乎失效了。

## 参考

- [Mac Setup for Web Development 2023](https://www.robinwieruch.de/mac-setup-web-development/)
- [My 2021 New Mac Setup](https://www.swyx.io/new-mac-setup-2021)

## 使用习惯

- 访达中个人文件夹：`~/workspace/`
  - 代码：`~/workspace/code/`
    - 学习：`./learn/`
    - 博客：`./myblogs/`、`./blog/`、`./MyBlog/`
    - 测试：`./test/`
    - 小 Demo：`./demos/`
  - 设计：`~/workspace/design/`
    - 素材：`~/workspace/design/resource/`
    - 收集：`~/workspace/design/collect/`
  - 临时目录：`~/workspace/temp`
  - 工作：`~/workspace/work`
  - 知识库：`~/workspace/MyKnowledgeBase`
- 系统自带文件夹：
  - 文档：`~/Documents/`
  - 下载：`~/Downloads/`
  - 音乐：`~/Music/`
  - 影视：`~/Movies/`
  - 图片：`~/Pictures/`
- 同步文件夹：`~/CloudSync/`
  - Onedrive：`./Onedrive/`
  - 百度同步：`./BaiduSync/`
- 虚拟机文件夹：`~/Parallels/`
- 个人配置文件夹：`~/.config/`
  - Clash：`./clash/`
  - Iterm2：`./iterm2/`
  - Nvim：`./nvim/`
  - Raycast：`./raycast/`
  - Thefuck：`./thefuck/`
  - ……
- 运行命令和打开文件夹：
  - 终端中打开访达：`open .`
  - 终端中用 VSCode 打开目录：`code .`
  - 访达中打开 iterm 进入目录：
    - 右键助手
    - Raycast

- 代理
  - Clash 进行代理，使用订阅进行配置，只设置全局，平常不开启系统代理，配置 `config.yaml` 中 `mixed-port: 10807`、`socks-port: 10808`、`port: 10809`，`socks5` 端口是 `10808`、`http`/`https` 端口号是 `10809`
  - 浏览器使用 SwitchyOmega 插件进行代理，配置好代理模式（`SOCKS5、127.0.0.1、10808`），和自动切换模式，平常只开启自动切换，每次需要代理就添加规则
  - 软件代理：使用和谐版 Proxifier，Proxies 添加一条 `127.0.0.1 10808 SOCKS5`，Rules 添加四条——直连 APPs（Clash 相关、Direct）、默认 Direct、代理网站（相关网站、SOCKS5...）、代理应用（相关应用 TG 等、SOCKS5...）
  - 终端代理：
    - 配置别名：之前添加了别名，需要代理的时候就输入 `fq`、恢复默认就 `fqexit`
    - 或者使用开源应用 proxychains，M1 需要自己编译，设置别名 `alias pc="proxychains4 -f ~/.proxychains.conf"`
- 包管理工具
  - brew
    - 通过 brew 安装的软件只通过 brew 更新
  - nvm
    - 只使用 pnpm：`alias npm="pnpm"`，需要用 npm 则使用 `\npm`
    - pnpm 中不需要 `^`：`npm config set save-prefix=""`
