# vi cheat sheet

---

## 进入 vi 编辑器

| 命令 | 说明 |
| :-: | :-: |
| vi filename | 如果 filename 存在，则打开；否则会创建一个新文件再打开。 |

## vi 工作模式

### 普通模式

由 Shell 进入 vi 编辑器时，首先进入普通模式。在普通模式下，从键盘输入任何字符都被当作命令来解释。普通模式下没有任何提示符，输入命令后立即执行，不需要回车，而且输入的字符不会在屏幕上显示出来。

普通模式下可以执行命令、保存文件、移动光标、粘贴复制等。

### 编辑模式

编辑模式主要用于文本的编辑。该模式下用户输入的任何字符都被作为文件的内容保存起来，并在屏幕上显示出来。

### 命令模式

命令模式下，用户可以对文件进行一些高级处理。尽管普通模式下的命令可以完成很多功能，但要执行一些如字符串查找、替换、显示行号等操作还是必须要进入命令模式。

### 工作模式切换

- 在普通模式下输入 **i**(插入)、**c**(修改)、**o**(另起一行) 命令时进入编辑模式；按 `esc` 键退回到普通模式。
- 在普通模式下输入`冒号(:)`可以进入命令模式。输入完命令按回车，命令执行完后会自动退回普通模式。

> 提示：如果不确定当前处于哪种模式，按两次 `Esc` 键将回到普通模式。

## 退出 vi 编辑器

| 命令 | 说明 |
| :-: | :-: |
| :q | 如果文件未被修改，会直接退回到 Shell；否则提示保存文件。 |
| :q! | 强行退出，不保存修改内容。 |
| :wq | w 命令保存文件，q 命令退出 vi，合起来就是保存并退出。 |
| ZZ | 保存并退出，相当于 wq，但是更加方便。 |

退出之前，你也可以在 w 命令后面指定一个文件名，将文件另存为新文件，例如：
> :w filename2

将当前文件另存为 filename2。

## 移动光标

为了不影响文件内容，必须在普通模式下移动光标。使用下表中的命令每次可以移动一个字符：

| 命令 | 说明 |
| :-: | :-: |
| h | 向左移动光标（移动一个字符） |
| j | 向下移动光标（移动一行） |
| k | 向上移动光标（移动一行） |
| l | 向右移动光标（移动一个字符） |

两点提醒：

- vi 是`区分`大小写的，输入命令时注意不要锁定大写。
- 可以在命令前边添加一个数字作为前缀，例如，2j 将光标向下移动两行。

当然，还有很多其他命令来移动光标，不过记住，一定要在普通模式下。

| 命令 | 说明 |
| :-: | :-: |
| 0 或 \| | 将光标定位在一行的开头。 |
| $ | 将光标定位在一行的末尾。 |
| w | 定位到下一个单词。 |
| b | 定位到上一个单词。 |
| ( | 定位到一句话的开头，句子是以 ! . ? 三种符号来界定的。 |
| ) | 定位到一句话的结尾。 |
| { | 移动到段落开头。 |
| } | 移动到段落结束。 |
| [[ | 回到段落的开头处。 |
| ]] | 向前移到下一个段落的开头处。 |
| n\| | 移动到第 n 列（当前行）。 |
| 1G 或 gg | 移动到文件第一行。 |
| G | 移动到文件最后一行。 |
| nG | 移动到文件第 n 行。 |
| :n | 移动到文件第 n 行。 |
| H | 移动到屏幕顶部。 |
| nH | 移动到距离屏幕顶部第 n 行的位置。 |
| M | 移动到屏幕中间。 |
| L | 移动到屏幕底部。 |
| nL | 移动到距离屏幕底部第 n 行的位置。 |
| n<space\> | 按下数字后再按空格键，光标会向右移动这一行的 n 个字符。 |
| n<Enter\> | 按下数字后再按回车键，光标向下移动 n 行。 |
| + | 光标移动到非空格符的下一行 |
| - | 光标移动到非空格符的上一行 |

## 滚屏

| 命令 | 说明 |
| :-: | :-: |
| CTRL + d | 向前滚动半屏 |
| CTRL + u | 向后滚动半屏 |
| CTRL + f | 向前滚动全屏 |
| CTRL + b | 向后滚动整屏 |
| CTRL + e | 向上滚动一行 |
| CTRL + y | 向下滚动一行 |

## 切换到编辑模式

