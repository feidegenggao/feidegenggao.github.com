---
layout: post
title: 我的第一篇博客
category: blog
description: 2012-12-29 这是我在github的博客上的第一篇博客。展示各种排版格式的使用方法
---

# [{{page.title}}][self]
2012-12-29 by {{site.author_info}}

[self]: {{page.url}} ({{page.title}})

##0、感谢
首先，我要感谢，在我搭建Github博客过程中帮助过我的人。

* 我是从我的好友[Smartegg][]处听说Github可以搭建博客的。
* [阮一峰][ruanyifeng]的博客是我看到的第一篇搭建的过程简介。我按照他的指导，
成功搭建了一个简易的博客。
* [BeiYuu][]美观雅致、简洁好用的style深深吸引了我。于是我直接fork了他的模板。谢谢！

##1、显示代码
我迫不及待的要贴上一段helloworld。测试一下代码显示功能如何。

    #include    <stdio.h>
    int main(void)
    {
        printf("Hello world!\n");
        return 0;
    }

##2、插入一张图片
感谢您的关注，我的Email:

![Higher email](/images/myemail.gif)

##3、结语
###3.1不要迷茫，不要彷徨。
###3.2敢问路在何方？路在脚下。


##Tips:
###在本博客中如何添加新的栏目?
比如，我想在此基础上增加C/C++栏目如何操作？

* 首先，切换到该博客的根目录，新建cplusplus.md，模仿现存的栏目md撰写新的md文档。
本步骤，是在根目录新建文件，之后更改两个地方：title更改为cplusplus，第7行的循环
策略的时候更改为cplusplus。

* 之后，在_layouts/page.html中的`<div class="nav right">`
容器内在你想的位置添加如下内容：`<a href="/cplusplus" title="C/C++">C/C++</a>`

* 最后，在_posts目录下新建cplusplus文件夹，从旧的栏目中拷贝template.md到本目录。修改
template.md。仅需修改一处：category: 为category: cplusplus（第4行）

*总结一下，新加本栏目后的git状态如下：

    #modified:   _layouts/page.html
    #new file:   _posts/cplusplus/template.md
    #new file:   cplusplus.md

***
**相信水滴石穿的力量！**

[smartegg]: http://smartegg.github.com/ "My friend, Smartegg"
[ruanyifeng]: http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html "搭建Github博客"
[beiyuu]: http://beiyuu.com/ "BeiYuu"
