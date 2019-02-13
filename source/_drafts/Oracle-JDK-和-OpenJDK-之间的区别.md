---
title: Oracle JDK 和 OpenJDK 之间的区别
author: strongant
tags: JDK,JAVA,OpenJDK,OracleJDK
---

## **1.简介**

在本文中，我们将探讨[Oracle Java Development Kit](https://www.oracle.com/technetwork/java/index.html)和[OpenJDK](http://openjdk.java.net/)之间的差异。我们先快速浏览一下，然后进行比较。之后，我们将看到其他JDK实现的列表。

## 2. Oracle JDK和Java SE历史

JDK（Java Development Kit）是Java平台编程中使用的软件开发环境。它包含一个完整的Java运行时环境，即所谓的私有运行时。该名称来自于它包含的工具多于独立的JRE以及开发Java应用程序所需的其他组件。

**Oracle强烈建议使用术语JDK来引用Java SE（标准版）开发工具包**（还有Enterprise Edition和Micro Edition平台）。

我们来看看Java SE的历史：

- *JDK Beta - 1995*
- *JDK 1.0 - 1996年1月*
- *JDK 1.1 - 1997年2月*
- *J2SE 1.2 - 1998年12月*
- *J2SE 1.3 - 2000年5月*
- *J2SE 1.4 - 2002年2月*
- *J2SE 5.0 - 2004年9月*
- *Java SE 6 - 2006年12月*
- *Java SE 7 - 2011年7月*
- **Java SE 8（LTS） - 2014年3月**
- *Java SE 9 - 2017年9月*
- *Java SE 10（18。3） - 2018年3月*
- **Java SE 11（18.9 LTS） - 2018年9月**
- Java SE 12（19。3） - 2019年3月

注意：不再支持斜体版本。

我们可以看到Java SE的主要版本大约每两年发布一次，直到Java SE 7.从Java SE 6开始花了五年时间，之后又花了三年时间升级到Java SE 8。

自Java SE 10以来，我们可以期待每六个月发布一次新版本。但是，并非所有版本都是长期支持（LTS）版本。由于Oracle的发布计划，LTS产品发布仅每三年发布一次。

Java SE 11是最新的LTS版本，Java SE 8将在2020年12月之前获得免费的公共更新，用于非商业用途。

在2010年Oracle收购Sun Microsystems之后，这个开发工具包得到了它的当前名称。在此之前，它的名字是SUN JDK，它是Java编程语言的官方实现。

## 3. OpenJDK

OpenJDK是Java SE 平台版本的免费开源实现。它最初于2007年发布，是Sun Microsystems于2006年开始开发的结果。

当然，我们应该强调  **OpenJDK是自SE 7版以来Java标准版的官方参考实现**。

最初，它仅基于JDK 7.但是，**从Java 10开始，Java SE平台的开源参考实现是JDK项目http://openjdk.java.net/projects/jdk/的责任**。而且，就像Oracle一样，JDK项目也将每六个月发布一次新功能。

我们应该注意到，在这个长期运行的项目之前，JDK Release Projects发布了一个功能，然后停止了。

现在让我们看看OpenJDK版本：

- *OpenJDK 6项目 - 基于JDK 7，但经过修改后提供了Java 6的开源版本*
- *OpenJDK 7项目 - 2011年7月28日*
- *OpenJDK 7u项目 - 该项目开发Java Development Kit 7的更新*
- *OpenJDK 8项目 - 2014年3月18日*
- *OpenJDK 8u项目 - 该项目开发Java Development Kit 8的更新*
- *OpenJDK 9项目 - 2017年9月21日*
- *JDK10项目于2018年3月10日至20日发布*
- **JDK11项目于2018年9月11日至25日发布**
- JDK12项目发布 - [稳定阶段](http://openjdk.java.net/jeps/3)

## 4. Oracle JDK与OpenJDK

在本节中，我们将重点介绍Oracle JDK和OpenJDK之间的主要区别。

### 4.1. 发布时间表

正如我们所提到的，**Oracle将每三年发布一次，**而**OpenJDK将每六个月发布一次**。

Oracle为其版本提供长期支持。另一方面，OpenJDK仅支持对发布的更改，直到下一个版本发布。

### 4.2. 许可证

**Oracle JDK根据Oracle二进制代码许可协议获得许可**，而**OpenJDK具有GNU通用公共许可证（GNU GPL）版本2，使用了一个修正版本**。

使用Oracle平台时会产生一些许可影响。如Oracle [宣布的](https://java.com/en/download/release_notice.jsp)那样，在没有商业许可的情况下，在2019年1月之后发布的Oracle Java SE 8的公开更新将无法用于商业，商业或生产用途。但是，OpenJDK是完全开源的，可以自由使用。

### 4.3. 性能

有**两者之间没有真正的技术差别，因为针对Oracle JDK构建过程是基于OpenJDK的的**。

在性能方面，**Oracle在响应能力和JVM性能方面要好得多**。由于其对企业客户的重要性，它更加关注稳定性。

相比之下，OpenJDK将更频繁地发布版本。结果，我们可能遇到不稳定的问题。根据[社区反馈](https://www.reddit.com/r/java/comments/6g86p9/openjdk_vs_oraclejdk_which_are_you_using/)，我们知道一些OpenJDK用户遇到了性能问题。

### 4.4. 功能

如果我们比较功能和选项，我们将看到  **Oracle产品具有Flight Recorder，Java Mission Control和Application Class-Data Sharing** **功能**，而**OpenJDK具有Font Renderer功能**。

此外，**Oracle有更多的垃圾收集选项和更好的渲染器**，我们可以在[另一个比较中](https://www.educba.com/oracle-vs-openjdk/)看到。

### 4.5. 发展与人气

**Oracle JDK由Oracle Corporation完全开发，**而**OpenJDK由Oracle，OpenJDK和Java Community开发**。然而，红帽，Azul Systems，IBM，Apple Inc.，SAP AG等顶级公司也积极参与其开发。

正如我们从前一小节的链接中看到的那样，当涉及到**在其工具中使用Java开发工具包的顶级公司（**例如Android Studio或IntelliJ IDEA）的**流行时**，**Oracle JDK是更****受欢迎的**。

另一方面，主要的Linux发行版（Fedora，Ubuntu，Red Hat Enterprise Linux）提供OpenJDK作为默认的Java SE实现。

## 5.自Java 11以来的变化

正如我们在[Oracle博客文章中](https://blogs.oracle.com/java-platform-group/oracle-jdk-releases-for-java-11-and-later)看到的那样  ，从Java 11开始有一些重要的变化。

首先，**Oracle将**使用Oracle JDK作为Oracle产品的一部分，将**开源****GNU通用公共许可证v2与Classpath Exception（GPLv2 + CPE）****和商业许可证结合**使用，或者**更改其历史“** **BCL** **”许可证，** 或者服务，或不欢迎开源软件。

每个许可证都有不同的版本，但这些版本在功能上只与一些装饰和包装差异相同。

此外，OpenJDK现在提供传统的“商业功能”，如Flight Recorder，Java Mission Control和Application Class-Data Sharing，以及Z Garbage Collector。因此，**Oracle JDK和OpenJDK构建从Java 11开始基本相同**。

让我们看看主要的区别：

- 使用*-XX：+ UnlockCommercialFeatures*选项时，Oracle的Java 11工具包会发出警告，而在OpenJDK版本中，此选项会导致错误
- Oracle JDK提供了一种配置，可将使用日志数据提供给“高级管理控制台”工具
- Oracle一直要求第三方加密提供程序由已知证书签名，而OpenJDK中的加密框架具有开放加密接口，这意味着可以使用哪些提供程序没有限制
- Oracle JDK 11将继续包括安装程序，品牌和JRE打包，而OpenJDK构建目前可用作*zip*和*tar.gz*文件
- 该*javac的-释放*命令行为有所不同了Java 9和Java 10个目标由于一些额外的模块在Oracle的版本存在
- *java -version*和*java -fullversion*命令的输出将Oracle的构建与OpenJDK构建区分开来

## 6.其他JDK实现

现在让我们快速浏览一下其他活动的Java Development Kit实现。

### 6.1. 自由开源

按字母顺序列出的以下实现是开源的，可以免费使用：

- [Amazon Corretto](https://aws.amazon.com/corretto/)
- Azul Zulu
- Bck2Brwsr
- CACAO
- Codename One
- DoppioJVM
- Eclipse OpenJ9
- GraalVM CE
- HaikuVM
- HotSpot
- Jamiga
- JamVM
- Jelatine JVM
- Jikes RVM (Jikes Research Virtual Machine)
- JVM.go
- leJOS
- Maxine
- Multi-OS Engine
- RopeVM
- uJVM

### 6.2. 专有实现

还有受版权保护的实施：

- Azul Zing JVM
- CEE-J
- Excelsior JET
- GraalVM EE
- Imsys AB
- JamaicaVM（aicas）
- JBlend（Aplix）
- MicroJvm（IS2T - 工业智能软件技术）
- OJVM
- PTC Perc
- SAP JVM
- Waratek CloudVM for Java

与上面列出的[有效实现一起](https://en.wikipedia.org/wiki/List_of_Java_virtual_machines#Active)，我们可以看到[非有效实现](https://en.wikipedia.org/wiki/List_of_Java_virtual_machines#Inactive)的列表   以及每个实现的简短描述。

## 7.结论

在本文中，我们专注于当今最流行的两个Java开发工具包。

我们首先描述了它们中的每一个，然后强调了它们之间最显着的差异。然后，我们特别关注自Java 11以来的变化和差异。最后，我们列出了今天可用的其他有效实现。

> 译自 [https://www.baeldung.com/oracle-jdk-vs-openjdk?fbclid=IwAR1OdHRjnypD4ShnAMHOd-Ef4iW1-3duKqaiGT2s5ijv48mEDXg8EMhWkZs](https://www.baeldung.com/oracle-jdk-vs-openjdk?fbclid=IwAR1OdHRjnypD4ShnAMHOd-Ef4iW1-3duKqaiGT2s5ijv48mEDXg8EMhWkZs)