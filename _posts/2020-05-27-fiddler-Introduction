---
layout: post
title: Fiddler 之基本介绍
categories: Fiddler
description: Fiddler背景介绍与原理
keywords: Fiddler, Filter, Device
---

### 背景介绍

Fiddler是一个http协议调试代理工具，它能够记录并检查所有你的电脑和互联网之间的http通讯，设置断点，查看所有的“进出”Fiddler的数据（指cookie,html,js,css等文件，这些都可以让你胡乱修改的意思）。 Fiddler 要比其他的网络调试器要更加简单，因为它不仅仅暴露http通讯还提供了一个用户友好的格式。Fiddler是用C#写出来的,它包含一个简单却功能强大的基于JScript.NET事件脚本子系统，它的灵活性非常棒，可以支持众多的http调试任务，并且能够使用.net框架语言进行扩展。？

注：Fiddler因为设置代理的原因，在使用中可能会出现网络问题，直接关闭或者点击关掉左下角的capture就好了

### Fiddler原理

在本机开启一个http的代理服务器，然后它会转发所有的http请求和响应到最终的服务器,如图所示
打开Fiddler后，Fiddler会自动篡改代理，打开ie的internet选项->连接->局域网设置->高级可以看到下图
通过更改浏览器的代理服务地址，Fiddler就可以截获所有发出的请求


*设计操作流程：*

1. 找到自己关心的设备发出的某一条请求，在它的右键弹出菜单里有我们添加的菜单项「开/关过滤单设备请求」。

2. 点击该菜单项后：
   * 若当前状态为「查看所有设备请求」，则切换为「查看单个设备请求」状态，该设备为此条请求的发送者，并清除当前已显示的所有不关心的设备的请求。
   * 若当前状态为「查看单个设备请求」，则切换为「查看所有设备请求」状态。

### 实现

*实现思路：*

* 通过修改 CustomRules.js，在右键弹出菜单上添加一个菜单项来切换请求筛选状态。

* 每一条请求都带有 ClientIP，它在没有网络切换之类的情况发生时能较好地唯一标识一台设备。

* 筛选规则是将非来自该 ClientIP 的请求隐藏掉。

*实现步骤：*

1. 打开 CustomRules.js。

   启动Fiddler，依次选择菜单 Rules > Customize Rules...

2. 在 `OnBeforeRequest` 前添加如下代码：

   ```js
   // 是否过滤单设备请求标志
   public static var gs_FilterDevice: boolean = false;
   // 显示请求的设备的 ClientIP
   public static var gs_FilterClientIP: String = null;

   static function IsUnMatchClientIP(oS:Session):Boolean {
       return (oS.m_clientIP != gs_FilterClientIP);
   }

   public static ContextAction("开/关过滤单设备请求")
   function ToggleDeviceFilter(oSessions: Fiddler.Session[]){
       if (gs_FilterDevice) {
           gs_FilterDevice = false;
           return;
       }
       var oS: Session = FiddlerApplication.UI.GetFirstSelectedSession();
       if (null == oS) return;
       if (!gs_FilterDevice) {
           gs_FilterDevice = true;
       }
       gs_FilterClientIP = oS.clientIP;

       // 删除当前已显示的非所关心设备的请求
       FiddlerApplication.UI.actSelectSessionsMatchingCriteria(IsUnMatchClientIP);
       FiddlerApplication.UI.actRemoveSelectedSessions();
   }
   ```

3. 在 `OnBeforeRequest` 函数里添加如下代码，用于在「查看单个设备请求」状态时将不关心的设备产生的新请求隐藏：

   ```js
   if (gs_FilterDevice && oSession.m_clientIP != gs_FilterClientIP) {
       oSession["ui-hide"] = "true";
   }
   ```

*最终效果如下图：*

* 筛选前

  ![](/images/posts/fiddler/fiddler-filter-by-device-before.png)

* 筛选后

  ![](/images/posts/fiddler/fiddler-filter-by-device-after.png)

### 缺陷

当前做法有如下缺陷，尚未想到好办法解决：  

* 菜单项并不能标明当前的状态，不知道筛选是开是关，这可以通过查看当前 Session 列表里是否有多种设备的请求来判断。

* 当设备有网络切换时，比如重启了路由或者离开又回到某 Wifi，ClientIP 可能发生了变化，需要关闭筛选后在设备以新的 ClientIP 产生的请求上右键再次开启筛选。

### 附注

我使用的完整最新的 CustomRules.js 文件我上传到了一个 Gist 里，详见：<https://gist.github.com/mzlogin/3c5f9781c5bedff3fcfb>，如果想直接使用可以复制脚本内容后放置到「我的文档/Fiddler 2/Scripts/CustomRules.js」，也可以在此目录下使用 git 抓取我的最新定制 js 文件。
