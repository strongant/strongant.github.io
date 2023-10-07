title: 分布式定时任务XXL-JOB在我司的选型
author: strongant
tags: '分布式任务调度,xxl-job'
date: 2020-09-16 23:39:44
---

## 任务系统

### 任务 
1. **什么时间**
2. **什么地点**
3. **做什么事**

### 一个简单的任务

![](http://ww1.sinaimg.cn/large/bc9918a2gy1gimyeiy1ooj20ya0retab.jpg)

### cron

![](http://ww1.sinaimg.cn/large/bc9918a2gy1gimyf1m8qnj21ck0kajsc.jpg)

### 早期的 cron
V7，1979
1. 在Version 7 Unix里是一个系统服务
2. 只用 root 运行任务
3. 算法简单直接

更多详情请参考: <https://en.wikipedia.org/wiki/Cron>


### 早期的 cron 运行逻辑

1. 读 /usr/lib/crontab 文件
2. 如果有命令要在当前时间执行，就用 root 用户去执行命令
3. Sleep 1 minute
4. 重新从步骤 1 开始

### 支持多用户的 cron
Unix System V，1983
1. 启动的时候读取所有用户下的 .crontab 文件
2. 计算出每个 crontab 文件里需要执行的命令的下一次执行时间
3. 把这些命令按下一次执行时间排序后放入队列里
4. 进入主循环
① 计算队列里第一个任务的执行时间与当前的时间差
② Sleep 直到第一个任务执行时间
③ 后台执行任务
④ 计算这个任务的下一次执行时间，放回队列，排序

### 近代的 cron

Linux，1991

1. Vixie cron(Paul Vixie 1987)
2. Version 3 Vixie cron(1993)
3. Version 4.1 ISC Cron(2004)
4. anacron, dcron, fcron

### cron 的局限性

1. 单机
2. 无界面
3. 功能比较简单
4. 多机器的情况下任务维护成本较高

## 分布式任务系统 

### 分布式系统的特点
1. 分布性
2. 对等性(没有控制系统的主机, 也没有被控制的从机)
3. 并发性
4. 缺乏全局时钟(缺乏全局时钟序列控制)
5. 故障总是会发生


### 分布式 cron

![](http://ww1.sinaimg.cn/large/bc9918a2gy1gimyft8mxsj21700hmdgr.jpg)

### 我只是不爱动，不是懒

![](http://ww1.sinaimg.cn/large/bc9918a2gy1gimyg82m1vj20z00koqjv.jpg)

### 分布式系统对任务调度的几点要求

1、平台：快速开发、业务复用、自维护和扩展；
2、HA/集群：避免单点故障，发挥集群优势
3、弹性扩缩：适应业务快速发展
4、故障处理：Failover、失败告警
5、阻塞处理：耗时任务阻塞
5、⾼性能：调度和任务解耦，全异步化
6、自运维：自助维护、实时监控、快速了解任务进展


### 我眼里的“西施”

1. 可替代 cron
2. 分布式、高可用
3. 支持多种任务属性
4. 易用
5. 易部署




##  为什么选择使用 XXL-JOB 
  项目中有这样的需求：需要使用定时器从 A 和 B 系统中同步不同的表中的数据，并且对数据进行一定的加工处理，最后将最终的数据写入到数据仓库DB，需要实现针对不同的数据源进行配置（这块也就是多数据源的支持），任务配置可以根据任务量的大小使用不同的资源。对数据同步的时效性和性能要求非常高，并且这些定时任务可以通过页面配置的方式做到灵活，可控制。

  通过以上的这些需求，我们对目前业界比较流行的任务调度框架进行了技术选型，通过研究发现，目前使用比较广泛的任务调度框架有 XXL-JOB 和 Elastic-JOB ，因此，参考 XXL-JOB 官方对不同任务调度平台的比对，如下图所示：

![](http://ww1.sinaimg.cn/large/bc9918a2gy1gimygpwsirj217s0naafe.jpg)    

针对以上对比，我们选择了 XXL-JOB 任务调度框架，因为它相比于其他任务调度框架来说，具有更好的用户体验、有良好的运维支持、任务依赖、任务路由原生支持，通过调研发现，框架自带的任务路由策略已经满足我们的业务场景，并且支持分片任务，当任务延迟较高时，可以利用分片的方案加速任务的处理。

##  XXL-JOB 介绍
> XXL-JOB是⼀个轻量级分布式任务调度框架。拥有“HA、弹性扩缩、故障处理、阻塞处
理、⾼性能、自运维”等特点。
其核⼼部分包括：
1、调度模块（调度中⼼）：负责管理任务信息，触发任务执⾏，自身不承担业务逻辑；
同时提供“日志、报表、告警、GLUE、注册中⼼”等功能；
2、执⾏模块（执⾏器）： 负责接收调度中⼼请求，进⾏任务逻辑执⾏、终⽌、日志加载
等操作；专注于任务执⾏相关操作；

### XXL-JOB 发展

• 2015年中，着⼿设计XXL-JOB，提交第⼀个Commit
• 2015-11月，发布首个Release版本，同期当选为开源中国月度热门项目
• 2016-01月，我司展开定制和接⼊，⾄今调度近百万次
• 2017-05-03，应邀参加“第62期开源中国源创会”现场分享XXL-JOB
• 2017-10月，当选为开源中国首批GVP项目
• ……
• ⾄今，XXL-JOB登记接⼊公司50+（点评、移动、平安、海尔、优信），
社区群8个，群成员约3000 ⼈

### XXL-JOB 架构图

![](http://ww1.sinaimg.cn/large/bc9918a2gy1gimyh8kl4vj219i0m8al6.jpg)
### XXL-JOB 特性全览

1、简单
2、动态
3、调度中心HA（中心式）
4、执行器HA（分布式）
5、任务Failover
6、一致性
7、自定义任务参数
8、调度线程池
9、弹性扩容缩容
10、邮件报警
11、状态监控
12、Rolling执行日志
13、GLUE：提供Web IDE
14、数据加密
15、任务依赖
16、推送maven中央仓库
17、任务注册
18、路由策略
19、运行报表
20、脚本任务
21、阻塞处理策略
22、失败处理策略
23、分片广播任务
24、动态分片
25、事件触发

### HA/集群

![](http://ww1.sinaimg.cn/large/bc9918a2gy1gin0cq0n2xj21s40ui4hv.jpg)

### 弹性扩缩

![](http://ww1.sinaimg.cn/large/bc9918a2gy1gin009ca4mj21nq0siwv3.jpg)

### 执行器路由策略

![](http://ww1.sinaimg.cn/large/bc9918a2gy1gin08gqqvgj21dc0nk0zb.jpg)

### 故障转移 & 忙碌转移

![](http://ww1.sinaimg.cn/large/bc9918a2gy1gin0dtlklbj21ik0p8afd.jpg)

### 分片任务 & 动态分片
![](http://ww1.sinaimg.cn/large/bc9918a2gy1gimyn5o76ij215i0p0tmi.jpg)

### 阻塞策略 & 失败处理策略

 ![](http://ww1.sinaimg.cn/large/bc9918a2gy1gimynngodnj21ii0qm43e.jpg)



### 触发规则

* Cron 表达式
如：每日凌晨 2 点，进行“PV 数据计算”的任务
* 任务依赖触发
如：父任务“PV 数据计算”执行结束后，触发多业务线的“PV 报表生成”的多个子任务
* 事件触发/API 服务
如：类 MQ 场景，短信验证码、订单创建等。

### 任务模式
1、BEAN 模式：JobHandler、Spring Bean
2、GLUE 模式(Java )：Web IDE、在线开发、版本回溯、Java 语言、动态编译（IOC）、实时生效、Rolling

Log
3、GLUE 模式(Shell)：Web IDE、在线开发、版本回溯、实时生效、Rolling Log
4、GLUE 模式(Python)
5、GLUE 模式(NodeJS)

（其中“GLUE 模式(NodeJS)”来源于 “icyblazek@github”同学提交的 PR，XXL-JOB 理论上支持任何类型脚本

语言的任务模式扩展）
### GLUE 模式

![](http://ww1.sinaimg.cn/large/bc9918a2gy1gimyo6rz8vj21fg0oaqam.jpg)

### 执行日志 & Rolling Log

 ![](http://ww1.sinaimg.cn/large/bc9918a2gy1gimyoojunwj21o00ts7jz.jpg)

## XXL-JOB 搭建
1、安装 Mysql，初始化 XXL-JOB 底层库表

• 2、编译部署“调度中心”

• 3、编译部署“执行器”（参考多个 Sample 项目）

》》》开发第一个 JobHandler
入门文档 （可参考文档 “快速入门”章节：）： <http://www.xuxueli.com/xxl-job/>


