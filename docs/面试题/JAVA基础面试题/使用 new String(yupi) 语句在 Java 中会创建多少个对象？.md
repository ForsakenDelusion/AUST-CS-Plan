会创建 1 或 2 个字符串对象。

主要有两种情况：

1、如果字符串常量池中不存在字符串对象“yupi”的引用，那么它会在堆上创建两个字符串对象，其中一个字符串对象的引用会被保存在字符串常量池中。

示例代码（JDK 1.8）：
```java
String s = new String("yupi");
```
对应的字节码：

<img src="https://pic.code-nav.cn/mianshiya/question_picture/1772087337535152129/3rIsIG49_image_mianshiya.png" alt="Snipaste_2024-04-27_22-18-22.jpg" width="100%" />

`ldc` 命令用于判断字符串常量池中是否保存了对应的字符串对象的引用，如果保存了的话直接返回，如果没有保存的话，会在堆中创建对应的字符串对象并将该字符串对象的引用保存到字符串常量池中。

2、如果字符串常量池中已存在字符串对象“yupi”的引用，则只会在堆中创建 1 个字符串对象“yupi”。

示例代码（JDK 1.8）：
```java
// 字符串常量池中已存在字符串对象“yupi”的引用
String s1 = "yupi";
// 下面这段代码只会在堆中创建 1 个字符串对象“yupi”
String s2 = new String("yupi");
```

对应的字节码：

<img src="https://pic.code-nav.cn/mianshiya/question_picture/1783397053004488705/Snipaste_2024-04-27_22-24-12_mianshiya.jpg" alt="Snipaste_2024-04-27_22-24-12.jpg" width="100%" />

这里的过程与上面差不多，我们可以看一下，7 这个位置的 `ldc` 命令不会在堆中创建新的字符串对象 “yupi”，这是因为 0 这个位置已经执行了一次 `ldc` 命令，已经在堆中创建过一次字符串对象 “yupi” 了。 7 这个位置执行 ldc 命令会直接返回字符串常量池中字符串对象“yupi”对应的引用。