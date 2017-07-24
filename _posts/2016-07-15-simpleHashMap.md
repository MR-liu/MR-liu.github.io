---
bg: "tools.jpg"
layout: post
title:  "简单实现HashMap方法"
crawlertitle: "简单实现HashMap方法"
summary: "简单实现HashMap方法"
date:   2017-07-24 10:09:47 +0800
categories: posts
tags: ['前端']
author: LZJ
---
在leetcode上碰到一些很有意思的题目。

比如：给定一个字符串，找到最长的子串的长度没有重复字符。

在ES6的map方法出来前，我们做法比较复杂。在网上搜索了一圈，在没有ES6之前，别人推荐使用类似JAVA的Hashmap方法，事实上hashmap方法跟ES6的map方法几乎一样的。

看到别人用js模拟hashmap简单实现，觉得很有意思，我也试试。

{% highlight js %}
	
	var hashmap = function () {}

	//增加key value

	hashmap.prototype.Set = function(key,value){this[key] = value};

	//获取key

	hashmap.prototype.Get = function(key){return this[key]};

	//是否包含key

	hashmap.prototype.Contains = function(key){return this.Get(key) == null?false:true};

	//删除key
	hashmap.prototype.Remove = function(key){delete this[key]};
	
{% endhighlight %}

使用结果
{% highlight js %}
	//先声明new一个出来
	var d = new hashmap();

	d.Set("name","LZJ");

	d.Get("name");

	d.Contains("name")

	d.Remove("name")

	d.Contains("name")

{% endhighlight %}