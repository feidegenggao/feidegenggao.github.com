---
layout: post
title: Android JNI 开发--准备篇
category: cplusplus 
description: 2013-05-21 Android JNI 开发前的准备工作
---

# [{{page.title}}][self]
2013-05-21 by {{site.author_info}}

[self]: {{page.url}} ({{page.title}})

##0、起因
我为什么要写这篇文章？

最近，我们教研室计划把之前做的C/C++程序移植到安卓上去。于是，我们就开始着手开始工作。
途中遇到的问题真是多，有些问题是始料未及的，也有些问题是很基础的，由于首次接触所以
还是绕了一些远路，我这篇文章就是想记下、分析这些问题，并给出解决方案。


##1、开发环境
Win7 旗舰版 32 位 + Eclipse SDK 3.7.2（由于使用Win7下的Eclipse，所以就以Win7为主要开发环境了）

Ubuntu 12.04.1 LTS 32 位 + android-ndk-r8e（Ubuntu的主要作用是NDK编译，要不然还得在Windows下安装cygwin）


##2、使用方法
本节主要讲述，这些个工具怎么使用？Win7就不用说怎么使用了。:)假设，你已经学会了如何新建
Android版的HelloWorld工程。

###2.1、Adb

本小节的内容在Win7下运行。

有时候，我们需要查看Android设备内部的状态，比如我当前是否打开了8080端口，我想杀死
某个进程。我们需要借用一种工具就是Adb。

开发的安卓机器可以通过数据线也可以通过Wifi进行Adb连接，Adb的全称是：Asian Development Bank
开玩笑的，Adb的全称是：Android Debug Bridge，是一个命令行的工具，可以让你连接到Android设备。
连接后，打开的是一个精简的linux shell。包含一些基础的命令工具。

* 数据线连接：数据线连接在Win7下，打开Cmd窗口即可。输入命令：adb devices查看当前设备的状态
可能会提示`'adb' 不是内部或外部命令，也不是可运行的程序或批处理文件。`这是因为你没有吧Adb.exe
所在目录放到环境变量中。

* Wifi连接：有一个工具叫ADBWifi可以通过wifi连接。

常用的Adb命令：

* adb devices

* adb shell

* adb install *.apk

* adb unistall *.apk

* adb push LocalFilePath RemotePath

* adb push RemoteFilePath LocalPath


###2.2、NDK
本小节的内容在Ubuntu下运行。

编译C/C++的代码到安卓上，得借用这个工具。但，NDK能帮你的不只是这些... ...

我在下一节结合JNI举一个详细的例子说明NDK是如何帮助我们工作的。


***
**相信水滴石穿的力量！**
