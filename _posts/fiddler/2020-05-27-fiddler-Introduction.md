---
layout: post
title: Fiddler 之基本介绍
categories: Fiddler
description: Fiddler背景介绍与原理
keywords: Fiddler, Filter, Device
---

### 背景介绍

Fiddler是一个http协议调试代理工具，它能够记录并检查所有你的电脑和互联网之间的http通讯，设置断点，查看所有的“进出”Fiddler的数据（指cookie,html,js,css等文件，这些都可以让你胡乱修改的意思）。 Fiddler 要比其他的网络调试器要更加简单，因为它不仅仅暴露http通讯还提供了一个用户友好的格式。
Fiddler是用C#写出来的,它包含一个简单却功能强大的基于JScript.NET事件脚本子系统，它的灵活性非常棒，可以支持众多的http调试任务，并且能够使用.net框架语言进行扩展。

注：Fiddler因为设置代理的原因，在使用中可能会出现网络问题，直接关闭或者点击关掉左下角的capture就好了

### Fiddler原理

在本机开启一个http的代理服务器，然后它会转发所有的http请求和响应到最终的服务器,如图所示

![](http://km.oa.com/files/post_photo/692/234692/05b5174ead9dbf9f738b1cc5aa0bd91a1462759742.jpg)

Fiddler就是一个代理层，打开Fiddler后，可以记录请求响应、修改经过它的文件、延迟传输、修改域名对应的IP等等。打开ie的internet选项->连接->局域网设置->高级可以看到下图

![](https://img-blog.csdn.net/20181023161456529?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xvbmVyX2Zhbmc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

通过更改浏览器的代理服务地址，Fiddler就可以截获所有发出的请求



### Fiddler两种代理模式

在Fiddler的工具栏的Stream可以进行两种模式的切换，默认是缓冲模式

- 流模式：（streaming） 实时传送给客户端（更接近于浏览器本身真实的行为）

- 缓冲模式： （buffering） 等http请求所有东西都准备好后才返回给应用程序（可控制最后的服务器响应）

  

### Fiddler使用场景

- 开发环境host配置，Tools->Hosts


- 前后端接口调试


- 线上bugfix，将线上项目代理到本地进行修改调试(AutoResponder,Willow)


- 性能分析和优化

  


### 工具栏常用功能介绍

- Replay，回放会话，选中会话并按R键即可回放会话（可多条）

- 清空监控面板，快捷键ctrl+x

- go 断点调试

- stream切换代理模式

- Decode 解压请求

- keep all session选项可选保存会话的数量，默认的保存所有，保存的会话越多，fiddler占用的内存越大，可以设置下，而且调试也不希望看到太多会话，可以根据需要清空监控面板或过滤请求

- All Process，可以用来控制如只捕获chrome浏览器的请求

- Find 可以查找会话并选择颜色高亮标明

- TextWizard 解码/编码功能，可选选项很多，避免去网上找解码工具

### 状态栏

状态栏功能较少，但也很重要：

- Capture用来控制Fiddler是否工作，点击即可切换状态
- All Process控制请求来源
- 旁边的数字代表当前会话数量

### 命令行

1. select命令

   选择所有响应类型（指content-type）为指定类型的HTTP请求，选中的部分会高亮显示：

   ```
   select image   选择图片请求
   
   select css        选择css请求
   
   select html     选择HTML的请求
   ```

2. allbut命令

   allbut命令用于选择给定类型的HTTP请求(删除其他类型请求)，该命令还有一个别名：keeponly.

   ```
   Eg:只保留image会话：allbut image
   ```

3. ?text命令

   选择所有 URL 匹配问号后的字符的全部 session

   ```
   Eg:?qq.com
   ```


4. 小于/大于size命令

   选择响应大小大于某个大小或者小于某个大小的所有HTTP请求  

   ```
   Eg:选择响应大小小于10k的请求：<10k
   ```

5. =status命令

   选择响应状态等于给定状态的所有HTTP请求

   ```
   Eg:选择所有状态为200的HTTP请求：=200
   ```

6. @host命令

   选择包含指定 HOST 的全部 HTTP请求。

   ```
   Eg：选择所有host包含csdn.net的请求：@csdn.net
   ```

7. Bpafter,Bps, bpv, bpm, bpu

   这几个命令主要用于批量设置断点:

   ```
   Bpafter xxx: 中断 URL 包含指定字符的全部 session 响应
    
   Bps xxx: 中断 HTTP 响应状态为指定字符的全部 session 响应。
   
   Bpv xxx: 中断指定请求方式的全部 session 响应
   
   Bpm xxx: 中断指定请求方式的全部 session 响应。等同于bpv xxx
    
   Bpu xxx:与bpafter类似。
    
   当这些命令没有加参数时，会清空所有设置了断点的HTTP请求。
   ```

8. help

   输入help会弹出这个页面 http://docs.telerik.com/fiddler/knowledgebase/quickexec，是fiddler的官方命令行文档

### 右侧窗口功能

- Stastics：统计选中的一个或多个请求相关数据，大小、耗时
  - 最下方会有一个不太容易发现的功能show charts，点击会对请求进行可视化处理

- Inspectors：多种方式查看Request或者Response的详细消息,如图：

- AutoResponder： 设置一些规则将符合规则的请求重定向到本地。

- Composer：创建发送HTTP请求/前后端接口联调

- Filters：设置会话过滤规则

- Log：日志

- Timeline：性能优化和分析

- Willow的使用：请求重定向（模拟响应）
  - 右键添加项目，规则，host
