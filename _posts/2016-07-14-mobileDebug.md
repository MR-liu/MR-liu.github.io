---
bg: "tools.jpg"
layout: post
title:  "移动web整理"
crawlertitle: "移动web整理"
summary: "移动web整理"
date:   2017-07-14 10:09:47 +0800
categories: posts
tags: ['前端']
author: LZJ
---
移动端与PC端一样，不同的浏览器有不同的兼容性。移动端也有些使用技巧是其他端没有的。注意这些技巧可以提高开发效率。以下的是开发移动端时整理的一些东西。

<h2>meta基础知识</h2>

H5页面窗口自动调整到设备宽度，并禁止用户缩放页面

{% highlight js %}
<meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no" />
{% endhighlight %}

忽略将页面中的数字识别为电话号码

{% highlight js %}
<meta name="format-detection" content="telephone=no" />
{% endhighlight %}

忽略Android平台中对邮箱地址的识别

{% highlight js %}
<meta name="format-detection" content="email=no" />
{% endhighlight %}

当网站添加到主屏幕快速启动方式，可隐藏地址栏，仅针对ios的safari

{% highlight js %}
<meta name="apple-mobile-web-app-status-bar-style" content="black" />
<!-- 可选default、black、black-translucent -->
{% endhighlight %}

viewport模板

viewport模板——通用

{% highlight js %}
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<meta content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no" name="viewport">
<meta content="yes" name="apple-mobile-web-app-capable">
<meta content="black" name="apple-mobile-web-app-status-bar-style">
<meta content="telephone=no" name="format-detection">
<meta content="email=no" name="format-detection">
<title>标题</title>
<link rel="stylesheet" href="index.css">
</head>

<body>
这里开始内容
</body>

</html>
{% endhighlight %}

viewport模板 - target-densitydpi=device-dpi，android 2.3.5以下版本不支持

{% highlight js %}
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=750, user-scalable=no, target-densitydpi=device-dpi"><!-- width取值与页面定义的宽度一致 -->
<meta content="yes" name="apple-mobile-web-app-capable">
<meta content="black" name="apple-mobile-web-app-status-bar-style">
<meta content="telephone=no" name="format-detection">
<meta content="email=no" name="format-detection">
<title>标题</title>
<link rel="stylesheet" href="index.css">
</head>

<body>
这里开始内容
</body>

</html>
{% endhighlight %}

<h2>常见问题</h2>

移动端如何定义字体font-family

中文字体使用系统默认即可，英文用Helvetica

{% highlight js %}
body{font-family:Helvetica;}
{% endhighlight %}

移动端字体单位font-size选择px还是rem

对于只需要适配少部分手机设备，且分辨率对页面影响不大的，使用px即可

对于需要适配各种移动设备，使用rem，例如只需要适配iPhone和iPad等分辨率差别比较挺大的设备

rem配置参考，适合视觉稿宽度为640px的：

{% highlight js %}
<meta content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no" name="viewport">
{% endhighlight %}

{% highlight js %}
html{font-size:10px}
@media screen and (min-width:321px) and (max-width:375px){html{font-size:11px}}
@media screen and (min-width:376px) and (max-width:414px){html{font-size:12px}}
@media screen and (min-width:415px) and (max-width:639px){html{font-size:15px}}
@media screen and (min-width:640px) and (max-width:719px){html{font-size:20px}}
@media screen and (min-width:720px) and (max-width:749px){html{font-size:22.5px}}
@media screen and (min-width:750px) and (max-width:799px){html{font-size:23.5px}}
@media screen and (min-width:800px){html{font-size:25px}}
{% endhighlight %}

<h2>移动端touch事件(区分webkit 和 winphone)</h2>

当用户手指放在移动设备在屏幕上滑动会触发的touch事件

以下支持webkit

· touchstart——当手指触碰屏幕时候发生。不管当前有多少只手指

· touchmove——当手指在屏幕上滑动时连续触发。通常我们再滑屏页面，会调用event的preventDefault()可以阻止默认情况的发生：阻止页面滚动

· touchend——当手指离开屏幕时触发

