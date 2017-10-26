title: groovy中的each坑小记
author: strongant
tags:
  - groovy
categories: []
date: 2017-10-26 15:29:00
---
### 前言

在`Java`编程中，如果要跳出`for`循环，直接使用`break`即可。但是在`groovy`的`each`方法中，如果使用`break`，则程序运行时就会报如下错误：`the break statement is only allowed inside loops or switches。`

### 如何跳出each循环呢？

  `groovy`的`each`方法是一个闭包操作，如果想跳出当前项，则可以使用`return true`。 但是存在一个问题：就是这里的`return true`并不完全等价于`java` `for`循环中的`break`操作。它更像是`java` `for`循环中的`continue`操作，跳出当前循环，继续下一次循环。至于这里的原因，有待研究。
  
### 诡异的产生

  当使用“==”操作符号进行比较时，`return true`等价于`java` `for`循环中的`continue`，但如果是“>=” 操作符的话，等价于`java` `for`循环中的`break`操作。测试代码如下：
  
```


def a = [1, 2, 3, 4]

println "each loop break use groovy"

a.each {
    // groovy each 循环中的return true类似于java for循环中的continue
    // 当遍历的元素等于2时，跳过当前元素，继续执行, 如果写>= 时，的确也等价于break
    if (it >= 2) return true // break
    println it  // do the stuff that you wanted to before break
}

println "for loop break use java"

for (int i = 0; i < a.size(); i++) {
    if (a[i] == 2) {
        // java for 循环中的break直接跳出当前循环
        // 当遍历的元素等于2时，直接跳出循环
        break
    }
    println a[i]
}
```

这便是`groovy`中的`each`闭包方法的诡异之处，奇怪的是，如果你对集合元素使用`find`方法遍历，当比较操作符是“==”时，并不会发生以上的问题，测试代码如下：
```
def a = [1, 2, 3, 4, 5, 6, 7]

a.find {
    if (it == 3) return true // break 此时的break等价于java for循环中的break
    println it  
    return false // 继续循环
}
```

### 建议

  当对遍历的元素进行迭代，并且在迭代的过程中需要跳出当前循环的，推荐使用`groovy`的`find`方法或者使用`java`的`for`循环，不要使用`groovy`的`each`方法，这样就可以保证流程控制没有错误。