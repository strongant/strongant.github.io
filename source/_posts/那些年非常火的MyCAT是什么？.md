title: 那些年非常火的MyCAT是什么？
author: strongant
tags: 'java,中间件,MyCAT'
date: 2020-02-29 23:28:09
---

## 什么是 MyCAT ？   

根据 MyCAT 官网 - http://mycat.io/ 的描述可以知道， MyCAT 是如下的一个东东：



* 一个彻底开源的，面向企业应用开发的大数据库集

* 支持事务、ACID、可以替代MySQL的加强版数据库

* 一个可以视为MySQL集群的企业级数据库，用来替代昂贵的Oracle集群

* 一个融合内存缓存技术、NoSQL技术、HDFS大数据的新型SQL Server

* 结合传统数据库和新型分布式数据仓库的新一代企业级数据库产品

* 一个新颖的数据库中间件产品

**总结一下就是： MyCAT 是一款数据库中间件，类似于Tomcat 容器或者相关的 Web 中间件。它主要用于解决数据库相关的问题。**

## MyCAT 能干什么？为什么要使用它？使用它可以解决什么问题？

* 用于支持海量数据存储，对海量数据进行分库分表

* 支持分库分表场景下的分布式事务

* 对多个数据源进行统一整合

* 高并发应用场景下，降低请求对单个数据库节点带来的灾难性压力

* 可以通过数据库中间间层面实现数据库读写分离，使其Java程序与数据库访问解耦

