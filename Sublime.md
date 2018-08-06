# Sublime Text

## 基础

* [Sublime Text](http://www.sublimetext.com/) - 官网。
* [Package Control Popular](https://packagecontrol.io/browse/popular) - 插件排行榜。

---

## 配置

``` json
{
    "auto_complete_commit_on_tab": true,
    "auto_complete_delay": 0,
    "auto_complete_with_fields": true,
    "color_scheme": "Packages/Solarized Color Scheme/Solarized (light).tmTheme",
    "create_window_at_startup": false,
    "draw_white_space": "all",
    "ensure_newline_at_eof_on_save": true,
    "font_face": "Input Sans Narrow",
    "font_size": 15,
    "highlight_line": true,
    "ignored_packages":
    [
        "CSS",
        "Vintage"
    ],
    "indent_guide_options":
    [
        "draw_normal",
        "draw_active"
    ],
    "indent_to_bracket": true,
    "rulers":
    [
        80
    ],
    "tab_size": 2,
    "translate_tabs_to_spaces": true,
    "trim_trailing_white_space_on_save": true,
    "word_wrap": true
}
```
---

## 快捷键

### 多行快速选择文本

Ctrl+D - 选中光标所占的文本，继续操作则会选中下一个相同的文本。  
Ctrl-K, Ctrl-D - 把当前选中所占文本的光标，跳转到下一个相同文本。（配合 Ctrl+D 很实用）  
Alt-F3 - 一次性选中 (当前选中的文本）相同的文本。等于多次实用 Ctrl+D。

### 行操作

#### 选择类

Ctrl+L - 选择光标当前行，重复可依次增加选择下一行，若多有行光标，则第一次选择多行。  
Ctrl+J - 将光标的下一行，合并到光标当前行。若选择多行，则合并选择的多行为一行，同时再合并当前行的下一行。

#### 操作类

Ctrl+G - 跳转到第几行。  
Ctrl+Shift+L - （前提先选中多行）会在每行行尾插入光标，即可同时编辑这些行。  
Ctrl+Shift+↑ ↓ - 当前行或当前选中行与上下行互换位置。  
Ctrl+Enter - 在当前光标的下一行插入新行并跳转光标。  
Ctrl+Shift+Enter - 在当前光标的在上一行插入新行并跳转光标。  
Ctrl+Shift+D - 复制光标或所选区所在的整行，插入到下一行。  

#### 删除类

Ctrl+Shift+K - 删除整行，没有空白符。  
Ctrl+k+k - 从光标处至行尾删除。  
Ctrl+K+Backspace - 从光标处至行首删除。  

### 注释

Ctrl+Shift+/ - 根据选择进行多行注释。  
Ctrl+/ - 单行注释。  

### 缩进

Ctrl+[ ] - 左右缩进当光标或光标所在的行。  
Tab - 向右缩进。  
Shift+Tab - 向左缩进。  

### 代码块

Ctrl+Shift+[ - 选中代码，按下快捷键，折叠代码。  
Ctrl+Shift+] - 选中代码，按下快捷键，展开代码。  
Ctrl+K+0 - 展开所有折叠代码。  
Ctrl+K+T - 折叠所有 html 的属性。（非常好用，看 html 结构的时候）  
Ctrl+M - 跳转到对应括号。  
Ctrl+Shift+J - 快速选择同级的内容，同级内容 = 兄弟内容。  

### 编辑

Ctrl+Y - 恢复撤销。  
Ctrl+Z -  撤销。  
Ctrl+K+U - 转换光标最近单词，或所选区域大写。  
Ctrl+K+L - 转换光标最近单词，或所选区域小写。  

### 查找

Ctrl+F: 在当前页面中查找  
Ctrl+shift+F - 高级查找，在文件夹内查找。  
Ctrl+P - 打开多功能搜索框。  
　　1\. 输入当前项目中的文件名，快速搜索文件。  
　　2\. 输入 @和关键字，查找文件中函数名。（Ctrl+R）  
　　3\. 输入 - 和数字，跳转到文件中该行代码。（Ctrl+G）  
　　4\. 输入 #和关键字，查找变量名。 （Ctrl+ - ）  
Ctrl+G - 打开搜索框，自动带 - ，输入数字跳转到该行代码。  
Ctrl+R - 打开搜索框，自动带 @，输入关键字，查找文件中的函数名。  
Ctrl+;  - 打开搜索框，自动带 #，输入关键字，查找文件中的变量名、属性名等。  

### 窗口

Alt+Shift+1 - 窗口分屏，恢复默认 1 屏（非小键盘的数字）。  
Alt+Shift+2 - 左右分屏 - 2 列。  
Alt+Shift+3 - 左右分屏 - 3 列。  
Alt+Shift+4 - 左右分屏 - 4 列。  
Alt+Shift+5 - 等分 4 屏。  
Alt+Shift+8 - 垂直分屏 - 2 屏。  
Alt+Shift+9 - 垂直分屏 - 3 屏。  
Ctrl+K,Ctirl+B - 开启 / 关闭侧边栏。  
Ctrl+N - 新建空面板。  
Ctrl+Shift+N - 在新建窗口中，创建空面板。  
Ctrl+Tab - 从左往右，切换当前窗口的标签页。  
Ctrl+Shift+Tab - 从右往左，切换当前窗口的标签页。  
Ctrl+W - 关闭当前标签，当窗口内没有标签时会关闭该窗口  
Ctrl+Shift+T - 恢复刚刚关闭的标签  

### 高级

Ctrl+Shift+Space - 选择当前光标最小块的代码。（非常好用）
Ctrl+Shift+' - emmet 插件下，这个可以在 html 中，选择光标最近的一组闭合标签。修改标签非常方便。
Ctrl+U - 软撤销，撤销快捷键的一些动作，比如撤销选中。（若快捷键冲突不起效果，请自定义快捷键）

---

## 插件

### 语言类

#### HTML/CSS

* [HTML5](https://packagecontrol.io/packages/HTML5) - HTML5 snippets/syntax

