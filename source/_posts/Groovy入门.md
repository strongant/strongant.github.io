title: Groovy入门-安装
author: strongant
tags:
  - groovy
categories: []
date: 2017-08-13 11:03:00
---
**使用groovy开发差不多已经四个多月了，这里分享一些自己在groovy方面的一些总结。**


## 介绍
* Groovy 是一种新兴的运行于 Java™ 平台之上的编程语言
* 它提供与已有 Java 代码的无缝集成，并引入了一些强大的新特性，比如闭包和元编程
* 简单来讲，Groovy 就是在 21 世纪 Java 语言的的效果
* Groovy是Java平台上脚本语言，抽象程度更高，可以更简单快速的开发，可以编写更少的代码
* 与Java语言无缝集成，可以称为“超级Java”
* 使用“类JAVA语法”，Java程序员可以快速过度
*  Groovy与Java二进制兼容，都生成字节码，所以可以与使用Java语言所编写的框架和组件完美集成，并且效率安全方面比其他脚本语言要高
* Groovy对象就是Java对象，使用JDK相同的API
* 可以保护整个Java产业在Java上巨大的投资
* 在中小型项目中可以替代Java，在大型Java项目中可以嵌入Groovy应用


## 安装，使用官网推荐的安装方法
首先安装SDKMAN! (一个软件开发工具包管理工具)
```
$ curl -s get.sdkman.io | bash
```
使其SDKMAN工具生效
```
$ source "$HOME/.sdkman/bin/sdkman-init.sh"
```
* 安装最新版本的Groovy:
```
$ sdk install groovy
```

* 等待一会儿之后，显示安装完毕，此时我们可以使用此命令验证groovy是否安装成功
```
$ groovy -version
```

## 安装2
1. 在官网下载groovy sdk
下载地址:
https://akamai.bintray.com/9a/9a20d8868edbbc82a8edd03b6ae6f7dfbe406e42a468f2c44d5285493f679676?__gda__=exp=1466580235~hmac=4c1a4086a45aca9a522aac513d022d04f90eec437163110a69a441bf823143a2&response-content-disposition=attachment%3Bfilename%3D%22apache-groovy-sdk-2.4.7.zip%22&response-content-type=application%2Fx-www-form-urlencoded
2. 进行解压：
```
$ unzip apache-groovy-sdk-2.4.7.zip
```
3. 配置到全局变量或者用户所在的变量环境
```
sudo vi /etc/profile
//添加groovy解压目录所在的位置
//我当前安装目录为：/home/devbwh/groovy-2.4.7，在/etc/profile文件末尾添加一下配置：
export GROOVY_HOME=/home/devbwh/groovy-2.4.7
export PATH=GROOVY_HOME/bin:$PATH
```
4. 使其生效
```
source /etc/profile
```

## 安装3(Mac安装)
```
brew install groovy
```



