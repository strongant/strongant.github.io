title: 阿里巴巴Java开发规约的IDEA插件使用
author: strongant
tags:
  - 工具
categories:
  - 工具
date: 2017-10-16 09:21:00
---
> 作者：不想当码农的程序员
>
> 原文：http://www.jianshu.com/p/2f271e6d675c编辑：Moon

就在10月15日上午9：00，阿里巴巴在杭州云栖大会《研发效能峰会》上，正式发布《阿里巴巴Java开发手册》扫描插件，该插件在扫描代码后，将不符合《手册》的代码按 `Blocker`/ `Critical`/ `Major`三个等级显示在下方，甚至在IDEA上，还基于Inspection机制提供了实时检测功能，编写代码的同时也能快速发现问题所在。对于历史代码，部分规则实现了批量一键修复的功能。

Git地址为：https://github.com/alibaba/p3c

# IDea的安装方式：

IDEA版的插件发布到了IDEA官方仓库中(最低支持版本14.1.7，JDK1.7+)，只需打开

```
 Settings >> Plugins >> Browse repositories 
```

输入 Alibaba 搜索一下便可以看到对应插件了，点击安装等待安装完成。

如图:

![img](http://mmbiz.qpic.cn/mmbiz_png/R3InYSAIZkGhoJb7iaWQumUzkaqD7EfucQlBLVlajIOpsRBVgS2zkt9vRmuq19ONe2iaQJZicNN4qbRBOJNl9hOjg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

这里写图片描述

# Eclipse的安装方式：

Eclipse版插件支持4.2（Juno，JDK1.8+）及以上版本，提供Update Site，通过

```
 Help >> Install New Software
```

然后输入 `https://p3c.alibaba.com/plugin/eclipse/update`即可看到安装列表，安装即可。

插件的更新，可以通过 `Help>>CheckforUdates` 进行新版本检测。

# 怎么用

呵呵 右键，，看图 --

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

## 还有自动提示的效果

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

可以说是非常棒了

![img](http://mmbiz.qpic.cn/mmbiz_png/R3InYSAIZkGhoJb7iaWQumUzkaqD7EfucAxVUicBBUX2WQvI9osBsh4uXOl4ibzlfT9j0M3zjOMDRWgZw9AKDub0w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

## **推荐阅读**

- [程序员你为什么这么累【续】：如何应对需求变更](http://mp.weixin.qq.com/s?__biz=MzAxODcyNjEzNQ==&mid=2247484377&idx=1&sn=1ad98afc78d5cc11a07410e9cf0a3c9c&chksm=9bd0ae41aca72757e4599d71717ed817a77b4e9a10c2b40f54793f1d5b0a95fd144bb48ae21e&scene=21#wechat_redirect)
- [Spring4All社区正式招募Spring Guides翻译小分队~](http://mp.weixin.qq.com/s?__biz=MzAxODcyNjEzNQ==&mid=2247484376&idx=1&sn=957c161c2a390347ba53c26f118475f1&chksm=9bd0ae40aca72756a7ade252454a8658d082b331a191d980c24a7f40ce82eab0dbee020fb5b2&scene=21#wechat_redirect)
- [海外IT工程师工作福利揭秘](http://mp.weixin.qq.com/s?__biz=MzAxODcyNjEzNQ==&mid=2247484375&idx=1&sn=ac19066f568d57e27ac319a5e5ddbed4&chksm=9bd0ae4faca72759f9c4af93cb083f68aceb4c9fee7388f42a41acd9e8d93e5a60a1e7c91f4f&scene=21#wechat_redirect)
- [一个不可思议的MySQL慢查分析与解决](http://mp.weixin.qq.com/s?__biz=MzAxODcyNjEzNQ==&mid=2247484272&idx=1&sn=a2f30419fc8e2c1cce86c79e0c44b264&chksm=9bd0aee8aca727fe3c78c9f9d2178f4b7e85bf0890d066fd9607091dcc36d8d8dbf647a3a379&scene=21#wechat_redirect)
- [都在说微服务，那么微服务的反模式和陷阱是什么](http://mp.weixin.qq.com/s?__biz=MzAxODcyNjEzNQ==&mid=2247484291&idx=1&sn=0794ce828d667fa5be8dc3494886282d&chksm=9bd0ae1baca7270d1089a923f45e70408673a9efb3f8753fb3b3014ec097302bcf52251601fa&scene=21#wechat_redirect)

长按指纹

一键关注

![img](http://mmbiz.qpic.cn/mmbiz_jpg/R3InYSAIZkHCWVvIZUEa8CQWAStjKkNYbXIicURV5tx4GzRBepUWO9sq8nrkVHwvVylyERaKgQyKvUianyIjelicQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1)

![img](http://mmbiz.qpic.cn/mmbiz_png/ich5amXrtqL2ZPTngbnFMYk4cXjia5JTX1Al0Q9NT8qfwAJoq3CWN1feicKU2VGUjiatLSXW2HDo73su4ZHxZoTABA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)