· touchcancel——系统停止跟踪触摸时候会触发。例如在触摸过程中突然页面alert()一个提示框，此时会触发该事件，这个事件比较少用

TouchEvent

· touches：屏幕上所有手指的信息

· targetTouches：手指在目标区域的手指信息

· changedTouches：最近一次触发该事件的手指信息

· touchend时，touches与targetTouches信息会被删除，changedTouches保存的最后一次的信息，最好用于计算手指信息

参数信息(changedTouches[0])

· clientX、clientY在显示区的坐标

· target：当前元素

以下支持winphone 8

· MSPointerDown——当手指触碰屏幕时候发生。不管当前有多少只手指

· MSPointerMove——当手指在屏幕上滑动时连续触发。通常我们再滑屏页面，会调用css的html{-ms-touch-action:none;}可以阻止默认情况的发生：阻止页面滚动

· MSPointerUp——当手指离开屏幕时触发

<h2>移动端click屏幕产生200-300 ms的延迟响应</h2>

移动设备上的web网页是有300ms延迟的，玩玩会造成按钮点击延迟甚至是点击失效。

以下是历史原因：

2007年苹果发布首款iphone上IOS系统搭载的safari为了将适用于PC端上大屏幕的网页能比较好的展示在手机端上，使用了双击缩放(double tap to zoom)的方案，比如你在手机上用浏览器打开一个PC上的网页，你可能在看到页面内容虽然可以撑满整个屏幕，但是字体、图片都很小看不清，此时可以快速双击屏幕上的某一部分，你就能看清该部分放大后的内容，再次双击后能回到原始状态。

双击缩放是指用手指在屏幕上快速点击两次，iOS 自带的 Safari 浏览器会将网页缩放至原始比例。

原因就出在浏览器需要如何判断快速点击上，当用户在屏幕上单击某一个元素时候，例如跳转链接<a href="#"></a>，此处浏览器会先捕获该次单击，但浏览器不能决定用户是单纯要点击链接还是要双击该部分区域进行缩放操作，所以，捕获第一次单击后，浏览器会先Hold一段时间t，如果在t时间区间里用户未进行下一次点击，则浏览器会做单击跳转链接的处理，如果t时间里用户进行了第二次单击操作，则浏览器会禁止跳转，转而进行对该部分区域页面的缩放操作。那么这个时间区间t有多少呢？在IOS safari下，大概为300毫秒。这就是延迟的由来。造成的后果用户纯粹单击页面，页面需要过一段时间才响应，给用户慢体验感觉，对于web开发者来说是，页面js捕获click事件的回调函数处理，需要300ms后才生效，也就间接导致影响其他业务逻辑的处理。

解决方案

· fastclick可以解决在手机上点击事件的300ms延迟

· zepto的touch模块，tap事件也是为了解决在click的延迟问题

· 使用touch事件替代

<h2>触摸事件的响应顺序</h2>

{% highlight js %}
1、ontouchstart 
2、ontouchmove 
3、ontouchend 
4、onclick
{% endhighlight %}

解决300ms延迟的问题，也可以通过绑定ontouchstart事件，加快对事件的响应

<h2>什么是Retina 显示屏，带来了什么问题</h2>

retina：一种具备超高像素密度的液晶屏，同样大小的屏幕上显示的像素点由1个变为多个，如在同样带下的屏幕上，苹果设备的retina显示屏中，像素点1个变为4个

在高清显示屏中的位图被放大，图片会变得模糊，因此移动端的视觉稿通常会设计为传统PC的2倍

那么，前端的应对方案是：

设计稿切出来的图片长宽保证为偶数，并使用backgroud-size把图片缩小为原来的1/2

{% highlight js %}
//例如图片宽高为：200px*200px，那么写法如下
.css{width:100px;height:100px;background-size:100px 100px;}
{% endhighlight %}

其它元素的取值为原来的1/2，例如视觉稿40px的字体，使用样式的写法为20px

{% highlight js %}
.css{font-size:20px}
{% endhighlight %}

<h2>ios系统中元素被触摸时产生的半透明灰色遮罩怎么去掉</h2>

