---
layout: post
title: "Ruby Block"
date: 2017-03-27 22:46:50 +0800
categories:
tags:
- Ruby
categories:
- Ruby notes
---

**Ruby Blocks**

代码块在Ruby中也是可以传递的，这很tricky，比如
{% highlight ruby %}
def test_method(a, b)
	a + yield(a, b)
end

test_method(2, 3) { |x, y| x + y }    # => 7
{% endhighlight %}
当然可以询问当前的方法调用是否包含块，可以通过方法Kernel#block_given?方法得到

**Scope**

***代码块是闭包***

代码块可以偷偷的吧变量带出原来的作用域。
可以运行的代码由两部分组成:代码和一组绑定，绑定在代码块结束的时候就消失了，
基于这种特性，代码块被称为闭包，就是说，代码块可以获取局部绑定并一直带着他们。

跟Java那些语言不同的是，Ruby并没有内部作用域(inner scope)或者外部作用域(outer scope)
这种概念，Ruby的作用域并不是嵌套的而是截然分开的，一旦进入到一个新的作用域中，
整组绑定都会被替换掉，比如
{% highlight ruby %}
class MyClassnn
    v2 = 2				
	local_variables		# => [:v2]
	def my_method
		v3 = 3
		local_variables
	end
	local_variables		# => [:v2]
end

obj = MyClass.new 
obj.my_method			# => [:v3]
obj.my_method			# => [:v3]
local_variables			# => [:v1, :obj]
{% endhighlight %}
这就意味着一旦进入到class的定义当中，v1就落在作用域范围之外，从而变得不可见了。
并且在调用my_method过程中，两个v3是完全不同的。
这就说明了，无论何时切换了作用域，有些绑定会被新的绑定所取代，
当然并不是对所有的绑定都是这样。

**Scope Gate**

程序会在三个地方关闭前一个作用域，同时打开一个新作用域
- 类定义
- 模块定义
- 方法

因此用class, module, def关键字作为标记，每个关键字都对应一个作用域门。

**Flattening the Scope**

比如下面的
{% highlight ruby%}
my_var = "test"
class MyClass
        # 希望这里打印my_var

	def my_method
		# 希望在这里打印my_var
	end
end
{% endhighlight %}
因为是类的定义，my_var并不能穿越，只有将class关键字替换某个
非作用域门的东西，比如方法调用才有可能获得my_var的值。

Ruby的文档中，Class.new是class的完美替身。用代码块传递
给Class.new，还不是美滋滋，真OO无双
{% highlight ruby %}
my_var = "test"
MyClass = Class.new do
	# my_var在这里可见
	p my_var

	def my_method
		# 暂时在这里不可见的my_var
	end
end
{% endhighlight %}
居然还不到my_method，都是def的锅，换!
{% highlight ruby %}
my_var = "test"
MyClass = Class.new do
	p my_var

	define_method :my_mythod 
		"#{my_var} in the method"
	end
end
{% endhighlight %}
诚心默念动态方法大法好(逃

好了扁平作用域见过了，如果想在方法间共享变量又不想其他方法访问，
就可以把这些方法定义在变量的扁平作用域中，这次来用动态派发
{% highlight ruby %}
def define_method
	share = 0

	Kernel.send :define_method, :function_f do
		share
	end

	Kernel.send :define_method, :function_s do
		share += 1
	end
end
define_method
{% endhighlight%}
share这个变量被层层的作用域门保护着，所以这个方法叫做共享作用域。

所以今天先到这里吧(逃
