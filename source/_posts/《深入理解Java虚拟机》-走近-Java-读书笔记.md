title: 《深入理解Java虚拟机》-走近 Java 读书笔记
author: strongant
tags:
  - JVM
categories:
  - JVM
date: 2018-03-26 22:48:00
---
## 走进Java

### 概述

#### Java 的优点

* 结构严谨
* 平台无关性，一次编写到处运行
* 提供安全的内存管理和访问机制，避免大部分的内存泄漏和指针越界
* 热点代码检测和运行时编译优化，使得 Java 应用随运行时间的增加而获得更高的性能
* 具有一套完善的应用程序接口，丰富的第三方库

#### Java 技术体系

* Java 程序设计语言
* 各种硬件平台上的 Java 虚拟机 
* Java API 类库
* Class 文件格式
* 来自商业机构和开源的第三方 Java 类库

##### JDK组成
Java 程序设计语言 + Java 虚拟机 + Java API 类库

##### JRE 组成
Java SE API 子集 + Java 虚拟机

##### Java 技术体系所包含的内容
![ Java 技术体系所包含的内容](http://p67ct12ik.bkt.clouddn.com/jvm%E6%8A%80%E6%9C%AF%E4%BD%93%E7%B3%BB.png)

##### Java  体系划分的 4 个平台
* Java Card
* Java ME
* Java SE
* Java EE

#### Java 发展史
![](http://p67ct12ik.bkt.clouddn.com/java_timeline.png)

* JDK 1.0: Java虚拟机、Applet、AWT等；
* JDK 1.1：JAR文件格式、JDBC、JavaBeans、RMI、内部类、反射；
* JDK 1.2：拆分为J2SE/J2EE/J2ME、内置JIT编译器、一系列Collections集合类；
* JDK 1.3：JNDI服务、使用CORBA IIOP实现RMI通信协议、Java 2D改进；
* JDK 1.4：正则表达式、异常链、NIO、日志类、XML解析器和XSLT转换器；
* JDK 1.5：自动装箱、泛型、动态注解、枚举、可变参数、遍历循环、改进了Java内存模型、提供了java.util.concurrent并发包；
* JDK 1.6：提供动态语言支持、提供编译API和微型HTTP服务器API、虚拟机优化（锁与同步、垃圾收集、类加载等）；
* JDK 1.7：G1收集器、加强对Java语言的调用支持、升级类加载架构；
* JDK 1.8：Lambda表达式等；

#### Java 虚拟机发展史

![](http://on-img.com/chart_image/5ab90628e4b0a248b0e637d5.png)

#### 展望 Java 技术的未来

* 模块化
* 混合语言
* 多核并行
* 进一步丰富的语法
* 64 位虚拟机



