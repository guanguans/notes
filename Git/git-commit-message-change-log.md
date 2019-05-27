# git commit message 和 Change log

## Commit message 的格式

每次提交，Commit message 都包括三个部分：Header，Body 和 Footer。

```plain
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
```

其中，`Header` 是必需的，`Body` 和 `Footer` 可以省略。
不管是哪一个部分，任何一行都不得超过 _72_ 个字符（或 _100_ 个字符）。这是为了避免自动换行影响美观。

### Header

Header 部分只有一行，包括三个字段：`type`（必需）、`scope`（可选）和`subject`（必需）。

*   **`type`**

`type`用于说明`commit`的类别，只允许使用下面 7 个标识。

> 1.  `feat` 新功能（feature）
> 2.  `fix` 修补 bug
> 3.  `docs` 文档（documentation）
> 4.  `style` 格式（不影响代码运行的变动）
> 5.  `ref` 重构（即不是新增功能，也不是修改 bug 的代码变动）
> 6.  `test` 增加测试
> 7.  `chore` 构建过程或辅助工具的变动

如果`type`为`feat`和`fix`，则该`commit`将肯定出现在`Change log`之中。其他情况（`docs`、`chore`、`style`、`refactor`、`test`）由你决定，要不要放入`Change log`，**建议是不要**。

*   **`scope`** `scope`用于说明`commit`影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

*   **`subject`** `subject`是`commit`目的的简短描述，不超过 _50_ 个字符。

> 1.  以动词开头，使用第一人称现在时，比如`change`，而不是 ~~`changed`~~或 ~~`changes`~~
>
>
> 2.  第一个字母小写
>
>
> 3.  结尾不加句号（.）

### Body

Body 部分是对本次 commit 的详细描述，可以分成多行。下面是一个范例。

```plain
More detailed explanatory text, if necessary.  Wrap it to
about 72 characters or so.

Further paragraphs come after blank lines.

- Bullet points are okay, too
- Use a hanging indent
```

有两个注意点。

> 1.  使用第一人称现在时，比如使用`change`而不是 ~~`changed`~~或 ~~`changes`~~
> 2.  应该说明代码变动的动机，以及与以前行为的对比

### Footer

Footer 部分只用于两种情况。

*   不兼容变动
    如果当前代码与上一个版本不兼容，则`Footer`部分以`BREAKING CHANGE`开头，后面是对变动的描述、以及变动理由和迁移方法。

```plain
BREAKING CHANGE: isolate scope bindings definition has changed.

    To migrate the code follow the example below:

    Before:

    scope: {
      myAttr: 'attribute',
    }

    After:

    scope: {
      myAttr: '@',
    }

    The removed `inject` wasn't generaly useful for directives so there should be no code using it.
```

*   关闭 Issue

如果当前`commit`针对某个`issue`，那么可以在`Footer`部分关闭这个`issue`。

```plain
Closes #234
```

也可以一次关闭多个 issue 。

```plain
Closes #123, #245, #992
```

### Revert

还有一种特殊情况，如果当前`commit`用于撤销以前的`commit`，则必须以**`revert:`**开头，后面跟着被撤销`Commit`的`Header`。

```plain
revert: feat(pencil): add 'graphiteWidth' option

This reverts commit 667ecc1654a317a13331b17617d973392f415f02.
```

`Body`部分的格式是固定的，必须写成`This reverts commit <hash>`，其中的`hash`是被撤销`commit`的`SHA`标识符。

如果当前`commit`与被撤销的`commit`，在同一个发布（`release`）里面，那么它们都不会出现在`Change log`里面。如果两者在不同的发布，那么当前`commit`，会出现在 `Change log`的`Reverts`小标题下面。

## Commitizen

[Commitizen](https://link.jianshu.com?t=https://github.com/commitizen/cz-cli) 是一个撰写合格`Commit message`的工具。

安装命令如下。(_遇到缺少 package.json 文件的解决办法在文章最后_)

```plain
$ npm install -g commitizen
```

```plain
$ npm install -g cz-conventional-changelog
```

```plain
echo '{ "path": "cz-conventional-changelog" }' > ~/.czrc
```

以后，凡是用到`git commit`命令，一律改为使用`git cz`。这时，就会出现选项，用来生成符合格式的`Commit message`。

## 生成 Change log

如果你的所有`Commit`都符合`Angular`格式，那么发布新版本时，`Change log`就可以用脚本自动生成（例 1:[karma/CHANGELOG.md](https://link.jianshu.com?t=https://github.com/karma-runner/karma/blob/master/CHANGELOG.md), 例 2:[btford/grunt-conventional-changelog](https://link.jianshu.com?t=https://github.com/btford/grunt-conventional-changelog/blob/master/CHANGELOG.md)）。

生成的文档包括以下三个部分。

> *   New features
> *   Bug fixes
> *   Breaking changes

每个部分都会罗列相关的`commit`，并且有指向这些`commit`的链接。当然，生成的文档允许手动修改，所以发布前，你还可以添加其他内容。

[conventional-changelog-cli](https://link.jianshu.com?t=https://github.com/conventional-changelog-archived-repos/conventional-changelog-cli) 就是生成`Change log`的工具，运行下面的命令即可。

```plain
$ npm install -g conventional-changelog-cli
$ cd my-project
```

打印到屏幕

```plain
$ conventional-changelog -p angular -i CHANGELOG.md -w
```

输出到文件

```plain
$ conventional-changelog -p angular -i CHANGELOG.md -s
```

上面命令不会覆盖以前的`Change log`，只会在`CHANGELOG.md`的头部加上自从上次发布以来的变动。

如果你想生成所有发布的`Change log`，要改为运行下面的命令。

```plain
$ conventional-changelog -p angular -i CHANGELOG.md -s -r 0
```

为了方便使用，可以将其写入`package.json`的`scripts`字段。

```plain
{
  "scripts": {
    "changelog": "conventional-changelog -p angular -i CHANGELOG.md -w -r 0"
  }
}
```

以后，直接运行下面的命令即可。

```plain
$ npm run changelog
```

### 缺少 package.json 文件

因为`commitizen`工具是基于 **Node.js** 的，而我们 **iOS** 项目工程目录下是没有`package.json`文件，所以会报错：

```plain
Error: ENOENT: no such file or directory, open '/Users/***/package.json
```

关于这个问题，可以参考这个`commitizen`的 **issue**：[Usage in non-node projects?](https://link.jianshu.com?t=https://github.com/commitizen/cz-cli/issues/102)，对于非 Node 的项目，我们可先在我们项目中添加一个空的`package.json`文件，然后再输入命令：

```plain
$ npm init --yes
```

先初始化配置 package.json 文件，然后再输入命令：

```plain
$ commitizen init cz-conventional-changelog --save --save-exact
```

## 参考链接

* [Commit message 和 Change log 编写指南](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)
