---
layout: post
title: IOS开发笔记(-)之Objective-C
description: IOS开发笔记(-)之Objective-C
category: ios
tags: [ios,objc,Objective-C,mac]
---
##IOS开发笔记(-)之Objective-C##

###问题与错误处理###

__1. ARC 与 内存管理__

```
	
	ARC forbids explicit message send of release/retainCount/retain...  -关闭xCode项目的ARC设置
	
	遇到 ARC forbids explicit message send of 'release'
	'release' is unavailable: not available in automatic reference counting mode
	类似这样的问题。
	
	错误原因：因为我们设置了用ARC来管理内存释放，我们却又调用了release方法去释放对象。
	
	ARC是什么？
	
	ARC是iOS 5推出的新功能，全称叫 ARC(Automatic Reference Counting)。简单地说，就是代码中自动加入了retain/release，原先需要手动添加的用来处理内存管理的引用计数的代码可以自动地由编译器完成了。该机制在 iOS 5/ Mac OS X 10.7 开始导入，利用 Xcode4.2 可以使用该机制。简单地理解ARC，就是通过指定的语法，让编译器(LLVM 3.0)在编译代码时，自动生成实例的引用计数管理部分代码。有一点，ARC并不是GC，它只是一种代码静态分析（Static Analyzer）工具。
	
	解决方法：
	选中项目=>Build Phases=>Compile Sources，设置Compiler Flags为：-fno-objc-arc
	或者：工程-->"Build Settings"-->找到Objective-C Automatic Reference Counting项-->将它的值设置为NO。
	
	详细参考：http://blog.sina.com.cn/s/blog_7b9d64af01019rqt.html
	         http://www.myexception.cn/mobile/1450680.html
	         
	
	遇到 ARC forbids explicit message send of 'retainCount'
	从字面上来解释就是，arc 禁止显示发送retain消息。
	其实就是使用ARC之后，不允许直接调用retain, release, autorelease, dealloc, retainCount这些方法了，编译器会在合适的地方将这些代码添加进去，解决这样的问题只需要删除与手动管理内存相关的代码（一般就是报错的代码）即可。
	解决步骤：打开当前工程，打开"Build Settings"，找到Objective-C Automatic Reference Counting项，将它的值设置为NO。
```


