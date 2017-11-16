title: Spring Security哈希认证记住我例子
author: strongant
tags:
  - SpringSecurity
categories:
  - SpringSecurity
date: 2017-11-17 00:19:00
---
在本教程中，我们将演示如何使用Spring Security 创建通过哈希认证记住我的应用程序。请记住，身份验证是一项功能，它允许网站在会话之间记住用户的身份。Spring Security提供了两种记住我的实现。一种使用哈希来保存基于cookie的令牌的安全性，我们将在本教程中解决这个问题。第二种是使用数据库或其他永久存储机制来存储生成的令牌。

## 基于哈希令牌的方法记住我

当用户启用记住我的身份验证时，会创建一个cookie并在后续登录时传递。这种方法使用散列来实现一个有用的记住我策略。该cookie的组成如下：

```
base64(username + ":" + expirationTime + ":" +
md5Hex(username + ":" + expirationTime + ":" password + ":" + key))

username:          As identifiable to the UserDetailsService
password:          That matches the one in the retrieved UserDetails
expirationTime:    The date and time when the remember-me token expires, expressed in milliseconds
key:               A private key to prevent modification of the remember-me token
```

> **注意：**记住我的记号只对指定的`expirationTime`和有效的`username`，`password`并且`key`不会改变。**警告：**这是一个潜在的安全问题。当记住我的令牌被恶意的用户代理捕获时，这个用户代理能够使用令牌直到它到期。如果需要更好的安全性，你应该使用这种`persistent remember-me token`方法。

## 项目结构

我们先看看项目结构。

![Spring Security记住我哈希认证的例子的项目结构](https://memorynotfound.com/wp-content/uploads/spring-security-remember-me-hashing-project-structure.png)

## Maven的依赖

我们使用Apache Maven来管理我们的项目依赖关系。确保以下依赖存在类路径中。

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>
    <groupId>com.memorynotfound.spring.security</groupId>
    <artifactId>hashing-remember-me</artifactId>
    <version>1.0.0-SNAPSHOT</version>
    <url>https://memorynotfound.com</url>
    <name>Spring Security - ${project.artifactId}</name>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.5.8.RELEASE</version>
    </parent>

    <properties>
        <java.version>1.8</java.version>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-security</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>
        <dependency>
            <groupId>org.thymeleaf.extras</groupId>
            <artifactId>thymeleaf-extras-springsecurity4</artifactId>
        </dependency>

        <!-- bootstrap and jquery -->
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>bootstrap</artifactId>
            <version>3.3.7</version>
        </dependency>
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>jquery</artifactId>
            <version>3.2.1</version>
        </dependency>

        <!-- testing -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.springframework.security</groupId>
            <artifactId>spring-security-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
```

## Spring Security记住我哈希认证配置

要想使记住我散列认证配置可用，我们需要在Spring中注册。在下一节中，我们将演示Java和XML配置。

###### SPRING JAVA配置

在这里，我们正使用Java代码的方式配置记住我身份认证的配置。通过扩展我们的Spring配置类`WebSecurityConfigurerAdapter`，我们可以简单地配置记住我的身份验证`configure(HttpSecurity http)`方法。我们需要配置一个安全和唯一的密钥。这个密钥通常是一个强大而独特的密码。我们可以随意配置“记住我”cookie名称并设置令牌有效期。默认为2周。

```
package com.memorynotfound.spring.security.config;

import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.builders.WebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.web.util.matcher.AntPathRequestMatcher;

// 使用注解方式配置SpringSecurity记住我配置时，开启此注解
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    public void configure(WebSecurity web) throws Exception {
        web.ignoring()
                .antMatchers(
                        "/js/**",
                        "/css/**",
                        "/img/**",
                        "/webjars/**");
    }

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
                .authorizeRequests()
                    .anyRequest().authenticated()
                .and()
                    .formLogin()
                        .loginPage("/login")
                            .permitAll()
                .and()
                    .logout()
                        .invalidateHttpSession(true)
                        .clearAuthentication(true)
                        .logoutRequestMatcher(new AntPathRequestMatcher("/logout"))
                        .logoutSuccessUrl("/login?logout")
                            .permitAll()
                .and()
                    .rememberMe()
                        .key("unique-and-secret")
                        .rememberMeCookieName("remember-me-cookie-name")
                        .tokenValiditySeconds(24 * 60 * 60);
    }

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.inMemoryAuthentication().withUser("user").password("password").roles("USER");
    }

}
```

###### SPRING XML配置

该文件`spring-security-config.xml`位于`src/main/resources/`文件夹中，是等效的Spring XML配置文件。

```
<?xml version="1.0" encoding="UTF-8"?>
<beans:beans xmlns="http://www.springframework.org/schema/security"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xmlns:beans="http://www.springframework.org/schema/beans"
             xsi:schemaLocation="http://www.springframework.org/schema/security
                                 http://www.springframework.org/schema/security/spring-security.xsd
                                 http://www.springframework.org/schema/beans
                                 http://www.springframework.org/schema/beans/spring-beans.xsd">

    <http>
        <intercept-url pattern="/login" access="permitAll()"/>
        <intercept-url pattern="/js/**" access="permitAll()"/>
        <intercept-url pattern="/css/**" access="permitAll()"/>
        <intercept-url pattern="/img/**" access="permitAll()"/>
        <intercept-url pattern="/webjars/**" access="permitAll()"/>
        <intercept-url pattern="/**" access="isAuthenticated()"/>
        <!--Spring Security 4.0以后默认开启宽展请求伪造保护，这里配置禁用，不安全的操作。-->
         <csrf disabled="true"/>

        <form-login 
                login-page="/login"/>
        <logout
                invalidate-session="true"
                logout-url="/logout"
                logout-success-url="/login?logout"/>
        <remember-me
                key="unique-and-secret"
                remember-me-cookie="remember-me-cookie-name"
                token-validity-seconds="86400"/>
    </http>

    <authentication-manager>
        <authentication-provider>
            <user-service>
                <user name="user"
                      password="password"
                      authorities="ROLE_USER" />
            </user-service>
        </authentication-provider>
    </authentication-manager>

