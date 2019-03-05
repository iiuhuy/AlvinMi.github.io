---
layout: post
title: Python基础如何学习Java[01]之从「Hello World」开始
category: 技术
tags: Java
keywords: Python, Java
description:
published: true
---

###Python 版本

适用于 Python 2：

```
#!/usr/bin/env python
print "Hello, world!"
```

适用于 Python 3：（print 变成了一个函数）

```
#!/usr/bin/env python
print("Hello, world!")
```

###Java 版本

```java
public class Hello{
    public static void main(String[] args){
        System.out.println("Hello, world!");
    }
}
```

##Java 程序的解析
第一行`public class Hello`

- `public`表示这个程序可以被任何人调用
- `class`表示定义的文件是一个 class(类)
- `Hello`是这个 class 的名字（名字取定以后保存的文件名一定要与这个 class 的名字相同）
- `.java`表示这个文件是一个 java 类型的文件

第 2 行`public static void main(String[] args)`，这是固定的用法：

- main 表示这是 java 程序的入口,编译器通过找到 main 来进入程序。

第 3 行`System.out.println("Hello world");`

- 这句话表示向系统输出一句话并换行,输出的内容是`" "`中间包含的内容,本行最后的`;`表示本段代码的结束．
- `System.out.println()`方法可以不包含任何参数,如果直接使用`System.out.println();`则系统会自动换行．
- 注意 JAVA 语言的每段代码都是以`;`结束,如果执行完功能而没有`;`系统会报出错误．

注意到其中的两对`{ }`,`{ }`总是成对出现的,用来确定其的管辖范围.

我们可以把程序看成这样：

`public class Hello{ }`的这个`{ }`中间包含的信息属于这个叫`Hello`的 class,那么它包含什么信息呢?

`public static void main(String[] args){ }`就是它所包含的信息,而这个`main()`方法也有它自己的信息包含在它的`{ }`中．

它包含的内容就是`System.out.println("Hello world");`

打个通俗的比喻,我们定义了一个叫图书馆的房子,图书馆里面有书柜,书柜里有书,那么用这个例子来解释上面的程序:

```
公共的 房子 图书馆 {
	公共的 不动的 主柜子(编号){
		书(雪山飞狐);
		书(JAVA入门);
     }
}
```

###Ruby 版本

```ruby
#!/usr/bin/ruby
puts "Hello, world!"
```
