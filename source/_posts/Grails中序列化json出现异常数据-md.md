title: Grails中序列化json出现异常数据
author: strongant
tags:
  - 'grails, JsonBuilder'
categories:
  - grails
date: 2017-09-29 17:24:00
---

[Httobuilder](https://github.com/jgritman/httpbuilder) 是一个基于groovy简单的HTTP客户端工具。它基本支持常用的几种HTTP请求方式(GET,PUT,POST,DELETE,HEAD,PATCH)。

发生解析url值异常项目环境：
| Grails Version: 3.0.7
| Groovy Version: 2.4.4
| JVM Version: 1.8.0_121

由于是使用post方式给对方推送数据，所以我们先模拟一个请求服务，使用grails快速创建一个项目，然后编写一个方法，用于处理post请求，在后端输出接收到的具体数据是什么。步骤如下：

1.进入我的目录`/Users/bwh/study/grails` 生成一个grails的项目
```
cd /Users/bwh/study/grails && cd $_ && grails create-app test111
```
使用grails脚手架生成项目，如果没有产生其他异常，一般情况下我们会得到如下提示：
```
| Application created at /Users/bwh/study/grails/test111
```

2.进入刚才生成的项目中，由于本地已经使用了8080端口，修改grails项目的默认端口：
在`/Users/bwh/study/grails/test111/grails-app/conf/application.yml` 修改默认的8080端口，修改如下
```
---
...
# 修改项目默认端口8080为7070
server:
  port: 7799
...
```

3.打开项目，在当前项目的controllers目录下新建一个测试Controller，暂时叫做TestController，使用如下脚本进行生成相应的Controller文件，其当前目录结构如下：
```
...
├── grails-app
│   ├── assets
│   │   ├── images
│   │   ├── javascripts
│   │   └── stylesheets
│   ├── conf
│   │   ├── application.yml
│   │   ├── logback.groovy
│   │   └── spring
│   ├── controllers
│   │   ├── TestController.groovy
│   │   └── UrlMappings.groovy
...
```

4.还原现场,在刚才新建的TestController中添加此方法，用于接收对方传递过来的数据：
```
def postReport() {
        println params
        def jsonObject = request.JSON
        println "jsonObject: ${jsonObject}"
        println "jsonObject String: ${jsonObject as JSON}"
        render([code: 10000, msg: "测试获取数据!", data: params] as grails.converters.JSON)
    }
```

5.启动项目
```
grails run-app
```

用于接收post请求的测试服务已经启动完毕，接下来修改响应的推送地址进行发送数据即可。
相关测试代码：
```
#Test.groovyimport groovyx.net.http.ContentType
import groovyx.net.http.HTTPBuilder
import static groovyx.net.http.Method.POST
def baseURL = "http://localhost:7799/test/postReport"
def data = ["url": "http://${baseURL}/test/postReport"]
def client = new HTTPBuilder(baseURL)
client.request(POST, ContentType.JSON) {
    body = data
    response.success = { resp, json ->
        println "resp: ${resp}"
        println "success data: ${json}"
    }
    response.failure = { resp, json ->
        println "resp:${resp}"
        println "failure data: ${json}"
    }
}
```
运行测试代码后，发现测试服务端收到如下结果：

```
jsonObject String: {"url":{"valueCount":1,"strings":["http://","/test/postReport"],"bytes":[104,116,116,112,58,47,47,104,116,116,112,58,47,47,108,111,99,97,108,104,111,115,116,58,55,55,57,57,47,116,101,115,116,47,112,111,115,116,82,101,112,111,114,116,47,116,101,115,116,47,112,111,115,116,82,101,112,111,114,116],"values":["http://localhost:7799/test/postReport"]}}
```
可以发现url是被转换成一个字符数组了，为什么呢？
通过跟踪源码，发现它的body数据构造位于此方法：
```
protected Object doRequest( URI uri, Method method, Object contentType, Closure configClosure )
            throws ClientProtocolException, IOException {
        HttpRequestBase reqMethod;
        try { reqMethod = method.getRequestType().newInstance();
        // this exception should reasonably never occur:
        } catch ( Exception e ) { throw new RuntimeException( e ); }
        reqMethod.setURI( uri );
        RequestConfigDelegate delegate = new RequestConfigDelegate( reqMethod, contentType,
                this.defaultRequestHeaders,
                this.defaultResponseHandlers );
        configClosure.setDelegate( delegate );
        configClosure.setResolveStrategy( Closure.DELEGATE_FIRST );
        configClosure.call( reqMethod );
        return this.doRequest( delegate );
    }
```

其中函数执行到configClosure.call( reqMethod )方法时，其代理对象的body值为GStringImpl对象。由此可以判断，对map中的对象类型数据没有进行转换，因此出现了以上问题。

解决办法，使用groovy自带的json序列化类JsonBuilder进行将map对象先序列化成字符串然后再传递即可。
修改后测试代码如下：
```
import groovy.json.JsonBuilder
import groovyx.net.http.ContentType
import groovyx.net.http.HTTPBuilder
import static groovyx.net.http.Method.POST
def baseURL = "http://localhost:7799/test/postReport"
def data = ["link": "http://${baseURL}/test/postReport"]
def dataString = new JsonBuilder(data).toString()
def client = new HTTPBuilder(baseURL)
client.request(POST, ContentType.JSON) {
    body = dataString
    response.success = { resp, json ->
        println "resp: ${resp}"
        println "success data: ${json}"
    }
    response.failure = { resp, json ->
        println "resp:${resp}"
        println "failure data: ${json}"
    }
}
```

