---
layout: post
title: "object_getClass(obj)和[NSObject class]的区别"
---

先对比文档原文:

object_getClass: Returns the class of an object.

NSObject class: Returns the class object.

一组对比示例：

{% highlight Objective-C%}
Class obj = [NSObject class];
Class cls = object_getClass(obj);
Class cls2 = [obj class];
NSLog(@"%p",cls);  // 0x7fff75f56840
NSLog(@"%p",cls2); // 0x7fff75f56868
{% endhighlight %}

当obj为‘类’的类对象时，两者返回不同的对象，一个是类对象（class object），一个是元类（meta class）即类对象的类（the class of the class）

{% highlight Objective-C%}
NSObject *obj = [NSObject new];
Class cls = object_getClass(obj);
Class cls2 = [obj class];
NSLog(@"%p",cls);  // 0x7fff75f56840
NSLog(@"%p",cls2); // 0x7fff75f56840
{% endhighlight %}

当obj为普通对象实例时，两者返回相同的对象——类对象（class object）

![Class关系图](/images/cocoa_class_hier.png)

由上图对象类的class isa指针图例，可以看出，object_getClass总是返回class isa指针，而[NSObject class]总是返回类对象，如果自己是类对象则返回自己。