具体更多的特性可以参考 http://mycat.io/ 对MyCAT 特性的介绍。总结下来的一般常用的用途有3个，分别如下：
* 数据读写分离
![](https://tva1.sinaimg.cn/large/0082zybpgy1gc6855wtn7j30rt0dejru.jpg)
* 数据分片
![](https://tva1.sinaimg.cn/large/0082zybpgy1gc686jnz0ej30oh0bmweu.jpg)
* 多数据源整合
![](https://tva1.sinaimg.cn/large/0082zybpgy1gc687jlxi9j30kp0f0dg5.jpg)

## MyCAT 是唯一的数据库分库分表的解决方案吗？与其它的数据库中间件有什么区别？

我们来看如下图，图片来源于网络：

![](https://tva1.sinaimg.cn/large/0082zybpgy1gc67evmj2yj30ng0ek0th.jpg)

具体介绍如下：

1. Cobar 属于阿里 B2B 事业群，始于 2008 年，在阿里服役 3 年多，接管 3000+ 个 MySQL 数据库的 schema,

集 群日处理在线 SQL 请求 50 亿次以上。由于 Cobar 发 起人的离职， Cobar 停止维护。

2. My cat 是开源社区在阿里 cobar 基础上进行二次开发，解决了 cobar 存在的问题，并且加入了许多新

的功能在其中。青出于蓝而胜于蓝。

3. OneProxy 基于 MySQL 官方的 proxy 思想利用 c 进行开发的， OneProxy 是一款商业收费的中间件。舍

弃了一些功能，专注在性能和稳定性上。

4. kingshard 由小团队用 go 语言开发，还需要发展，需要不断完善 。

5. Vite ss 是 Youtube 生产在使用 架构很复杂。不支持 MySQL 原生协议，使用需要大量改造成本 。

6. Atlas 是 3 60 团队基于 mysql proxy 改写 ，功能还需完善 ，高并发下不稳定 。

7. MaxScale 是 mariadb MySQL 原作者维护的一个版本 研发的中间件

8. MySQLRout e 是 MySQL 官方 Oracle 公司发布的中间件

除了这些之外，我们去github 搜罗了一下，还有如下的一些数据库中间件：

1. Oceanus - 58同城数据库中间件，github star 数 500+；
2. SOHU-DBProxy - 是由 搜狐 数据库团队开发维护的一个基于MySQL协议的数据中间层项目。它在MySQL官方推出的MySQL-Proxy 0.8.3版本的基础上， 修改了大量bug，添加了很多功能特性。现在已经在sohu的多个业务线上使用， github star 数 700+；
3. Cetus是由C语言开发的关系型数据库MySQL的中间件，主要提供了一个全面的数据库访问代理功能。Cetus连接方式与MySQL基本兼容，应用程序几乎不用修改即可通过Cetus访问数据库，实现了数据库层的水平扩展和高可用。 ， github star 数 1000+；
4. Zebra是一个基于JDBC API协议上开发出的高可用、高性能的数据库访问层解决方案，是美团点评内部使用的数据库访问层中间件。github star 数 1500+;

## MyCAT作为分库分表中间件的原理是什么？
  Mycat收到一条SQL语句时， 首先解析SQL语句涉及的表， 接着查看此表的定义， 如果该表存在分片规则， 则获取SQL语句里分片字段的值， 并匹配分片函数， 得到该SQL语旬对应的分片列表， 然后将SQL语句发送到相应的分片去执行， 最后处理所有分片返回的数据并返回给客户端。 以 select* from Orders where prov=? 语句为例， 查找prov=wuhan, 按照分片函数， wuhan值存放在dnl上， 于是SQL语句被发送到Mysql l , 把DBI上的查询结果返回给用户。
  这里使用过阿里巴巴数据源 Druid 的同学不知道有没有发现，在Druid 中有一个叫做 SQLParser 的东东，这个玩意其实就是可以用来对原始的SQL语句，根据SQL语法树，对SQL进行加强改造的一个解析器，如果你们项目中有做过表数据的行权限或者列权限，则用这个Druid 的SQLParser 对所有的SQL 进行拦截改写是一个不错的方案，我之前在做数据权限的时候，参考相关实现时，也发现了MyCAT 中对于SQL的解析和改写也使用的这个，具体可以参考：https://github.com/MyCATApache/Mycat-Server/blob/f929f96a16852869bc9dc63f4c0f192ee02818e0/src/main/java/io/mycat/statistic/stat/UserSqlHighStat.java

## MyCAT 入门
  对于一款开箱即用的数据库分库分表中间件来说，MyCAT的入门相对简单，只需要按照官方的入门指导一步步往下走即可。

### 安装
安装之前我们首先准备环境，这里我们以企业中生产使用最多的Centos 7 为示例，进行下面的实操，本次CentOS 7 的内核版本如下：
```
Linux VM_0_14_centos 3.10.0-862.el7.x86_64
```
由于 MyCAT 源码是通过 Java 语言进行开发的，因此在我们使用之前，需要先检查自己的CentOS 7 主机具备不具备Java 环境，使用`java -version` 进行验证，如果没有安装JDK，则首先需要安装JDK并且配置Java环境变量才阔以，Centos 7 安装Java8 比较容易，只需要如下一行命令即可：
```
yum -y install java-1.8.0-openjdk
```
JDK8 安装完毕之后，进行如下验证，没有错误即可：
```
java -version 
```
```
openjdk version "1.8.0_242"
OpenJDK Runtime Environment (build 1.8.0_242-b08)
OpenJDK 64-Bit Server VM (build 25.242-b08, mixed mode)
```
接下来我们根据官方的入门指导，下载mycat server 包，下载地址为：http://dl.mycat.io/ , 这里我们实验时使用MyCAT  1.6.7.3 release 版本即可，下载 1.6.7.3 release 安装包到自己主机的 /opt 目录下 , 操作命令如下:
```
cd /opt/ && wget  /usr/local/ http://dl.mycat.io/1.6.7.3/20190927161129/Mycat-server-1.6.7.3-release-20190927161129-linux.tar.gz
```

下载完成之后，我们对mycat 安装包进行解压即可，命令如下：
```
tar -zxvf Mycat-server-1.6.7.3-release-20190927161129-linux.tar.gz
```
解压完成之后，我们看到 /opt 目录下有了一个 mycat 目录，我们进入到该目录下，发现它的子目录主要有如下：
```
.
├── bin
├── catlet
├── conf
├── lib
├── logs
├── tmlogs
└── version.txt
```
这里我们进入到conf 目录下，只关注如下的几个配置文件即可,其它的配置文件先不用关心：
```
server.xml  定义逻辑库，表、分片节点等内容
schema.xml  定义用户以及系统相关变量，如端口等
```
### 修改相关配置
为了对用户进行区分，此时，我们先修改 server.xml 中的 root 用户为 mycat，当使用 mycat 用户连接时，就代表我们直连的是 mycat，其它的配置不动，具体修改如下：

```
...
 <!-- 修改之前的 root 用户为 mycat  -->
	<user name="mycat" defaultAccount="true">
		<property name="password">123456</property>
		<property name="schemas">TESTDB</property>

		<!-- 表级 DML 权限设置 -->
		<!--
		<privileges check="false">
			<schema name="TESTDB" dml="0110" >
				<table name="tb01" dml="0000"></table>
				<table name="tb02" dml="1111"></table>
			</schema>
		</privileges>
		 -->
	</user>
...

</mycat:server>
```
接下来我们修改 schema.xml 

删除 <schema> 标签间的 表信息 dataNode 标签只留一个 dataHost 标签只留一个 writeHost
<readHost 只留一 对，如下:
```
<?xml version="1.0"?>
<!DOCTYPE mycat:schema SYSTEM "schema.dtd">
<mycat:schema xmlns:mycat="http://io.mycat/">

<schema name="TESTDB" checkSQLschema="false" sqlMaxLimit="100" dataNode="dn1" />
	<dataNode name="dn1" dataHost="host1" database="testdb" />
	<dataHost name="host1" maxCon="1000" minCon="10" balance="3"
			  writeType="0" dbType="mysql" dbDriver="native" switchType="1"  slaveThreshold="100">
		<heartbeat>select user()</heartbeat>
		<!-- can have multi write hosts -->
		<writeHost host="hostM1" url="118.25.102.189:3306" user="mycat"
				   password="123456"></writeHost>
	</dataHost>
</mycat:schema>
```

其中 <writeHost host="hostM1" 表示 MySQL 的主数据库，等会我们启动 MyCAT 之后进行验证读写否可以正常进行操作。

### 启动 MyCAT 前验证数据库远程访问情况
在验证之前由于我们的主数据库目前并没有创建mycat 这个用户，我们需要登录到 118.25.102.189:3306 数据库实例进行创建用户，脚本如下：
```sql
# 在 118.25.102.189 主机上登录 mysql 服务器
mysql -uroot 
# 登录成功后进行创建用户并授权
CREATE USER 'mycat'@'%' IDENTIFIED BY '123456';

```



### 开始登陆验证MyCAT登陆

在我们配置并创建完毕MyCAT 用户之后，就可以尝试登陆MyCAT 了， 通过以下方式登陆，进行验证，登陆方式如下：

```shell
# 完事之后我们开始尝试登陆MyCAT , mycat 默认的端口为 8066
mysql -umycat -h118.26.102.189  -p123456 -P8066
```

通过上述方式登陆成功后，如下图所示：

![](https://tva1.sinaimg.cn/large/00831rSTgy1gcdoqz49h4j30qq0h43yw.jpg)



