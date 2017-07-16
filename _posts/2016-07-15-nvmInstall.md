---
bg: "tools.jpg"
layout: post
title:  "window下安装使用NVM"
crawlertitle: "window下安装使用NVM"
summary: "window下安装使用NVM"
date:   2017-07-16 15:09:47 +0800
categories: posts
tags: ['工具']
author: LZJ
---
一、由于node有多种版本号，每个版本号的API肯定也有些细微的差别，在工作中有可能要经常切换node的版本号，因此可以下载nvm使其来管理node的版本号。

首先下载nvm，官网：https://github.com/coreybutler/nvm-windows/releases/download/1.1.0/nvm-noinstall.zip
或者去我的网盘下载（64位）：http://pan.baidu.com/s/1dEXeusD

二、配置环境变量

1.把下载后的nvm解压到一个全英文路径下，解压后的样子：

<img src="https://app.yinxiang.com/shard/s72/res/db570cca-f31e-4819-984c-633c66caba96" alt="">

2.打开nvm里的settings.txt(如果官网下载的nvm中没有这个文件，自己新建一个也行)，然后配置里面的内容。

	root:配置为当前nvm.exe所在目录；

　　path:配置为node快捷方式所在目录；

　　arch:配置为当前操作系统的位置（32/64）；

	proxy：代理，一般先不用配置，如果以后下载包时被墙了可以FQ或者配置淘宝的镜像；

如下图为我的配置，我在E盘新建了一个mynode文件夹来存放nvm文件夹：

<img src="https://app.yinxiang.com/shard/s72/res/1cc7567f-eee8-43bd-95a6-0c58fa8756e9" alt="">

3.右击“计算机”－属性－高级系统设置－环境变量，在用户变量中新建：

	NVM_HOME = 当前 nvm.exe 所在目录,即settings.txt中root中的值；

	NVM_SYMLINK = node 快捷方式所在的目录,即settings.txt中path的值；

	Path=%NVM_HOME%;%NVM_SYMLINK%;（即在你的Path后面加一分号后再加上%NVM_HOME%;%NVM_SYMLINK%;）

然后一路确定下去，下图为我的配置；

<img src="https://app.yinxiang.com/shard/s72/res/4143b2c5-a156-4699-bdb9-c61419731e84" alt="">

3.打开cmd，输入set NVM_HOME（和set NVM_SYMLINK）可以看到你已经配置了此环境变量，然后输入nvm ls可以查看你拥有的node的版本号，输入nvm use 版本号便是你所要使用哪个版本的node了，此命令输完后便发现你所配置的node快捷方式所在的目录下多了nodejs这个快捷方式。如下图为我的操作：

<img src="https://app.yinxiang.com/shard/s72/res/53dc5051-064c-4b25-add1-a6b8716c5927" alt="">

此时node就配置成功啦！

4.windows使用nvm来升级node的版本

在cmd中输入nvm install 最新node版本号，时间有点长，耐心等会，升级成功后再使用nvm use 版本号即可。如下

<img src="https://app.yinxiang.com/shard/s72/res/3eb5c017-b5e7-4c30-82e0-d1dbd3c6659e" alt="">

配置node的下载路径

nvm默认的下载地址是http://nodejs.org/dist/，这是国外的服务器，在国内下载速度很慢。

在控制台输入nvm，我们看到了

<img src="https://app.yinxiang.com/shard/s72/res/83344143-d3ac-440d-bfca-59bfe09365d4" alt="">

好像是有设置下载镜像的命令，但是我配置了一下，不行。查看issues发现好像是作者忘记加上去了= =。

解决办法：

在你nvm的安装路径下，找到settings.txt打开，在后面加加上

node_mirror: https://npm.taobao.org/mirrors/node/

npm_mirror: https://npm.taobao.org/mirrors/npm/

<img src="https://app.yinxiang.com/shard/s72/res/0c8949fe-7cb5-4758-af96-f3f2886cf3d8" alt="">

通过 nvm 安装任意版本的 node

nvm 默认是从 http://nodejs.org/dist/ 下载的, 国外服务器, 必然很慢,

npm也是从国外服务器下载的，基本下载不下来

好在 nvm 以及支持从镜像服务器下载包, 于是我们可以方便地从淘宝的 node dist 镜像下载:

set "NVMW_NODEJS_ORG_MIRROR=https://npm.taobao.org/mirrors/node"

set "NVMW_NPMJS_COM_MIRROR=https://npm.taobao.org/mirrors/npm"

nvm install 4.3.2

如果你不想每次都输入环境变量 NVMW_NODEJS_ORG_MIRROR, 那么我建议你在全局环境变量中增加它.

然后你可以继续非常方便地安装各个版本的 node 了, 你可以查看一下你当前已经安装的版本:

nvm list