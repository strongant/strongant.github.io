title: Ubuntu安装Java8环境
author: strongant
date: 2017-07-26 21:32:41
tags:
---
## Ubuntu 系统安装Java8 JDK

1.添加ppa
```
sudo add-apt-repository ppa:webupd8team/java
```
2.更新系统
```
sudo apt-get update
```
3.开始安装
```
sudo apt-get install oracle-java8-installer -y
```

4.验证是否安装成功
```
java -version
```

5.安装脚本gist地址(执行脚本时记得回车继续，其中弹出确认安装提示选择是即可，脚本执行完毕后就已经成功安装Java8了，安装大约得等待一段时间，请耐心等待！):
<https://gist.github.com/strongant/740f58dd6f116a4ff4d156805340bb95>
