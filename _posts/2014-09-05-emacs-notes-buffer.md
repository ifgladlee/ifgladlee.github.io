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

    见名知意。   

    ![buffer_menu] (/images/emacs/buffer_menu_1.png)
    <img src="/images/emacs/buffer_menu_1.png" alt="buffer menu"/>
