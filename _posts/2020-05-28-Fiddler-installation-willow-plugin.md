---
layout: post
title: Fiddler 之安装willow插件
categories: Fiddler
description: Fiddler安装willow插件
keywords: Fiddler, Filter, Device

---

Willow是一个Fiddler的插件，提供重定向和host主机等功能，通过可视化的方式去管理host
注：Fiddler2和Fiddler4，对应的Willow插件版本也是不一样的

### Willow的下载与安装

Fiddler4的Willow插件下载地址：https://github.com/QzoneTouch/commonWidget/releases<br/>
官方说明：https://qzonetouch.github.io/commonWidget/willow

![img](/images/posts/fiddler/2020-05-28-Fiddler-installation-willow-plugin-img1.png)

安装插件之前，需要把fiddler客户端关闭，下载完插件压缩包之后，将其放到fiddler的安装目录中解压，如有文件重复就需要替换

![img](/images/posts/fiddler/2020-05-28-Fiddler-installation-willow-plugin-img2.png)

文件解压完成后，重新启动Fiddler，在右边的窗口中，可看到willow插件，至此，willow安装成功！

![img](/images/posts/fiddler/2020-05-28-Fiddler-installation-willow-plugin-img3.png)


<br/>


> 注：win10安装willow前需先安装.NET framework3.5

------

下面介绍，安装.NET framework3.5的方法：



### win10安装.NET framework3.5

随便在一个盘新建一个文件夹，将下载的win10操作系统镜像盘解压到文件夹中；

以管理员身份运行cmd，输入如下命令：

```
DISM.exe /Online /Enable-Feature /FeatureName:NetFX3 /Source:F:\win10\sources\sxs；
```

可能会出现如下错误：“未识别命令”

![img](file:///C:\Users\V_ZHYA~1\AppData\Local\Temp\ksohtml15996\wps2.png) 

解决办法是输入dism.exe /?，在帮助命令中找到所要用的命令，复制粘贴，递归上述步骤，直至复制示例的完整的命令DISM.exe /Online /Enable-Feature /FeatureName:

![img](file:///C:\Users\V_ZHYA~1\AppData\Local\Temp\ksohtml15996\wps3.jpg) 

然后补上后面的参数，路径地址为自己解压的系统文件夹下\sources\sxs文件夹整个路径。

回车运行，100%后显示操作成功。

![img](file:///C:\Users\V_ZHYA~1\AppData\Local\Temp\ksohtml15996\wps4.png) 

可在控制面板程序和功能->启用或关闭Windows功能查看，.Net framework3.5前复选框已选择则安装成功。

![img](file:///C:\Users\V_ZHYA~1\AppData\Local\Temp\ksohtml15996\wps5.jpg) 

 ![img](file:///C:\Users\V_ZHYA~1\AppData\Local\Temp\ksohtml15996\wps6.jpg)
