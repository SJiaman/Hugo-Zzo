---
title: "Java正则表达式"
date: 2020-05-02T09:23:01+08:00
draft: false
author: 世今
toc: true
categories: 
- Java
tags: 
- Regex
- Java
---

##  <span id="inline-toc">1.</span>什么是正则表达式

​    正则表达式（regular expression）regex 是一个字符串，用于描述匹配一个字符串集的模式。

​    正则表达式是对字符串操作的一种逻辑公式，就是用事先定义好的一些特定字符、及这些特定字符的组合，组成一个“规则字符串”，这个“规则字符串”用来表达对字符串的一种过滤逻辑。

​    正则表达式可以用来搜索、编辑或处理文本。

​    正则表达式并不仅限于某一种语言，但是在每种语言中有细微的差别。

##  <span id="inline-toc">2.</span>Java中的regex

Java.util.regex包有三个类：

+ Pattern 类：

  pattern 对象是一个正则表达式的编译表示。Pattern 类没有公共构造方法。要创建一个 Pattern 对象，你必须首先调用其公共静态编译方法，它返回一个 Pattern 对象。该方法接受一个正则表达式作为它的第一个参数。

+ Matcher 类：

  Matcher 对象是对输入字符串进行解释和匹配操作的引擎。与Pattern 类一样，Matcher 也没有公共构造方法。你需要调用 Pattern 对象的 matcher 方法来获得一个 Matcher 对象。

+ PatternSyntaxException：

  PatternSyntaxException 是一个非强制异常类，它表示一个正则表达式模式中的语法错误。



## <span id="inline-toc">3.</span>编写规则

#### 常见匹配符号

| **正则表达式** | **匹配**                                                     |
| -------------- | ------------------------------------------------------------ |
| `.`            | 匹配所有单个字符，除了换行符（Linux 中换行是 `\n`，Windows 中换行是 `\r\n`） |
| `^regex`       | 正则必须匹配字符串开头                                       |
| `regex$`       | 正则必须匹配字符串结尾                                       |
| `[abc]`        | 复选集定义，匹配字母 a 或 b 或 c                             |
| `[abc][vz]`    | 复选集定义，匹配字母 a 或 b 或 c，后面跟着 v 或 z            |
| `[^abc]`       | 当插入符 `^` 在中括号中以第一个字符开始显示，则表示否定模式。此模式匹配所有字符，除了 a 或 b 或 c |
| `[a-d1-7]`     | 范围匹配，匹配字母 a 到 d 和数字从 1 到 7 之间，但不匹配 d1  |
| `XZ`           | 匹配 X 后直接跟着 Z                                          |
| X\|Z           | 匹配 X 或 Z                                                  |
|                |                                                              |
| `\d`           | 匹配一个数字，是 `[0-9]` 的简写                              |
| `\D`           | 匹配一个非数字，是 `[^0-9]` 的简写                           |
| `\s`           | 匹配一个空格，是 `[ \t\n\x0b\r\f]` 的简写                    |
| `\S`           | 匹配一个非空格                                               |
| `\w`           | 匹配一个单词字符（大小写字母、数字、下划线），是 `[a-zA-Z_0-9]` 的简写 |
| `\W`           | 匹配一个非单词字符（除了大小写字母、数字、下划线之外的字符），等同于 `[^\w]` |
|                |                                                              |
| `*`            | 匹配 >=0 个，是 `{0,}` 的简写                                |
| `+`            | 匹配 >=1 个，是 `{1,}` 的简写                                |
| `?`            | 匹配 1 个或 0 个，是 `{0,1}` 的简写                          |
| `{X}`          | 只匹配 X 个字符                                              |
| `{X,Y}`        | 匹配 >=X 且 <=Y 个                                           |
| `*?`           | 如果 `?` 是限定符 `*` 或 `+` 或 `?` 或 `{}` 后面的第一个字符，那么表示**非贪婪模式**（尽可能少的匹配字符），而不是默认的**贪婪模式** |
|                |                                                              |

#### 分组

小括号 `()` 可以达到对正则表达式进行分组的效果。

#### 指定正则表达式的模式

- `(?i)` 使正则忽略大小写。
- `(?s)` 表示*单行模式*（"single line mode"）使正则的 `.` 匹配所有字符，包括换行符。
- `(?m)` 表示*多行模式*（"multi-line mode"），使正则的 `^` 和 `$` 匹配字符串中每行的开始和结束。

#### Java中的反斜杠

