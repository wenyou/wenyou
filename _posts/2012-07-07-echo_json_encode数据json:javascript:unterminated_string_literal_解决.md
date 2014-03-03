---
layout: post
title: json_encode数据json/javascript:unterminated string literal 解决
description: "echo json_encode数据json/javascript:unterminated string literal 解决"
category: php
tags: [php,json]
---
###echo json_encode数据json/javascript:unterminated string literal 解决###


unterminated string literal，js输出数据库中的数据

用Js输出从数据库中读取出的文本时，出错提示unterminated string literal，主要是因为js里输出里包含了\n。解决办法是先将数据通过以下方式去掉\n，然后再传值给js.

例如：

	$audit_http_list = $this->dbo->query($sql);

	ob_start();
	include template(‘listhttp’,STK_M,”,false);
	$list = ob_get_contents();
	ob_end_clean();
	echo str_replace(array(‘\n’,'\t’,'\r’), ”,json_encode(array($pages,$list)));