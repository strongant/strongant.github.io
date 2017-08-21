title: Java 微服务实践- Spring Boot 系列（十四）WebService-学习笔记
author: strongant
tags:
  - springboot
  - webservices
categories: []
date: 2017-08-21 22:46:00
---
写在前面的话，之前曾在项目中使用过Webservices，记得当时使用过Apache的CXF，Apache CXF = Celtix + XFire。 随着RESTful服务的越来越流行，渐渐地WebService技术已经渐渐被人们所淘汰。下面主要为了技术的温习，跟上小马哥一起再次复习下那些年我们使用过的WebService。

* Web Services    定义：
又称之为 Web Service，是一种设计通过网络来支持相互协作的机器间交互的软件系统。它拥有被机器可处理的格式所描述的接口（如：WSDL），规定使用 SOAP消息的方式与其他系统交互，典型地以HTTP传输、XML序列化以及联合其他Web 相关标准。
— W3C, Web Services Glossary

* 标准整合方式
&emsp;XML（可扩展标记语言）
&emsp;SOAP（对象访问）
&emsp;WSDL（网络服务描述语言）
&emsp;UDDI（通用描述、发现与集成服务）

* 什么是 SOAP？
> SOAP 指简易对象访问协议
> SOAP 是一种通信协议
> SOAP 用于应用程序之间的通信
> SOAP 是一种用于发送消息的格式
> SOAP 被设计用来通过因特网进行通信
> SOAP 独立于平台
> SOAP 独立于语言
> SOAP 基于 XML
> SOAP 很简单并可扩展
> SOAP 允许您绕过防火墙
> SOAP 将被作为 W3C 标准来发展

* SOAP 数据封装
> SOAP 消息：在SOAP节点之间表达交换的信息
> SOAP 信封：鉴定SOAP 消息的XML封装元素
> SOAP 头块：SOAP 头的基本单元
> SOAP 头：一个或多个SOAP 头块集合
> SOAP 主体：交给接收端包含消息的主体
> SOAP 故障：SOAP 节点故障时处理消息
![ SOAP 数据封装](https://ws2.sinaimg.cn/large/006tKfTcgy1fiqkb2bp47j305205ejrh.jpg)

* 什么是WSDL?
> WSDL 指网络服务描述语言
> WSDL 使用 XML 编写
> WSDL 是一种 XML 文档
> WSDL 用于描述网络服务
> WSDL 也可用于定位网络服务
> WSDL 还不是 W3C 标准

* 什么是 UDDI？
> UDDI 是一个独立于平台的框架，用于通过使用 Internet 来描述服务，发现企业，并对企业服务进行集成。
> UDDI 指的是通用描述、发现与集成服务
> UDDI 是一种用于存储有关 web services 的信息的目录。
> UDDI 是一种由 WSDL 描述的 web services 界面的目录。
> UDDI 经由 SOAP 进行通信
> UDDI 被构建入了微软的 .NET 平台

以上概念定义解释来自[w3cschool](http://www.w3school.com.cn/)

其中需要注意的有使用Java6以后自带的xjc工具根据xsd生成webservices相关实体代码命令：
```
xjc -d src/main/java -p com.example.springbootwebservices.domain src/main/resources/META-INF/schemas/user.xsd
```
-d表示指定java包路径的相对目录

具体SpringBoot中使用webservices案例请参考：<https://github.com/mercyblitz/segmentfault-lessons/tree/master/spring-boot/lesson-14/spring-boot-lesson-14>




