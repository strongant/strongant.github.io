title: Mac下使用jenvs安装Java9
author: strongant
tags:
  - java
  - jdk
categories:
  - java
date: 2017-10-23 16:36:00
---
JDK9已经距离现在发布了好一段时间了，如果你还没有尝试一下，建议安装体验体验！一般情况下，我们的PC上基本都会安装多个版本的JDK，此时我们为了多个JDK版本的切换，这里，强烈推荐使用[jenvs](https://github.com/gcuisinier/jenv),关于具体使用请参考作者的详细介绍。这里不多做介绍。

已经安装了jenvs的同学，则跳过上面的内容，直接看下面内容--如何将JDK9添加到jenvs的管理中。

1.[下载JDK9](http://www.oracle.com/technetwork/java/javase/downloads/jdk9-downloads-3848520.html)

2.安装完毕后，只需要打开终端做如下操作即可（jdk9安装完毕后，默认在mac系统的/Library/Java/JavaVirtualMachines/）：
```bash
jenv add /Library/Java/JavaVirtualMachines/jdk-9.0.1.jdk/Contents/Home
```

3.以上操作执行完毕后，会得到如下提示：
```
oracle64-9.0.1 added
9.0.1 added
9.0 added
```

4.切换Java9
```
jenv shell 9.0.1
```
5.此时我们便可以使用jenv进行切换，尝试使用java9的新特性了！

