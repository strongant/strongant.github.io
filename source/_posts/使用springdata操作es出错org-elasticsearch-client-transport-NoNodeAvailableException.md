title: 使用springdata操作es出错org.elasticsearch.client.transport.NoNodeAvailableException
author: strongant
date: 2017-07-21 09:48:10
tags: [SpringData,Elasticsearch]
categories: [SpringData]
comments: true
reward: true
---
  之前的项目中使用的是http-client操作es，比较轻量级。目前为了学习下springdata，使用Java API 的方式来操作ES，但是在引入SpringData的es模块依赖后，操作es并未成功，出现以下错误：
```
org.elasticsearch.client.transport.NoNodeAvailableException: None of the configured nodes are available: [{#transport#-1}{127.0.0.1}{127.0.0.1:9300}]
```

**注意：**如果你下载elasticsearch的压缩包安装的话，可能不会出现该问题！因为es默认的配置文件cluster.name是elasticsearch。但是奇葩的是使用brew安装es之后，默认的elasticsearch.yml的配置项成了这样：cluster.name: elasticsearch_bwh，就是这个原因导致了这个问题的产生，项目启动后控制台一直抛这个错：
```
transport#-1}{127.0.0.1}{127.0.0.1:9300} not part of the cluster Cluster [Assassin], ignoring...
```
当执行添加操作时，提示：
```
org.elasticsearch.client.transport.NoNodeAvailableException: None of the configured nodes are available: [{#transport#-1}{127.0.0.1}{127.0.0.1:9300}]
```
最后需要注意的是，如果你修改了es默认的集群名称，则需要在src/main/resources/application.properties配置文件中进行指定：

spring.data.elasticsearch.clusterName=elasticsearch_bwh
通过源码org.springframework.boot.autoconfigure.data.elasticsearch.ElasticsearchProperties可以看到，默认的
clusterName为elasticsearch。
 
希望可以帮助遇到此类问题的同学。