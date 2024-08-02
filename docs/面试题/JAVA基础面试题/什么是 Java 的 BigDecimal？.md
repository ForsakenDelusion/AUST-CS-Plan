`BigDecimal`  是 Java 中提供的一个用于高精度计算的类，属于 java.math 包。它提供对浮点数和定点数的精确控制，特别适用于金融和科学计算等需要高精度的领域。

主要特点：
- 高精度：BigDecimal 可以处理任意精度的数值，而不像 float 和 double 存在精度限制。
- 不可变性：BigDecimal 是不可变类，所有的算术运算都会返回新的 BigDecimal 对象，而不会修改原有对象（所以要注意性能问题）。
- 丰富的功能：提供了加、减、乘、除、取余、舍入、比较等多种方法，并支持各种舍入模式。

通常情况下，大部分需要浮点数精确运算结果的业务场景（比如涉及到钱的场景）都是通过 BigDecimal 来做的。

《阿里巴巴 Java 开发手册》中提到：浮点数之间的等值判断，基本数据类型不能用 == 来比较，包装数据类型不能用 equals 来判断。
<img src="https://pic.code-nav.cn/mianshiya/question_picture/1783397053004488705/image-20211213101646884_mianshiya.png" alt="image-20211213101646884.png" width="100%" />

想要解决浮点数运算精度丢失这个问题，可以直接使用 BigDecimal 来定义浮点数的值，然后再进行浮点数的运算操作即可。

```java
BigDecimal a = new BigDecimal("1.0");
BigDecimal b = new BigDecimal("0.9");
BigDecimal c = new BigDecimal("0.8");

BigDecimal x = a.subtract(b);
BigDecimal y = b.subtract(c);

System.out.println(x.compareTo(y));// 0
```

### 扩展：创建 BigDecimal 对象

可以通过多种方式创建 BigDecimal 对象：

1）使用字符串（推荐方式，因为字符串可以精确表示数值）：

```java
BigDecimal bd1 = new BigDecimal("123.45");
```
2）使用数值（不推荐，因为 double 和 float 有精度问题）

```java
BigDecimal bd2 = new BigDecimal(123.45); // 可能会引入精度问题
```
3）使用 BigDecimal.valueOf 方法（推荐方式）：

```java
BigDecimal bd3 = BigDecimal.valueOf(123.45);
```

### 扩展：四舍五入模式介绍

- RoundingMode.UP：向远离零的方向舍入。
- RoundingMode.DOWN：向接近零的方向舍入。
- RoundingMode.CEILING：向正无穷方向舍入。
- RoundingMode.FLOOR：向负无穷方向舍入。
- RoundingMode.HALF_UP：向“最近”的数字舍入，如果有两个相等的最近数字，则向上舍入。
- RoundingMode.HALF_DOWN：向“最近”的数字舍入，如果有两个相等的最近数字，则向下舍入。
- RoundingMode.HALF_EVEN：向“最近”的数字舍入，如果有两个相等的最近数字，则向相邻的偶数舍入
