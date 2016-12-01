---
layout: post
title:  "Linode-Tokyo2 购入!"
date: 2016-12-01 12:00:00
image: ''
date:   2016-09-12 00:06:31
tags:
- VPS
description: ''
categories:
- 折腾纪实
---

**Bandwagon => Linode-Tokyo2**
---
这个月的Bandwagon真是抽风的厉害，晚上在实验室什么也干不成，而且已经续费了十四个月马上到期，这是前提。

于是我就比对了一下周围近一些的提供商

|-----------------+------------+-----------------+----------------+-----------------|
| 提供商           | 位置        | 优点             |缺点            | 价格             |
|-----------------|------------|-----------------|----------------|-----------------|
| Bandwagon       | US         | 特别便宜          | 超售!晚上爆炸   | M:2.99$ Y:19.99$ |
| Vultr           | JP SG      | **便宜 活动多**   | 买的人多线路爆炸 | 全是活动没法算价格  |
| Linode          | JP SG      | **快** 稳定 管理强 | 贵! 也是NTT线路 | M:10$ Y:120$    |
|-----------------+------------+-----------------+----------------|-----------------|

当看完这几家后，我觉得Vultr强!无敌!就是它了，然后就打开了Speedtest，然后就没有然后了，因为实在是太慢了，
和B家一样人太多线路太繁忙，于是作罢。

转念一想，和我一起租用VPS的都是高富帅，我们为什么不搞一个高富帅主机呢？就决定是你了Linode!
Linode-Tokyo1机房早就变成传家宝了，价格高的无法接受，退而求其次，Linode-Tokyo2也是不错的选择。

Linode-Tokyo2的配置
1-CORE\|2GB-RAM\|24GB-STORTAGE\|2TB-TRANSFER

**配置方法**
---
不安装锐速的话，四个人是一定不能用的，所以安装好CentOS 7和Shadowsocks后第一件事情就是安装锐速
{% highlight bash %}
> wget -N --no-check-certificate https://raw.githubusercontent.com/91yun/serverspeeder/master/serverspeeder-all.sh && bash serverspeeder-all.sh

{% endhighlight %}
如果内核是在[支持的内核](https://www.91yun.org/wp-content/plugins/91yun-serverspeeder/systemlist.html)里面的话，
执行上一步就可以了，然而我的内核并不是受到支持的，需要更换VPS的内核。
这个时候就要请出Linode的后台管理了 强!无敌! 在管理页面里更换成受支持的内核就可以了，锐速一开在Youtube上看1440P的视频都没有问题了。

**依旧存在的问题**
---
Linode-Tokyo2机房是刚开的，IP是刚广播的，APNIC的数据库还没更新，所以显示的地址还是SG

再就是Ping值有时候还是高，到了200ms，一般在130ms，希望以后的线路优化能好点，毕竟老牌大厂。


现在，可以静静看着那些用着Bandwagon的那些人了。
