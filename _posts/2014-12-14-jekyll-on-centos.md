---
layout: post
title: "CentOS7.0安装jekyll笔记"
categories: notes
---

发现好久没有用实验室的台式机了，今天装了CentOS，打算专心用做开发用服务器了><.首先想到的是把日记环境搭起来。

折腾了一个小时，终于搞定啦，呼！

和Ubuntu不同，CentOS这安装软件源需要用`yum`命令来安装。所以：

1. `yum install ruby ruby-devel... rubygems`
2. 下载`RubyGems`安装
3. 下载`Node.js`并解压，将`bin`添加到环境变量里（`/etc/profile`）
4. `gem install json`
5. `gem install jekyll`

搞定。

总结起来，除了`yum`这一点不一样以外，安装`ruby-devel...`这个也是不同于Ubuntu/Debian的。如果不安装这个，会出现找不到头文件的情况。第4步更为关键，如果不安装json,jekyll是不能成功运行的。

最后的最后，还有一个坑爹的地方,用`jekyll serve`跑起来之后，发现只有本机能够访问，局域网的其他主机都不能访问这个站点= =原因是CentOS默认打开了防火墙，而且CentOS 7.0默认的防火墙软件是`firewalld`，好吧，反正开发用，我就先关了好惹:

`sudo service firewalld stop`
