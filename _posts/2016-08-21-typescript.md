---
bg: "tools.jpg"
layout: post
title:  "typescript尝试"
crawlertitle: "typescript尝试"
summary: "typescript尝试"
date:   2017-08-20 15:09:47 +0800
categories: posts
tags: ['JS']
author: LZJ
---

TypeScript是一种由微软开发的自由和开源的编程语言是JavaScript的一个超集，而且本质上向这个语言添加了可选的静态类型和基于类的面向对象编程。

TypeScript 编译器，名称叫 tsc, 是用可以被编译为可以被执行在任何 JavaScript 引擎中，在任何宿主 - 如浏览器 - 中的常规 JavaScript 的 TypeScript 写的。编译器包被绑定于一个可以执行编译器的脚本宿主。使用 Node.js 作为宿主的 Node.js 包同样可以获得。


我使用npm安装使用

{% highlight js %}

npm install -g typescript

{% endhighlight %}

<img src="http://liuzejin.top/assets/images/showHow/typescript/1.png" alt="">
<img src="http://liuzejin.top/assets/images/showHow/typescript/2.png" alt="">

新建typescript类型的文件typescript.ts，使用官网提供的案例。

{% highlight js %}
function greeter(person) {
    return "Hello, " + person;
}

var user = "Jane User";

document.body.innerHTML = greeter(user);

{% endhighlight %}

使用tsc命令运行.ts文件生成js文件

<img src="http://liuzejin.top/assets/images/showHow/typescript/3.png" alt="">

我们可以看到生成后的文件跟生成前的文件对比

.ts
<img src="http://liuzejin.top/assets/images/showHow/typescript/4.png" alt="">
.js
<img src="http://liuzejin.top/assets/images/showHow/typescript/5.png" alt="">

<h4>类型注解</h4>

TypeScript里的类型注解是一种轻量级的为函数或变量添加约束的方式。 在这个例子里，我们希望 greeter函数接收一个字符串参数。 然后尝试把 greeter的调用改成传入一个数字：

{% highlight js %}

function greeter(person: string) {
    return "Hello, " + person;
}

var user = 111;

document.body.innerHTML = greeter(user);

{% endhighlight %}

<img src="http://liuzejin.top/assets/images/showHow/typescript/6.png" alt="">

命令行报错
<img src="http://liuzejin.top/assets/images/showHow/typescript/7.png" alt="">

但是文件还是生成了

<img src="http://liuzejin.top/assets/images/showHow/typescript/8.png" alt="">

<h4>接口</h4>

我们使用接口来描述一个拥有firstName和lastName字段的对象。 在TypeScript里，只在两个类型内部的结构兼容那么这两个类型就是兼容的。 这就允许我们在实现接口时候只要保证包含了接口要求的结构就可以，而不必明确地使用 implements语句。

{% highlight js %}

interface Person {
    firstName: string;
    lastName: string;
}

function greeter(person: Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}

var user = { firstName: "Jane", lastName: "User" };

document.body.innerHTML = greeter(user);

{% endhighlight %}

<img src="http://liuzejin.top/assets/images/showHow/typescript/9.png" alt="">

生成的
<img src="http://liuzejin.top/assets/images/showHow/typescript/11.png" alt="">

<h4>类</h4>

这个是令我惊喜的功能，TypeScript支持JavaScript的新特性，比如支持基于类的面向对象编程。让我们创建一个Student类，它带有一个构造函数和一些公共字段

还要注意的是，在构造函数的参数上使用public等同于创建了同名的成员变量。

{% highlight js %}

class Student {
    fullName: string;
    constructor(public firstName, public middleInitial, public lastName) {
        this.fullName = firstName + " " + middleInitial + " " + lastName;
    }
}

interface Person {
    firstName: string;
    lastName: string;
}

function greeter(person : Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}

var user = new Student("Jane", "M.", "User");

document.body.innerHTML = greeter(user);

{% endhighlight %}


<img src="http://liuzejin.top/assets/images/showHow/typescript/12.png" alt="">

解析后的
<img src="http://liuzejin.top/assets/images/showHow/typescript/13.png" alt="">


我只是做个尝试，有时间可以做个深入研究，作为JS的补充这是很不错的。TypeScript可以和React还有webpack结合在一起使用。真的很有意思。

<a href="https://www.tslang.cn/docs/home.html" target="_blank">文档</a>