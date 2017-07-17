---
bg: "tools.jpg"
layout: post
title:  "MAC OS上安装nodejs开发环境"
crawlertitle: "MAC OS上安装nodejs开发环境"
summary: "MAC OS上安装nodejs开发环境"
date:   2017-07-16 14:09:47 +0800
categories: posts
tags: ['工具']
author: LZJ
---

1.首先，需要安装包管理工具，我们需要安装homebrew。从homebrew官网获取安装指令，复制好。打开终端粘贴。


{% highlight js %}

/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
{% endhighlight %}

按enter输入系统密码，确认。

OK 安装完成。

2.接下来安装nodejs输入：

{% highlight js %}

brew install nodejs 
{% endhighlight %}

等待安装完成。

<img src="http://liuzejin.top/assets/images/showHow/nodeInstall/1.png" alt="">

3.接下来来安装文档数据库 mongoDB 

输入指令：

{% highlight js %}

brew install mongodb
{% endhighlight %}

<img src="http://liuzejin.top/assets/images/showHow/nodeInstall/2.png" alt="">

<img src="http://liuzejin.top/assets/images/showHow/nodeInstall/3.png" alt="">

<img src="http://liuzejin.top/assets/images/showHow/nodeInstall/4.png" alt="">

等待安装完成

<img src="http://liuzejin.top/assets/images/showHow/nodeInstall/5.png" alt="">

4.接下来安装缓存 redis 

输入指令:

{% highlight js %}

brew install redis
{% endhighlight %} 

<img src="http://liuzejin.top/assets/images/showHow/nodeInstall/6.png" alt="">

<img src="http://liuzejin.top/assets/images/showHow/nodeInstall/7.png" alt="">

5.所有的安装完成 进行测试 在终端中输入vi test.js 创建一个测试文件

<img src="http://liuzejin.top/assets/images/showHow/nodeInstall/8.png" alt="">

按确定键

<img src="http://liuzejin.top/assets/images/showHow/nodeInstall/9.png" alt="">

输入：

{% highlight js %}

console.log(‘你好，nodejs’);
{% endhighlight %}

<img src="http://liuzejin.top/assets/images/showHow/nodeInstall/10.png" alt="">

按ESC 退出到命令行 按

{% highlight js %}

:wq 
{% endhighlight %}
保存退出 

6.输入node test.js执行那段代码

<img src="http://liuzejin.top/assets/images/showHow/nodeInstall/11.png" alt="">

7.到此nodejs开发环境搭建完成。可以借助sublime， WebStorm等IDE工具进行开发。



