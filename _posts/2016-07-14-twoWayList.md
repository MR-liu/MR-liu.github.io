---
bg: "tools.jpg"
layout: post
title:  "使用JS模拟双向链表"
crawlertitle: "JS模拟双向链表"
summary: "JS模拟双向链表"
date:   2017-07-17 15:09:47 +0800
categories: posts
tags: ['数据结构']
author: LZJ
---
双向链表也叫双链表，是链表的一种，它的每个数据结点中都有两个指针，分别指向直接后继和直接前驱。所以，从双向链表中的任意一个结点开始，都可以很方便地访问它的前驱结点和后继结点。一般我们都构造双向循环链表。

<img src="http://liuzejin.top/assets/images/showHow/twoWay/%E9%93%BE%E8%A1%A8.jpg" alt="">

使用JS模拟出双向链表的结构

首先，需要创建一个链表节点结构。我们使用构造函数形式进行模拟。
双向链表与单向链表不同，每个节点都有一个前驱，指向前面的节点。


{% highlight js %}
	/*
	*  param：单链表的特点是有节点以及节点后继指向的下一个节点的地址
	*  param：单链表的特点是有节点以及节点前驱指向的前一个节点的地址
	*  return：element指的是节点值
	 */

	var Node = function(element) {
        this.element = element;
        this.next = null;
        this.pre = null;
    }

{% endhighlight %}

接下来，我们需要模拟出双向链表的。

{% highlight js %}
	/*
	*  return：length指的节点长度
	*  return：value是指是头结点
	 */

	var LinkedList = function() {
    	this.head = new Node(null);
    	this.length = 0;
    	this.value = 'head';
    }


{% endhighlight %}

基本的双向链表就建立了，我们需要向双向链表中添加节点。编写增加节点方法。

头插法：
<img src="http://liuzejin.top/assets/images/showHow/twoWay/%E5%8F%8C%E5%90%91%E5%88%97%E8%A1%A8%E5%A4%B4%E6%8F%92.png" alt="">
{% highlight js %}
	/*
	*  param：头插法，在链表的前面插入节点
	*  return：element是传入节点的值
	 */

	let nextChild = new Node(element);

	if (this.head.next) {
		nextChild.next = this.head.next;
    	this.head.next.pre = nextChild
	}  

	nextChild.pre = this.head;
	this.head.next = nextChild;
	this.length++;	

{% endhighlight %}

尾插法
<img src="http://liuzejin.top/assets/images/showHow/twoWay/%E5%8F%8C%E5%90%91%E5%88%97%E8%A1%A8%E5%B0%BE%E6%8F%92%E6%B3%95.png" alt="">
{% highlight js %}
	/*
	*  param：尾插法，在链表的后面插入节点
	*  return：element是传入节点的值
	 */
	LinkedList.prototype.appendNext = function(element) {
		let head = this.head;
        let next = new Node(element);
        while(head.next!=null){
            head = head.next;
        }
        head.next = next;
        next.pre = head;
        this.length++
	};
{% endhighlight %}

指定位置增加
<img src="http://liuzejin.top/assets/images/showHow/twoWay/%E5%8F%8C%E5%90%91%E5%88%97%E8%A1%A8%E6%8C%87%E5%AE%9A%E4%BD%8D%E7%BD%AE%E6%8F%92%E5%85%A5.png" alt="">

{% highlight js %}
	/*
	*  param：指定位置增加，在链表指定位置插入节点
	*  return：index是传入节点的位置
	*  return：element是传入节点的值
	*  warm：无法在传入小于0或者大于链表长度的位置指定节点
	 */
	LinkedList.prototype.appendIndex = function(index, element) {
		let node = this.head,
			indexEle = new Node(element);

		if (index<0 || index>this.length) return;
		for (var i = 0; i<index; i++){
			if (i === index-1) {
				indexEle.pre = node;
				indexEle.next = node.next;
				node.next.pre = indexEle
				node.next = indexEle;
				this.length++;
			} else {
				node = node.next;
			}
		}
	};
{% endhighlight %}

