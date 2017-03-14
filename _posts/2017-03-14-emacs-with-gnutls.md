---
layout: post
title: "Emacs with GnuTLS"
date: 2017-03-14 13:19:03 +0800
categories:
tags:
- Daily
categories:
- SYH的自留地
---

**Emacs换源产生的依赖问题**

Gnu software在windows上总是有一些缺少依赖的问题，
今天在给Emacs切换Emacs-China的Melpa源的时候有错误产生 "GnuTLS library is not found"

然后查了查，原来是因为Emacs从24版本以后开始直接允许使用GnuTLS库来直接创建TLS网络链接，
而不是调用其他的Terminal app。要触发这个问题的话，也是有一定的条件的。
原来的源的配置我是直接扔到了
{% highlight clojure %}
(custom-set-variables)
{% endhighlight %}
这样是没有任何问题的，只有我使用了新的init-packages.el之后这个问题才会出现
(源配置移动到packages-list到这个文件)
{% highlight clojure %}
(when (>= emacs-major-version 24)
  (require 'package)
  (add-to-list 'package-archives '("gnu" . "http://elpa.emacs-china.org/gnu/") t)
  (add-to-list 'package-archives '("melpa", "http://elpa.emacs-china.org/melpa/") t)
  (add-to-list 'package-archives '("popkit" . "http://elpa.popkit.org/packages/") t))
{% endhighlight %}

解决起来也是很方便的，不出现各种问题一点也不GNU好不好!

访问[***GnuTLS***](http://www.gnutls.org/download.html) 然后找到针对Windows的预先编译版本，
解压之后直接将解压后bin文件夹里面的dll文件扔到emacs里的bin文件夹，Done!

如果你觉得我扯的太多的话，Emacs offical pages也给了教程你大可以看看
[The site](https://www.gnu.org/software/emacs/manual/html_mono/emacs-gnutls.html)