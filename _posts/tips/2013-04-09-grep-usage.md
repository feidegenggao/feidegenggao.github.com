---
layout: post
title: grep的用法简介
category: tips
description: 2013-04-09 展示grep的简单基本用法
---

# [{{page.title}}][self]
2013-04-09 by {{site.author_info}}

[self]: {{page.url}} ({{page.title}})

##0、grep是什么？
grep是一个用于用于纯文本搜索的工具。grep搜索时时基于行匹配，意思是只要某行中有符合查询条件的字符出现，grep就会把该行的内容打印出来。

##1、基本用法
grep \[-acinv\] \[\-\-(两个中划线，中间无空格)color=auto\] 'keywords' filename，例如：

	#grep 'title' 2013-04-09-grep-usage.md 
	title: grep
	page.title
	this.title

-a ： 将binary文件当做纯文本来搜索  
-c ： 计算找到搜索字符串的次数  
-i ： ignore，忽略大小写的不同  
-n ： 顺便打印出行号  
-v ： 反向选择，打印出没有搜索字符串的行  
--color=auto ： 显示搜索结果时，高亮搜索字符串。你可以在你的.bashrc文件里添加：`alias grep='grep --color=auto'`

##2、进阶用法
grep \[-A\] \[-B\] \[\-\-color=auto\] '搜索字符串' filename  
-A ： 后跟数字n，A意思是after。就是指显示匹配行之后的n行  
-B ： 后跟数字n，B意思是before。就是指显示匹配行之前的n行  
举个栗子：

	 #ifconfig | grep 'lo' -A 2 -B 3  
结果如下：
![grepAB](/images/tips/2013-04-09-grep-usage/grepAB.PNG)  
如何查找多个文件？就在filename处替换成多个文件名即可，比如`grep 'class' *.cpp *.h`即可。  
如何递归查找本目录？`grep 'class' -r .`  


***
**相信水滴石穿的力量！**

[beiyuu]: http://beiyuu.com/ "BeiYuu"