</beans:beans>
```

## 创建控制器

我们创建了一些简单的导航控制器

```
package com.memorynotfound.spring.security.web;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class HomeController {

    @GetMapping("/")
    public String greeting(){
        return "index";
    }

    @GetMapping("/login")
    public String login() {
        return "login";
    }
}
```

## 启动Spring

我们使用Spring Boot来启动我们的应用程序。

```
package com.memorynotfound.spring.security;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
// uncomment if you want to use Spring Security XML Configuration
// 当使用xml的方式配置时，开启此注解注释掉Java代码方式的配置
// @ImportResource("classpath:spring-security-config.xml")
public class Run {

    public static void main(String[] args) {
        SpringApplication.run(Run.class, args);
    }
}
```

## Thymeleaf模板

我们用Thymeleaf来创建我们的视图。这些模板使用`bootstrap`和`jquery`，它们从`org.webjars`中加载。

### 创建登录页面

该`login.html`页面位于该`src/main/resources/templates`文件夹中。在表单中我们创建了一个`remember-me`复选框。当用户启用记住我的身份验证时，cookie会传递给浏览器，该浏览器将以指定的时间到期。当用户在会话之间访问页面时，Spring Security会使用基于记住我的token自动认证。

```
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="utf-8"/>
    <meta http-equiv="X-UA-Compatible" content="IE=edge"/>
    <meta name="viewport" content="width=device-width, initial-scale=1"/>

    <link rel="stylesheet" type="text/css" th:href="@{/webjars/bootstrap/3.3.7/css/bootstrap.min.css}"/>
    <link rel="stylesheet" type="text/css" th:href="@{/css/main.css}"/>

    <title>Login</title>
</head>
<body>
<div class="container">
    <div class="row">
        <div class="col-md-4 col-md-offset-4">
            <div class="panel panel-default">
                <div class="panel-body">
                    <div class="text-center">
                        <h3><i class="glyphicon glyphicon-lock" style="font-size:2em;"></i></h3>
                        <h2 class="text-center">Login</h2>
                        <div class="panel-body">

                            <div th:if="${param.error}">
                                <div class="alert alert-danger">
                                    Invalid username or password.
                                </div>
                            </div>
                            <div th:if="${param.logout}">
                                <div class="alert alert-info">
                                    You have been logged out.
                                </div>
                            </div>

                            <form th:action="@{/login}" method="post">
                                <div class="form-group">
                                    <div class="input-group">
                                        <span class="input-group-addon">@</span>
                                        <input id="username"
                                               name="username"
                                               autofocus="autofocus"
                                               class="form-control"
                                               placeholder="Username"/>
                                    </div>
                                </div>
                                <div class="form-group">
                                    <div class="input-group">
                                        <span class="input-group-addon">
                                            <i class="glyphicon glyphicon-lock"></i>
                                        </span>
                                        <input id="password"
                                               name="password"
                                               class="form-control"
                                               placeholder="Password"
                                               type="password"/>
                                    </div>
                                </div>
                                <div class="form-group">
                                    <label>
                                        <input id="remember-me"
                                               name="remember-me"
                                               type="checkbox"/> Remember me
                                    </label>
                                </div>
                                <div class="form-group">
                                    <button type="submit" class="btn btn-success btn-block">Login</button>
                                </div>
                            </form>

                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>

