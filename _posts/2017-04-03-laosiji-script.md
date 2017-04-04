---
layout: post
title: "Laosiji Script"
date: 2017-04-03 15:43:37 +0800
categories:
tags:
- Ruby
categories:
- Ruby notes
---

**老司机发车了**

最近混破群混的多，结果被破群的人喷Chrome装了很多开车插件，
我是那种整天伸手的人吗？？从零开始写一个简单的开车Bot好了。

想到这里，我就打开了我的工具包，找到了[btkiki](http://www.btkiki.com)
这个网站，这个网站的好处很多啊，但是也有不少缺点
- 资源全
- 链接新
- 请求简单

- 有广告
- 有时候点击没反应(利用Ruby客户端完美规避)
好了不要说了就是你了。

利用前一阵子未完成的爬虫中学习的知识，nokogiri和rest-client
完成链接的请求和解析。

首先是请求，经过charles抓包发现，Get一个base url + 番号.html就可以
那么利用rest-client来完成
{% highlight ruby %}
require 'rest-client'

baseurl = "www.btkiki.com/s/"
url = baseurl + "#{str}.html"

response = RestClient.get url

{% endhighlight %}

好了，现在已经获得相关的番号的页面了，保存在response.body里面，
现在就是要解析它了，经过分析，下一个子页面请求的链接里面就包含
着每一个磁力链的散列值，只要提取出它的值加上车头就是完美的磁力
链了，perfect，这时候就要用nokogiri完成这一个工作了，真是相当
好用的解析神器
{% highlight ruby %}
require 'nokogiri'

header = "magnet:?xt=urn:btih:"
magnet = String.new

doc = Nokogiri::HTML(response.body)
details = doc.search('//div[@class="g"]/h2/a').each do |row|
	magnet << header + row['href'].split("/")[-1][0..-6] + "\n\n"
end

return magnet
{% endhighlight %}
要说难一点的就是nokogiri的解析函数构造了，这里用search函数配合
xml里面的xpath完成这一切，后面的是将解析出的字串去除无关字符提取
相关的散列值，Ruby原则能一行坚决不两行，这里给出doc的一个例子

{% highlight HTML %}
<div class="std2">大小:<span> 9.2 GB</span> &nbsp;&nbsp;&nbsp;&nbsp;
文件数:<span> 1</span> &nbsp;&nbsp;&nbsp;&nbsp;
创建日期:<span> 4 月前</div>
</div>
<div class="g"><h2><a title="SUPD-115" target="_blank" href="http://www.btkiki.com/torrent/f0779d9bd17e15ac7c861b297f883813bc2a5a05.html"><span class="em">SUPD</span>-<span class="em">115</span></a></h2>
<div class="std">
<div class="list">SUPD-115.mp4
</div>
<div class="list">Watch JAV Stream Online - JAVChan.com.url
</div>
</div>
{% endhighlight %}

好了加上车头就可以用了，具体还有telegram机器人的实现就等有机会
写一写把，反正核心就这个样子。

如果需要关注的话就先下载telegram然后关注
[@ujnlaosijibot](http://telegram.me/ujnlaosijibot)，注意身体(逃