ios用户点击一个链接，会出现一个半透明灰色遮罩, 如果想要禁用，可设置-webkit-tap-highlight-color的alpha值为0，也就是属性值的最后一位设置为0就可以去除半透明灰色遮罩

{% highlight js %}
a,button,input,textarea{-webkit-tap-highlight-color: rgba(0,0,0,0;)}
{% endhighlight %}


<h2>部分android系统中元素被点击时产生的边框怎么去掉</h2>

android用户点击一个链接，会出现一个边框或者半透明灰色遮罩, 不同生产商定义出来额效果不一样，可设置-webkit-tap-highlight-color的alpha值为0去除部分机器自带的效果

{% highlight js %}
a,button,input,textarea{
-webkit-tap-highlight-color: rgba(0,0,0,0;)
-webkit-user-modify:read-write-plaintext-only; 
}
{% endhighlight %}

-webkit-user-modify有个副作用，就是输入法不再能够输入多个字符

另外，有些机型去除不了，如小米2

对于按钮类还有个办法，不使用a或者input标签，直接用div标签

<h2>winphone系统a、input标签被点击时产生的半透明灰色背景怎么去掉</h2>

{% highlight js %}
<meta name="msapplication-tap-highlight" content="no">
{% endhighlight %}

<h2>webkit表单元素的默认外观怎么重置</h2>

{% highlight js %}
.css{-webkit-appearance:none;}
{% endhighlight %}

<h2>伪元素改变number类型input框的默认样式</h2>

{% highlight js %}
input[type=number]::-webkit-textfield-decoration-container {
    background-color: transparent;    
}
input[type=number]::-webkit-inner-spin-button {
     -webkit-appearance: none;
}
input[type=number]::-webkit-outer-spin-button {
     -webkit-appearance: none;
}
{% endhighlight %}

<h2>webkit表单输入框placeholder的颜色值能改变么</h2>