删除节点
<img src="http://liuzejin.top/assets/images/showHow/twoWay/%E5%8F%8C%E5%90%91%E5%88%97%E8%A1%A8%E5%88%A0%E9%99%A4%E8%8A%82%E7%82%B9.png" alt="">
{% highlight js %}
	/*
	*  param：指定位置删除节点
	*  return：index是传入节点的位置
	*  warm：无法在传入小于0或者大于链表长度的位置指定节点
	 */
	LinkedList.prototype.removeNode = function(index) {
		let node = this.head;

		if (index<0 || index>this.length) return;
		for (let i = 0; i < index; i++){
			if (i === index-1) {
				node.next.next.pre = node;
				node.next = node.next.next;
			} else {
				node = node.next;
			}
		}
		this.length--;
	}
{% endhighlight %}

指定位置替换修改节点值
<img src="http://liuzejin.top/assets/images/showHow/twoWay/%E5%8F%8C%E5%90%91%E5%88%97%E8%A1%A8%E6%8C%87%E5%AE%9A%E4%BD%8D%E7%BD%AE%E6%8F%92%E5%85%A5.png" alt="">
{% highlight js %}
	/*
	*  param：指定位置修改节点
	*  return：index是传入节点的位置
	*  return：element是传入节点的值
	*  warm：无法在传入小于0或者大于链表长度的位置指定节点
	 */
	LinkedList.prototype.repIndex = function(index, element) {
		let node = this.head,
			indexEle = new Node(element);

		if (index<0 || index>this.length) return;
		for (var i = 0; i<index; i++){
			if (i === index-1) {
				indexEle.next = node.next.next;
				indexEle.pre = node;
				node.next.next.pre = indexEle;
				node.next = indexEle;
			} else {
				node = node.next;
			}
		}
	};
{% endhighlight %}

获取长度
{% highlight js %}
	/*
	*  param：获取链表长度
	 */
	LinkedList.prototype.getListLength = function(){
		let length = 0,
			node = this.head;

		while(node.next != null){
			node = node.next;
			length++
		}
		this.length = length;
		return length;
	};
{% endhighlight %}
	
获取节点
{% highlight js %}
	/*
	*  param：指定位置获取节点值
	*  return：index是传入节点的位置
	*  warm：无法在传入小于0或者大于链表长度的位置指定节点
	 */
	LinkedList.prototype.getNode = function(index) {
		let node = this.head;

		if (index<0 || index>this.length) return;
		for (let i = 0; i<index; i++){
			node = node.next;
		}
		return node;
	};
{% endhighlight %}

传入指定值获取值的位置
{% highlight js %}
	/*
	*  param：传入指定值获取值的位置
	*  return：value需要查询的参数
	*  warm：未找到参数无返回
	 */
	LinkedList.prototype.getValIndex = function(value) {
		let node = this.head,
			length = this.getListLength();

		// 为空的头结点不要忘记
		for (let i = 0; i <= this.length; i++) {
			if (node.element === value) {
				return i;
			} else {
				node = node.next;
			}
		}
	}
{% endhighlight %}

反转链表
{% highlight js %}
	/*
	*  param：反转链表
	 */
	LinkedList.prototype.reverseList = function () {
		let head = this.head,
			node = this.head,
			arr = [],
			length = this.getListLength();

		for (let i = 0; i <= length; i++){
			arr.push(node.element);
			node = node.next;
		}
		
		head.next.pre = null;
		head.next = null;
		for (let i = length; i > 0 ; i--){
			if (arr[i] !== null) {
				this.appendNext(arr[i]);
			}
		}
		this.getListLength();
	}
{% endhighlight %}

new出链表使用方法查看链表
{% highlight js %}
	var list = new LinkedList();

	list.appendNext(1);
	list.appendNext(2);
	list.appendNext(3);
	list.appendNext(4);
	list.appendNext(5);
	list.appendNext(6);
	list.appendNext(7);
	list.appendNext(8);
	list.appendNext(9);
	list.appendNext(10);

	console.log(list);
{% endhighlight %}