反斜杠 \ 在 Java 中表示转义字符，这意味着 \ 在 Java 拥有预定义的含义。

这里例举两个特别重要的用法：

+ 在匹配 . 或 { 或 [ 或 ( 或 ? 或 $ 或 ^ 或 * 这些特殊字符时，需要在前面加上 \\\\，比如匹配 . 时，Java 中要写为 \\\\.，但对于正则表达式来说就是 \\.。
+ 在匹配 \ 时，Java 中要写为 \\\\\\\\，但对于正则表达式来说就是 \\\\。

注意：Java 中的正则表达式字符串有两层含义，首先 Java 字符串转义出符合正则表达式语法的字符串，然后再由转义后的正则表达式进行模式匹配。

## <span id="inline-toc">4.</span>实例

+ (aaa){5}，匹配’aaa’5次

+ "food|f"匹配的是foo（d或f），而"(food)|f"匹配的是food或f

+ 数值 ： ^[+\-]?\d+(\.\d+)?$

+ 密码(以字母开头，长度在6~18之间，只能包含字母、数字和下划线)：^[a-zA-Z]\w{5,17}$

+ 中文  ：  [\u4e00-\u9fa5]

+ E-mail ：^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$

  ​                s.matches("^[+\\-]?\\d*(\\.\\d+)?$")

#### Java内置的字符串正则处理方法

在 Java 中有四个内置的运行正则表达式的方法，分别是 matches()、split())、replaceFirst()、replaceAll()。注意 replace() 方法不支持正则表达式。

| **方法**                                 | **方法**                                |
| ---------------------------------------- | --------------------------------------- |
| `s.matches("regex")`                     | 当仅且当正则匹配整个字符串时返回 `true` |
| `s.split("regex")`                       | 按匹配的正则表达式切片字符串            |
| `s.replaceFirst("regex", "replacement")` | 替换首次匹配的字符串片段                |
| `s.replaceAll("regex", "replacement")`   | 替换所有匹配的字符                      |

####  示例代码

```java
public class RegexTest {

    public static void main(String[] args) {
        System.out.println("wxj".matches("wxj"));
        System.out.println("----------");

        String[] array = "w x j".split("\\s");
        for (String item : array) {
            System.out.println(item);
        }
        System.out.println("----------");

        System.out.println("w x j".replaceFirst("\\s", "-"));
        System.out.println("----------");

        System.out.println("w x j".replaceAll("\\s", "-"));
    }
}
```

```java
true
----------
w
x
j
----------
w-x j
----------
w-x-j
```

#### 模式与匹配

Java 中使用正则表达式需要用到两个类，分别为 java.util.regex.Pattern 和 java.util.regex.Matcher。

1. 通过正则表达式创建模式对象 Pattern。

2. 通过模式对象 Pattern，根据指定字符串创建匹配对象 Matcher。

3. 通过匹配对象 Matcher，根据正则表达式操作字符串。

```java
// 数字的匹配

import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class RegexTest {

    public static void main(String[] args) {
        String str = "1990\n2010\n2017";
        // 这里应用了 (?m) 的多行匹配模式，只为方便我们测试输出
        // "^1990$|^199[1-9]$|^20[0-1][0-6]$|^2017$" 为判断 1990-2017 正确的正则表达式
        Pattern pattern = Pattern.compile("(?m)^1990$|^199[1-9]$|^20[0-1][0-6]$|^2017$");
        Matcher matcher = pattern.matcher(str);
        while (matcher.find()) {
            System.out.println(matcher.group());
        }
    }
}
```

```java
1990
2010
2017
```

```java
// 图片的匹配

import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class RegexTest {

    public static void main(String[] args) {
        String str = "<img  src='aaa.jpg' /><img src=bbb.png/><img src=\"ccc.png\"/>" +
                "<img src='ddd.exe'/><img src='eee.jpn'/>";
        // 这里我们考虑了一些不规范的 img 标签写法，比如：空格、引号
        Pattern pattern = Pattern.compile("<img\\s+src=(?:['\"])?(?<src>\\w+.(jpg|png))(?:['\"])?\\s*/>");
        Matcher matcher = pattern.matcher(str);
        while (matcher.find()) {
            System.out.println(matcher.group("src"));
        }
    }
}
```

```java
aaa.jpg
bbb.png
ccc.png
```

------参考吴仙杰的java正则表达式详解

## 五、总结

正则表达式在日常的编程中使用还是比较多的，一时间可能学不会，但是在实践中边学习边用是比较好的。