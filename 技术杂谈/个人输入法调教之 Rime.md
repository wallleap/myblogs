---
title: 个人输入法调教之 Rime
date: 2023-03-10 11:20
updated: 2023-03-10 11:20
cover: //cdn.wallleap.cn/img/pic/cover/202303Njy53E.jpg
category: 技术杂谈
tags:
  - 电脑
  - 输入法
description: 个人输入法调教之 Rime
---

一直以来使用的都是搜狗输入法，使用体验还是不错的，但是~~身为一个从事互联网行业的人，怎么可以直接用一直记录你隐私并能上传到云端的输入法呢~~身为一个折腾爱好者，怎么能不搞搞事呢

在对比了一些开源且无需联网的输入法之后，选择了 Rime，它支持双拼、拼音、五笔等输入方案，可以导入自己用熟了的词库（例如搜狗的），而且它的算法服务也很 Nice

本文调教主要目的是让 Rime 成为使用舒心的中文输入法，包括：

- [x] 只保留小鹤双拼
- [x] 调一个舒适的外观
- [x] 只使用 Rime 的中文，英文留给系统输入法（快捷键切换 <kbd>Control</kbd> + <kbd>Space</kbd>）
- [x] 加入 emoji 支持
- [x] 不需要模糊音，双拼下一般不会打错，有模糊音只会让前面的候选项位被占
- [x] 加入一些常用的自定义短语文本
- [x] 转换自己的词库并加入
- [ ] 拆字词库，不知道文字的拼音的时候用，例如先按 <kbd>Ctrl</kbd> + <kbd>u</kbd> 再输入单字（搜狗的 u 模式）
- [x] 添加 `/` 加 `fh` 显示符号之类的操作
- [x] 支持使用 <kbd>【</kbd>/<kbd>】</kbd>、<kbd>Control</kbd> + <kbd>j</kbd>/<kbd>k</kbd> 切换上/下页
- [x] 支持时间和日期动态输入
- [x] 使用 iCloud 进行同步

在配置的时候尽可能保证配置文件的简洁性和规整性，不需要的配置项就不加

仓库地址：<https://github.com/wallleap/rime-conf>

