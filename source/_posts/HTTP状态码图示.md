title: HTTP状态码图示
author: strongant
tags:
  - http
categories: []
reward: true
date: 2017-08-13 16:00:00
---
这里总结下我们日常开发中常用的HTTP状态码，分享一个老外对HTTP状态码形象化用图片表示的网站：<https://http.cat/>

总结如下：

<center>
![](https://ws2.sinaimg.cn/large/006tKfTcgy1fii4a1juo9j30ee0bj3zw.jpg)
**表示服务器已经接收到了请求头，并且客户端应该继续发送请求体。**
![](https://ws2.sinaimg.cn/large/006tKfTcgy1fii4a0xeytj30dw0b40t4.jpg)
**表示请求方已经要求服务器切换协议，并且服务器已经接受并会进行处理。**
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fii4a0l292j30dk0b4wfc.jpg)
**HTTP 请求成功的标准应答。实际的应答内容由请求使用的方法来决定。**
![](https://ws2.sinaimg.cn/large/006tKfTcgy1fii4a01i3rj30do0b4gmt.jpg)
**请求已经被接受，并且请求所对应的资源已经被创建。**
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fii49zt676j30dw0b4q3l.jpg)
**请求已被接受，尚未完成处理，也有可能会被拒绝。**
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fii49zmp71j30dw0b474u.jpg)
**在成功处理请求后服务器并没有返回任何实体内容。**
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fii49zfw3vj30dw0b4aak.jpg)
**依照子请求的数量的不同，消息体包含不同的响应代码。**
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fii49z28hnj30b40dwjs1.jpg)
**表示被请求的资源可以提供多种选项让客户端进行选择**
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fii49yvwcaj30dw0b4t9b.jpg)
**该请求应当被定向到给定的URI（统一资源定位符）**
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fii49yrg7qj30dl0b40u3.jpg)
**这是一个工业实践和标准相互矛盾的例子。一些Web应用和框架会使用302状态码**
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fii49yl9uuj30dw0b4q3h.jpg)
**对应当前请求的响应可以使用GET方法从另一个URI获取**
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fii49yc066j30b40dwwfb.jpg)
**表示资源自上次请求以来没有被改变。**
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fii49y6afmj30dw0b4mxp.jpg)
**（译注：被请求的资源必须通过指定的代理才能被访问） 大多数HTTP客户端不会正确响应这个状态码，主要是出于安全性的原因**
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fii49y3ty9j30b40dwq3l.jpg)
**在这种情况下，请求会从另外的URI响应但是未来的请求仍会使用原始的URI**
![](https://ws2.sinaimg.cn/large/006tKfTcgy1fii45xt3cpj30dw0b43zb.jpg)
**因为错误的语法，请求不能完成**
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fii45xk04fj30df0b43zy.jpg)
**当需要授权，但授权失败或还没有授权时返回的状态码**
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fii45xd1i2j30dw0b4aav.jpg)
**该状态码是为了将来可能的需求而预留的。这个代码通常不使用，但是其最初的意图是可以被某种电子货币所使用。**
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fii45x75byj30dr0b4aaw.jpg)
**请求有效，但是服务器拒绝响应它。**
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fii45wzw3qj30dt0b4q4o.jpg)
**请求的资源不能找到，但是将来也许可用。**
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fii45wvyv0j30dm0b4aaz.jpg)
**请求某资源时使用的请求方法不能被该资源所支持。**
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fii45wlh8kj30de0b475n.jpg)
**被请求资源能够产生的内容不满足请求头中指定的类型。**
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fii45w9496j30dr0b4t9z.jpg)
**服务器等待请求超时**
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fii45vuqk7j30dr0b4t9z.jpg)
**因为请求中存在冲突导致请求无法被处理**
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fii45vcm96j30dw0b4mxq.jpg)
**被请求的资源已不可用，同时后续也不再可用。**
![](https://ws2.sinaimg.cn/large/006tKfTcgy1fii45uwpztj30dw0b4gma.jpg)
**请求所对应的资源需要指明长度，但请求中并没有包含长度。**
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fii45ug6rkj30dk0b40tl.jpg)
**其请求数据实体过大，超过服务器处理能力。**
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fii45u41r2j309h0dw0tq.jpg)
**URI过长，服务器不能处理**
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fii45tomc8j30dw0b4dgb.jpg)
**客户端请求部分文件，但是服务器并不能提供这个范围值。**
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fii45tgczyj30di0b4jse.jpg)
**服务器不能满足请求头重指定的要求。**
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fii45t9fuzj30dw0b4t93.jpg)
**在实际HTTP服务器中不会实现该状态码**
![](https://ws2.sinaimg.cn/large/006tKfTcgy1fii45t5bqvj30b40dw0ta.jpg)
**请求格式正确但是因为存在语意错误无法响应。**
![](https://ws2.sinaimg.cn/large/006tKfTcgy1fii45szla3j30dw0b4758.jpg)
**当前资源被上锁**
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fii45ssuddj30dw0b4mxx.jpg)
**因为之前的请求失败而导致了本次请求失败**
![](https://ws2.sinaimg.cn/large/006tKfTcgy1fii45sob45j30dw0b43za.jpg)
**在WebDav Advanced Collections 草案中定义**
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fii45sg74yj30dk0b4wfm.jpg)
**客户端应该切换到不同的协议**
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fii45s8zp7j30dh0b4gn4.jpg)
**用户在指定时间内发送的请求过多。**
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fii45s1jgbj30dm0b4jss.jpg)
**因为请求中的单个域过大、或者全部域全加起来过大。**
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fii45rv5zjj30ds0b4wfo.jpg)
**在Nginx记录中使用，表示服务器没有向客户端返回信息并且已经关闭了连接**
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fii45ropewj30dw0b4gm5.jpg)
**微软所扩展的一个状态码**
![](https://ws2.sinaimg.cn/large/006tKfTcgy1fii45ri7x7j30dd0b4abj.jpg)
**当没有其他更加确切的信息可以给出时，给出的一个一般性错误信息。**
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fii45rd75fj30da0b4wff.jpg)
**作为网关或者代理工作的服务器尝试执行请求时，从上游服务器接收到无效的响应**
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fii45r4qr0j30dw0b4mxs.jpg)
**服务器当前不可用。**
![](https://ws2.sinaimg.cn/large/006tKfTcgy1fii45qt3zuj30dw0b40tg.jpg)
**请求的透明内容协商导致循环引用**
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fii45qnic4j30da0b40tl.jpg)
**服务器无法存储完成请求所必须的内容。**
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fii45qi54qj30de0b43za.jpg)
**服务器在处理请求时发现一个无限循环**
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fii45qbsaoj30b40dwgm6.jpg)
**尽管很多服务器使用该协议，但其并没有在任何RFC中说明**
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fii45q4f5qj30df0b4t9r.jpg)
**这个状态码没有在任何RFC中说明，但微软公司在用。**
</center>