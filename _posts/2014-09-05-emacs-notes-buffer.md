---
layout: post
title: "emacs学习笔记之buffer"
categories: notes
---

　　Emacs可以有多个buffer，每个buffer都有各自的名字，它们有的与文件关联，有的不然。任意时刻，只有一个buffer是被选中的。如果emacs只有一个window，则这个window里的buffer自然就是被选中的状态。而如果有多个window，则被选中的window里的buffer为被选中。

- 创建和选择buffers

  + `C-x b buffer RET`

    选择或创建一个被命名的buffer。

  + `C-x 4 b buffer RET`

    类似。不过是对另外一个window操作。

  + `C-x 5 b buffer RET`

    类似，不过是对另外一个frame操作。

  + `C-x LEFT/RIGHT`

    选择前/后一个buffer.

  + `C-u M-g M-g`

    `C-u M-g g`

    读取一个数字n，在另外一个window中打开最近一个buffer的第n行。

- 列出存在的buffers

  + `C-x C-b`

    列出存在的buffer列表。可用`C-u C-x C-b`只列出关联文件的buffers。

- 其他buffer操作

  + `C-x C-q`

    开关当前buffer的只读状态。

  + `M-x rename-buffer RET name RET`

    重命名当前buffer。

  + `M-x rename-uniquely`

    重命名当前buffer，在末尾加上`<number>`。

  + `M-x view-buffer RET buffer RET`

    在`buffer`中滚动浏览。

    `M-x rename-uniquely`会自动给当前buffer名字加上一个独特的数字使之与其他不重复。

    另外，`M-x append-to-buffer`和`M-x insert-buffer`可以从一个buffer复制文字到另一个buffer。

- 清除buffer。

  + `C-x k bufname RET`

    清除`bufname`这个buffer。

  + `M-x kill-some-buffer`

    逐一清除buffers。

  + `M-x kill-matching-buffers`

    清除匹配正则表达式的buffers。

- 若干个buffers的操作

  + `M-x buffer-menu`

    编辑一个列出所有buffer的buffer（听上去貌似挺拗口的呢:P）

  + `M-x buffer-menu-other-window`

    见名知意。<br/><br/>
    
    ![buffer_menu](/images/emacs/buffer_menu_1.png "buffer menu")

    在buffer列表允许以下的操作。

    *标记*。<br/><br/>

    标记是指在列表中可以用以下的操作对某一个buffer进行标记，在完成所有的标记之后可以用`x`执行。

    * `d`

      标记当前buffer为待清除对象，并将光标下移一行。以后可以用`x`执行清除。

    * `C-d`

      类似，但是光标上移。


    * `s`

      标记当前buffer为待保存。

    * `x`

      执行所有的保存或清除的标记。

    * `u`

      撤销当前的`d`标记。

    * `DEL`

      移至前一行并清除前一行的`d`标记。

    *立即操作*。

    以下命令可以立即执行。

    * `~`

      标记当前buffer为未修改过的。

    * `%`

      开/关当前buffer的只读状态。

    * `t`

      以tags table访问当前buffer。

    * `q`

      退出当前buffer菜单（泪流满面终于知道怎么退出了T_T）。

    * `RET`

      `f`

      选择当前的buffer并显示。

    * `o`

      类似以上，不过在另外一个window显示当前选中的buffer。

    * `C-o`

      类似上，不过并不选中那个buffer（不切换过去）。

    * `1`

      选中当前buffer并在一个full-frame window中显示。

    * `2`

      拆分出一个window并分别显示打开buffer菜单之前的buffer的当前的buffer。

    * `b`

      将当前buffer移至列表底部。

    * `m`

      标记当前buffer。当执行`v`命令的时候再另外一个窗口中显示这些buffer。

    * `v`

      和已经用`m`标记的buffer都用各自的buffer显示。

    *影响整个buffer列表的命令*

    * `S`

      根据当前光标所在的栏对buffer列表进行排序。可用数字前缀指定要排序的列。

    * `T`

      开关对非文件的buffer的显示、<br/><br/>

    一般来说，buffer list并不会自动更新，可以用`g`来更新。

- 间接buffers

  间接buffer是指以其他buffer为基buffer的一种buffer。

  * `M-x make-indirect-buffer RET base-buffer RET indirect-name RET`

  创建一个叫indirect-name的间接buffer，以base-buffer为基buffer。

  * `M-x clone-indirect-buffer RET`

  以当前buffer为基buffer，创建一个复制的间接buffer。

  `C-x 4 c`

  类似上面，并且在新的窗口打开这个间接buffer并选中。

  间接buffer与基buffer里的内容总是保持一致的。其中一个buffer内容的修改会直接影响另一个buffer的内容。但是除此之外，它们是两个独立的buffer，它们有不同的名字，不同的光标位置，不同的major mode的本地变量等等。

  间接buffer不能访问文件，所以对间接buffer执行保存操作实际是对基buffer进行保存。清除基buffer也会清除其间接buffer，而反之则不会。

- 方便的特性和自定义buffer的操作

  * _使buffer的名字惟一化_

  如果多个buffer访问的文件名都一样，那么buffer的名字就需要变得惟一以方便区别。emacs默认是将文件名后面加上数字（'<2>','<3>'）。加载`uniquify`库（`require 'uniquify`）可以使用其他规则来定义buffer的名字。这主要是通过设置变量`uniquify-buffer-name-style`来实现的。

    + `forward` /u/rms/tmp/Makefile -> 'tmp/Makefile';/usr/projects/zaphod/Makefile -> 'zaphod/Makefile'.
	+ `post-forward` 'file|top1/middle1' & 'file|top2/middle2'
	+ `reverse` 'file\middle1\top1' & 'file\midlle2\top2'

  * 使用子字符串切换buffer

    __istwitch__这个minor mode允许使用子字符串来在切换buffer的时候用子字符串匹配buffer name。先用`C-x b`打开buffer列表后，就可以输出子字符串进行匹配，按`RET`会选中当前匹配的第一个buffer.用`C-s`和`C-r`可以翻转当前匹配的buffer名单。

  * 自定义buffer菜单

  `M-x bs-show`

  显示一个类似于`M-x list-buffers`的buffer列表，但是这个列表可以自定义。

  
