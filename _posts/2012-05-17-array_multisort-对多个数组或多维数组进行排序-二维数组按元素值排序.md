---
layout: post
title: array_multisort-对多个数组或多维数组进行排序-二维数组按元素值排序
description: "array_multisort-对多个数组或多维数组进行排序-二维数组按元素值排序"
category: php
tags: [array_multisort,数组排序]
---
###array_multisort-对多个数组或多维数组进行排序-二维数组按元素值排序###

- array_multisort()php函数库自带的方法。用于对多个数组或多维数组进行排序。
php官方网址为：http://cn.php.net/manual/zh/function.array-multisort.php

我的应用为，有一个二维数组，我要按照其中二个元素的值的大小，把这个二维数组中的第一维从大到小排序。

	$all_list = array_merge((array)$this->dbo->query($sql_1),(array)$this->dbo->query($sql_2));
	foreach ($all_list as $key => $row) {
		$all_list[$key]['packets'] = round($row['ps_orgin']+$row['ps_reply'],0);
		$all_list[$key]['bs_orgin'] = $row['bs_orgin'] + $row['bs_reply'];
		$packets[$key] = $all_list[$key]['packets'];
		$bs_orgin[$key] = $all_list[$key]['bs_orgin'];
		unset($all_list[$key]['bs_reply']);
		unset($all_list[$key]['ps_orgin']);
		unset($all_list[$key]['ps_reply']);
	}
	array_multisort($bs_orgin, SORT_DESC, $packets, SORT_DESC, $all_list);

更多用法见：http://cn.php.net/manual/zh/function.array-multisort.php