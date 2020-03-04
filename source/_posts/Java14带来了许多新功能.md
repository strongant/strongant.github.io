title: Java14带来了许多新功能
author: strongant
tags: 'java,java14,java语言'
date: 2020-03-04 22:17:47
---

Java 14包含比前两个发行版更多的新功能-其中大多数旨在简化编码。

劳尔·加布里埃尔·乌尔玛（Raoul-Gabriel Urma）

2020年2月27日

> [下载本文的PDF](https://app.compendium.com/api/post_attachments/07a7a6fa-9588-4206-aa38-cf507df7a1ed/view)

https://app.compendium.com/api/post_attachments/07a7a6fa-9588-4206-aa38-cf507df7a1ed/view


Java 14计划于3月17日发布。版本14包含的[JEP](https://openjdk.java.net/projects/jdk/14/)（Java增强建议）比Java 12和13的总和还多。那么，对于每天编写和维护代码的Java开发人员来说，最重要的是什么呢？

https://openjdk.java.net/projects/jdk/14/

在本文中，我研究了以下主要方面：

- 改进的 switch 表达式，该表达式最初在Java 12和Java 13中作为预览出现，现在已完全成为Java 14的一部分
- 模式匹配`instanceof`（一种语言功能）
- 有用`NullPointerException`的（JVM功能）

如果您阅读本文并尝试在代码库中使用其中的某些功能，建议您通过向[Java团队](mailto:amber-dev@openjdk.java.net)提供[反馈来](mailto:amber-dev@openjdk.java.net)分享您的经验。这样，您就有机会为Java的发展做出贡献。

## switch表达式

在Java 14中，switch表达式变为永久性的。如果您需要回顾一下什么是switch表达式，那么[在前](https://blogs.oracle.com/javamagazine/new-switch-expressions-in-java-12) [两篇文章](https://blogs.oracle.com/javamagazine/inside-java-13s-switch-expressions-and-reimplemented-socket-api)中已广泛讨论了它们。

https://blogs.oracle.com/javamagazine/new-switch-expressions-in-java-12

https://blogs.oracle.com/javamagazine/inside-java-13s-switch-expressions-and-reimplemented-socket-api


在早期版本中，switch 表达式是“预览”功能。提醒一下，将指定为“预览”版本以收集反馈，并且根据反馈可能会更改甚至删除这些功能。但预计大多数最终将在Java中永久化。

新的switch表达式的优点包括由于没有中断行为，穷举以及由于表达式和复合形式而易于编写，从而减小了错误的范围。作为一个示例，switch表达式现在可以利用箭头语法，例如在以下示例中：

```
var log = switch (event) {
    case PLAY -> "User has triggered the play button";
    case STOP, PAUSE -> "User needs a break";
    default -> {
        String message = event.toString();
        LocalDateTime now = LocalDateTime.now();
        yield "Unknown event " + message + 
              " logged on " + now;
    }
};
```

## 文本块

Java 13引入了文本块作为预览功能。文本块使使用多行字符串文字更加容易。此功能将通过Java 14进行第二轮预览，并进行了一些调整。作为编写带有许多字符串连接和转义序列的代码以提供适当的多行文本格式非常普遍。下面的代码显示了HTML格式的示例：

```
String html = "<HTML>" +
"\n\t" + "<BODY>" +
"\n\t\t" + "<H1>\"Java 14 is here!\"</H1>" +
"\n\t" + "</BODY>" +
"\n" + "</HTML>";
```

使用文本块，您可以简化此过程并使用界定文本块开头和结尾的三个引号来编写更优雅的代码：

```
String html = """
<HTML>
  <BODY>
    <H1>"Java 14 is here!"</H1>
  </BODY>
</HTML>""";
```

与普通字符串文字相比，文本块还提供了更高的表达能力。您可以在较早的[文章中](https://blogs.oracle.com/javamagazine/text-blocks-come-to-java)了解有关此内容的更多信息。

https://blogs.oracle.com/javamagazine/text-blocks-come-to-java

Java 14中添加了两个新的转义序列。首先，您可以使用新的`\s`转义序列表示单个空格。其次，您可以使用反斜线`\`来禁止在行尾插入新行字符。当您想分隔很长的行以简化文本块内的可读性时，这很有用。

例如，当前处理多行字符串的方法是

```
String literal = 
         "Lorem ipsum dolor sit amet, consectetur adipiscing " +
         "elit, sed do eiusmod tempor incididunt ut labore " +
         "et dolore magna aliqua.";
```

使用`\`文本块中的转义序列，可以将其表示为：

```
String text = """
                Lorem ipsum dolor sit amet, consectetur adipiscing \
                elit, sed do eiusmod tempor incididunt ut labore \
                et dolore magna aliqua.\
                """;
```

## instanceof的模式匹配

Java 14引入了预览功能，该功能有助于消除对在进行条件`instanceof`检查之前进行显式强制转换的需求。例如，考虑以下代码：

```
if (obj instanceof Group) {
  Group group = (Group) obj;

  // use group specific methods
  var entries = group.getEntries();
}
```

可以使用预览功能将其重构为：

```
if (obj instanceof Group group) {
  var entries = group.getEntries();
}
```

因为条件检查断言`obj`是type `Group`，所以为什么要在第一个代码段中用条件块再次说该`obj`类型`Group`？这种需求可能会增加错误的范围。

较短的语法将删除典型Java程序中的许多强制转换。（A [研究论文](http://www.cs.williams.edu/FTfJP2011/6-Winther.pdf)从2011年提出了一个相关的语言特性报告说，所有铸件约24％遵循`instanceof`的条件语句。）

http://www.cs.williams.edu/FTfJP2011/6-Winther.pdf

[JEP 305](https://openjdk.java.net/jeps/305)涵盖了此更改，并从Joshua Bloch 的*Effective Java*书中指出了一个示例，该示例通过以下相等方法进行说明：

https://openjdk.java.net/jeps/305

 

```
@Override public boolean equals(Object o) { 
    return (o instanceof CaseInsensitiveString) && 
            ((CaseInsensitiveString) o).s.equalsIgnoreCase(s); 
}
```

通过删除冗余的显式强制转换为，可以将前面的代码简化为以下形式`CaseInsensitiveString`：

```
@Override public boolean equals(Object o) { 
    return (o instanceof CaseInsensitiveString cis) &&
            cis.s.equalsIgnoreCase(s); 
}
```

这是一个有趣的预览功能，因为它为更广泛的模式匹配打开了大门。模式匹配的思想是为语言功能提供方便的语法，以便根据某些条件提取对象的成分。`instanceof`运算符就是这种情况，因为条件是类型检查，并且提取操作正在调用适当的方法或访问特定字段。

换句话说，此预览功能仅仅是个开始，您可以期待一种语言功能，它可以帮助进一步减少冗长性，从而减少错误的可能性。

## 记录

还有另一种预览语言功能：records。像到目前为止提出的其他想法一样，此功能遵循减少Java冗长并帮助开发人员编写更简洁的代码的趋势。记录集中在某些域类上，这些类仅用于将数据存储在字段中，并且不声明任何自定义行为。

为了直接解决该问题，请使用一个简单的域类，该类`BankTransaction`通过三个字段对交易进行建模：日期，金额和描述。声明类时，您需要担心多个组件：

- 构造函数
- equals方法
- `toString()`
- `hashCode()` 和 `equals()`

此类组件的代码通常由IDE自动生成，并占用大量空间。这是`BankTransaction`该类的完整生成的实现：

```
public class BankTransaction {
    private final LocalDate date;
    private final double amount;
    private final String description;


    public BankTransaction(final LocalDate date, 
                           final double amount, 
                           final String description) {
        this.date = date;
        this.amount = amount;
        this.description = description;
    }

    public LocalDate date() {
        return date;
    }

    public double amount() {
        return amount;
    }

    public String description() {
        return description;
    }

    @Override
    public String toString() {
        return "BankTransaction{" +
                "date=" + date +
                ", amount=" + amount +
                ", description='" + description + '\'' +
                '}';
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        BankTransaction that = (BankTransaction) o;
        return Double.compare(that.amount, amount) == 0 &&
                date.equals(that.date) &&
                description.equals(that.description);
    }

    @Override
    public int hashCode() {
        return Objects.hash(date, amount, description);
    }
}
```

Java的14提供了一种方法来去除冗长，使意图明确指出，所有你想要的是，只有拥有的实现数据聚合在一起的一类`equals`，`hashCode`和`toString`方法。您可以`BankTransaction`按以下方式重构：

```
public record BankTransaction(Date date,
                              double amount,
                              String description) {}
```

有了记录，你“自动”得到的实现`equals`，`hashCode`以及`toString`除了构造函数和getter。

要尝试该示例，请记住您需要使用预览标志来编译文件：

```
javac --enable-preview --release 14 BankTransaction.java
```

记录的字段是隐式的`final`。这意味着您无法重新分配它们。但是请注意，这并不意味着整个记录都是不变的。存储在字段中的对象本身可以是可变的。

如果您对有关记录的更详细的文章感兴趣，请参阅[*Java杂志上*](https://blogs.oracle.com/javamagazine/records-come-to-java) Ben Evans的最新[文章](https://blogs.oracle.com/javamagazine/records-come-to-java)。

https://blogs.oracle.com/javamagazine/records-come-to-java


敬请关注。从教育的角度来看，唱片还为下一代Java开发人员提出了有趣的问题。例如，如果您指导初级开发人员，那么什么时候应该在课程中引入记录：在引入OOP和类之前还是之后？

## 有用的NullPointerExceptions

有人说throw `NullPointerException`应该是Java中新的“ Hello world”，因为您无法逃避它们。除了笑话，它们还导致挫败感，因为当代码在生产环境中运行时，它们经常出现在应用程序日志中，这可能使调试变得困难，因为原始代码不容易获得。例如，考虑以下代码：

```
var name = user.getLocation().getCity().getName();
```

在Java 14之前，您可能会收到以下错误：

```
Exception in thread "main" java.lang.NullPointerException
    at NullPointerExample.main(NullPointerExample.java:5)
```

不幸的是，如果在第5行，则有一个具有多个方法调用的赋值- `getLocation()`和- `getCity()`两者都可能返回null。实际上，变量`user`也可以为null。因此，目前尚不清楚是什么原因引起的`NullPointerException`。

现在，使用Java 14，有一个新的JVM功能，通过它您可以收到更多信息的诊断信息：

```
Exception in thread "main" java.lang.NullPointerException: Cannot invoke "Location.getCity()" because the return value of "User.getLocation()" is null
    at NullPointerExample.main(NullPointerExample.java:5)
```

该消息现在具有两个明确的组成部分：

- **结果：** `Location.getCity()`无法调用。
- **原因：**的返回值为`User.getLocation()`null。

仅当您使用以下标志运行Java时，增强型诊断才有效：

```
-XX:+ShowCodeDetailsInExceptionMessages
```

这是一个例子：

```
java -XX:+ShowCodeDetailsInExceptionMessages NullPointerExample
```

在Java的未来版本中，这项功能可能会被默认启用，据报道[在这里](https://bugs.openjdk.java.net/browse/JDK-8233014)。

https://bugs.openjdk.java.net/browse/JDK-8233014

此增强功能不仅可用于方法调用，而且还可在可能导致的其他地方使用`NullPointerException`，包括字段访问，数组访问和赋值。

## 结论

在Java 14中，有新的预览语言功能和更新可帮助开发人员进行日常工作。例如，Java 14引入了`instanceof`模式匹配，这是减少显式转换的一种方法。而且，Java 14引入了记录，这是一种新的结构，用于简洁地声明仅用于聚合数据的类。此外，`NullPointerException`消息已通过更好的诊断得到了增强，并且开关表达式现在已成为Java 14的一部分。文本块是一种可帮助您处理多行字符串值的功能，在引入了两个新的转义序列后，将进行另一轮预览。Java操作的一部分技术人员可能会感兴趣的另一项更改是[JDK Flight Recorder中的事件流](https://openjdk.java.net/jeps/349)。该选项在[本埃文斯的这篇文章](https://blogs.oracle.com/javamagazine/java-flight-recorder-and-jfr-event-streaming-in-java-14)。

https://openjdk.java.net/jeps/349

https://blogs.oracle.com/javamagazine/java-flight-recorder-and-jfr-event-streaming-in-java-14

如您所见，Java 14带来了很多创新。您绝对应该使用一下，并将有关预览功能的反馈发送给Java团队。