{% highlight js %}
input::-webkit-input-placeholder{color:#AAAAAA;}
input:focus::-webkit-input-placeholder{color:#EEEEEE;}
{% endhighlight %}

<h2>webkit表单输入框placeholder的文字能换行么</h2>

ios可以，android不行~

在textarea标签下都可以换行~

<h2>IE10（winphone8）表单元素默认外观如何重置</h2>

禁用 select 默认下拉箭头

::-ms-expand 适用于表单选择控件下拉箭头的修改，有多个属性值，设置它隐藏 (display:none) 并使用背景图片来修饰可得到我们想要的效果。


{% highlight js %}
select::-ms-expand {
display: none;
}
{% endhighlight %}

<h2>禁用 radio 和 checkbox 默认样式</h2>

::-ms-check 适用于表单复选框或单选按钮默认图标的修改，同样有多个属性值，设置它隐藏 (display:none) 并使用背景图片来修饰可得到我们想要的效果。

{% highlight js %}
input[type=radio]::-ms-check,input[type=checkbox]::-ms-check{
display: none;
}
{% endhighlight %}

<h2>禁用PC端表单输入框默认清除按钮</h2>

当表单文本输入框输入内容后会显示文本清除按钮，::-ms-clear 适用于该清除按钮的修改，同样设置使它隐藏 (display:none) 并使用背景图片来修饰可得到我们想要的效果。

{% highlight js %}
input[type=text]::-ms-clear,input[type=tel]::-ms-clear,input[type=number]::-ms-clear{
display: none;
}
{% endhighlight %}

<h2>禁止ios 长按时不触发系统的菜单，禁止ios android长按时下载图片</h2>

{% highlight js %}
.css{-webkit-touch-callout: none}
{% endhighlight %}

<h2>禁止ios和android用户选中文字</h2>

{% highlight js %}
.css{-webkit-user-select:none}
{% endhighlight %}

<h2>打电话发短信写邮件怎么实现</h2>

打电话

{% highlight js %}
<a href="tel:0755-10086">打电话给:0755-10086</a>
{% endhighlight %}

发短信，winphone系统无效

{% highlight js %}
<a href="sms:10086">发短信给: 10086</a>
{% endhighlight %}

写邮件

{% highlight js %}
<a href="mailto:peun@foxmail.com">peun@foxmail.com</a>
{% endhighlight %}

<h2>模拟按钮hover效果</h2>

移动端触摸按钮的效果，可明示用户有些事情正要发生，是一个比较好体验，但是移动设备中并没有鼠标指针，使用css的hover并不能满足我们的需求，还好国外有个激活移动端css的active效果。

直接在body上添加ontouchstart，同样可激活移动端css的active效果，比较推荐这种方式，代码如下：

{% highlight js %}
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<meta content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no" name="viewport">
<meta content="yes" name="apple-mobile-web-app-capable">
<meta content="black" name="apple-mobile-web-app-status-bar-style">
<meta content="telephone=no" name="format-detection">
<meta content="email=no" name="format-detection">
<style type="text/css">
a{-webkit-tap-highlight-color: rgba(0,0,0,0);}
.btn-blue{display:block;height:42px;line-height:42px;text-align:center;border-radius:4px;font-size:18px;color:#FFFFFF;background-color: #4185F3;}
.btn-blue:active{background-color: #357AE8;}
</style>
</head>
<body ontouchstart>
<div class="btn-blue">按钮</div>

</body>
</html>
{% endhighlight %}

或者：

{% highlight js %}
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<meta content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no" name="viewport">
<meta content="yes" name="apple-mobile-web-app-capable">
<meta content="black" name="apple-mobile-web-app-status-bar-style">
<meta content="telephone=no" name="format-detection">
<meta content="email=no" name="format-detection">
<style type="text/css">
a{-webkit-tap-highlight-color: rgba(0,0,0,0);}
.btn-blue{display:block;height:42px;line-height:42px;text-align:center;border-radius:4px;font-size:18px;color:#FFFFFF;background-color: #4185F3;}
.btn-blue:active{background-color: #357AE8;}
</style>
</head>
<body>

<div class="btn-blue">按钮</div>

<script type="text/javascript">
document.addEventListener("touchstart", function(){}, true)
</script>
</body>
</html>
{% endhighlight %}

兼容性ios5+、部分android 4+、winphone 8

要做到全兼容的办法，可通过绑定ontouchstart和ontouchend来控制按钮的类名

{% highlight js %}
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<meta content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no" name="viewport">
<meta content="yes" name="apple-mobile-web-app-capable">
<meta content="black" name="apple-mobile-web-app-status-bar-style">
<meta content="telephone=no" name="format-detection">
<meta content="email=no" name="format-detection">
<style type="text/css">
a{-webkit-tap-highlight-color: rgba(0,0,0,0);}
.btn-blue{display:block;height:42px;line-height:42px;text-align:center;border-radius:4px;font-size:18px;color:#FFFFFF;background-color: #4185F3;}
.btn-blue-on{background-color: #357AE8;}
</style>
</head>
<body>

<div class="btn-blue">按钮</div>

<script type="text/javascript">
var btnBlue = document.querySelector(".btn-blue");
btnBlue.ontouchstart = function(){
    this.className = "btn-blue btn-blue-on"
}
btnBlue.ontouchend = function(){
    this.className = "btn-blue"
}
</script>
</body>
</html>
{% endhighlight %}

<h2>屏幕旋转的事件和样式</h2>

事件

window.orientation，取值：正负90表示横屏模式、0和180表现为竖屏模式；

{% highlight js %}
window.onorientationchange = function(){
    switch(window.orientation){
        case -90:
        case 90:
        alert("横屏:" + window.orientation);
        case 0:
        case 180:
        alert("竖屏:" + window.orientation);
        break;
    }
}
{% endhighlight %}

样式

{% highlight js %}
//竖屏时使用的样式
@media all and (orientation:portrait) {
.css{}
}

//横屏时使用的样式
@media all and (orientation:landscape) {
.css{}
}
{% endhighlight %}

<h2>audio元素和video元素在ios和andriod中无法自动播放</h2>

应对方案：触屏即播

{% highlight js %}
$('html').one('touchstart',function(){
    audio.play()
})
{% endhighlight %}

<h2>摇一摇功能</h2>

HTML5 deviceMotion：封装了运动传感器数据的事件，可以获取手机运动状态下的运动加速度等数据。

<h2>手机拍照和上传图片</h2>

<p>"<input type="file"> 的accept 属性"</p>

{% highlight js %}
<!-- 选择照片 -->
<input type=file accept="image/*">
<!-- 选择视频 -->
<input type=file accept="video/*">
{% endhighlight %}

使用总结：

· ios 有拍照、录像、选取本地图片功能

· 部分android只有选取本地图片功能

· winphone不支持

· input控件默认外观丑陋

<h2>微信浏览器用户调整字体大小后页面矬了，怎么阻止用户调整</h2>

原因

· android侧是复写了layoutinflater 对textview做了统一处理

· ios侧是修改了body.style.webkitTextSizeAdjust值

解决方案：

android使用以下代码，该接口只在微信浏览器下有效(感谢jationhuang同学提供)

{% highlight js %}
/**
 * 页面加入这段代码可使Android机器页面不再受到用户字体缩放强制改变大小
 * 但是会有一个1秒左右的延迟，期间可以考虑通过loading展示
 * 仅供参考
 */
(function(){
    if (typeof(WeixinJSBridge) == "undefined") {
        document.addEventListener("WeixinJSBridgeReady", function (e) {
            setTimeout(function(){
                WeixinJSBridge.invoke('setFontSizeCallback',{"fontSize":0}, function(res) {
                    alert(JSON.stringify(res));
                });
            },0);
        });
    } else {
        setTimeout(function(){
            WeixinJSBridge.invoke('setFontSizeCallback',{"fontSize":0}, function(res) {
                alert(JSON.stringify(res));
            });
        },0);
    }
})();
{% endhighlight %}

<h2>ios使用-webkit-text-size-adjust禁止调整字体大小</h2>

{% highlight js %}
body{-webkit-text-size-adjust: 100%!important;}
{% endhighlight %}

最好的解决方案：

整个页面用rem或者百分比布局

<h2>消除transition闪屏</h2>

网络都是这么写的，但我并没有测试出来

{% highlight js %}
.css{
/*设置内嵌的元素在 3D 空间如何呈现：保留 3D*/
-webkit-transform-style: preserve-3d;
/*（设置进行转换的元素的背面在面对用户时是否可见：隐藏）*/
-webkit-backface-visibility: hidden;
}
{% endhighlight %}

<h2>开启硬件加速</h2>

· 解决页面闪白

· 保证动画流畅

{% highlight js %}
.css {
   -webkit-transform: translate3d(0, 0, 0);
   -moz-transform: translate3d(0, 0, 0);
   -ms-transform: translate3d(0, 0, 0);
   transform: translate3d(0, 0, 0);
}

{% endhighlight %}

<h2>取消input在ios下，输入的时候英文首字母的默认大写</h2>

{% highlight js %}
<input autocapitalize="off" autocorrect="off" />
{% endhighlight %}

<h2>android 上去掉语音输入按钮</h2>

{% highlight js %}
input::-webkit-input-speech-button {display: none}
{% endhighlight %}

<h2>android 2.3 bug</h2>

· @-webkit-keyframes 需要以0%开始100%结束，0%的百分号不能去掉

· after和before伪类无法使用动画animation

· border-radius不支持%单位

· translate百分比的写法和scale在一起会导致失效，例如-webkit-transform: translate(-50%,-50%) scale(-0.5, 1)

<h2>android 4.x bug</h2>

· 三星 Galaxy S4中自带浏览器不支持border-radius缩写

· 同时设置border-radius和背景色的时候，背景色会溢出到圆角以外部分

· 部分手机(如三星)，a链接支持鼠标:visited事件，也就是说链接访问后文字变为紫色

· android无法同时播放多音频audio

<h2>设计高性能CSS3动画的几个要素</h2>

· 尽可能地使用合成属性transform和opacity来设计CSS3动画，不使用position的left和top来定位

· 利用translate3D开启GPU加速

<h2>fixed bug</h2>

· ios下fixed元素容易定位出错，软键盘弹出时，影响fixed元素定位

· android下fixed表现要比iOS更好，软键盘弹出时，不会影响fixed元素定位

· ios4下不支持position:fixed

解决方案

· 可用isroll.js，暂无完美方案

<h2> 如何阻止windows Phone的默认触摸事件</h2>

winphone下默认触摸事件事件使用e.preventDefault是无效的

目前解决方法是使用样式来禁用

{% highlight js %}
html{-ms-touch-action: none;}/* 禁止winphone默认触摸事件 */
{% endhighlight %}

<h2>播放视频不全屏</h2>

{% highlight js %}
<!--
1.目前只有ios7+、winphone8+支持自动播放
2.支持Airplay的设备（如：音箱、Apple TV)播放
x-webkit-airplay="true" 
3.播放视频不全屏，ios7+、winphone8+支持，部分android4+支持（含华为、小米、魅族）
webkit-playsinline="true" 
-->
<video x-webkit-airplay="true" webkit-playsinline="true" preload="auto" autoplay src="http://"></video>
{% endhighlight %}

<h2>常用的移动端框架</h2>

<h3>zepto.js</h3>

语法与jquery几乎一样，会jquery基本会zepto~

最新版本已经更新到1.16

官网：http://zeptojs.com/

中文(非官网)：http://www.css88.com/doc/zeptojs_api/

常使用的扩展模块：

浏览器检测：https://github.com/madrobby/zepto/blob/master/src/detect.js

tap事件：https://github.com/madrobby/zepto/blob/master/src/touch.js

<h3>iscroll.js</h3>

解决页面不支持弹性滚动，不支持fixed引起的问题~

实现下拉刷新，滑屏，缩放等功能~

最新版本已经更新到5.0

官网：<a href="http://cubiq.org/iscroll-5">http://cubiq.org/iscroll-5</a>

<h3>underscore.js</h3>

笔者没用过，不过听说好用，推荐给大家~

该库提供了一整套函数式编程的实用功能，但是没有扩展任何JavaScript内置对象。

最新版本已经更新到1.8.2

官网：<a href="http://underscorejs.org/">http://underscorejs.org/</a>

<h3>flex布局</h3>

flex布局目前可使用在移动中，并非所有的语法都全兼容，但以下写法笔者实践过，效果良好~

{% highlight js %}
/* ============================================================
   flex：定义布局为盒模型
   flex-v：盒模型垂直布局
   flex-1：子元素占据剩余的空间
   flex-align-center：子元素垂直居中
   flex-pack-center：子元素水平居中
   flex-pack-justify：子元素两端对齐
   兼容性：ios 4+、android 2.3+、winphone8+
   ============================================================ */
.flex{display:-webkit-box;display:-webkit-flex;display:-ms-flexbox;display:flex;}
.flex-v{-webkit-box-orient:vertical;-webkit-flex-direction:column;-ms-flex-direction:column;flex-direction:column;}
.flex-1{-webkit-box-flex:1;-webkit-flex:1;-ms-flex:1;flex:1;}
.flex-align-center{-webkit-box-align:center;-webkit-align-items:center;-ms-flex-align:center;align-items:center;}
.flex-pack-center{-webkit-box-pack:center;-webkit-justify-content:center;-ms-flex-pack:center;justify-content:center;}
.flex-pack-justify{-webkit-box-pack:justify;-webkit-justify-content:space-between;-ms-flex-pack:justify;justify-content:space-between;}
{% endhighlight %}

示例：两端对齐

{% highlight js %}
</head>
<body>

<div class="flex flex-pack-justify">
    <div>模块一</div>
    <div>模块二</div>
    <div>模块三</div>
    <div>模块四</div>
</div>

</body>
</html>
{% endhighlight %}

使用注意：

· flex下的子元素必须为块级元素，非块级元素在android2.3机器下flex失效

· flex下的子元素宽度和高度不能超过父元素，否则会导致子元素定位错误，例如水平垂直居中

<style>

</style>