---
layout: post
categories: notes
title: "CentOS 7环境下的VPN服务器搭建"
---

换新台式机了真开心，于是又到了折腾装系统和搭VPN的时候= =

首要的一步，就是CentOS 7采用了*firewall*作为防火墙，如果要按照网上那些方法就得先停用*firewall*然后安装*iptables-services*。


关闭firewall

{% highlight Batch shell scripts %}
systemctl stop firewalld.service #停止firewall
systemctl disable firewalld.service #禁止firewall开机启动
{% endhighlight %}

安装*iptables*。之前我发现系统已经安装了*iptables*以为不用装了，结果并没有*iptables*这个service。原来是需要安装：

{% highlight Batch shell scripts %}
yum install iptables-services
{% endhighlight %}

然后主要依靠这位仁兄的[文章][1]了，其中最有用的信息就是添加EPEL的源，有了它，安装*pptpd*就超级容易了。

{% highlight Batch %}
yum install ppp iptables pptpd
{% endhighlight %}

编辑**pptpd.conf** ```
vi /etc/pptpd.conf
```

修改`localip`和`remoteip`字段

{% highlight Batch %}
localip 192.168.3.1
remoteip 192.168.3.200-250
{% endhighlight %}

编辑**options.pptpd** `vi /etc/ppp/options.pptpd`

{% highlight Batch %}
ms-dns 8.8.8.8
ms-dns 8.8.4.4
{% endhighlight %}

编辑**chap-secrets**设置用户名和密码 `vi /etc/ppp/chap-secrets`

{% highlight Batch %}
name  pptpd  password *
{% endhighlight %}

修改**sysctl.conf** `vi /etc/sysctl.conf`

{% highlight batch %}
net.ipv4.ip_forward=1
{% endhighlight %}

使之生效 `sysctl -p`.

接下来便是设置`iptables`的规则了。

{% highlight batch %}
iptables -A INPUT -p gre -j ACCEPT
iptables -A INPUT -p tcp -m tcp --dport 1723 -j ACCEPT
iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD -s 192.168.3.0/24 -o p4p1 -j ACCEPT
iptables -A FORWARD -d 192.168.3.0/24 -i p4p1 -j ACCEPT
iptables -t nat -A POSTROUTING -s 192.168.3.0/24 -o p4p1 -j MASQUERADE
{% endhighlight %}

其中`192.168.3.0`换成刚才设置的ip段的地址。`p4p1`指的服务器上的连接外网的网卡名称。

开始运行.`service pptpd start`。

保存`iptables`规则，可用`service iptables save`，会将配置保存到`/etc/sysconfig/iptables`，下次开机可用`iptables-restore /etc/sysconfig/iptables`恢复配置。

[1]: http://www.wanghailin.cn/centos-7-vpn/
