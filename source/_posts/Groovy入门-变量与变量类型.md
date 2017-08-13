title: Groovy入门-变量与变量类型
author: strongant
reward: true
tags:
  - groovy
categories: []
date: 2017-08-13 14:34:00
---
## Groovy的变量与变量类型

### 变量与常量的定义，维基百科对其定义如下

变量：变量通常是可被修改的，即可以用来表示可变的状态。
常量：指一个数值固定不变的常量，例如圆周率、自然对数的底。与之相反的是变量。

### 动态变量与静态变量

动态变量：动态变量在程序执行过程中建立，随函数的调用需要动态的分配存储空间，调用结束释放所占用存储空间。
静态变量：静态变量（Static Variable）在计算机编程领域指在程序执行前系统就为之静态分配（也即在运行时中不再改变分配情况）存储空间的一类变量。

### Groovy中的变量类型

Groovy中可以使用的变量类型有数字（Number）类型、字符串（String）类型、布尔（Boolean）类型以及引用（Reference）类型。

1.数字（Number）类型：包括整数类型和浮点数类型。

* 其中，整数包含正数、负数和零，都是Integer类的实例，比如1、-1和0都属于整数类型。
* 浮点数包含小数部分，都是BigDecimal类的实例，比如1.11、-3.11都属于常见的浮点数类型。在数字字面值加上可显示指定变量的类型，整数Long型（Long）、整数BigInteger型（BigInteger）、浮点型Float（Float）、浮点数Double（Double）。

2.字符串（String）类型：通过使用引号将文本值组织起来，如'Hello'、"Hello"、"""Hello"""，其中使用单引号（‘）、双引号("")、三双引号（"""）都是允许的。

3.布尔（Boolean）类型： 包含true和false。如def judge = true,def 在groovy中表示任意类型，在程序运行期动态推到其最终类型。

4.引用（Reference）类型：用于表示指向一个对象。比如：def user = new User(name:"张三")。其中user表示的就是User对象的实例。

### Groovy中变量的声明和使用

  声明的变量名称通常被称为标识符。在Groovy中，标识符的命名规则如下：
- 标识符必须由字母和数字组成，大小写敏感，标识符的首字符必须是字母。下划线(_)允许出现在标识符中，以字母看待。标识符绝对不允许是 Groovy关键词。
  声明变量时需要引入变量名称，可以为变量指定初始值，也可以确定变量能被引用的作用域或者作用范围。当在程序中首次使用某个变量时，需要使用Groovy关键`def`关键字声明，不能在同一个作用域内声明两次相同的变量名。

示例：
```
/**
 * Groovy中对不同类型变量的定义和使用
 * @author strongant
 * Contact me at <a href="mailto:strongant1994@gmail.com">strongant1994@gmail.com</a>
 * @see
 * @since 2017/8/13
 */
class DefineUseVariable {
    public static void main(String[] args) {
        // 声明一个值为admin，类型为String的变量
        def name = 'admin'
        // 声明一个值为10的数字，类型为Integer
        def age = 10
        // 声明一个值为20.0的数字，类型为BigDecimal
        def money = 20.0
        // 声明一个值为true的布尔变量，类型为Boolean
        def isMale = true
        // 再次声明一个值为admin，类型为String的变量，下面代码将运行错误。
        //def name = "Bob"
        // 输出变量的值和类型。
        //注意，在输出的时候，如果要使用'$'符号进行输出变量，则字符串必须使用双引号的三双引号的情况下，才可以正常输出变量值。
        // 如果是单引号，则不会输出变量值，原样输出
        println "name is ${name}. I'm ${age} years old. I hava ${money} dollars."
        println "name type: ${name.class}"
        println "age type: ${age.class}"
        println "money type: ${money.class}"
        println "isMale type: ${isMale.class}"
        // 声明一个值为10.0的浮点型的变量，类型为Float
        def floatTypeVariable = 10.0F
        println "floatTypeVariable type: ${floatTypeVariable.class}"
        // 声明一个值为10.0的浮点型的变量，类型为Double
        def doubleTypeVariable = 10.0D
        println "doubleTypeVariable type: ${doubleTypeVariable.class}"
        // 声明一个值为10000的长整型的变量，类型为Long
        def longTypeVariable = 10000L
        println "longTypeVariable type: ${longTypeVariable.class}"
        // 声明一个值为10000的长整型的变量，类型为大长整型BigInteger
        def bigIntegerTypeVariable = 10000G
        println "bigIntegerTypeVariable type: ${bigIntegerTypeVariable.class}"
    }
}
```
示例的代码也可以在此地址找到：<https://gist.github.com/strongant/22c489f5a51f416d1bf3e97d86f031dd>

### Groovy变量自动转换和强制转换示意图

![Groovy变量自动转换和强制转换示意图](https://ws1.sinaimg.cn/large/006tKfTcgy1fii2v2bh27j31by0y6wl6.jpg)

### Groovy中关键字
**abstract** **case** **do** **finally** **instanceof** **package** **strictfp** **throws** **with** **any** **catch** **double** **float** **int** **private** **super** **transient** **as** **assert** **char** **class** **else** **enum** **for** **if** **interface** **long** **protected** **public** **switch** **synchronized** **true** **try** **boolean** **continue** **extends** **implements** **native** **return** **this** **void** **break** **def** **false** **import** **new** **short** **threadsafe** **volatile** **byte** **default** **final** **in** **null** **static** **throw** **while**


