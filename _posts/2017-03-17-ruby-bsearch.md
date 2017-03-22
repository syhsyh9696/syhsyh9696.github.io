---
layout: post
title: "Ruby bsearch"
date: 2017-03-17 15:01:59 +0800
categories:
tags:
- Ruby
categories:
- Ruby notes
---

**Ruby Array#bsearch**

---
最近遇到了很多查询查找的问题，各个方法的效率又天差地别。
Ruby Module#enumerable 提供了很多方法，比如
Array#select Array#reject Array#find Array#bsearch

我看老师天天讲分治法，自然就经常使用典型的Array#bsearch方法了

相比于Array#find要一直找到整个Array的末尾不同， bsearch
方法就相当的快了，复杂度O(log n)，具体实现方法可以看
Ben Lewis's
[Blog](https://fluxusfrequency.github.io/blog/2014/01/31/building-a-binary-search/)

也可以自己扔到一个脚本里面看看他们之间的差异
{% highlight ruby %}
require 'benchmark' 

data = (0..20000000)

Benchmark.bm do |test|
    test.report(:find) { data.find { |num| num > 10000000 } }
	test.report(:bsearch) { data.bsearch { |num| num > 10000000 } }
end
{% endhighlight %}

反正在我这里，Bsearch的方法是要比Find快非常的多。
这样Leetcode里面的很多题目就可以用这个方法给题目加速了。

不过Bsearch方法也是有一定缺点的，要求数组一定是要排序后的数组才行,
如果要找的数字在整个数组的最后面，好像性能也没什么差别了。
