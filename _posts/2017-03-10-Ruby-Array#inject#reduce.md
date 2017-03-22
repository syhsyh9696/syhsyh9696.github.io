---
layout: post
title:  "Ruby Array#inject#reduce"
date: 2017-03-10 1:00:00
image: ''
tags:
- Ruby
description: ''
categories:
- Ruby notes
---

**Array#inject#reduce其实是一回事**
---

其实reduce是一个inject的别名，两者的能实现一样的功能，但我觉得reduce更好理解一些。

这两个方法在[Leetcode 17](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)
里可以用到，具体的实现方法(我更喜欢reduce这个叫法)
{% highlight ruby %}
# encoding:utf-8
# @param {String} digits
# @return {String[]}
def letter_combinations(digits)
    ar = []
    ar[2] = ['a', 'b', 'c']
    ar[3] = ['d', 'e', 'f']
    ar[4] = ['g', 'h', 'i']
    ar[5] = ['j', 'k', 'l']
    ar[6] = ['m', 'n', 'o']
    ar[7] = ['p', 'q', 'r', 's']
    ar[8] = ['t', 'u', 'v']
    ar[9] = ['w', 'x', 'y', 'z']

    return [] if digits.size == 0
    return ar[digits.to_i] if digits.size == 1

    letters = []
    digits.chars.each do |i|
        letters << ar[i.to_i]
    end
    letters.reduce(&:product).map(&:join)
end
{% endhighlight %}

有了Array#reduce这个方法，可以方便的对多层嵌套的数组或者一些混合的数据结构进行处理(hash table)

Demonstration
{% highlight ruby %}
# 未指定开始值时，默认第一个为初始值
(1..10).reduce(:+)
(1..10).reduce { |sum, n| sum + n }

# 指定开始值
(1..10).reduce(1, :+)
{% endhighlight %}

当然reduce后面可以跟着很多别的方法，比如17题中的product方法，merge方法等等。
合理的利用可以明显的减少代码量，excited！
