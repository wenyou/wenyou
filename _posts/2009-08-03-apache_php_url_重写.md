---
layout: post
title: Apache&php&URL重写
description: "url重写一例"
category: web
tags: [url重写,apache,php]
---
###Apache php URL 重写###

1、LoadModule rewrite_module modules/mod_rewrite.so 启动（将前面的#去了）
2、修改：

	<Directory />
		Options FollowSymLinks
		AllowOverride All
		Order deny,allow
		Deny from all
	</Directory>
	
AllowOverride none 改为 All