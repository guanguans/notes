# macOS

## [使我的 macOS 体验更加惊人的应用程序和工具列表](https://github.com/nikitavoloboev/my-mac-os)

## [在 macOS 上安装开发环境](https://github.com/sb2nov/mac-setup)

## [我的 macOS 配置文件](https://github.com/nikitavoloboev/dotfiles)

## 命令行增强

过去这些年我的命令行本领在逐步加强，我经常会去搜寻工作中能用的更好的命令行工具。下面就是我现在使用的用于增强原有命令行工具的列表。

### 怎么忽略我所做的命令行增强

通常情况下我会用别名将新的增强的命令行工具覆盖原来的命令（如 `cat` 和 `ping`）。

如果我需要运行原来的命令的话（有时我确实需要这么做），我会像下面这样来运行未加修改的原始命令。（我用的是 Mac，你的用法可能不一样）

``` bash
$ \cat # 忽略叫 "cat" 的别名 - 具体解释: https://stackoverflow.com/a/16506263/22617
$ command cat # 忽略函数和别名
```

### bat > cat

`cat` 用于打印文件的内容，如果你平时用命令行很多的话，例如语法高亮之类的功能会非常有用。我首先发现了 [ccat](https://github.com/jingweno/ccat)[1] 这个有语法高亮功能的工具，然后我发现了 [bat](https://github.com/sharkdp/bat)[2]，它的功能有语法高亮、分页、行号和 git 集成。

`bat` 命令也能让我在（多于一屏的）输出里使用 `/` 搜索（和用 `less` 搜索功能一样）。

![](https://dn-linuxcn.qbox.me/data/attachment/album/201810/29/204653xppy14y8y4zu6h7s.gif)

_Sample bat output_

我将别名 `cat` 指到了 `bat` 命令：

``` bash
alias cat='bat'
```

*   [安装指引](https://github.com/sharkdp/bat) [3]

### prettyping > ping

`ping` 非常有用，当我碰到 “糟了，是不是 X 挂了？/ 我的网不通了？” 这种情况下我最先想到的工具就是它了。但是 `prettyping`（“prettyping” 可不是指 “pre typing”）在 `ping` 的基础上加了友好的输出，这可让我感觉命令行友好了很多呢。

![](https://dn-linuxcn.qbox.me/data/attachment/album/201810/29/204655zcznq3x70xjexzv3.gif)

_Sample ping output_

我也将 `ping` 用别名链接到了 `prettyping` 命令：

``` bash
alias ping='prettyping --nolegend'
```

*   [安装指引](http://denilson.sa.nom.br/prettyping/) [4]

### fzf > ctrl+r

在终端里，使用 `ctrl+r` 将允许你在命令历史里[反向搜索](https://lifehacker.com/278888/ctrl%252Br-to-search-and-other-terminal-history-tricks) [5] 使用过的命令，这是个挺好的小技巧，尽管它有点麻烦。

`fzf` 这个工具相比于 `ctrl+r` 有了**巨大的**进步。它能针对命令行历史进行模糊查询，并且提供了对可能的合格结果进行全面交互式预览。

> 此处应有视频，地址： [https://dn-linuxcn.qbox.me/static/video/cli%20-%20fuzzy-history-217497007.mp4](https://dn-linuxcn.qbox.me/static/video/cli%20-%20fuzzy-history-217497007.mp4)[](https://dn-linuxcn.qbox.me/static/video/cli%20-%20fuzzy-history-217497007.mp4)[6]

除了搜索命令历史，`fzf` 还能预览和打开文件，我在下面的视频里展示了这些功能。

> 此处应有视频，地址： [https://dn-linuxcn.qbox.me/static/video/cli%20-%20fuzzy%20enhanced-286345188.mp4](https://dn-linuxcn.qbox.me/static/video/cli%20-%20fuzzy%20enhanced-286345188.mp4)[](https://dn-linuxcn.qbox.me/static/video/cli%20-%20fuzzy%20enhanced-286345188.mp4)[7]

为了这个预览的效果，我创建了一个叫 `preview` 的别名，它将 `fzf` 和前文提到的 `bat` 组合起来完成预览功能，还给上面绑定了一个定制的热键 `ctrl+o` 来打开 VS Code：

``` bash
alias preview="fzf --preview 'bat --color \"always\" {}'"
# 支持在 VS Code 里用 ctrl+o 来打开选择的文件
export FZF_DEFAULT_OPTS="--bind='ctrl-o:execute(code {})+abort'"
```

*   [安装指引](https://github.com/junegunn/fzf) [8]

### htop > top

`top` 是当我想快速诊断为什么机器上的 CPU 跑的那么累或者风扇为什么突然呼呼大做的时候首先会想到的工具。我在生产环境也会使用这个工具。讨厌的是 Mac 上的 `top` 和 Linux 上的 `top` 有着极大的不同（恕我直言，应该是差的多）。

不过，`htop` 是对 Linux 上的 `top` 和 Mac 上蹩脚的 `top` 的极大改进。它增加了包括颜色输出，键盘热键绑定以及不同的视图输出，这对理解进程之间的父子关系有极大帮助。

一些很容易上手的热键：

*   `P` —— 按 CPU 使用率排序
*   `M` —— 按内存使用排序
*   `F4` —— 用字符串过滤进程（例如只看包括 node 的进程）
*   `space` —— 锚定一个单独进程，这样我能观察它是否有尖峰状态

![](https://dn-linuxcn.qbox.me/data/attachment/album/201810/29/204657hnfne1peg857gtdq.jpg)

_Sample htop output_

在 Mac Sierra 上 htop 有个奇怪的 bug，不过这个 bug 可以通过以 root 运行来绕过（我实在记不清这个 bug 是什么，但是这个别名能搞定它，有点讨厌的是我得每次都输入 root 密码。）：

``` bash
alias top="sudo htop" # 给 top 加上别名并且绕过 Sierra 上的 bug
```

*   [安装指引](http://hisham.hm/htop/) [9]

### diff-so-fancy > diff

我非常确定我是几年前从 Paul Irish 那儿学来的这个技巧，尽管我很少直接使用 `diff`，但我的 git 命令行会一直使用 `diff`。`diff-so-fancy` 给了我代码语法颜色和更改字符高亮的功能。

![](https://dn-linuxcn.qbox.me/data/attachment/album/201810/29/204658r8zajeo2b98ase4b.jpg)

_Sample diff output_

在我的 `~/.gitconfig` 文件里我用了下面的选项来打开 `git diff` 和 `git show` 的 `diff-so-fancy` 功能。

``` bash
[pager]
    diff = diff-so-fancy | less --tabs=1,5 -RFX
    show = diff-so-fancy | less --tabs=1,5 -RFX
```

*   [安装指引](https://github.com/so-fancy/diff-so-fancy) [10]

### fd > find

尽管我使用 Mac，但我绝不是 Spotlight 的粉丝，我觉得它的性能很差，关键字也难记，加上更新它自己的数据库时会拖慢 CPU，简直一无是处。我经常使用 [Alfred](https://www.alfredapp.com/)[11]，但是它的搜索功能也不是很好。

我倾向于在命令行中搜索文件，但是 `find` 的难用在于很难去记住那些合适的表达式来描述我想要的文件。（而且 Mac 上的 `find` 命令和非 Mac 的 `find` 命令还有些许不同，这更加深了我的失望。）

`fd` 是一个很好的替代品（它的作者和 `bat` 的作者是同一个人）。它非常快而且对于我经常要搜索的命令非常好记。

几个上手的例子：

``` bash
$ fd cli # 所有包含 "cli" 的文件名
$ fd -e md # 所有以 .md 作为扩展名的文件
$ fd cli -x wc -w # 搜索 "cli" 并且在每个搜索结果上运行 `wc -w`
```

![](https://dn-linuxcn.qbox.me/data/attachment/album/201810/29/204700varcm94gce19m91g.png)

_Sample fd output_

*   [安装指引](https://github.com/sharkdp/fd/) [12]

### ncdu > du

对我来说，知道当前磁盘空间被什么占用了非常重要。我用过 Mac 上的 [DaisyDisk](https://daisydiskapp.com/)[13]，但是我觉得那个程序产生结果有点慢。

`du -sh` 命令是我经常会运行的命令（`-sh` 是指结果以 “汇总” 和“人类可读”的方式显示），我经常会想要深入挖掘那些占用了大量磁盘空间的目录，看看到底是什么在占用空间。

`ncdu` 是一个非常棒的替代品。它提供了一个交互式的界面并且允许快速的扫描那些占用了大量磁盘空间的目录和文件，它又快又准。（尽管不管在哪个工具的情况下，扫描我的 home 目录都要很长时间，它有 550G）

一旦当我找到一个目录我想要 “处理” 一下（如删除，移动或压缩文件），我会使用 `cmd` + 点击 [iTerm2](https://www.iterm2.com/)[14] 顶部的目录名字的方法在 Finder 中打开它。

![](https://dn-linuxcn.qbox.me/data/attachment/album/201810/29/204701qk3aaia5w0z9505o.png)

_Sample ncdu output_

还有另外[一个叫 nnn 的替代选择](https://github.com/jarun/nnn) [15]，它提供了一个更漂亮的界面，它也提供文件尺寸和使用情况，实际上它更像一个全功能的文件管理器。

我的 `du` 是如下的别名：

``` bash
alias du="ncdu --color dark -rr -x --exclude .git --exclude node_modules"
```

选项说明：

*   `--color dark` 使用颜色方案
*   `-rr` 只读模式（防止误删和运行新的 shell 程序）
*   `--exclude` 忽略不想操作的目录

*   [安装指引](https://dev.yorhel.nl/ncdu) [16]

### tldr > man

几乎所有的命令行工具都有一个相伴的手册，它可以被 `man <命令名>` 来调出，但是在 `man` 的输出里找到东西可有点让人困惑，而且在一个包含了所有的技术细节的输出里找东西也挺可怕的。

这就是 TL;DR 项目（LCTT 译注：英文里 “文档太长，没空去读” 的缩写）创建的初衷。这是一个由社区驱动的文档系统，而且可以用在命令行上。就我现在使用的经验，我还没碰到过一个命令没有它相应的文档，你[也可以做贡献](https://github.com/tldr-pages/tldr#contributing) [17]。

![](https://dn-linuxcn.qbox.me/data/attachment/album/201810/29/204703q98ze88c128p93ip.png)

_Sample tldr output for fd_

一个小技巧，我将 `tldr` 的别名链接到 `help`（这样输入会快一点……）

``` bash
alias help='tldr'
```

*   [安装指引](http://tldr-pages.github.io/) [18]

### ack || ag > grep

`grep` 毫无疑问是一个强力的命令行工具，但是这些年来它已经被一些工具超越了，其中两个叫 `ack` 和 `ag`。

我个人对 `ack` 和 `ag` 都尝试过，而且没有非常明显的个人偏好，（也就是说它们都很棒，并且很相似）。我倾向于默认只使用 `ack`，因为这三个字符就在指尖，很好打。并且 `ack` 有大量的 `ack --bar` 参数可以使用！（你一定会体会到这一点。）

`ack` 和 `ag` 默认都使用正则表达式来搜索，这非常契合我的工作，我能使用类似于 `--js` 或 `--html` 这种标识指定文件类型搜索。（尽管 `ag` 比 `ack` 在文件类型过滤器里包括了更多的文件类型。）

两个工具都支持常见的 `grep` 选项，如 `-B` 和 `-A` 用于在搜索的上下文里指代 “之前” 和“之后”。

![](https://dn-linuxcn.qbox.me/data/attachment/album/201810/29/204704c433kka72aki0kk7.png)

_Sample ack output with grep args_

因为 `ack` 不支持 markdown（而我又恰好写了很多 markdown），我在我的 `~/.ackrc` 文件里加了以下定制语句：

``` bash
--type-set=md=.md,.mkd,.markdown
--pager=less -FRX
```

*   安装指引：[ack](https://beyondgrep.com)[19]，[ag](https://github.com/ggreer/the_silver_searcher)[20]
*   [关于 ack & ag 的更多信息](http://conqueringthecommandline.com/book/ack_ag) [21]

### jq > grep 及其它

我是 [jq](https://stedolan.github.io/jq)[22] 的忠实粉丝之一。当然一开始我也在它的语法里苦苦挣扎，好在我对查询语言还算有些使用心得，现在我对 `jq` 可以说是每天都要用。（不过从前我要么使用 `grep` 或者使用一个叫 [json](http://trentm.com/json/)[23] 的工具，相比而言后者的功能就非常基础了。）

我甚至开始撰写一个 `jq` 的教程系列（有 2500 字并且还在增加），我还发布了一个[网页工具](https://jqterm.com) [24] 和一个 Mac 上的应用（这个还没有发布。）

`jq` 允许我传入一个 JSON 并且能非常简单的将其转变为一个使用 JSON 格式的结果，这正是我想要的。下面这个例子允许我用一个命令更新我的所有 node 依赖。（为了阅读方便，我将其分成为多行。）

``` bash
$ npm i $(echo $(\
    npm outdated --json | \
    jq -r 'to_entries | .[] | "\(.key)@\(.value.latest)"' \
))
```

上面的命令将使用 npm 的 JSON 输出格式来列出所有过期的 node 依赖，然后将下面的源 JSON 转换为：

``` json
{
    "node-jq": {
        "current": "0.7.0",
        "wanted": "0.7.0",
        "latest": "1.2.0",
        "location": "node_modules/node-jq"
    },
        "uuid": {
        "current": "3.1.0",
        "wanted": "3.2.1",
        "latest": "3.2.1",
        "location": "node_modules/uuid"
    }
}
```

转换结果为：

``` bash
node-jq@1.2.0
uuid@3.2.1
```

上面的结果会被作为 `npm install` 的输入，你瞧，我的升级就这样全部搞定了。（当然，这里有点小题大做了。）

### 很荣幸提及一些其它的工具

我也在开始尝试一些别的工具，但我还没有完全掌握它们。（除了 `ponysay`，当我打开一个新的终端会话时，它就会出现。）

*   [ponysay](https://github.com/erkin/ponysay)[25] > `cowsay`
*   [csvkit](https://csvkit.readthedocs.io/en/1.0.3/)[26] > `awk 及其它`
*   [noti](https://github.com/variadico/noti)[27] > `display notification`
*   [entr](http://www.entrproject.org/)[28] > `watch`

### Mac 上怎么调节 Launchpad(启动台) 的图标大小，基本就是三行终端命令

``` bash
# 先调整每列显示多少个
$ defaults write com.apple.dock springboard-rows -int 6

# 再调整每行显示多少个
$ defaults write com.apple.dock springboard-columns -int 11

# 重置一下
$ defaults write com.apple.dock ResetLaunchPad -bool TRUE;killall Dock
```

### 原文链接

* [https://linux.cn/article-10171-1.html?utm_source=rss&utm_medium=rss](https://linux.cn/article-10171-1.html?utm_source=rss&utm_medium=rss)
