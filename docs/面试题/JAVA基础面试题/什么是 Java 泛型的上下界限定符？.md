上界限定符是 extends ，下界限定符是 super

`<? extends T>` 表示类型的上界，？这个类型要么是 T ，要么是 T 的子类

下面就是一个典型的例子：

```java
// 定义一个泛型方法，接受任何继承自Number的类型
public <T extends Number> void processNumber(T number) {
    // 在这个方法中，可以安全地调用Number的方法
    double value = number.doubleValue();
    // 其他操作...
}
```

`<? super T>` 表示类型的下界（也叫做超类型限定），？这个类型是 T 的超类型（父类型），直至 Object

下面也是一个典型的例子：

```java
// 定义一个泛型方法，接受任何类型的List，并向其中添加元素
public <T> void addElements(List<? super T> list, T element) {
    list.add(element);
    // 其他操作...
}
```

我们在使用上下界通配符的时候，需要遵循 pecs 原则，即Producer Extends, Consumer Super；上界生产，下界消费。

什么意思呢？

如果要从集合中读取类型 T 的数据，**并且不能写入**，可以使用 ? extends 通配符；(Producer Extends)，如上面的 `processNumber` 方法，我们是要从方法中得到 T 类型，也就是方法给我们生产。

如果要从集合中写入类型 T 的数据，**并且不需要读取**，可以使用 ? super 通配符；(Consumer Super)，如上面的  `addElements` 方法，我们是要往方法中传入 T 类型，也就是方法帮我们消费。