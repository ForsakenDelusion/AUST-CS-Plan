`String` 是 Java 中基础且重要的类，并且 `String` 也是 `Immutable` 类的典型实现，被声明为 `final class`，除了 `hash` 这个属性其它属性都声明为 `final`。

因为它的不可变性，所以例如拼接字符串时候会产生很多无用的中间对象，如果频繁的进行这样的操作对性能有所影响。
 
**StringBuffer 就是为了解决大量拼接字符串时产生很多中间对象问题而提供的一个类**，提供 `append` 和 `add` 方法，可以将字符串添加到已有序列的末尾或指定位置。

它的本质是一个线程安全的可修改的字符序列，把所有修改数据的方法都加上了 `synchronized`。但是保证了线程安全是需要性能的代价的。

在很多情况下我们的字符串拼接操作不需要线程安全，这时候 **StringBuilder** 登场了，`StringBuilder`是`JDK1.5`发布的，它和 `StringBuffer` 本质上没什么区别，就是**去掉了保证线程安全的那部分，减少了开销**。

`StringBuffer` 和 `StringBuilder` 二者都继承了 `AbstractStringBuilder` ，底层都是利用可修改的 `char` 数组(JDK 9 以后是 `byte` 数组)。

所以如果我们有大量的字符串拼接，如果能预知大小的话最好在 `new StringBuffer` 或者 `StringBuilder` 的时候设置好 `capacity`，避免多次扩容的开销（扩容要抛弃原有数组，还要进行数组拷贝创建新的数组）。

### 选择建议
- String：适用于少量字符串操作或需要字符串常量池优化的场景。
- StringBuffer：适用于多线程环境下频繁的字符串操作。
- StringBuilder：适用于单线程环境下频繁的字符串操作。