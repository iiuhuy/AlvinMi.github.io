---
title: strstr 函数的用法
date: 2017-11-10 13:05:47
tags: C/C++
---

>  阅读本文大约需要 2.8 分钟。

# 简介 

关于一个 C 语言字符串查找的函数。在 **「 C 和指针 」** 中有提到子串查找的问题。

## 01 strstr 函数原型

在 C 标准库中有模板, 即  `strstr` 函数, 其原型应该是 

	char*strstr(const char*s1,const char* s2);

我在 `keil` 开发环境下 `string.h` 头文件里面找到的是如下图的声明, 只是提供了一个 `_ARMABI` 接口。


![strstr](https://i.imgur.com/n57v8Ne.png)

这个函数的作用就是在 s1 中查找子串 s2 , 如果找到, 则返回 s1 中 s2 的位置, 否则返回 NULL。

于是上网查询了下, 才知道这涉及了字符匹配算法。而字符匹配算法中最常用的就是 KMP 算法。 关于 KMP 算法可以看看 `Matrix67` 的这篇 [KMP 算法详解](http://www.matrix67.com/blog/archives/115) 介绍。

## 02 strstr 函数简单例程

从字串 `string1 one_string string2 two_` 中寻找 `yyy`

	#include <stdio.h>  
	#include <conio.h>  
	#include <string.h>  
	int main(void)  
	{  
	    char *s="string1 onexxx string2 oneyyy";  
	    char *p;  
	    p=strstr(s,"string2");  
	    printf("%s\n",p);  
	    if (p==NULL)  
	    {  
	        printf("Not Found!\n");  
	    }  
	    p=strstr(p,"one");  
	    printf("%s\n",p);  
	    if (p==NULL)  
	    {  
	        printf("Not Found!\n");  
	    }  
	    p+=strlen("one");  
	    printf("%s\n",p);  
	  
	    getch();  
	    return 0;  
	}  


这个函数, 在解析一些数据, 例如 GPS 报文解析的时候, 还是挺常用的。 