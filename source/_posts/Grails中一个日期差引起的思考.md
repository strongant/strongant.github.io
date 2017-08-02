title: Grails中一个日期差引起的思考
author: strongant
tags:
  - groovy
  - grails
  - gorm
categories: []
date: 2017-08-02 22:02:00
---
### 需求如下

** 对某表中的数据进行查询限制，当根据某个条件进行查询表记录时，如果该记录的查询时间与当前服务器时间相差大于一周，则允许查询操作，否则不允许重复查询操作。 **

#### 编码

根据当前需求进行编码，代码如下：
```
class ExampleController {
    def test() {
        ...
        def obj = XXX.findByName('xxx')
        def limitDays = 7
        if(obj && daysBetween(obj.queryTime,new Date())<=7){
                            render([code: 10101, msg: "查询失败，7天内不允许重复查询", data: []] as grails.converters.JSON)
                            return
 
        }
        ...
    }
    //TODO: 将此处判断移动至service或者util类
    static def daysBetween(def startDate, def endDate) {
        use(groovy.time.TimeCategory) {
            def duration = endDate - startDate
            return duration.days
        }
    }
}
```

出现bug:
**本地测试程序可以正常执行，但是发现在生产环境下并没有正常执行**

错误解决：
**以为是groovy.time.TimeCategory原生类有bug，将比较日期间隔天数的方法修改为如下:**

```
//TODO: 将此处判断移动至service或者util类
static boolean keep7Days(endDate){
     return (System.currentTimeMillis()-endDate.getTime())<3600*1000*24*7
}
```

修改结果：
问题依然存在。

进行分析：

** 当我们从某张表中根据某个条件查询一条记录，如果该条件对一个多条重复记录，那数据库将按照表中的记录插入顺序返回最初插入的一条记录。因此，当根据某条件进行匹配查询时，应该按照id降序排列后取得第一条即可。 **

解决办法：
```
...
def obj = XXX.find("from XXX as b where b.xxx=:xxx order by b.id desc",[xxx:xxx])
...

```

通过以上方式，我们便可以得到最后插入的记录，此时再使用时间差进行判断就不会出现匹配不正确问题。

#### 总结

当项目中遇到bug时应该找到问题的根源再进行解决。在测试的过程中数据应该保持和生产环境数据一致！

#### 彩蛋

推荐两个不错的播客平台：

 [内核恐慌](https://ipn.li/kernelpanic/)
 [比特新声](http://banlan.show/bitvoice)