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

	/*
	 代理商子网站处理
	 DOMAIN代理商二级域名前缀 GE: coca
	 BASEDOMAIN 网站真实域名，不带www.  EG: asia.com
	 SITEDOMAIN 访问时网站地址，可能是二级域名，可以为： *.asia.com或www.asia.com或asia.com
	 代理商子网站二级域名组合形式如下： coca.asia.com
	*/
	$site_url = $_SERVER['HTTP_HOST'];
	$site_url = explode('.',$site_url);
	if(count($site_url)<3)
	{
		define('DOMAIN','www');
		define('SITEDOMAIN',$_SERVER['HTTP_HOST']);
		define('BASEDOMAIN',SITEDOMAIN);
	}
	else
	{
		define('DOMAIN',$site_url[0]);
		if(DOMAIN == 'www')
		{
			define('SITEDOMAIN',$_SERVER['HTTP_HOST']);
			define('BASEDOMAIN',str_replace('www.','',SITEDOMAIN));
		}
		else
		{
			define('BASEDOMAIN',str_replace(array(DOMAIN.'.',DOMAIN),array('',''),$_SERVER['HTTP_HOST']));
			define('SITEDOMAIN',DOMAIN.'.'.BASEDOMAIN);
		}
	}