---
layout: post
title: 可重入和线程安全
category: netProgram
description: 2013-04-18 可重入函数和线程安全的区别以及我自己的思考
---

# [{{page.title}}][self]
2013-04-18 by {{site.author_info}}

[self]: {{page.url}} ({{page.title}})

##0、起因
两三天前，我在写一个类，大致功能是：fork一些子进程，之后在收到kill子进程指令后，kill掉子进程。显然我要捕捉SIGCHLD信号。代码如下：

	void sig_child(int signo)
	{
		...
		while (-1 == (pid = waitpid(-1, &stat, WNOHANG)))
		{
			NFO_LOG("child %d terminated\n", pid);
		}
		...
	}

多次、大量fork进程，kill进程后，程序会进入睡眠状态。 

##1、定位问题  

ps -elf 打印结果进程的WCHAN列显示：futex_。查找[stackoverflow][futex_mean]才明白程序是死锁了。于是开始GDB调试，由于这种情况很容易出现，所以很容易我就找到了问题的根源。进程睡眠到了INFO\_LOG了。就是while循环内部的话。INFO\_LOG是一个日志类中一个方法，具体睡眠到的函数是：locltime\_r。  
[futex_mean]: http://stackoverflow.com/questions/9581732/what-does-mean-futex
这个时候翻看《环境编程》查看到这个函数是可重入的。仔细看了一遍才明白，可重入是对两种情况而言：
>如果一个函数对多个线程说是可重入的，则说这个函数是线程安全的，但这并不能说明对信号处理函数也是可重入的。  
>如果一个函数对异步信号处理程序的重入是安全的，则说这个函数是异步-信号安全的。

哦，这个时候，我明白了localtime\_r是可重入的，所以末尾有一个\_r后缀，但，这个可重入是对多线程而言的。并没有人告诉我\_r结尾的函数localtime\_r也是异步-信号安全的。那他们有什么联系呢？  

##2、可重入

如果一个函数f在执行期间被中断，在中断处理过程中依旧可以安全的调用f则f可称为是可重入的。也称为是异步信号安全。
  
哪一种情况才会导致函数不可重入呢？  
函数有以下行为会导致不可重入：  

>* 含有静态（全局）非常量数据   
>* 返回静态（全局）非常量数据的地址   
>* 依赖于单实例模式的资源锁  
>* 调用了不可重入的函数   


举个例子：
	
	//不安全的版本
	int temp_g;
	int f(int i)
	{
		temp_g = i + 1;
		return temp_g;
	}

	int  g(void)
	{
		int i = 0;
		f(i);
	}

这两个函数f和g都不是可重入的，进行如下改动后就是可重入的了。

	//可重入版本
	int f(int i)
	{
		i++;
		return temp_g;
	}

	int  g(void)
	{
		int i = 0;
		f(i);
	}

##3、线程安全

这种比较好理解就是说，对资源的访问互斥的访问即可，即使你使用了全局变量，即使你使用了静态数据。对不安全的版本进行如下修改即可满足线程安全：

	//线程安全版本
	int temp_g;
	int f(int i)
	{
		pthread_mutex_lock(&mutex);
		temp_g = i + 1;
		int temp_auto = temp_g;
		pthread_mutex_unlock(&mutex);
		return temp_auto;
	}

	int  g(void)
	{
		int i = 0;
		f(i);
	}
##4、二者的关系

可重入是在单线程环境下被引入的，而线程安全是在多线程环境下引入的概念。

###4.1、可重入的不能保证是线程安全的
虽说大部分情况下，可重入可以保证线程安全，但例外也是存在的，比如：

	int g;
	
	void swap(int* x, int* y)
	{
		int t;
		t = g;
		
		g = *x;
		*x = *y;
		//中断发生处
		*y = g;

		g = t;
	}

`swap(int*, int*)`是可重入的，因为我们每次调用swap时都把全局变量g保存到当前栈上。在swap的最后一句话又恢复了全变量g的值。  
但是，当两个线程并行执行到`*x = *y;`这句话时，如果从此刻到第二个线程执行完swap前，第一个线程并未执行，则第一个线程执行swap则不会得到期望的结果，所以这不是线程安全的。

###4.2、线程安全的程序也没有必要是可重入的
第三节的那个例子就可以很好地说明问题。这个线程安全版本满足了线程安全，但是却不是可重入的。为什么呢？假设f(int)执行到了pthread\_mutex\_lock时重入f(int)会发生进程的死锁，就像我一开始遇到的那个问题。

##5、结论
所以，我们得出结论**可重入的不能保证是线程安全的，线程安全不能保证是可重入的。**  



***
**相信水滴石穿的力量！**

[wiki]: http://zh.wikipedia.org/wiki/%E5%8F%AF%E9%87%8D%E5%85%A5
