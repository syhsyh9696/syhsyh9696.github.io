---
layout: post
title:  "历史的进程 - Emacs配置初篇"
date: 2016-12-21 8:00:00
image: ''
tags:
- Daily
description: ''
categories:
- SYH的自留地
---

**Emacs的包管理**
---

一位一些大家都知道的原因， Emacs的源有一些是不能用的，
如果是在Linux下的话，用proxychains还是可以很方便的，
但是如果是Emacs for windows，这个问题不知道该怎么解决了，除非你用WSL。
所以没办法，换别的源吧

所谓的包管理，在Emacs里面叫做package mode，
想查看自己目前的packages-list的话，使用组合键 M+x list-packages 可以查看自己现在可用的包
在这个buffer里可以使用C-h m了解更多的操作帮助。

这个packages-list是从网络上下载下来的，这个下载地址叫做Package Archives，
使用组合键 C-h v package-archives 可以查看这个变量值，默认情况下只有一个源，导致包不是很多。

为了实现更多的扩展功能我还是要添加更多的Package源，
利用组合键 M-x customize-variable RET package-archives 可以进入到一个新的buffer，
就可以在这个里面添加常用的源了，一般来说，中科大的和清华大学的源都是很好用的，
不过还有一个

1. ("popkit" . "http://elpa.popkit.org/packages/")

这个源有的时候也是非常的好用，是以为大陆的Emacs用户个人维护的，有的时候也是非常的快。

**Emacs Theme**
---

在用了几天自带的主题之后，我实在是被自带的mode-line丑的不要不要的，
找了好几天终于发现了一个很对我口味的主题

1. Emacs-Dracula https://draculatheme.com/emacs/

这个主题配色非常的好看，主要是mode-line不是那么反人类了，写起东西来也变得非常舒服了。

在我的调教下，Emacs逐渐变得越来越好用了。
