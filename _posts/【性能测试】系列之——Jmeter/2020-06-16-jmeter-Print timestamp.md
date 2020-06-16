---
layout: post
title: Jmeter常用操作(1)_打印时间戳
categories: 【性能测试】系列之——Jmeter
description: Jmeter常用操作(1)_打印时间戳
keywords: jmeter
---

## 1、Jmeter常用操作(1)_打印时间戳

<br/>
**Jmeter中提供了一种函数，可以打印时间戳，如下图：**

![image-20200616150259736](https://github.com/nnnnmkaka/nnnnmkaka.github.io/blob/master/images/posts/Jmeter/2020-06-16-jmeter-Print%20timestamp_1.png?raw=true)

<br/>关于时间戳的格式，可以自由组合定义，例如：**<font color=red>yyyy-MM-dd HH:mm:ss</font>**，生成的函数：${__time(yyyy-MM-dd HH:mm:ss,)}

|  年  |  月  |  日  |  时  |  分  |  秒  |
| :--: | :----: | :----: | :----: | :----: | :----: |
| yyyy |  MM  |  dd  |  HH  |  mm  |  ss  |



将上图生成的函数，写入下一个接口：

![image-20200616154310388](https://github.com/nnnnmkaka/nnnnmkaka.github.io/blob/master/images/posts/Jmeter/2020-06-16-jmeter-Print%20timestamp_3.png?raw=true)

执行，查看结果树，可以看到结果中，将当前时间打印出来了哦~

![image-20200616154426444](https://github.com/nnnnmkaka/nnnnmkaka.github.io/blob/master/images/posts/Jmeter/2020-06-16-jmeter-Print%20timestamp_4.png?raw=true.png)

<br/>
此函数适用于一些需要填写时间参数的接口，用于实时获取当前时间。时间参数如果写死的话，过段时间接口就会报错啦~<br/>

<br/>下面说一下<font color=red>时间偏移如何打印</font>。

<br/>说到时间偏移，就是说我不光想打印当前时间，我还想打印明天，后台，甚至是明年的时间，那么我们要怎么去处理?这里就需要用到 **BeanShell Sampler**



添加BeanShell取样器

![image-20200616155451772](https://github.com/nnnnmkaka/nnnnmkaka.github.io/blob/master/images/posts/Jmeter/2020-06-16-jmeter-Print%20timestamp_6.png?raw=true)

添加脚本：

![image-20200616161549491](https://github.com/nnnnmkaka/nnnnmkaka.github.io/blob/master/images/posts/Jmeter/2020-06-16-jmeter-Print%20timestamp_7.png?raw=true)

附:脚本代码
```java
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Date;

try{
Date date =new Date(); //获取当前时间
SimpleDateFormat sf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
String nowDate = sf.format(date);
Calendar cal = Calendar.getInstance();
cal.setTime(sf.parse(nowDate));
cal.add(Calendar.DAY_OF_YEAR,+0);  //此处+0为当前时间，+1为加1天，类推
String orderDate = sf.format(cal.getTime());
cal.add(Calendar.DAY_OF_YEAR,+365);  //此处在之前的时间变量基础上叠加，1为一天，365为一年
String senderDate = sf.format(cal.getTime());
vars.put("orderDate",orderDate);
vars.put("senderDate",senderDate);  //传递两个变量，orderDate和senderDate

}
catch(Exception e){

}
```

![image-20200616161933144](https://github.com/nnnnmkaka/nnnnmkaka.github.io/blob/master/images/posts/Jmeter/2020-06-16-jmeter-Print%20timestamp_8.png?raw=true)

执行后，查看结果树：

![image-20200616162300701](https://github.com/nnnnmkaka/nnnnmkaka.github.io/blob/master/images/posts/Jmeter/2020-06-16-jmeter-Print%20timestamp_9.png?raw=true)