| 命令 | 说明 |
| :-: | :-: |
| i | 在当前光标位置之前插入文本 |
| I | 在当前行的开头插入文本 |
| a | 在当前光标位置之后插入文本 |
| A | 在当前行的末尾插入文本 |
| o | 在当前位置下面创建一行 |
| O | 在当前位置上面创建一行 |

## 删除字符

| 命令 | 说明 |
| :-: | :-: |
| x | 删除当前光标下的字符 |
| X | 删除光标前面的字符 |
| dw | 删除从当前光标到单词结尾的字符 |
| d0 | 删除从当前光标到行首的字符 |
| d$ | 删除从当前光标到行尾的字符 |
| D | 删除从当前光标到行尾的字符 |
| d1G | 删除光标所在到第一行的所有数据 |
| dG | 删除光标所在到最后一行的所有数据 |
| dd | 删除当前光标所在的行 |

可以在命令前面添加一个数字前缀，表示重复操作的次数，例如，2x  表示连续两次删除光标下的字符，2dd 表示连续两次删除光标所在的行。

## 复制粘贴

| 命令 | 说明 |
| :-: | :-: |
| yy | 复制当前行 |
| nyy | 复制 n 行 |
| y0 | 复制光标所在的那个字符到该行行首的所有数据 |
| y$ | 复制光标所在的那个字符到该行行尾的所有数据 |
| y1G | 复制光标标所在行到第一行的所有数据 |
| yG | 复制光标所在行到最后一行的所有数据 |
| 小写 p | 将复制的文本粘贴到光标后面 |
| 大写 P | 将复制的文本粘贴到光标前面 |

## 修改文本

| 命令 | 说明 |
| :-: | :-: |
| cc | 删除当前行，并进入编辑模式。 |
| r | 替换当前光标下的字符。 |
| R | 从当前光标开始替换字符，按 Esc 键退出。 |
| s | 用输入的字符替换当前字符，并进入编辑模式。 |
| S | 用输入的文本替换当前行，并进入编辑模式。 |

## 高级命令

| 命令 | 说明 |
| :-: | :-: |
| J | 将当前行和下一行连接为一行 |
| << | 将当前行左移一个单位（一个缩进宽度） |
| \>> | 将当前行右移一个单位（一个缩进宽度） |
| ~ | 改变当前字符的大小写 |
| ^G | Ctrl + G 组合键可以显示当前文件名和状态 |
| U | 撤销对当前行所做的修改，再次按 `U` 恢复 |
| u | 撤销上次操作，Ctrl + r 反撤销？ |
| :w filename | 保存修改到 filename |

## 文本查找

如果希望进行全文件搜索，可以在普通模式下输入 / 命令，这时状态栏（最后一行）出现"/"并提示输入要查找的字符串，回车即可。  
/ 命令是向下查找，如果希望向上查找，可以使用 ? 命令。  
这时，输入 n 命令可以按相同的方向继续查找，输入 N 命令可以按相反的方向继续查找。  
搜索的字符串中可以包含一些有特殊含义的字符，如果希望搜索这些字符本身，需要在前面加反斜杠(\\)。  
部分特殊字符列表：

| 字符 | 说明 |
| :-: | :-: |
| ^ | 匹配一行的开头 |
| . | 匹配一个字符 |
| * | 匹配 0 个或多个字符 |
| $ | 匹配一行的结尾 |
| [ ] | 匹配一组字符 |

> 两个骚操作：
- `:1,$s/word1/word2/g`：从第一行到最后一行寻找 word1 字符串，并将该字符串取代为 word2 ！
- `:1,$s/word1/word2/gc`：从第一行到最后一行寻找 word1 字符串，并将该字符串取代为 word2 ！且在取代前显示提示字符给用户确认 (confirm) 是否需要取代！

## set 命令

| 命令 | 说明 |
| :-: | :-: |
| :set nu | 显示行号。 |
| :set nonu | 与 set nu 相反，为取消行号！ |

## Reference

- [最简单的 vi 编辑器教程](http://c.biancheng.net/cpp/html/2735.html)
- [Linux vi/vim | 菜鸟教程](http://www.runoob.com/linux/linux-vim.html)
- [Vim - 适合自己的，才是最好的](http://geekplux.com/2015/06/06/vim-those-fit-yourself-are-the-best.html)
- [What is your most productive shortcut with Vim?](https://stackoverflow.com/questions/1218390/what-is-your-most-productive-shortcut-with-vim)
- [Vim for Beginners](https://computers.tutsplus.com/tutorials/vim-for-beginners--cms-21118)
- [使用 vi 编辑文件](https://www.ibm.com/developerworks/cn/linux/l-lpic1-v3-103-8/index.html)