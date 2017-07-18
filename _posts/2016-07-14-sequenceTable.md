---
bg: "tools.jpg"
layout: post
title:  "使用JS模拟顺序表"
crawlertitle: "使用JS模拟顺序表"
summary: "使用JS模拟顺序表"
date:   2017-07-18 14:09:47 +0800
categories: posts
tags: ['数据结构']
author: LZJ
---
顺序表是在计算机内存中以数组的形式保存的线性表，是指用一组地址连续的存储单元依次存储数据元素的线性结构。线性表采用顺序存储的方式存储就称之为顺序表。顺序表是将表中的结点依次存放在计算机内存中一组地址连续的存储单元中。

顺序表与链表的区别在于

线性表用一段连续的存储单元依次存储线性表的数据元素

链表采用链式存储结构，用一组任意的存储单元存放线性表的元素

若线性表需要频繁查找，很少进行插入和删除操作时，宜采用顺序存储结构。若需要频繁插入和删除时，宜采用单链表结构。

当线性表中的元素个数变化较大或者根本不知道有多大时，最好用单链表结构，这样可以不需要考虑存储空间的大小问题。而如果事先知道线性表的大致长度，用顺序存储结构效率会高很多。


使用JS模拟出链顺序表的结构

JS数组封装的方法可以很方便使用并模拟顺序表操作

<img src="http://liuzejin.top/assets/images/showHow/sequenceTable/1.png" alt="">

{% highlight js %}
	var arr = [];
{% endhighlight %}

<h4>头插法</h4>
<img src="http://liuzejin.top/assets/images/showHow/sequenceTable/2.png" alt="">
{% highlight js %}
// 头插法
// 使用unshift()方法可以方便的像数组头部添加元素

arr.unshift();
{% endhighlight %}

<h4>尾插法</h4>
<img src="http://liuzejin.top/assets/images/showHow/sequenceTable/3.png" alt="">
{% highlight js %}
// 使用push()方法可以方便的像数组头部添加元素
arr.push();
{% endhighlight %}

<h4>指定位置增加元素，删除元素</h4>
<img src="http://liuzejin.top/assets/images/showHow/sequenceTable/4.png" alt="">

<img src="http://liuzejin.top/assets/images/showHow/sequenceTable/5.png" alt="">
{% highlight js %}
// 指定位置增加元素，删除元素
// 使用splice()方法可以非常方便的在指定位置添加元素
// splice()方法需要传入3个参
// splice(index,howmany,item); 
// index参：是必填的,指的是数组中需要被添加或删除的位置
// howmany参：是必填的，指的是在数组中需要被删除的元素数量，如果不删除填0即可
// item参：非必填，指的是要在指定位置加入的参数，可以是多参

 eg: 删除元素 
     arr = [1,2,3,4,5];
     arr.splice(2,1) ==>[3]
     arr = [1,2,4,5];

 eg: 增加元素
 	   arr = [1,2,3,4,5];
 	   arr.splice(2,0,7,7,7);
 	   arr = 1,2,7,7,7,3,4,5

 eg: 同时删除增加元素
 	   arr = [1,2,3,4,5];
 	   arr.splice(2,1,8) ==> [3]
 	   arr = [1,2,8,4,5];
{% endhighlight %}

<h4>删除头部的第一个元素</h4>
<img src="http://liuzejin.top/assets/images/showHow/sequenceTable/6.png" alt="">
{% highlight js %}
// 使用shift()方法可以方便的删除数组第一个元素，并返回
eg: arr = [1,2,3,4];
    arr.shift() ==> 1;
    此时arr = [2,3,4];
{% endhighlight %}

<h4>删除最后的一个元素</h4>
<img src="http://liuzejin.top/assets/images/showHow/sequenceTable/7.png" alt="">
{% highlight js %}
// 使用pop()方法可以方便的删除数组最后一个元素，并返回
eg: arr = [1,2,3,4];
    arr.pop() ==> 4;
    arr = [1,2,3];

{% endhighlight %}

修改指定位置的元素最简单 直接覆盖参数即可
{% highlight js %}
eg: arr = [1,2,3,4,5];
    arr[1] = 8;
    arr = [1,8,3,4,5];
{% endhighlight %}

查找单个参数直接取值就可以
{% highlight js %}
 eg: arr = [1,2,3,4,5];
     arr[1] = 2;
	 注意：超出范围的参数返回的是undeifind 比如arr[-1],arr[10]返回的都是underfind
{% endhighlight %}

<h4>查找多个连续的参数</h4>

可以使用slice()方法

slice(start,end)包含两个参数

start是必须的指的是取值的开始位置 可以为负值 负值就从尾部向头部算值

end是非必填的 指的是取值结尾的位置

{% highlight js %}
eg: arr = [1,2,3,4];
    arr.slice(1,2) ==> [2,3]
    arr.slice(-2,4) ==> [3,4]
{% endhighlight %}

<h4>倒置顺序表</h4>
<img src="http://liuzejin.top/assets/images/showHow/sequenceTable/8.png" alt="">
{% highlight js %}
使用reverse()方法实现倒置
eg: arr = [1,2,3,4];
	arr.reverse() ==> [4,3,2,1];
{% endhighlight %}


以上是数组模拟顺序表的一些方法
除此之外数组包含的方法还有
concat():连接两个数组生成新数组,注意这事生成"新"数组
join(): 数组放入字符串,结果是个字符串
sort(): 数组按ascii顺序进行比较排序的
toString()：把数组转换为字符串，并返回结果
等等。

这些方法组合起来可以解决很多事情，比如<b>模拟栈</b>，<b>模拟队列</b>，<b>数组去重</b>，<b>字符串倒置</b>等等问题。