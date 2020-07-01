---
layout: post
title: 正则表达式的运用
categories: 功能测试
description: 正则表达式
keywords: Regular expression,正则表达式
---

在日常工作中使用“正则表达式”语法是非常普遍的，所谓正则表达式，就是一种描述字符串结构模式的形式化表达方法。许多工具都支持正则表达式（文本编辑器、文字处理软件、系统工具、数据库引擎，等等）。当然，它还成为了编程语言的一部分。例如：C、C++、C#、JAVA、Go、JavaScript、elisp、Perl、Python、Php、Ruby、Tcl、Sed、Awk、Lua等等......

本文将介绍正则表达式的常见用法：

### 1、元字符



<center>表1.常用的元字符</center>

<table  style="width:600px; margin:auto;">
  <thead>
    <tr>
      <th>代码</th>
      <th align="left">说明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>.</td>
      <td align="left">小数点可以匹配除了换行符（\n）以外的任意一个字符</td>
    </tr>
    <tr>
      <td>\w</td>
      <td align="left">任意一个字母或数字或下划线，也就是 A~Z,a~z,0~9,_ 中任意一个</td>
    </tr>
    <tr>
      <td>\s</td>
      <td align="left">包括空格、制表符、换页符等空白字符的其中任意一个</td>
    </tr>
    <tr>
      <td>\d</td>
      <td align="left">任意一个数字，0~9 中的任意一个</td>
    </tr>
    <tr>
      <td>\b</td>
      <td align="left">匹配单词的开始或结束</td>
    </tr>
    <tr>
      <td>^</td>
      <td align="left">匹配一行的开头位置</td>
    </tr>
    <tr>
      <td>$</td>
      <td align="left">匹配一行的结束位置</td>
    </tr>
  </tbody>
</table>


示例：

>  [举例1：表达式 "<font color="red">\d\d</font>"，在匹配 "abc123" 时](http://www.regexlab.com/zh/workshop.asp?pat=\d\d&txt=abc123)，匹配的结果是：成功；匹配到的内容是："12"；匹配到的位置是：开始于3，结束于5。
>
>   [举例2：表达式 "<font color="red">a.\d</font>"，在匹配 "aaa100" 时](http://www.regexlab.com/zh/workshop.asp?pat=a.\d&txt=aaa100)，匹配的结果是：成功；匹配到的内容是："aa1"；匹配到的位置是：开始于1，结束于4。
>
> [举例3：表达式"<font color="red">\d+</font>"，在匹配"abc123"时](http://www.regexlab.com/zh/workshop.htm?pat=%5Cd%2B&txt=abc123&dlt=0)，匹配的结果是：成功；匹配到的内容是："123"；匹配到的位置是：开始于3，结束于5。"<font color="red">\d+</font>"表示匹配1个或更多连续的数字。这里的+是和* 类似的元字符，不同的是*匹配重复任意次(可能是0次)，而+则匹配重复1次或更多次。
> 
><font color="red">\ba\w**\b*  </font> 
> 匹配以字母a开头的单词——先是某个单词开始处(\b)，然后是字母a,然后是任意数量的字母或数字(\w*)，最后是单词结束处(\b)
> 
><font color="red">\b\w{6}\b </font>
> 匹配刚好6个字符的单词。



### 2、重复

<center>表2.常用的限定符代码</center>

<table  style="width:600px; margin:auto;">
  <thead>
    <tr>
      <th>代码</th>
      <th align="left">说明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>*</td>
      <td align="left">重复零次或更多次11111111111111111111111111</td>
    </tr>
    <tr>
      <td>+</td>
      <td align="left">重复一次或更多次</td>
    </tr>
    <tr>
      <td>?</td>
      <td align="left">重复零次或一次</td>
    </tr>
    <tr>
      <td>{n}</td>
      <td align="left">重复n次</td>
    </tr>
    <tr>
      <td>{n,}</td>
      <td align="left">重复n次或更多次</td>
    </tr>
    <tr>
      <td>{n,m}</td>
      <td align="left">重复n到m次</td>
    </tr>
  </tbody>
</table>

下面是一些使用重复的例子：

> [Windows\d+](http://www.regexlab.com/zh/workshop.htm?pat=Windows%5Cd%2B&rto=1&txt=Windows12345%0AWindowsaaaaa%0AWindows%u55EF%u55EF%u55EF%u55EF%u55EF%u55EF&dlt=0)   匹配Windows后面跟1个或更多数字
> 
> [13\d{9}](http://www.regexlab.com/zh/workshop.htm?pat=Windows%5Cd%2B&rto=1&txt=Windows12345%0AWindowsaaaaa%0AWindows%u55EF%u55EF%u55EF%u55EF%u55EF%u55EF&dlt=0)            匹配13后面跟9个数字(中国的手机号)
> 
>[^\w+](http://www.regexlab.com/zh/workshop.htm?pat=Windows%5Cd%2B&rto=1&txt=Windows12345%0AWindowsaaaaa%0AWindows%u55EF%u55EF%u55EF%u55EF%u55EF%u55EF&dlt=0)                 匹配一行的第一个单词(或整个字符串的第一个单词，具体匹配哪个意思得看选项设置)



### 3、测试工具

俗话说，要想攻其事，必先利其器。

![img](http://km.oa.com/files/photos/captures/201810/1539061573_1_w290_h52.png)

在线测试：

https://regex101.com/（推荐）

http://www.regexpal.com/

http://tool.chinaz.com/regex

[https://jex.im/regulex/#!flags=&re=%5E(a%7Cb)*%3F%24](https://jex.im/regulex/#!flags=&re=^(a|b)*%3F%24) \(正则分析)

本地测试：

http://www.regexbuddy.com/



### 4、测试工作中常见的一些需求

匹配中文字符的正则表达式：[\u4e00-\u9fa5] 　　

获取日期正则表达式：\d{4}[年|\\-|\\.]\d{\1-\12}[月|\\-|\\.]\d{\1-\31}日? 　　　

匹配双字节字符(包括汉字在内)：\[^\x00-\xff]　　

匹配空白行的正则表达式：\n\s*\r 　

匹配HTML标记的正则表达式：<(\S\*?)\[^>]\*>.\*?</>|<.*?/> 　

匹配首尾空白字符的正则表达式：^\s*|\s\*$　　

匹配Email地址的正则表达式：\w+([-+.]\w+)\*@\w+([-.]\w+)\*\.\w+([-.]\w+)*　

匹配网址URL的正则表达式：[a-zA-z]+://\[^\s]*　　

匹配帐号是否合法(字母开头，允许5-16字节，允许字母数字下划线)：^\[a-zA-Z][a-zA-Z0-9_{4,15}$　　

匹配国内电话号码：\d{4}-\d{7}|\d{3}-\d{8}　

匹配腾讯QQ号：\[1-9][0-9]\\{4,\\}　　

匹配中国邮政编码：[1-9]\d{5}(?!\d)　　

匹配身份证：\d{17}[\d|X]|\d{15}　

匹配ip地址：((2[0-4]\d|25[0-5]|[01]?\d\d?)\.){3}(2[0-4]\d|25[0-5]|[01]?\d\d?)


