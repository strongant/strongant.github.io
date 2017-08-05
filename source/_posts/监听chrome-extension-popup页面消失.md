title: 监听chrome extension popup页面消失
author: strongant
tags:
  - chrome扩展
  - JavaScript
  - ''
  - ''
categories: []
date: 2017-08-05 16:46:00
---
## 需求
*  当用户不小心点击了鼠标或者离开了扩展的popup页面，此时需要对一些数据进行清空或者删除一些不必要的数据.

## 遇到的问题
* 然而chrome 扩展官方并没有对popup或者browserAction提供相关页面消失时的监听事件

## 解决办法
* 通过不断的查找资料和查阅chrome扩展开发文档，我们可以使用消息通信连接的方式解决了这个问题
### 具体步骤:
* 首先在你需要监听页面消失事件的js文件中与background建立连接，相关代码:
```
//这里主要是为了与background建立连接，当页面关闭的时候连接就会断开，此时background中你注册的连接关闭函数此时会执行，因为background环境一直存在，除非你关闭了电脑
 var port = chrome.runtime.connect();
```
*  在background环境注册断开连接时需要处理的方法，相关代码:
```
  chrome.runtime.onConnect.addListener(function (externalPort) {
        externalPort.onDisconnect.addListener(function() {
        var ignoreError = chrome.runtime.lastError;
        console.log("onDisconnect");
        });
    });
```

### 总结
* 通过以上的方式便实现了类似对popup页面消失时做一些事情的需求。感谢StackOverFlow，神一样的解决问题社区，致敬！