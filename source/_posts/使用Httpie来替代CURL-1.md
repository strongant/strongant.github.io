title: 使用Httpie来替代CURL
author: strongant
tags:
  - 工具
categories: []
date: 2017-09-10 21:51:00
---
当下的一些比较人们的测试接口的客户端工具大概有以下几种：

Postman（使用最多，一个基于Chrome的app）

CURL（在终端下工作的文件传输工具）

Httpie（终端下比较友好、简洁、特性更多，功能更强大）

个人在终端下比较推荐使用Httpie，原因如下：

举个例子，如果我们发起一个请求，获取一个JSON字符串，如果我们使用CURL进行获取的话，需要使用管道命令结合python自带的json.tool这个脚本才能完成，` curl  https://httpbin.org/get | python -m json.tool`

如果我们使用Httpie的话，只需要这样：`http  https://httpbin.org/get`,可以发现它不仅返回了body内容，也同时返回了header信息。当然如果我们只需要看body内容，此时只需要进行筛选即可，使用如下命令请求即可：`http  https://httpbin.org/get --body`,如果只需要header信息，可以这样：`http  https://httpbin.org/get --header`。更多特性，请参考：https://httpie.org/

Httpie默认会将返回的JSON数据进行格式化，不再需要二次转换，并且它会使用颜色将一些不同类型的数据加以区分，这样也方便我们进行查看。

这里介绍下Mac下的安装方式：
由于Httpie依赖Python，一般情况下Mac下已经自带了Python环境，只不过版本可能并不是最新的。使用brew安装即可：

```
brew install httpie
```

安装成功后我们进行测试是否可用：
```
http ifconfig.me/all.json
```

正常情况下便可以得到带颜色的格式良好的JSON数据。