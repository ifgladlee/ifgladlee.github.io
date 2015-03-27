---
layout: post
title: "手动升级Emacs的org-mode模块"
categories: notes
---

今天做开题ppt,用org拟提纲，然后想导出为markdown文件，可是发现emacs里导出选项没有org文档说的那样有markdown格式，然后才发现emacs24.3自带的org-mode是7.9版本的，而导出markdown的选项在8.0之后才有。本文将介绍如何手动将org升级到最新版(8.2)。其实操作很简单，不过有一些关于可能遇到的问题的tips.

1\. 去官网 [org](http://orgmode.org) 下载org的最新archive并解压。

2\.   在`.emacs`里添加org的路径

		{% highlight  text %}
(add-to-list 'load-path "~/path/to/orgdir/lisp")\\
(add-to-list 'load-path "~/path/to/orgdir/contrib/lisp" t)
		{% endhighlight %}
   
   **注意：路径分隔符一定要用`/`，包括在windows环境也是!**

3\. 删除emacs目录下面的org包.`~path/to/emacs/list/org/`.

OK,现在打开emacs，将org导出markdown门门达╭(′▽`)╯
