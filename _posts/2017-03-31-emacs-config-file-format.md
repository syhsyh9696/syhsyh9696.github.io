---
layout: post
title: "Emacs 配置文件格式化"
date: 2017-03-31 22:56:28 +0800
categories:
tags:
- Daily
categories:
- SYH的自留地
---

**纯属吃饱了撑的**

反正那个爬虫一时半会做不出来，还是来折腾一下emacs吧。
要说最近看什么不爽，就是看那个长长的***init.el***非常的不爽，
里面堆满了各种

- 自动生成的custom代码
- package源配置代码
- 各种mode开启关闭
- 各种键位的自定义
- ui的自定义

够了！邪魔退散！开始拆分。

长长的配置文件重新分为几类保存在 ~/.emacs.d/lisp，
- custom.el 主要保存自动生成的custom代码
- init-better-defaults.el 模式的开关
- init-keybindings.el 键位设置
- init-org.el org模式相关配置
- init-packages.el package源配置和自动安装函数定义
- init-ui.el 工具栏或者主题设置

好了拆分完成，下一步就是在init.el中引用调用了。
首先指定你的配置文件保存在哪个位置，emacs会找到那个文件夹
并索引文件，这一步用 ***(add-to-list load-path "FILL_IN")***搞定。
之后就是require相关设置增加相应的功能，不过这一步一定不要包括
***custom.el***文件，要单独处理这个大麻烦。

最后就是load custom variable，需要set一个变量，
用***(setq custom-file)***搞定并在最后load一下搞定。

具体的实现方法 
{% highlight clojure %}
(package-initialize)

(add-to-list 'load-path "~/.emacs.d/lisp/")

;; Set F2 to open init.el
(defun open-my-init-file()
  (interactive)
  (find-file "~/.emacs.d/init.el"))

;; add more personal func
(require 'init-packages)
(require 'init-ui)
(require 'init-better-defaults)
(require 'init-org)
(require 'init-keybindings)

;; load custom variable
(setq custom-file (expand-file-name "lisp/custom.el" user-emacs-directory))
(load-file custom-file)
{% endhighlight %}
Done!又水了一篇
