title: Grails中神奇的HibernateCriteriaBuilder
author: strongant
tags:
  - Grails
  - Hibernate
categories:
  - Grails
date: 2018-01-28 10:13:00
---
Grails 中 HibernateCriteriaBuilder 用于动态为类构建一些常用的查询方法。

通过 metaClass 绑定方法，也就是 groovy 的 MOP 特性进行动态绑定方法。

HibernateCriteriaBuilder 派生于  AbstractHibernateCriteriaBuilder，AbstractHibernateCriteriaBuilder派生于GroovyObjectSupport。

其中 GroovyObjectSupport 实现了 GroovyObject 接口。

其中动态支持分页列表的实现在AbstractHibernateCriteriaBuilder中的invokeMethod有详细的说明。平时我们使用的时候只需要 键入 find 然后就会根据当前类的属性进行自动补全，你是要查询一条还是要查询多条记录，至于它的转化操作也定义在此，如图：

![upload successful](/images/pasted-0.png)

grails.properties   = params 绑定属性存在恶意风险，比如用户会伪造一些属性，从而导致类的一些属性修改被自动注入，影响到数据库中对应的表的具体记录。

具体的类图：


![upload successful](/images/pasted-1.png)

其中常用的方法接口定义在此：org.grails.orm.hibernate.IHibernateTemplate
