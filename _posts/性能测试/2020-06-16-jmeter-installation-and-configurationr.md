---
layout: post
title: Jmeter的安装与配置
categories: 性能测试
description: Jmeter的安装与配置
keywords: jmeter
---



## 1、环境部署

- 安装jmeter之前，需要安装并配置好jdk，参考[【window10】jdk8的下载和安装步骤][https://blog.csdn.net/qq_39720249/article/details/80721719]

- jmeter安装与配置，参考[故三殇【Jmeter 下载、安装、汉化】][https://blog.csdn.net/qq_39720249/article/details/80721777]




<br/>

## 2、Jmeter目录介绍

![image-20200615213126504](https://github.com/nnnnmkaka/nnnnmkaka.github.io/blob/master/images/posts/Jmeter/image-20200615213126504.png?raw=true)

```
bin                       包含启动、配置等相关命令

docs                      官方本地文档目录

extras                    辅助库

lib                       核心库，包含 JMeter 用到的各种基础库和插件

licenses                  包含 non-ASF 软件的许可证

printable_docs            可打印版本文档目录

LICENSE JMeter            许可说明

NOTICE JMeter             简单信息说明

README.md JMeter          官方基本介绍
```



#### 2.1bin 目录，如图：

![image-20200615213503142](https://github.com/nnnnmkaka/nnnnmkaka.github.io/blob/master/images/posts/Jmeter/image-20200615213503142.png?raw=true)

```
jmeter.properties JMeter  核心配置文件，各种配置基本在这完成

log4j.conf JMeter         日志配置管理

jmeter.log JMeter         运行日志记录，什么输出信息、警告、报错都在这里进行了记录

jmeter.bat                windows 下 jmeter 启动文件

shutdown.cmd              windows 下 jmeter 关闭文件

stoptest.cmd              windows 下 jmeter 测试停止文件

jmeter-server.bat         windows 下 jmeter 服务器模式启动文件
```



#### 2.2<font color = "red">关键配置：</font>

```
#默认语言设置   
language=en

#捕捉cookie开关
CookieManager.save.cookies=true

#配置编辑器的字体和尺寸
jsyntaxtextarea.font.family=宋体
jsyntaxtextarea.font.size=20

#配置默认编码格式
sampleresult.default.encoding=UTF-8

# 配置远程主机host
remote_hosts=127.0.0.1

# 设置日志输出级别
log_level.jmeter=INFO

# 设置junit日志输出级别
log_level.jmeter.junit=DEBUG

# 设置输出报告模板格式
jmeter.save.saveservice.output_format = csv
```



#### 2.3：面板

![image-20200615215304478](https://github.com/nnnnmkaka/nnnnmkaka.github.io/blob/master/images/posts/Jmeter/image-20200615215304478.png?raw=true)

<br/>
**快捷菜单栏功能（从左到右）**

```
● 新建测试计划
● 选择测试计划模板创建一个新的测试计划
● 选择已经存在的测试计划并打开
● 关闭当前脚本
● 保存测试计划
● 另存测试计划
● 删除选定的元件，如果元件是父节点，那么其子节点元件也一同被删除
● 复制选定的元件及子元件
● 粘贴复制的元件及子元件
● 展开目录树
● 收起目录树
● 禁用或者启用元件，禁用元件的子元件也会被禁用
● 本机开始运行当前测试计划，按线程组的设置来启动
● 立即开始在本机运行当前测试计划
● 停止运行状态的测试计划，当前线程执行完成后停止
● 停止运行测试计划，立即终止，类似于杀进程
● 开启远程运行测试计划
● 停止运行远程测试计划，当前线程执行完成后停止
● 停止运行远程测试计划，类似于杀进程
● 清除运行过程中元件显示的响应数据，比如查看结果树中的内容，聚合报告中的内容，但不能清除日志控制台中的内容
● 清除所有元件的响应数据，包括日志
● 查找
● 清除查找 
● 函数助于对话框，这些函数在做参数化时会用到
● 帮助文档快捷方式
```






