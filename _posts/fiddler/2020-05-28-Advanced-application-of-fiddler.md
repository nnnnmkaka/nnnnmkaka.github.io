---
layout: post
title: Fiddler 之高级应用
categories: Fiddler
description: Fiddler高级使用
keywords: Fiddler, Filter, Device
---

### 网速限速

我们为什么要限速？
限速对于web前端研发是非常重要的，由于开发者的机器一般配置都很高，并且是在localhost下来调试程序，所以很难模拟到用户的真实使用情况，如正在下载JS,css等静态资源的时候，页面的一个渲染情况。
当网速很慢的时候，我们更希望看到的是先渲染出用户界面，而不是让用户看到一片空白。那么这个时候，网络限速就能很方便在localhost针对类似的情况来做性能调试与优化。

方法一：Fiddler script（自定义延时）
```
需要的插件：Fiddler script，下载地址：http://www.telerik.com/download/fiddler/fiddlerscript-editor
下载完直接安装就行了，安装之前必须关闭fiddler，再打开fiddler就会在右侧tab看到fiddler script选项
fiddler script原理：把请求完全代码化
Eg：模拟延时3s发送请求：
选中会话，在fiddler-script——>Go to->OnBeforeRequest添加代码如下：
oSession["request-trickle-delay"] = "3000"
点击save script保存，再replay会话就会发现会话延迟了三秒才发送
延时响应同理
```
### fiddler断点调试

设置断点有两种方法:
```
第一种：打开Fiddler 点击Rules-> Automatic Breakpoint ->Before Requests(这种方法会中断所有的会话)

如何消除命令呢？ 点击Rules-> Automatic Breakpoint ->Disabled
```
```
第二种: 在命令行中输入命令: bpu www.baidu.com (这种方法只会中断www.baidu.com)

如何消除命令呢？ 在命令行中输入命令 bpu
```



> 看个实例，模拟QQ邮箱的登录，输入错误的用户名和密码，用Fiddler中断会话，修改成正确的用户名密码,这样就能成功登录:
>
> 1. 登录qq邮箱，输入错误的密码
> 2. 打开Fiddler, 在命令行中输入bpu
> 3. 输入错误的用户名和密码 点击登录
> 4. Fiddler 能中断这次会话，选择被中断的会话，点击Inspectors tab下的WebForms tab 修改用户名密码，然后点击Run to Completion。
> 5. 结果是正确地登录了qq邮箱



###  禁用缓存

两种方法，一种暂时的，一种永久的（通过fiddler script）

暂时的方法：

```
Tools->Performance->Disable Caching
```

永久的方法：

```
在fiddler script里查找

> var m_DisableCaching: boolean = false;

把值改成true并保存就可以了
```



### 扩展Fiddler script的一些用法

#####  *实例 :让所有qq的会话都显示红色*
------

把这段脚本放在OnBeforeRequest(oSession: Session) 方法下，并且点击"Save script"

```
if (oSession.HostnameIs("www.cnblogs.com")) {

      oSession["ui-color"] = "red";
    
  }
这样所有的cnblogs的会话都会显示红色
```



#####  *如何在Fiddler Script中修改Cookie*
------

cookie其实就是request 中的一个header.
```
// 删除所有的cookie

oSession.oRequest.headers.Remove("Cookie");

// 新建cookie
oSession.oRequest.headers.Add("Cookie", "username=testname;testpassword=P@ssword1");
```
注意: Fiddler script不能直接删除或者编辑单独的一个cookie， 你需要用replace方法或者正则表达式的方法去操作cookie的string

复制代码
```
static function OnBeforeRequest(oSession: Session) { 

   if (oSession.HostnameIs('www.example.com') && 

         oSession.uriContains('pagewithCookie') && 
         oSession.oRequest.headers.Contains("Cookie")) 

   { 

   var sCookie = oSession.oRequest["Cookie"]; 

   //  用replace方法或者正则表达式的方法去操作cookie的string

   sCookie = sCookie.Replace("cookieName=", "ignoreme="); 

   oSession.oRequest["Cookie"] = sCookie; 

  } 
```


##### *一点小的tips：*
------
1、我在使用Fiddler的过程中碰到过无法抓包的情况，原因是之前因为测试配置了autoresponder或者filter等没有改回去，如果碰到这个情况请确保Fiddler的选项都配置正确

2、chrome和firefox浏览器无法被监听
fiddler安装之后，默认会在IE浏览器中安装一个fiddler的插件，所以它对IE及国内基于IE内核的各类浏览器都能实现监听，但其他内核的浏览器无法被监听。

解决办法：禁用chrome和firefox中具有代理功能的插件，比如chrome如果安装了switchSharp，禁用它或选择“使用系统代理设置”
