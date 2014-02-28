---
layout: post
title: 分析 ecshop 里的$GLOBALS
---
###分析 ecshop 里的$GLOBALS###
<p>搞ec二次开发 或研究ec的一些网友 经常在论坛里提到 $GLOBALS['db']; $GLOBALS['ecs'];在哪定义的等帖子。 下来就$GLOBALS我说一点：</p>
<p>想搞明白的朋友 执行 这段代码</p>
代码:
<pre><code>
&lt;?php
$xaphp = ‘合肥php服务中心’;
echo $GLOBALS['xaphp'];
?&gt;
</code></pre>
<p>浏览器当然会打印出  西安php服务中心  这就是 $GLOBALS的作用  “就像大部份的结构化程序，有所谓的全局变量与局部变量，PHP  在这方面也是有相同的处理方式。</p>

<p>在  PHP  的程序执行时，系统会在内存中保留一块全局变量的区域。实际运用时，可以透过  $GLOBALS["变量名称"]  将需要的变量取出。在用户自定的函数或程序中，就可以用  $GLOBALS  数组取出需要的变量”</p>
<p>在ec里 大家打开 init.php 会看到</p>
代码:
<pre><code>
$db = new cls_mysql($db_host, $db_user, $db_pass, $db_name);
</code></pre>
<p>定义了这样的类  顾名思义 $GLOBALS['db']</p>
<p>搞ec二次开发 或研究ec的一些网友 经常在论坛里提到 $GLOBALS['db']; $GLOBALS['ecs'];在那定义的等帖子。 下来就$GLOBALS我说一点：</p>
<p>想搞明白的朋友 执行 这段代码</p>
代码:
<pre><code>&lt;?php
$xaphp = ‘西安php服务中心’;
echo $GLOBALS['xaphp'];
?&gt;
</code></pre>
<p>浏览器当然会打印出  西安php服务中心  这就是 $GLOBALS的作用  “就像大部份的结构化程序，有所谓的全局变量与局部变量，PHP  在这方面也是有相同的处理方式。  在  PHP  的程序执行时，系统会在内存中保留一块全局变量的区域。实际运用时，可以透过  $GLOBALS["变量名称"]  将需要的变量取出。在用户自定的函数或程序中，就可以用  $GLOBALS  数组取出需要的变量”</p>
<p>在ec里 大家打开 init.php 会看到</p>
代码:
<pre><code>$db = new cls_mysql($db_host, $db_user, $db_pass, $db_name);</code></pre>
<p>定义了这样的类  顾名思义 $GLOBALS['db']</p>
