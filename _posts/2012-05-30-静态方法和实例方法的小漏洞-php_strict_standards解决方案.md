---
layout: post
title: 静态方法和实例方法的小漏洞-PHP Strict Standards解决方案
description: "静态方法和实例方法的小漏洞-PHP Strict Standards解决方案"
category: php
tags: [php静态方法]
---
###静态方法和实例方法的小漏洞-PHP Strict Standards解决方案###

- php报错：Strict Standards: Non-static method request::set() should not be called statically。

原因：
php5.3+开始执行严格错误检查，并且继承类必须在父类以后定义
解决方法如下 :

	error_reporting(E_ALL & ~(E_STRICT | E_NOTICE));

静态方法和实例方法的小漏洞

<p>原文出处：深入理解PHP内核http://www.php-internal.com/book/?p=chapt05/05-02-class-member-variables-and-methods</p>

<p>细心的读者应该注意到前面提到静态方法和实例方法都是保存在类结构体 zend_class_entry.function_table中，那这样的话， Zend引擎在调用的时候是怎么区分这两类方法的，比如我们静态调用实例方法或者实例调用静态方法会怎么样呢？</p>

<p>可能一般人不会这么做，不过笔者有一次错误的这样调用了，而代码没有出现任何问题，在review代码的时候意外发现笔者像实例方法那样调用的静态方法，而什么问题都没有发生(没有报错)。在理论上这种情况是不应发生的，类似这这样的情况在PHP中是非常的多的，例如前面提到的create_function方法返回的伪匿名方法，后面介绍访问控制时还会介绍访问控制的一些瑕疵，PHP在现实中通常采用Quick and Dirty的方式来实现功能和解决问题，这一点和Ruby完整的面向对象形成鲜明的对比。</p>
我们先看一个例子：

	error_reporting(E_ALL);
	class A {
		public static function staticFunc() {
			echo "static";
		}
		public function instanceFunc() {
			echo "instance";
		}
	}
	A::instanceFunc(); // instance
	$a = new A();
	$a ->staticFunc(); // static

<p>上面的代码静态的调用了实例方法，程序输出了instance，实例调用静态方法也会正确输出static，这说明这两种方法本质上并没有却别。唯一不同的是他们被调用的上下文环境，例如通过实例方法调用方法则上下文中将会有$this这个特殊变量，而在静态调用中将无法使用$this变量。</p>

<p>不过实际上Zend引擎是考虑过这个问题的，将error_reporting的级别增加E_STRICT，将会出出现E_STRICT错误:</p>

	Strict Standards: Non-static method A::instanceFunc() should not be called statically

<p>这只是不建议将实例方法静态调用，而对于实例调用静态方法没有出现E_STRICT错误，有人说：某些事情可以做并不代表我们要这样做。</p>

<p>PHP在实现新功能时通常采用渐进的方式，保证兼容性，在具体实现上通常采用打补丁的方式，这样就造成有些”边界“情况没有照顾到。</p>