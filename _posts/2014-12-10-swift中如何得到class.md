---
layout: post
title: swift中如何得到class
---

因为RestKit中需要传入class参数，可OC中NSObject的class在swift是没有的，那么去哪了呢？原来swift文档中有：


{% highlight swift %}
SomeClass.self
SomeInstance.dynamicType

{% endhighlight %}

* .self相当于原来的
* .class.dynamicType只有在运行时有效

和.self相比，应该是在运行时显示在继承体系中的不同类型：一个是实际类型，一个是“当时”的类型？

有时间再测试了...
