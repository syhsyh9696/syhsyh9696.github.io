---
layout: post
title:  "Ruby的集合遍历"
date: 2016-12-10 9:00:00
image: ''
tags:
- Ruby
description: ''
categories:
- Ruby notes
---

**Ruby的遍历方法**
---

因为最近经常需要用到集合的遍历，看完镐头书(Ruby Programming)
相关章节后总结下常见的方法。

***each***
基本上来说就是处于取代了for的作用，当你需要迭代一个集合的时候
each都是可以的选择，而且each比for方便很多
{% highlight ruby %}
[1, 2, 3].each do |e|
    # Do something
end
{% endhighlight %}

***map***
和each的作用大概相同，最大的不同就是map会将处理后的结果返回，
省了temp一类的中间变量
{% highlight ruby %}
[1, 2, 3].map { |e| e * 2 }
# Return [2, 4, 6]

['a', 'b', 'c'].map(&:upcase)
# Return ['A', 'B', 'C']
{% endhighlight %}

***select***
从前向后的迭代计算计算结果为true的元素，当作正向的filter
{% highlight ruby %}
[1, 2, 3, 4].select { |e| e % 2 == 0 }
# Return [2, 4]
{% endhighlight %}

***reject***
与select结果相反，可以看作反方向filter，返回结果为false的元素

***partition***
根据传入的代码块中条件，把集合结果分为两部分:满足条件true和false
类似同时应用了select和reject
{% highlight ruby %}
[1, 2, 3, 4].select { |e| e % 2 == 0 }
# Return [[2, 4], [3, 5]]
{% endhighlight %}

***find***
正向查找满足条件的第一个值，并作为结果返回 如果想查询所有的同类值的话，find是无效的
{% highlight ruby %}
[1, 3, 5, 7].find { |e| e > 4 }
# Return 5
{% endhighlight %}

***all?***
通过迭代判断某个集合是否满足传代码块的所给条件，只有都满足返回true，否则返回false
{% highlight ruby %}
[2, 4, 6].all?{ |e| e.even? }
# Return true
{% endhighlight %}

***any?***
集合内有一个满足条件就返回true,代码同all

***each_with_index***
在遍历的时候可以给出元素的下标位置
{% highlight ruby %}
['a', 'b', 'c'].each_with_index do |e, i|
    # Do something
end

['a', 'b', 'c'].map.with_index do |e, i|
    # Do something
end
{% endhighlight %}

还有的其他用法，类似while for loop until太简单了就不用说了
