---
layout: post
title: PHP Filter 函数 – 严格控制输入的数据格式 – 防XSS
description: "PHP Filter 函数 – 严格控制输入的数据格式 – 防XSS"
category: php
tags: [php filter,防XSS]
---
###PHP Filter 函数 – 严格控制输入的数据格式 – 防XSS###

- PHP 过滤器用于对来自非安全来源的数据（比如用户输入）进行验证和过滤。
- filter 函数是 PHP 核心的组成部分。无需安装即可使用这些函数。
- 把表单里的值封装成严格的数据格式匹配入库，从输入就杜绝XSS，举个例子，表单里只让填EMAIL格式的字符串，什么时候允许让进< >‘ “这样的字符了。