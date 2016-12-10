---
layout: post
title:  "历史的进程 - Emacs学习初篇"
date: 2016-12-10 8:00:00
image: ''
tags:
- Daily
description: ''
categories:
- SYH的自留地
---

**The Editor of God's**
---
Atom.AlwaysBug?()  

Atom又一次抽风了，这一次是如果不外接显示器的话，
它是默认在屏幕显示外面的而且根本拖动不回来。
加之Sublime的输入法漂移，我能怎么办，我也很绝望啊。

于是，我就打开了在我电脑存放了很长时间的Emacs 25.1-The Editor of God's。
初次上手Emacs很不习惯，所有的命令都和Ctrl挂钩，而且x1-carbon的ctrl在一个很奇怪的位置。
没过一会Emacs卡的不行，找了半天原因发现原来是Emacs用一种韩文字体显示中文，所以一直在
fallback，导致编辑器变得很卡。

所以安装好Emacs之后一定要做的 (Windows)
- 更换一个字体
- 更换ctrl和capslock(如果你的手不想疼的话)
- 如果用WSL的话，在'.bashrc'或者'.zshrc'加上这么一条 alias vim='emacs'(心无旁骛 逃

因为很看好在Emacs下可以收发邮件，所以在vim和Emacs中选择了Emacs，等看完所有的教程再
写一篇常用的命令集合，命令太多了根本记不住。

