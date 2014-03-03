---
layout: post
title: PHP&Apache泛域名应用
description: "PHP&Apache泛域名应用"
category: web
tags: [php,apache,泛域名]
---
###PHP&Apache泛域名应用###

以Windows开发环境
1、windows 下的 hosts文件

	127.0.0.1    asia.t
	127.0.0.1    *.asia.t
	127.0.0.1    www.asia.t
	127.0.0.1    coca.asia.t
2、apache 下的 httpd-vhosts.conf文件

	<VirtualHost *:80>
		DocumentRoot E:\www\asia\www
		ServerName *.asia.t
		ServerAlias *.asia.t
	</VirtualHost>
3、php处理

	