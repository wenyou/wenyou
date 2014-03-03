---
layout: post
title: json_encode不能处理中文或中文乱码解决方案
description: "json_encode不能处理中文或中文乱码解决方案"
category: php
tags: [json,中文乱码]
---
###json_encode不能处理中文或中文乱码解决方案###

<p>php调用json_encode时，如果有中文，则为生成null，中文无法转换，不能生成json格式的字符串。</p>

如果确定所有的中文都用一个编码格式如：gb2312则可以用以下解决方案：

	<?php

	foreach ($data_list as $key=>$val)
	{
		$data_list[$key]['name']    = urlencode(iconv(‘gb2312′,’utf-8′,		$val['name']));
	}
	echo json_encode($data_list);

	?>

客户端js处理：

	var data=eval(json);
	var html = ‘<select>’;
	$.each(data, function(k)
	{
		html = ‘<option value=”‘+data[k]['id']+’”>’+decodeURIComponent/		decodeURI(json[k]['name'])+’</option>’;
	});
	html  =”</select>”;

就可以了。

<p>但是如果，数据库/数组里的中文编码不统一，有多种编码utf-8,gbk,gb2312都有，或者原始数据本身就有乱码。上面的方法就行不通了。</p>

可以用下面这种方案，例如我给公司做审计系统的方案：

	foreach($audit_http_list as $k=>$v){
		$audit_http_list[$k]['title'] = urlencode($v['title']);
		$audit_http_list[$k]['url'] = urlencode($v['url']);
	}

这里只需把含有中文的地方urlencode一下,不管它有没有乱码还是什么编码。

<p>然后json_encode 一下：</p>

	$data_json = json_encode(array($pages,$list))；

最后再urldecode一下：

	echo urldecode($data_json);

客户端，就不需要decodeURI了。

js:

	$.get(uri, function(json){
		var data = eval(json);
		$(‘#content_list’).html(data[1]);
		$(‘#pages’).html(data[0]);
	});