<script type="text/javascript" th:src="@{/webjars/jquery/3.2.1/jquery.min.js/}"></script>
<script type="text/javascript" th:src="@{/webjars/bootstrap/3.3.7/js/bootstrap.min.js}"></script>

</body>
</html>
```

### 创建一个安全的页面

该`index.html`页面位于`src/main/resources/templates`目录中。

```
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org"
      xmlns:sec="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="utf-8"/>
    <meta http-equiv="X-UA-Compatible" content="IE=edge"/>
    <meta name="viewport" content="width=device-width, initial-scale=1"/>

    <link rel="stylesheet" type="text/css" th:href="@{/webjars/bootstrap/3.3.7/css/bootstrap.min.css}"/>
    <link rel="stylesheet" type="text/css" th:href="@{/css/main.css}"/>

    <title>Registration</title>
</head>
<body>
<div class="container">
    <h1>Spring Security Remember Me Hashing Configuration Example</h1>

    <div sec:authorize="isRememberMe()">
        The user: <span sec:authentication="name"></span> is logged in by "Remember Me Cookies".
    </div>

    <div sec:authorize="isFullyAuthenticated()">
        The user: <span sec:authentication="name"></span> is logged in by "Username / Password".
    </div>

</div>
<footer>
    <div class="container">
        <p>
            &copy; Memorynotfound.com
            <span sec:authorize="isAuthenticated()" style="display: inline-block;">
                    | Logged user: <span sec:authentication="name"></span> |
                    Roles: <span sec:authentication="principal.authorities"></span> |
                    <a th:href="@{/logout}">Sign Out</a>
            </span>
        </p>
    </div>
</footer>

<script type="text/javascript" th:src="@{/webjars/jquery/3.2.1/jquery.min.js/}"></script>
<script type="text/javascript" th:src="@{/webjars/bootstrap/3.3.7/js/bootstrap.min.js}"></script>

</body>
</html>
```

## 演示

访问`http://localhost:8080`和页面被重定向到`http://localhost:8080/login`。

![Spring Security哈希认证的记住我](https://memorynotfound.com/wp-content/uploads/spring-security-remember-me-hashing-form-login.png)

当*用户*和*密码*填写正确后，页面被重定向到`http://localhost:8080/`。

![img](https://memorynotfound.com/wp-content/uploads/spring-security-remember-me-hashing-login-success.png)

当检查我们的应用程序的cookie时，我们可以看到Spring创建了我们之前配置的`remember-me-cookie-name`cookie。

![img](https://memorynotfound.com/wp-content/uploads/spring-security-remember-me-hashing-cookies.png)

当您删除`JSESSIONID`Cookie并刷新页面时，当”remember-me“Cookie未过期时，您将自动登录。

![img](https://memorynotfound.com/wp-content/uploads/spring-security-remember-me-hashing-remove-app-cookie.png)

## 参考

- [Spring Security Remember Me Documentation](https://docs.spring.io/spring-security/site/docs/current/reference/htmlsingle/#remember-me-hash-token)
- [WebSecurityConfigurerAdapter JavaDoc](https://docs.spring.io/spring-security/site/docs/current/apidocs/org/springframework/security/config/annotation/web/configuration/WebSecurityConfigurerAdapter.html)
- [RememberMeConfigurer JavaDoc](https://docs.spring.io/spring-security/site/docs/current/apidocs/org/springframework/security/config/annotation/web/configurers/RememberMeConfigurer.html)

## 下载

下载它 - [spring-security-remember-me-hashing-authentication-configuration-example](https://memorynotfound.com/wp-content/uploads/spring-security-remember-me-hashing-authentication-configuration-example.zip)

> 原文链接：<https://memorynotfound.com/spring-security-remember-hashing-authentication-example/>