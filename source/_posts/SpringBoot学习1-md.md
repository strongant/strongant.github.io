---
title: SpringBoot学习1.md
date: 2017-03-12 23:42:17
tags: SpringBoot
---
## SpringBoot

> Takes an opinionated view of building production-ready Spring applications. Spring Boot favors convention over configuration and is designed to get you up and running as quickly as possible.

**遵循建立生产就绪Spring应用程序的观点。SpringBoot支持约定优于配置的惯例，旨在让您尽快启动和运行。**

> Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run". We take an opinionated view of the Spring platform and third-party libraries so you can get started with minimum fuss. Most Spring Boot applications need very little Spring configuration.

**SpringBoot可以轻松的创建单独的，生产级的基于Spring的应用，您可以“直接运行”。我们为Spring平台和第三方库提供了开箱即用的设置，这样你就可以有条不斋的开始。大多数的SpringBoot程序只需要很少的Spring配置。 **

### Features
* Create stand-alone Spring applications
* Embed Tomcat, Jetty or Undertow directly (no need to deploy WAR files)
* Provide opinionated 'starter' POMs to simplify your Maven configuration
* Automatically configure Spring whenever possible
* Provide production-ready features such as metrics, health checks and externalized configuration
* Absolutely no code generation and no requirement for XML configuration

### 功能
* 创建标准独立的Spring应用程序
* 直接嵌入Tomcat、Jetty或者Undertow（不需要部署WAR文件）
* 提供建议的‘starter’POM模板以简化您的Maven配置
* 每当可能时自动配置Spring
* 提供生产就绪的功能，如指标，运行状况检查和外部化配置
* 绝对没有代码生成和不需要XML配置


The reference guide includes detailed descriptions of all the features, plus an extensive howto for common use cases.
该[参考指南](https://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle)包含所有功能的详细说明，以及广泛的[如何使用](https://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#howto)共同使用情况。

### Quick Start
If you are Java developer you can use start.spring.io to generate a basic project, follow the "Quick Start" example below, or read the reference documentation getting started guide.

### 快速开始
如果你是一名Java程序员，你可以通过[start.spring.io](https://start.spring.io/)生成基本项目，按照下面的“快速开始”示例或者阅读参考文档的[入门指南](https://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#getting-started)。

The recommended way to get started using spring-boot in your project is with a dependency management system – the snippet below can be copied and pasted into your build. Need help? See our getting started guides on building with Maven and Gradle.

spring-boot在项目中开始使用的推荐方法是使用依赖关系管理系统 - 下面的代码段可以复制并粘贴到您的构建中。需要帮忙？请参阅我们使用[Maven](https://spring.io/guides/gs/maven/)和 [Gradle](https://spring.io/guides/gs/gradle/)构建的入门指南。

Maven
```
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>1.5.1.RELEASE</version>
</parent>
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```
Gradle
```
dependencies {
    compile("org.springframework.boot:spring-boot-starter-web:1.5.1.RELEASE")
}
```

```
hello/SampleController.java
```
```
package hello;

import org.springframework.boot.*;
import org.springframework.boot.autoconfigure.*;
import org.springframework.stereotype.*;
import org.springframework.web.bind.annotation.*;

@Controller
@EnableAutoConfiguration
public class SampleController {

    @RequestMapping("/")
    @ResponseBody
    String home() {
        return "Hello World!";
    }

    public static void main(String[] args) throws Exception {
        SpringApplication.run(SampleController.class, args);
    }
}
```

### Spring Boot CLI
Spring Boot ships with a command line tool that can be used if you want to quickly prototype with Spring. It allows you to run Groovy scripts, which means that you have a familiar Java-like syntax, without so much boilerplate code. Follow the instructions in our main documentation if you want to install the Spring Boot CLI.

### Spring Boot 命令行工具
Spring Boot附带一个命令行工具，如果你想快速使用Spring原型，可以使用它。它允许你运行Groovy脚本，这意味着你有一个熟悉的类似Java的语法，没有那么多的样板代码。如果要[安装Spring Boot CLI](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#getting-started-installing-the-cli)，请按照我们的主要文档中的说明进行[操作](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#getting-started-installing-the-cli)。


