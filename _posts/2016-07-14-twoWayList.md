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

<img src="http://img.my.csdn.net/uploads/201211/17/1353130061_1546.png" alt="">

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

接下来，我们需要模拟出链表的。

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

基本的链表就建立了，我们需要向链表中添加节点。编写增加节点方法。

头插法：
<img src="http://see.xidian.edu.cn/cpp/uploads/allimg/140709/1-140F9152T3201.jpg" alt="">
{% highlight js %}
	/*
	*  param：头插法，在链表的前面插入节点
	*  return：element是传入节点的值
	 */

	LinkedList.prototype.appendHead = function(element) {
		let nextChild = new Node(element);//新建節點
		nextChild.next = this.head.next;//
		this.head.next = nextChild;
		this.length++;
	};

{% endhighlight %}

尾插法
<img src="http://img2.imgtn.bdimg.com/it/u=3984852701,646563853&fm=26&gp=0.jpg" alt="">
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
        this.length++
	};
{% endhighlight %}

指定位置增加
<img src="http://img1.imgtn.bdimg.com/it/u=3885900004,1516156657&fm=26&gp=0.jpg" alt="">
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
				indexEle.next = node.next;
				node.next = indexEle;
				this.length++;
			} else {
				node = node.next;
			}
		}
	};
{% endhighlight %}

删除节点
<img src="http://img3.imgtn.bdimg.com/it/u=2583993628,2824655199&fm=26&gp=0.jpg" alt="">
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
				node.next = node.next.next;
			} else {
				node = node.next;
			}
		}
		this.length--;
	}
{% endhighlight %}

指定位置替换修改节点值
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
		
		for (let i = length; i > 0 ; i--){
			if (arr[i] !== null) {
				head.next = new Node(arr[i]);
				head = head.next;
			}
		}
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
<style>
	.font-12{
		line-height: 10px;font-size: 12px; margin: 4px 0; color: #2d2d2d;
	}
</style>