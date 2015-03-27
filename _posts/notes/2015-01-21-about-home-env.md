---
layout: post
title: "Trouble Maker:%HOME%环境变量"
categories: notes
---

要说，*%HOME%*在windows下真是一个trouble maker。

首先，windows下其实是没有*%HOME%*这个环境变量的，但是[这篇文章][1]说git的用户要保存用户名密码就得设置这样一个环境变量，好吧，那就设吧。

```
将HOME设置为%USERPROFILE%
```

那么问题就来了，当我打开*cygwin*的窗口时，却发现*home*目录已经不是*cygwin*目录下的*/home/[username]/*了，而是变成了刚刚设置的windows的*%HOME%*目录，也就是*%USERPROFILE%*!

这一下可乱套了，我之前装的*jekyll*自然是运行不了了，*cygwin*里的*emacs*配置当然也无效了，因为这些配置信息都是存在以前的**~**目录下的，*%HOME%*变量被设定之后，这些配置自然都无效了。

所以说*%HOME%*是个讨厌的trouble maker了吧。

怎么办，此技可谓奇技淫巧吧，就是把**%HOME%**改成**%home%**。对，你懂了，因为windows是不区分大小写的，改成小写无所谓，而 \*nix系统是区分大小写的，改成小写之后相当于就没有设定*$HOME*这个环境变量了，一进cygwin，*~*目录又恢复了，噗。

[1]: http://www.cnblogs.com/dudu/archive/2011/07/06/git_save_username_password.html



