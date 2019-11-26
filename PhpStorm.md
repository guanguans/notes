# PhpStorm

## 相关链接

* [插件](http://plugins.jetbrains.com/phpstorm) - 官网插件。
* [注册](http://idea.lanyus.com/) - IntelliJ IDEA 注册码。

## 插件

* **[Symfony Plugin](https://plugins.jetbrains.com/plugin/7219-symfony-plugin)** - 支持 Symfony 2,3,4 ...
* **Laravel Plugin** - 支持 Laravel
* **.env files support** - 支持.env 文件
* **BashSupport** - 支持 Bash
* **EditorConfig** - 支持 EditorConfig 标准
* **Handlebars/Mustache** - 支持 Handlebars、Mustache
* **Ideolog** - 有好的插件 .log 文件
* **Material Theme UI** - Material Theme 主题
* **.ignore** - 友好的查看 .ignore 文件
* **NodeJS** - 集成 Node.js
* **Markdown support** - 支持 Markdown
* **IdeaVim** - 支持 Vim
* **LiveEdit** - 可以实时编辑 HTML/CSS/JavaScript
* **Markdown Navigator** - 支持 Markdown
* **PHP composer.json support** - 支持 composer.json 文件
* **Php Inspections (EA Extended)** - PHP 的静态代码分析工具
* **Nyan Progress Bar** - 改变进度条样式
* **Grep Console** - Grep 控制台
* **String Manipulation** - 有好的操作字符串
* **CodeGlance** - 类似于 Sublime 中的代码小地图
* **Styled Components** - 利用标记的模板文字和 CSS 的强大功能，样式化组件允许您编写实际的 CSS 代码来设置组件样式
* **Translation** - 最好用的翻译插件
* **Key promoter** - 这款插件适合新手使用。当你点击鼠标一个功能的时候，可以提示你这个功能快捷键是什么。这是一个非常有用的功能，很快就可以熟悉软件的快捷功能了。 如果有快捷键的，会直接显示快捷键
* **ApiDebugger** - 一个开源的接口调试插件
* **[SmartQQ](https://github.com/Jamling/SmartQQ4IntelliJ)** - QQ、Wechat
* **[PHP Annotations](https://github.com/Haehnchen/idea-php-annotation-plugin)** - PhpStorm 注释
* **[BrowseWordAtCaret](https://plugins.jetbrains.com/plugin/201-browsewordatcaret)** - 高亮选中的词语
* **[PhpStorm-Plugins](https://github.com/zgh-yuanshang/PhpStorm-Plugins)** - 排序 php 类中的 use 包
* **[leetcode-editor](https://github.com/shuzijun/leetcode-editor)** - leetcode
* **[SonarLint](https://plugins.jetbrains.com/plugin/7973-sonarlint)** - 综合检查代码质量，可持续集成
* **[Embedded Web Browser](https://plugins.jetbrains.com/plugin/12282-embedded-web-browser)** - 编辑器内使用 web 浏览器

## 优化 PhpStorm 速度

### Java VM options

PHPStorm 依赖 java 运行环境，说白了也就是 java 虚拟机，找到`help > Edit Custom VM Options`，然后在这个文件里可以根据需要增加或减少 PHPstorm 使用的内存

```plain
-Xms500m
-Xmx1500m

-Dawt.useSystemAAFontSettings=lcd
-Dawt.java2d.opengl=true

# 这一条只适合于Mac, 可以使java调用优化过的图形引擎
-Dapple.awt.graphics.UseQuartz=true
```

当然这里还有其他的一些设置，你可以网上搜搜别人都是怎么设置的，然后相应地自行探索

### 自定义 properties

进入`help > Edit Custom Properties`来设置 PHPStorm 的自定义属性.

```plain
editor.zero.latency.typing=true
```

上面这条，改变的是 PHPstorm 如何渲染字体：立即渲染文字，而不是先进行内容分析。可能会因此导致偶尔有那么一瞬间文字都是不带样式的，但是整体上会顺畅很多。

### Inspections and plugins（检查和插件）

PHPstorm 的一大问题就是太强大了，默认加了很多功能，而我们可能平时根本用不到。

找到`preferences -> plugins`，把我们根本用不到的很多插件`plugin`，禁用掉！

不要担心禁的太多，如果你勾掉一个插件的时候，它又被另外一个插件依赖，它会提示你的；而且，在特定的情境下，当 PHPstorm 觉得你应该启用一个插件的时候，它也会提示你的。

禁用不必要的插件是第一步，但是禁用代码检查（inspections），往往可能影响更大。找到`Settings > Editor > Inspections`，根据自己的情况看看哪些时候其实不需要实时的代码检查

### Language injection（其它语言的插入）

有一个插件其实特别影响性能，就是`IntelliLang`. 这个插件支持一种语言在其他的文件格式中也照样能被识别，比如说当你在一个 PHP 文件中插入 HTML，或者用到 HTML 的代码自动补齐或高亮显示功能时。

当然，并不建议完全禁用掉这个插件，但是呢，可能有些特定的语言插入支持，你并不会用到，这个时候你可以到`Settings > Editor > Language Injections`下，把当前项目里不可能用到的第三方语言插入，都勾掉。

### 排除对特定项目目录的索引

在 `Settings > Directories` 下可以将特定的目录标记排除，然后 PHPstorm 就不会索引其中的文件了。建议排除的目录一般是类似`cache`、`public`、`storage`等包含资源编译文件的，当然还有两个大头，就是`vendor` 和`node_modules`目录。

#### vendor 目录的问题

排除掉`vendor`目录，意味着就不能基于那里面的组件进行自动补全（auto-complete）了，所以这可能不是个好主意。但是呢，有个小技巧就是，你可以整体上排除掉`vendor`目录，然后在`Settings > Languages & Frameworks > PHP`下，将你真正用到的组件目录给额外添加上。

#### 关于 Node modules 目录

`Node modules`目录实际上默认已经被排除掉了，但是呢，在 `Settings > Languages & Frameworks > JavaScript > Libraries`下，你会看到，它们又被额外引入进来了，假设说你写 js 不是那么多，你也可以在这里将其完全排除掉。当然这些呢，都是基于项目的，你可以在不同的项目作不同的选择。

### 删除之前版本的 phpstorm 缓存文件夹

经常，每次你更新了 PHPstorm，它就会创建一个新的 cache 文件，而不会自动删除你上一个版本的 cache 文件夹，这往往会占用大量的系统盘空间，如果你用了某一个版本的 PHPstorm 很长时间，这个文件夹一般都是好几 GB。

在 Mac 上，你可以查找类似`‘PhpStorm2016.x’`或`~/Library/Caches`的文件夹，然后删除它；

在 windows 上，在你的当前用户目录查找类似`.WebIde`的文件夹，将多出来的删掉。

### phpstorm 不断重新索引（re-index）的问题

在新近版本的 PS 上，这里一般指 2018 以后的版本，你可能会发现 PS 老是自动地不断重新索引，在右下角会出现 indexing 的状态条，导致你编辑文件的操作很容易被打断，或者说 PS 的各种方便的提示、补全功能会因此而暂停，遇到这个问题，可以尝试如下解决：

* 重建缓存： `File > Invalidate Caches/Restart`, 也即重新生成缓存，然后重启，一般此问题会解决
* 如果第一步没解决问题，那么到 plugin 中禁用掉`.ignore`插件，该插件存在的 bug 也会导致此问题，重启后观察解决情况

## 快捷键（Win/Linux/Mac）

下面的 ~ 符号记得改成 \`，markdown 语法会转义。使用频率是我自己为准。仅供参考

### Mac 符号

| 符号 | 解释 |
| --- | --- |
| ⌘ | Command |
| ⇧ | Shift |
| ⌃ | Control |
| ↩ | Enter/Return |
| ⌥ | Option / Alt |

### 编辑

| Win / Linux | Mac | 注释 | 使用频率 |
| --- | --- | --- | --- |
| Ctrl + Space | ⌃Space | 代码自动完成（一般与输入法冲突） | ★☆☆☆☆ |
| Ctrl + Shift + Enter | ⌘ ⇧ ↩ | 智能完善代码（如: if()） | ★☆☆☆☆ |
| Ctrl + P | ⌘P | 方法参数提示，显示默认参数 | ★☆☆☆☆ |
| Ctrl + Q | ⌃J | 显示注释代码 | ★☆☆☆☆ |
| Ctrl + mouse over code | ⌘+mouse over code | 查看到简短的函数介绍 | ★★★☆☆ |
| Ctrl + F1 | ⌘F1 | 显示错误或警告信息的描述（需要把光标放到错误或警告位置） | ★☆☆☆☆ |
| Alt + Insert | ⌘N,⌃↩,⌃N | 生成代码段（ 包括函数或类注释，版权信息，构造方法，抽象方法等） | ★★★★☆ |
| Ctrl + O | ⌃O | 插入覆盖父类的方法 | ★☆☆☆☆ |
| Ctrl + I | ⌃I | 实现抽象方法 | ★☆☆☆☆ |
| Ctrl + Alt + T | ⌘⌥T | 选中的代码放在 if..else..、for、foreach 里, 或者函数里，或者为选中的代码块添加区域解释（可以折叠该段代码，折叠后只显示解释，便于代码管理） | ★☆☆☆☆ |
| Ctrl + / | ⌘/ | 以添加 “//” 的方式添加注释 | ★★★★☆ |
| Ctrl + Shift + / | ⌘⌥/ | 添加 “/**/” 的方式添加注释 | ★★★★☆ |
| Ctrl + W | ⌥↑ | 增量式的选中当前块 | ★★☆☆☆ |
| Ctrl + Shift + W | ⌥↓ | 与 Ctrl + W 对应，减小选中范围 | ★★☆☆☆ |
| Alt + Q | ⌃⇧Q | 显示包含光标所在位置的标签头 | ★☆☆☆☆ |
| Alt + Enter | ⌥↩ | 显示意图行动。 Show Intention Action | ★★☆☆☆ |
| Ctrl + Alt + L | ⌘⌥L | 格式化代码 | ★★☆☆☆ |
| Ctrl + Alt + I | ⌃⌥I | 自动缩进。 | ★★★☆☆ |
| Tab / Shift + Tab | tab,⇧+tab | 手动缩进 / 反向缩进 | ★★★★★ |
| Ctrl + X or Shift + Delete | ⌘X | 剪切 | ★★★★★ |
| Ctrl + C or Ctrl + Insert | ⌘C | 复制 | ★★★★★ |
| Ctrl + V or Shift + Insert | ⌘V | 粘贴 | ★★★★★ |
| Ctrl + Shift + V | ⌘⇧V | 从粘贴板中选择内容进行粘贴 | ★★★☆☆ |
| Ctrl + D | ⌘D | 将当前行或者选择的内容复制到下一行或光标处 | ★★★☆☆ |
| Ctrl + Y | ⌘del | 删除光标所在的行 | ★★★☆☆ |
| Ctrl + Shift + J | ⌃⇧J | 合成选中代码到一行。格式化代码的反向动作 | ★☆☆☆☆ |
| Ctrl + Enter | ⌘↩ | 智能线分割 | ★★☆☆☆ |
| Shift + Enter | ⇧↩ | 另起一新行。无论光标在行的那个位置 | ★★☆☆☆ |
| Ctrl + Shift + U | ⌘⇧U | 字符大小写切换 | ★★☆☆☆ |
| Ctrl + Shift + ] / [ | ⌘⇧],⌘⇧[ | 以区块为单位，从光标处 向后 / 向前 选择，再次点击增加选择范围 | ★☆☆☆☆ |
| Ctrl + Delete | ⌥ + del | 删除光标之后的部分单词 | ★★★★☆ |
| Ctrl + Backspace | ⌥ + Backspace | 删除光标之前的部分单词 | ★★★★☆ |
| Ctrl + +/- | ⌘ +,- | 折叠 / 打开代码块，再次点击扩大折叠 / 打开范围 | ★★★★☆ |
| Ctrl + Shift +  + | ⌘ ⇧+ | 打开全部 | ★★☆☆☆ |
| Ctrl + Shift +  - | ⌘ ⇧- | 折叠全部 | ★★☆☆☆ |
| Ctrl + F4 | ⌘W | 关闭当前页面 | ★★★☆☆ |

### 搜索 / 替换

| Win / Linux | Mac | 注释 | 使用频率 |
| --- | --- | --- | --- |
| Ctrl + F | ⌘F | 查找 | ★★★★★ |
| F3 | ⌘G | 查找下一个，结合查找使用 | ★★☆☆☆ |
| Shift + F3 | ⌘⇧G | 查找前一个，结合查找使用 | ★★☆☆☆ |
| Ctrl + R | ⌘R | 替换 | ★★★★★ |
| Ctrl + Shift + F | ⌘⇧F | 在文件中查找 | ★★☆☆☆ |
| Ctrl + Shift + R | ⌘⇧R | 在文件中替换 | ★★☆☆☆ |

### 被使用搜索

| Win / Linux | Mac | 注释 | 使用频率 |
| --- | --- | --- | --- |
| Alt + F7 / Ctrl + F7 | ⌥F7/⌘F7 | 全项目被使用查找 / 当前文件声明变量处 | ★☆☆☆☆ |
| Ctrl + Shift + F7 | ⌘⇧F7 | 在文件中变量或函数被使用处高亮 | ★☆☆☆☆ |
| Ctrl + Alt + F7 | ⌘⌥F7 | 显示详细被使用的位置列表 | ★☆☆☆☆ |

### 项目运行

| Win / Linux | Mac | 注释 | 使用频率 |
| --- | --- | --- | --- |
| Alt + Shift + F10 | ⌃⌥R | 选择配置并运行 | ★☆☆☆☆ |
| Alt + Shift + F9 | ⌃⌥D | 选择配置并 debug | ★☆☆☆☆ |
| Shift + F10 | ⌃R | 运行 | ★☆☆☆☆ |
| Shift + F9 | ⌃D | debug | ★☆☆☆☆ |
| Ctrl + Shift + F10 | ⌃⇧R,⌃⇧D | 运行上次运行的配置 | ★☆☆☆☆ |
| Ctrl + Shift + X | ⌘⇧X | 运行命令行 | ★☆☆☆☆ |

### debug 相关（在 debug 的时候使用）

| Win / Linux | Mac | 注释 | 使用频率 |
| --- | --- | --- | --- |
| F8 | F8 | 步过。继续执行断点后程序，按行执行，按一次执行一行 | ★☆☆☆☆ |
| F7 | F7 | 步进。进入到断点执行的内容程序 | ★☆☆☆☆ |
| Shift + F7 | ⇧F7 | 智能进入 | ★☆☆☆☆ |
| Shift + F8 | ⇧F8 | 步骤 | ★☆☆☆☆ |
| ALT + F9 | ⌥F9 | 运行到光标 | ★☆☆☆☆ |
| ALT + F8 | ⌥F8 | 计算表达式 | ★☆☆☆☆ |
| F9 | ⌘⌥R | 继续执行断点以后的程序，停到下一个断点处 | ★☆☆☆☆ |
| Ctrl + F8 | ⌘F8 | 为光标所在行打上断点 | ★☆☆☆☆ |
| Ctrl+Shift+F8 | ⌘⇧F8 | 浏览断点 | ★☆☆☆☆ |

### 导航相关

| Win / Linux | Mac | 注释 | 使用频率 |
| --- | --- | --- | --- |
| Ctrl + N | ⌘O | 搜索类。全项目范围 | ★☆☆☆☆ |
| Ctrl + Shift + N | ⌘⇧O | 根据文件名搜索文件。全项目范围 | ★★★★☆ |
| Ctrl + Alt + Shift + N | ⌘⌥O | 搜索函数。全项目范围 | ★★★★☆ |
| Alt + Right/Left | ⌃←,⌃→ | 左右切换打开的文件 | ★★★☆☆ |
| F12 | F12 | 放回上次打开的工具窗口 | ★☆☆☆☆ |
| Esc | Esc | 返回编辑器界面 | ★☆☆☆☆ |
| Shift+ Esc | ⇧ + Esc | 光标返回编辑框, 关闭无用的窗口 | ★☆☆☆☆ |
| Ctrl+ Shift + F4 | ⌘⇧F4 | 关闭活动运行 / 消息 / / ... 选项卡 | ★☆☆☆☆ |
| Ctrl + G | ⌘L | 按行号快速定位 | ★★★☆☆ |
| Ctrl + E | ⌘E | 打开最近打开过的文件列表 | ★★★★☆ |
| Ctrl + Alt + Left/Right | ⌘⌥←,⌘⌥→ | 返回 / 前进到上次导航操作 | ★☆☆☆☆ |
| Ctrl + Shift + Backspace | ⌘⇧ + Backspace | 返回到上次编辑的位置 | ★☆☆☆☆ |
| Alt + F1 | ⌥F1 | 调出目标窗口 | ★☆☆☆☆ |
| Ctrl + B or Ctrl + Click | ⌘B or ⌘ Click | 跳转到函数的声明处 | ★★★★★ |
| Ctrl + Alt + B | ⌘⌥B | 到实施（S） | ★☆☆☆☆ |
| Ctrl + Shift + I | ⌥Space,⌘Y | 打开快速定义查询 | ★☆☆☆☆ |
| Ctrl + Shift + B | ⌃⇧B | 找变量的 类 | ★☆☆☆☆ |
| Ctrl + U | ⌘U | 转到 super-method/super-class | ★☆☆☆☆ |
| Alt + Up/Down | ⌃↑,⌃↓ | 上下切换函数 | ★★★☆☆ |
| Ctrl + ] / [ | ⌘],⌘[ | 定位到右 / 左侧最近的大括号处。连续点击扩大范围 | ★☆☆☆☆ |
| Ctrl + F12 | ⌘F12 | 打开文件结构的弹出窗 | ★☆☆☆☆ |
| Ctrl + H | ⌃H | 浏览选定类的层次结构 | ★☆☆☆☆ |
| F2 / Shift + F2 | F2,⇧F2 | 下 / 上高亮错误或警告快速定位 | ★☆☆☆☆ |
| F4 / Ctrl + Enter | F4/⌘↓ | 查找变量来源 | ★☆☆☆☆ |
| Alt + Home | ⌥ Home | 组合显示导航栏 | ★☆☆☆☆ |
| F11 | F3 | 切换书签 | ★★★★☆ |
| Ctrl + F11 | ⌥F3 | 切换书签助记符 | ★★★★☆ |
| Ctrl + #[0-9] | ⌃0...⌃9 | 转到编号书签 | ★☆☆☆☆ |
| Shift + F11 | ⌘F3 | 显示书签 | ★★★☆☆ |

### 重构相关

| Win / Linux | Mac | 注释 | 使用频率 |
| --- | --- | --- | --- |
| F5 | F5 | 复制文件 | ★★★☆☆ |
| F6 | F6 | 移动文件 | ★★★☆☆ |
| Alt + Delete | ⌘ Del | 安全删除 | ★☆☆☆☆ |
| Shift + F6 | ⇧F6 | 为所选文件重命名 | ★★★☆☆ |
| Ctrl + Alt + N | ⌘⌥N | 内联变量 | ★☆☆☆☆ |
| Ctrl + Alt + M | ⌘⌥M | 引入方法 | ★☆☆☆☆ |
| Ctrl + Alt + V | ⌘⌥V | 引入变量 | ★☆☆☆☆ |
| Ctrl + Alt + F | ⌘⌥F | 类似引入变量 | ★☆☆☆☆ |
| Ctrl + Alt + C | ⌘⌥C | 引入常量 | ★☆☆☆☆ |

### 版本控制 / 本地历史记录

| Win / Linux | Mac | 注释 | 使用频率 |
| --- | --- | --- | --- |
| Alt + ~ | ⌃V | 打开版本操作控制台 | ★☆☆☆☆ |
| Ctrl + K | ⌘K | 提交代码 | ★★★★★ |
| Ctrl + T | ⌘T | 更新代码到本地 | ★★★★★ |
| Alt + Shift + C | ⌥⇧C | 浏览最近更改记录 | ★☆☆☆☆ |

### 普通操作

| Win / Linux | Mac | 注释 | 使用频率 |
| --- | --- | --- | --- |
| Ctrl + Shift + A | ⌘⇧A | 查找操作 | ★★★★★ |
| Alt + #[0-9] | ⌘0...⌘9 | 打开对应的工具窗口 | ★☆☆☆☆ |
| Ctrl + Shift + F12 | ⌘⇧F12 | 编辑区窗口最大化 | ★★★☆☆ |
| Alt + Shift + F | ⌥⇧F | 添加到搜藏 | ★☆☆☆☆ |
| Alt + Shift + I | ⌥⇧I | 检查当前文件 | ★☆☆☆☆ |
| Ctrl + ~ | ⌃~ | 快速切换主题 | ★☆☆☆☆ |
| Ctrl + Alt + S | ⌘, | 打开设置窗口 | ★☆☆☆☆ |
| Ctrl + Tab | ⌃+Tab | 切换活动文件 | ★★★★★ |
