---
layout: post
title: php中ini_set函数使用方法
description: "php中ini_set函数使用方法"
category: php
tags: [php,ini_set]
---
###php中ini_set函数使用方法###

- ini_set是php自带的用来设置php.ini配置文件的函数。

- 语法:ini_set(“选项”,”值”)
- 该函数用时最好放到php的脚本最头部
- 比如:
- ini_set(”max_execution_time”, ”180”);
- 设置php的脚本超时时间为180秒 php程序员站
- ini_set(“asp_tags”,”On”) www~phperz~com
- 打开asp脚本标记的支持 比如：<% echo “aaa”%>
- ini_set(“display_errors”,”On”)
- 打脚本错误信息
- 等等