---
published: true
layout: post
title: javascript ajax
category: JS
tags: 
  - JS
  - 数据交互
  - ajax
time: 2016.02.06 18:23:37
excerpt: AJAX即“Asynchronous Javascript And XML”（异步JavaScript和XML），是指一种创建交互式网页应用的网页开发技术。

---

### javascript ajax

## 什么是AJAX

AJAX即“Asynchronous Javascript And XML”（异步JavaScript和XML），是指一种创建交互式网页应用的网页开发技术。
AJAX = 异步 JavaScript和XML（标准通用标记语言的子集）。
AJAX 是一种用于创建快速动态网页的技术。
通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。
传统的网页（不使用 AJAX）如果需要更新内容，必须重载整个网页页面。

## AJAX优势

AJAX不是一种新的编程语言，而是一种用于创建更好更快以及交互性更强的Web应用程序的技术。
使用Javascript向服务器提出请求并处理响应而不阻塞用户！核心对象XMLHTTPRequest。通过这个对象，您的 JavaScript 可在不重载页面的情况与Web服务器交换数据，即在不需要刷新页面的情况下，就可以产生局部刷新的效果。
AJAX 在浏览器与 Web 服务器之间使用异步数据传输（HTTP 请求），这样就可使网页从服务器请求少量的信息，而不是整个页面。
AJAX 可使因特网应用程序更小、更快，更友好。
AJAX 是一种独立于 Web 服务器软件的浏览器技术。　AJAX 基于下列 Web 标准：
JavaScriptXMLHTMLCSS在 AJAX 中使用的 Web 标准已被良好定义，并被所有的主流浏览器支持。AJAX 应用程序独立于浏览器和平台。
Web 应用程序较桌面应用程序有诸多优势；它们能够涉及广大的用户，它们更易安装及维护，也更易开发。
不过，因特网应用程序并不像传统的桌面应用程序那样完善且友好。
通过 AJAX，因特网应用程序可以变得更完善，更友好。

### AJAX的几种方式

ajax的技术核心是 XMLHttpRequest 对象；
ajax 请求过程：创建 XMLHttpRequest 对象、连接服务器、发送请求、接收响应数据；

- 创建对象
  new XMLHttpRequest();
- 连接和发送
  - open()函数的三个参数：请求方式、请求地址、是否异步请求(同步请求的情况极少，至今还没用到过)；
  - GET 请求方式是通过URL参数将数据提交到服务器的，POST则是通过将数据作为 send 的参数提交到服务器；
  - POST 请求中，在发送数据之前，要设置表单提交的内容类型；

- 接收
  - 接收到响应后，响应的数据会自动填充XHR对象，相关属性如下
responseText：响应返回的主体内容，为字符串类型；
responseXML：如果响应的内容类型是 "text/xml" 或 "application/xml"，这个属性中将保存着相应的xml 数据，是 XML 对应的 document 类型；
status：响应的HTTP状态码；
statusText：HTTP状态的说明；
  - XHR对象的readyState属性表示请求/响应过程的当前活动阶段，这个属性的值如下
    - 0-未初始化，尚未调用open()方法；
    - 1-启动，调用了open()方法，未调用send()方法；
    - 2-发送，已经调用了send()方法，未接收到响应；
    - 3-接收，已经接收到部分响应数据；
    - 4-完成，已经接收到全部响应数据；

- javascript/js的ajax的GET请求代码如下所示：
{% highlight ruby %}
 <script type="text/javascript">
 #创建 XMLHttpRequest 对象
var xmlHttp;
function GetXmlHttpObject(){
　　if (window.XMLHttpRequest){
　　　　#code for IE7+, Firefox, Chrome, Opera, Safari
　　　　xmlhttp=new XMLHttpRequest();
　　}else{// code for IE6, IE5
　　　　xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
　　}
　　return xmlhttp;
}
 #-----------ajax方法-----------
function getLabelsGet(){
　　xmlHttp=GetXmlHttpObject();
　　if (xmlHttp==null){
　　　　alert('您的浏览器不支持AJAX！');
　　　　return;
　　}
　　var id = document.getElementById('id').value;
　　var url="http://www.Leefrom.com?id="+id+"&t/"+Math.random();
　　xmlHttp.open("GET",url,true);
　　xmlHttp.onreadystatechange=favorOK;//发送事件后，收到信息了调用函数
　　xmlHttp.send();
}
function getOkGet(){
　　if(xmlHttp.readyState==1||xmlHttp.readyState==2||xmlHttp.readyState==3){
　　　　// 本地提示：加载中
　　}
　　if (xmlHttp.readyState==4 && xmlHttp.status==200){
　　　　var d= xmlHttp.responseText;
　　　　// 处理返回结果
　　}
}
</script>
{% endhighlight %}
- javascript/js的ajax的POST请求：
{% highlight ruby %}
<script type="text/javascript">
#创建 XMLHttpRequest 对象
var xmlHttp;
function GetXmlHttpObject(){
if (window.XMLHttpRequest){
# code for IE7+, Firefox, Chrome, Opera, Safari
xmlhttp=new XMLHttpRequest();
}else{// code for IE6, IE5
xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
}
return xmlhttp;
}
# -----------ajax方法-----------
function getLabelsPost(){
xmlHttp=GetXmlHttpObject();
if (xmlHttp==null){
alert('您的浏览器不支持AJAX！');
return;
}
var url="http://www.lifefrom.com/t/"+Math.random();
xmlhttp.open("POST",url,true);
xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xmlhttp.send();
xmlHttp.onreadystatechange=getLabelsOK;//发送事件后，收到信息了调用函数
}
function getOkPost(){
if(xmlHttp.readyState==1||xmlHttp.readyState==2||xmlHttp.readyState==3){
# 本地提示：加载中/处理中
}
if (xmlHttp.readyState==4 && xmlHttp.status==200){
var d=xmlHttp.responseText; // 返回值
# 处理返回值
}
}
</script>
{% endhighlight %}