部分配置参考自：[Lufs](https://blog.isteed.cc/)

## 认识 Rime

Rime 是一种输入法框架，各平台可以下载相应发行版进行安装（安装的时候可以选择配置存放的目录，也可以选用默认的目录）

- Windows 下小狼毫 [Weasel](https://github.com/rime/weasel/releases/latest)
- macOS 下鼠须管 [Squirrel](https://github.com/rime/squirrel/releases/latest)
- Linux 下 [ibus-rime](https://github.com/rime/home/wiki/RimeWithIBus)、[fcitx-rime](https://github.com/fcitx/fcitx-rime)
- Android 下[同文输入法](https://github.com/osfans/trime/releases)

*个人只用了 macOS 和 Win，所以后面的配置应该不会出现 Linux 的*

修改配置

- 所有的配置在【用户文件夹/用户设定...】中，可以在菜单栏中右键【Rime】图标后选择进入
- 修改配置文件（UTF-8 编码 使用 LF 换行符）
- 修改完成之后需要右键【Rime】图标后点击【重新部署】配置才能生效

## 阅读 WIKI

Rime 有专门的指南可以查阅：[WIKI](https://github.com/rime/home/wiki)

建议通篇阅读之后再进行配置的修改

- <https://github.com/rime/home/wiki/UserGuide>（用户指南）  
- <https://github.com/rime/home/wiki/Configuration>（配置文件）  
- <https://github.com/rime/home/wiki/CustomizationGuide>（定制指南、必知必会）  
- <https://github.com/rime/home/wiki/RimeWithSchemata>(設定項速查手冊、Schema.yaml 詳解)

**其他**

基础配置文件可以在这里下载：

- [rime-prelude](https://github.com/rime/rime-prelude/tree/master)
- [Schema.yaml 详解](https://github.com/KyleBing/rime-wubi86-jidian/wiki/Schema.yaml-%E8%AF%A6%E8%A7%A3)
- `Schema.yaml` 詳解 [Rime_descriptionb](https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/Rime_description.md)
- 更多输入方案 <https://gist.github.com/lotem/2309739>

## 调教中文输入法

大部分输入方案（在 `default.custom.yaml` 文件中）注意 `yaml` 文件对格式检测很严格，例如缩进和冒号后面需要保留一个空格，千万别弄错层级，也别忽略掉空格，不需要的内容可以用 `#` 注释掉或者删掉：

```yaml
# default.custom.yaml
# save it to:
# ~/.config/ibus/rime (linux)
# ~/Library/Rime (macos)
# %APPDATA%\Rime (windows)
patch:
	schema_list:
		- schema: luna_pinyin # 明月拼音
		- schema: luna_pinyin_simp # 明月拼音 简化字模式
		- schema: luna_pinyin_tw # 明月拼音 臺灣正體模式
		- schema: terra_pinyin # 地球拼音 dì qiú pīn yīn
		- schema: bopomofo # 注音
		- schema: bopomofo_tw # 注音 臺灣正體模式
		- schema: jyutping # 粵拼
		- schema: cangjie5 # 仓颉五代
		- schema: cangjie5_express # 仓颉 快打模式
		- schema: quick5 # 速成
		- schema: wubi86 # 五笔86
		- schema: wubi_pinyin # 五笔拼音混合輸入
		- schema: double_pinyin # 自然码双拼
		- schema: double_pinyin_mspy # 微軟双拼
		- schema: double_pinyin_abc # 智能 ABC 双拼
		- schema: double_pinyin_flypy # 小鹤双拼
		- schema: wugniu # 吳語上海話（新派）
		- schema: wugniu_lopha # 吳語上海話（老派）
		- schema: sampheng # 中古汉语三拼
		- schema: zyenpheng # 中古汉语全拼
		- schema: ipa_xsampa # X-SAMPA 国际音标
		- schema: emoji # emoji 表情
```

代码片段来自：[在Rime輸入方案選單中添加五筆、雙拼、粵拼、注音](https://gist.github.com/lotem/2309739)

个人一般只用小鹤双拼，因此其他的都去掉了，`default.custom.yaml` 文件中只保留小鹤双拼（也可以直接使用 [rime/plum: 東風破](https://github.com/rime/plum)以命令的方式安装）

```yaml
patch:
	schema_list:
		- schema: double_pinyin_flypy # 小鹤双拼
```

除了需要在用户自定义全局配置文件中加入上述字段，还需要新增相应的方案文件（`对应方案名称.schema.yaml`），例如小鹤双拼：需要下载 `double_pinyin_flypy.schema.yaml` 这个文件放到用户文件夹下

小鹤双拼的这个文件可以直接到官方仓库下载：[雙拼輸入方案](https://github.com/rime/rime-double-pinyin)

其他的方案可以去找相应的官方仓库：[RIME](https://github.com/orgs/rime/repositories)

把 `double_pinyin_flypy.schema.yaml` 放到用戶文件夹且新增了 `patch-schema_list-schema` 字段之后，重新部署，这个时候就可以使用小鹤双拼了，但是输入文字会发现是繁体字

这个时候可以使用快捷键 <kbd>Ctrl</kbd> + <kbd>`</kbd> 调出切换选框，使用上下键切换选择内容，<kbd>Tab</kbd> 键切换下页，回车选中当前项

但是我们一般使用的是简体中文，所以最好把它改成默认的：修改  `double_pinyin_flypy.schema.yaml` 的下述字段

```yaml
switches:
  - name: ascii_mode
    reset: 0  # 通过 reset 设置初始值 0 代表第一项
    states: [ 中文, 西文 ]
  - name: full_shape
    states: [ 半角, 全角 ]
  - name: simplification
    reset: 1  # 1 代表第二项
    states: [ 漢字, 汉字 ]
  - name: ascii_punct
    states: [ 。，, ．， ]
```

## 调一个舒适的外观

个人喜欢横排展示候选词，皮肤的话是根据网上找来的进行了修改

候选词设定 4 个：

```yaml
# default.custom.yaml ← 文件名是这个
patch:
	menu/page_size: 4 # 候选项数
```

### 小狼毫

新建文件 `weasel.custom.yaml` 输入内容

```yaml
# weasel.custom.yaml
patch:
  style:
    horizontal: true          # 候選橫排
    inline_preedit: true      # 內嵌編碼（僅支持TSF）
    display_tray_icon: false  # 顯示托盤圖標
    layout:
      border: 0
      margin_x: 12
      margin_y: 12
      hilite_padding: 12
      hilite_spacing: 4
      spacing: 12
      candidate_spacing: 24
      round_corner: 8
    color_scheme: blue
  preset_color_schemes:
    blue:
      name: "蓝色／blue"
      author: "web"
      candidate_format: "%c\u2005%@" # 编号 %c 和候选词 %@ 前后的空间
      font_face: "PingFangSC" # 候选词字体
      font_point: 16 # 候选字词大小
      label_font_face: "PingFangSC" # 候选词编号字体
      label_font_point: 12 # 候选编号大小
      back_color: 0xFFFFFF # 候选条背景色，24位色值，16进制，ABGR顺序
      border_color: 0xFCF4EB # 边框颜色
      candidate_text_color: 0x2E2E2E # 预选项文字颜色
      comment_text_color: 0xE0E0E0 # 拼音等提示文字颜色
      hilited_candidate_label_color: 0xFFDEA6 # 候选编号颜色
      hilited_candidate_text_color: 0xF4953C # 候选文字颜色
      hilited_candidate_back_color: 0xFCF4EB # 候选文字背景色
      label_color: 0xE0E0E0 # 预选栏编号颜色
      text_color: 0x2E2E2E # 高亮选中词颜色
```

配色到这里调整：[Rime西米](https://bennyyip.github.io/Rime-See-Me/)

### 鼠鬚管

新建文件 `squirrel.custom.yaml` 输入内容

```yaml
# squirrel.custom.yaml
patch:
  show_notifications_via_notification_center: true
  app_options: {} # 清除应用默认输入法，防止无法输入中文
  style:
    color_scheme: blue
    translucency: true # 背景半透明总开关，不需要关掉即可
  preset_color_schemes:
    blue:
      name: "蓝色/blue"
      author: "web"
      alpha: 0.95 # 透明度
      horizontal: true # 水平排列
      inline_preedit: true # 单行显示，false 双行显示
      candidate_format: "%c\u2005%@" # 编号 %c 和候选词 %@ 前后的空间
      corner_radius: 8 # 候选条圆角
      border_height: 0
      border_width: 0
      font_face: "PingFangSC" # 候选词字体
      font_point: 16 # 候选字词大小
      label_font_face: "PingFangSC" # 候选词编号字体
      label_font_point: 12 # 候选编号大小
      color_space: display_p3
      back_color: 0xFFFFFF # 候选条背景色，24位色值，16进制，ABGR顺序
      border_color: 0xFCF4EB # 边框颜色
      candidate_text_color: 0x2E2E2E # 预选项文字颜色
      comment_text_color: 0xE0E0E0 # 拼音等提示文字颜色
      hilited_candidate_label_color: 0xFFDEA6 # 候选编号颜色
      hilited_candidate_text_color: 0xF4953C # 候选文字颜色
      hilited_candidate_back_color: 0xFCF4EB # 候选文字背景色
      label_color: 0xE0E0E0 # 预选栏编号颜色
      text_color: 0x2E2E2E # 高亮选中词颜色
```

除了上面这个，也可以参照这个模板配置：[【鼠鬚管】定製檔](https://gist.github.com/lotem/2290714)

具体样子是这样的：

![](https://cdn.wallleap.cn/img/pic/illustration/202303091415860.png)

配色到这里调整：[Rime 西米 for Squirrel](https://gjrobert.github.io/Rime-See-Me-squirrel/)

## 中英文切换

macOS 和 Win 下我都使用 <kbd>Ctrl</kbd> + <kbd>Space</kbd> 进行切换中英文，即 Rime 只负责中文双拼输入，英文输入则由系统输入法来承担

**macOS** 下进入系统设置-键盘-输入法，点击编辑，点击左下角 `-` 删除 `ABC` 之外的输入法，点击 `+` 添加简体中文-鼠须管，点击完成，之后就只剩下【鼠须管】和 【ABC】输入法了

之后点击键盘快捷键，选择输入法，将【选择上一个输入法】设置设置为【<kbd>^</kbd><kbd>空格键</kbd>】（如果就是这个的话就无需修改）

**Win** 的话，由于更习惯 mac 的 <kbd>⌘</kbd> 键，所以直接使用 **PowerToys** 中键盘快捷键将 <kbd>Win</kbd> 和 <kbd>Ctrl</kbd> 键进行了调换，并且 Win 11 切换输入法语言的快捷键是  <kbd>Win</kbd> + <kbd>Space</kbd>，所以这样就和 mac 下统一了

![](https://cdn.wallleap.cn/img/pic/illustration/202303091431703.png)

注：win 下如果之前选择的是中文输入法的话，需要在设置-时间和语言-输入-语言和区域中添加英文，我这里添加的是 **English (United States)**，这样就会安装英文的输入法，之后再将其他输入法卸载掉，只保留【小狼毫】和【美式键盘】就可以了

## emoji 输入

具体的仓库是 [rime/rime-emoji](https://github.com/rime/rime-emoji)

**方式一**：直接按照 README 里的自动安装使用命令安装

**方式二**：

1. 下载仓库里的 `opencc` 文件夹，并放到【用户文件夹】下
2. 在拼音方案文件（`double_pinyin_flypy.schema.yaml`）里添加内容

```yaml
switches:
  # 其他内容（直接把下面的这个放到该字段最后 注意缩进）
  - name: emoji_suggestion
    reset: 0
    states: ["🈚️️", "🈶️"]
# 其他内容
emoji_suggestion:
  opencc_config: emoji.json
  option_name: emoji_suggestion
  tips: all
# 其他内容
engine:
  # 其他内容
  filters:
    - simplifier@emoji_suggestion
    #其他内容
```

需要使用的时候，按快捷键 <kbd>Ctrl</kbd> + <kbd>`</kbd>（Esc 下面那个按键）或者 <kbd>F4</kbd>，使用空格键、上下键调出选项，调到【🈚→🈶】按空格键确认转换

![](https://cdn.wallleap.cn/img/pic/illustration/202303100949837.png)

这样输入相应的文字的时候就可以出现 emoji 了

![](https://cdn.wallleap.cn/img/pic/illustration/202303091513765.png)

不过我还是喜欢通过快捷键直接调用系统自带的 emoji：

- Win 下 <kbd>Win</kbd> + <kbd>.</kbd> / <kbd>;</kbd>（如果和我一样该了键盘映射那么快捷键就是 <kbd>Ctrl</kbd> + <kbd>.</kbd> / <kbd>;</kbd>）
- macOS 下 <kbd>Command</kbd> + <kbd>Control</kbd> + <kbd>Space</kbd>）

![](https://cdn.wallleap.cn/img/pic/illustration/202303091446451.png)

## 模糊音

如果没有设置的话，那默认是没有模糊音的，也正是我需要的；但考虑到以后可能会用到，所以还是加上吧，在下载 [rime/symbols.yaml](https://github.com/loaden/rime/blob/master/symbols.yaml) 文件之后放到【用户文件夹】

接着在 `double_pinyin_flypy.schema.yaml` 文件中加入内容（只适用于小鹤双拼）

```yaml
speller:
  # 其他内容
  algebra:
    # 其他内容
    # 模糊音区域（依据个人情况修改注释）
    # 声母部分
    # - derive/^([z])h/$1/ # zh => z
    # - derive/^([z])([^h])/$1h$2/ # z => zh
    # - derive/^([c])h/$1/ # ch => c
    # - derive/^([c])([^h])/$1h$2/ # c => ch
    # - derive/^([s])h/$1/ # sh => s
    # - derive/^([s])([^h])/$1h$2/ # s => sh
    # - derive/^l/n/ # l => n
    # - derive/^n/l/ # n => l
    # - derive/^r/l/ # r => l
    # - derive/^r/y/ # r => y
    # - derive/^hu$/fu/ # hu => fu
    # - derive/^fu$/hu/ # fu => hu
    # 韵母部分
    # - derive/([^iu])([a])n$/$1$2ng/ # an => ang
    # - derive/([^iu])([a])ng$/$1$2n/ # ang => an
    # - derive/([e])n$/$1ng/ # en => eng
    # - derive/([e])ng$/$1n/ # eng => en
    # - derive/([i])n$/$1ng/ # in => ing
    # - derive/([i])ng$/$1n/ # ing => in
    # - derive/([i])an$/$1ang/ # ian => iang
    # - derive/([i])ang$/$1an/ # iang => ian # 由于小鹤双拼特性，无需 uang <=> iang
    # 其它模糊音
    #- derive/^hui$/fei/ # hui => fei
    #- derive/^fei$/hui/ # fei => hui
    #- derive/^huang$/wang/ # huang => wang
    #- derive/^wang$/huang/ # wang => huang
```

## 定义常用短语

在用户文件夹下新建文件 `custom_phrase.txt`

输入内容，每行由这些组成： `文字`、`短语`、`权重`，它们之间使用 `Tab` 制表符分隔，其中权重可以省略

例如：

```txt
JavaScript	js
React	react
Vue	vue	3
Vue 3	vue	2
Vue 2	vue	1
```

建议这个文件直接使用系统自动的文本编辑器编辑，且使用 UTF-8、LF 编码和回车（毕竟代码编辑器的 Tab 键可能设置成了空格）

这个文件编辑完成之后就可以到输入方案文件（`double_pinyin_flypy.schema.yaml`）里添加内容：

```yaml
engine:
  translators:
	# 把下面这条添加到这个字段下
    - table_translator@custom_phrase # 用户自定义词典
# 可以把下面的放到文件末尾
custom_phrase:
  dictionary: ""
  user_dict: custom_phrase
  db_class: stabledb
  enable_completion: false
  enable_sentence: true
  initial_quality: 1
```

保存重新部署之后，输入相应的短语就可以显示相应内容了，例如

![](https://cdn.wallleap.cn/img/pic/illustration/202303091606148.png)

## 导入自己的词库

Rime 输入法的词库是以 `.dict.yaml` 结尾的文件

我们在搜狗输入法里把自己的词库导出，应该是 `.bin` 文件，我们需要借助 [imewlconverter-v3.0.0](https://github.com/studyzy/imewlconverter/releases/tag/v3.0.0) 深蓝词库转换这个工具把它转成  Rime 支持的词库（这个版本是支持 Win 和 mac 的）

打开软件之后选择文件、需要转换成哪个软件的词库，然后点击转换，之后保存的时候输入文件名并选择存储位置

![](https://cdn.wallleap.cn/img/pic/illustration/202303091619237.png)

由于之后不仅仅只有这个词库，所以可以创建一个专门存放词库的文件夹例如 `dicts`

然后将刚刚保存的文件重命名为 `sougou_own.dict.yaml` 并在文件最上面加上描述内容

```yaml
# Rime dictionary
# encoding: utf-8

---
name: sougou_own
version: "1.0"
sort: by_weight
...

# 上面留个空行
```

然后把这个文件移动到 `dicts` 目录下

之后在用户文件夹下新建文件 `extended.dict.yaml`，并输入内容

```yaml
# Rime dictionary
# encoding: utf-8

---
name: extended
version: "2023.03.09"
sort: by_weight
vocabulary: essay-zh-hans
use_preset_vocabulary: true
import_tables:
  - dicts/sougou_own
  # 之后新增的词典都按这种写在这下面
...
```

接着修改输入方案文件（`double_pinyin_flypy.schema.yaml`）的这个字段：

```yaml
translator:
  dictionary: extended
```

## 输入符号

下载 [rime/symbols.yaml](https://github.com/loaden/rime/blob/master/symbols.yaml) 文件之后放到【用户文件夹】

接着修改 `double_pinyin_flypy.schema.yaml` 文件

```yaml
punctuator:
  import_preset: symbols
  full_shape:
  symbols:
    # 把常用的指令写到这，方便查看
    "/help": [ 符号：/fh, 单位：/dw, 标点：/bd, 数学：/sx, 拼音：/py, 星号：/xh, 方块：/fk, 几何：/jh, 箭头：/jt, 电脑：/dn, 罗马数字：/lm, 大写罗马数字：/lmd, 拉丁：/ld, 上标：/sb, 下标：/xb, 希腊字母：/xl, 大写希腊字母：/xld, 数字：/0到/9, 分数：/fs, いろは順：/iro, 假名：/jm或/pjm或/jmk到/jmo, 假名+圈：/jmq, 假名+半角：/jmbj, 俄语：/ey, 大写俄语：/eyd, 韩文：/hw, 韩文+圈：/hwq, 韩文+弧：/hwh, 结构：/jg, 偏旁：/pp, 康熙（部首）：/kx, 笔画：/bh, 注音：/zy, 声调：/sd, 汉字+圈：/hzq, 汉字+弧：/hzh, 数字+圈：/szq, 数字+弧：/szh, 数字+点：/szd, 字母+圈：/zmq, 字母+弧：/zmh, 表情：/bq, 音乐：/yy, 月份：/yf, 日期：/rq, 曜日：/yr, 时间：/sj, 天干：/tg, 地支：/dz, 干支：/gz, 节气：/jq, 象棋：/xq, 麻将：/mj, 色子：/sz, 扑克：/pk, 八卦：/bg, 八卦名：/bgm, 六十四卦：/lssg, 六十四卦名：/lssgm, 太玄经：/txj, 天体：/tt, 星座：/xz, 星座名：/xzm, 十二宫：/seg, 苏州码：/szm ]
  half_shape:
    "/": ["/", "÷"]
recognizer:
  patterns:
    # 添加下面这个
    punct: "^/([0-9]+[a-z]*|[a-z]+)$"
```

![](https://cdn.wallleap.cn/img/pic/illustration/202303091750855.png)

## 按键绑定

下载 [rime-prelude/key_bindings.yaml](https://github.com/rime/rime-prelude/blob/master/key_bindings.yaml) 文件后移动到用户文件夹，之后进行个性化配置

在 `default.custom.yaml` 或输入方案里设置都可以，我一般在全局里面配置

```yaml
patch:
  schema_list:
    - schema: double_pinyin_flypy
  menu/page_size: 4 # 候选项数
  "ascii_composer/good_old_caps_lock": false
  "ascii_composer/switch_key":
    Eisu_toggle: clear
    Shift_L: commit_code
    Shift_R: commit_code
  "key_binder/bindings":
    - {accept: "Control+j", send: Page_Down, when: composing}
    - {accept: "Control+k", send: Page_Up, when: composing}
    - {accept: Tab, send: Page_Down, when: composing}
    - {accept: "Shift+Tab", send: Page_Up, when: composing}
    - {accept: semicolon, send: 2, when: has_menu} # 分号
    - {accept: apostrophe, send: 3, when: has_menu} # 引号
    - {accept: comma, send: 4, when: has_menu} # 逗号
    - {accept: equal, send: Page_Down, when: composing}
    - {accept: minus, send: Page_Up, when: composing}
    - {accept: bracketleft, send: Page_Up, when: composing}
    - {accept: bracketright, send: Page_Down, when: composing}
```

这样输入完选词的时候：

- 上翻页：`[`、`Shift+Tab`、`-`、`Ctrl+k`
- 下翻页：`]`、`Tab`、等于号、`Ctrl+j`
- 选词：数字 `1-9`、空格、`;`、`"`、`,`

其他的可以看下这个：[按键设置](https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/Rime_description.md#%E5%85%AB%E5%85%B6%E5%AE%83)

## 动态输入时间

需要借助 lua 脚本实现，获取当前时间

新建文件夹 `lua` 之后还有脚本就放这里面

在目录 lua 下新建文件 `date_translator.lua`，输入内容

```lua
local function date_translator(input, seg)
    if (input == "date") then
        --- Candidate(type, start, end, text, comment)
        yield(Candidate("date", seg.start, seg._end, os.date("%Y-%m-%d"), ""))
        yield(Candidate("date", seg.start, seg._end, os.date("%Y年%m月%d日"), ""))
        yield(Candidate("date", seg.start, seg._end, os.date("%Y%m%d"), ""))
    end
    if (input == "time") then
        --- Candidate(type, start, end, text, comment)
        yield(Candidate("time", seg.start, seg._end, os.date("%H:%M:%S"), ""))
        yield(Candidate("time", seg.start, seg._end, os.date("%H时%M分%S秒"), ""))
        yield(Candidate("time", seg.start, seg._end, os.date("%H%M%S"), ""))
    end
    if (input == "datetime") then
        --- Candidate(type, start, end, text, comment)
        yield(Candidate("datetime", seg.start, seg._end, os.date("%Y-%m-%d %H:%M:%S"), ""))
        yield(Candidate("datetime", seg.start, seg._end, os.date("%Y%m%d%H%M"), ""))
    end
    if (input == "week") then
        local weekTab = {'日', '一', '二', '三', '四', '五', '六', '七'}
        yield(Candidate("week", seg.start, seg._end, "周" .. weekTab[tonumber(os.date("%w") + 1)], ""))
        yield(Candidate("week", seg.start, seg._end, "星期" .. weekTab[tonumber(os.date("%w") + 1)], ""))
        yield(Candidate("week", seg.start, seg._end, os.date("%A"), ""))
        yield(Candidate("week", seg.start, seg._end, os.date("%a"), ""))
        yield(Candidate("week", seg.start, seg._end, os.date("%W"), "周数"))
    end
    if (input == "month") then
        yield(Candidate("month", seg.start, seg._end, os.date("%B"), ""))
        yield(Candidate("month", seg.start, seg._end, os.date("%b"), ""))
    end
end
return date_translator
```

之后在【用户文件夹】下新建 `Rime.lua` 文件，将脚本导入

```lua
-- date_translator: 动态日期时间输入
-- 文件在 `lua/date_translator.lua`
date_translator = require("date_translator")
```

在 `double_pinyin_flypy.schema.yaml` 文件中添加

```yaml
engine:
  translators:
    # 添加下面字段
    - lua_translator@date_translator # 动态日期时间输入
```

更多脚本可以前往：[librime-lua](https://github.com/hchunhui/librime-lua/tree/master)

## 同步

需要修改 `installation.yaml` 文件

mac 上：

```yaml
installation_id: "rimemacsync"
sync_dir: '/Users/luwang/Library/Mobile Documents/com~apple~CloudDocs/Backup/Config/RimeSync'
```

win 上：

```yaml
installation_id: "rimewinsync"
sync_dir: 'C:\Users\luwang\iCloudDrive\Backup\Config\RimeSync'
```

设置 `id` 来区分来自不同的机器/系统的用户词典，会自动生成这个 `id` 值为文件夹的名字

设置 `dir` 为 iCloud 下同一目录，之后经常点击【用户资料同步】/【同步用户数据】就可以备份配置和输入习惯啦

> 同步时，依次將各子文件夾中的詞典快照合併到用戶詞典，最後爲合併後的用戶詞典生成一份新的快照文件。 另外，還會把用戶文件夾中非自動生成的 YAML 文件及 .txt 文件單向 備份 到同步文件夾。

---

> 使用体验：用这个输入法也有一段时间了，个人感觉 macOS 和 iOS 上使用体验完美，但是 win 上由于切换窗口会导致输入法失效，需要经常切换，使用体验相对而言没那么完美
