这个题目的答案其实非常简单：这个操作主要是为了**节省内存空间，提高内存利用率**。

在 JDK 9 之前，String 类是基于 `char[]` 实现的，内部采用 UTF-16 编码，每个字符占用两个字节。

<img src="https://pic.code-nav.cn/mianshiya/question_picture/1772087337535152129/mze5GBYU_image_mianshiya.png" alt="image.png" width="100%" />


但是，如果当前的字符仅需一个字节的空间，这就造成了浪费。例如一些 `Latin-1` 字符用一个字节即可表示。

因此 JDK 9 做了优化采用 `byte` 数组来实现：

<img src="https://pic.code-nav.cn/mianshiya/question_picture/1772087337535152129/jmO17779_image_mianshiya.png" alt="image.png" width="100%" />

并引入了 coder 变量来标识编码方式（Latin-1 或 UTF-16）。对于大多数只包含 Latin-1 字符（即每个字符可以用一个字节表示）的字符串，内存使用量减半。

### 扩展 Latin1

Latin1 是国际标准编码 ISO-8859-1 的别名。Latin1 也是单字节编码，在 ASCII 编码的基础上，利用了 ASCII 未利用的最高位，扩充了 128 个字符，因此 Latin1 可以表示 256 个字符，并向下兼容 ASCII。

Latin1收录的字符除 ASCII 收录的字符外，还包括西欧语言、希腊语、泰语、阿拉伯语、希伯来语对应的文字符号。欧元符号出现的比较晚，没有被收录在 ISO-8859-1 当中，在后来的修订版 ISO-8859-15 加入了欧元符号。

Latin1的编码范围是 0x00-0xFF，ASCII的编码范围是 0x00-0x7F。

Latin1 相对 ASCII 而言，较少被提及，其实 Latin1 的使用还是比较广泛的，比如 MySQL（8.0之前）的数据表存储默认编码就是 Latin1。