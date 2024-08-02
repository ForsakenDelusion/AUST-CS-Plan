迭代器（Iterator）其实是一种**设计模式**，用于遍历集合（例如 List、Set、Map 等）中的元素，而不需要暴露集合的内部实现，即不需要了解集合的底层结构。

在 Java 中 Iterator 是一个接口，在 java.util 包中的，常用的方法是：

- hasNext()：如果迭代器还有更多的元素可以迭代，则返回 true，否则返回 false。
- next()：返回迭代器的下一个元素。如果没有更多元素，调用该方法将抛出 NoSuchElementException。
- remove()：从底层集合中移除 next() 方法返回的上一个元素。这个方法是可选的，不是所有的实现都支持该操作。如果不支持，调用时会抛出 UnsupportedOperationException。

简单示例代码如下：
```java

public class IteratorExample {
    public static void main(String[] args) {
        // 创建一个 List 集合
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");

        // 获取集合的迭代器
        Iterator<String> iterator = list.iterator();

        // 使用迭代器遍历集合
        while (iterator.hasNext()) {
            String element = iterator.next();
            System.out.println(element);
        }

        // 移除集合中的元素
        iterator = list.iterator();  // 重新获取迭代器
        while (iterator.hasNext()) {
            String element = iterator.next();
            if (element.equals("Banana")) {
                iterator.remove();
            }
        }

        // 再次遍历集合，确认元素已被移除
        System.out.println("After removal:");
        iterator = list.iterator();
        while (iterator.hasNext()) {
            System.out.println(iterator.next());
        }
    }
}
```

迭代器模式带来了很多好处：

1）封装性：它将集合遍历行为和具体的实现分离，使得使用者不需要了解集合具体的内部实现。
2）一致性：所有的集合都实现了 Iterator 接口，因此对于不同集合的遍历代码都是一致的。
3）灵活性：因为遍历接口一致，使得可以很灵活的替换底层实现的集合而不需要改变上层的遍历代码。

Iterator 提供了单向遍历方法，如果需要支持双向遍历，可以使用 ListIterator 接口。