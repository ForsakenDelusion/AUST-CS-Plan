内部类顾名思义就是定义在一个类的内部的类。它主要作用**是为了封装和逻辑分组，提供更清晰的代码组织结构**。

通过内部类，可以把逻辑上相关的类组织在一起，提升封装性和代码的可读性。后期维护时都在一个类里面，不需要在各地方找来找去。

按位置分：在成员变量的位置定义，则是成员内部类，在方法内定义，则是局部内部类。

如果用 static 修饰则为静态内部类，最后还有匿名内部类。

1）成员内部类，定义在另一个类中的类，可以使用外部类的所有成员变量以及方法，包括 private 的。

```java
public class OuterClass {
    private String outerField = "Outer Field";

    class InnerClass {
        void display() {
            System.out.println("Outer Field: " + outerField);
        }
    }

    public void createInner() {
        InnerClass inner = new InnerClass();
        inner.display();
    }
}
```

2）静态内部类，只能访问外部类的静态成员变量以及方法，其实它就等于一个顶级类，可以独立于外部类使用，所以更多的只是表明类结构和命名空间。

```java
public class OuterClass {
    private static String staticOuterField = "Static Outer Field";

    static class StaticInnerClass {
        void display() {
            System.out.println("Static Outer Field: " + staticOuterField);
        }
    }

    public static void createStaticInner() {
        StaticInnerClass staticInner = new StaticInnerClass();
        staticInner.display();
    }
}
```
3）局部内部类，指在方法中定义的类，只在该方法内可见，可以访问外部类的成员以及方法中的局部变量（需要声明为 final 或 effectively final）。

```java
public class OuterClass {
    void outerMethod() {
        final String localVar = "Local Variable";

        class LocalInnerClass {
            void display() {
                System.out.println("Local Variable: " + localVar);
            }
        }

        LocalInnerClass localInner = new LocalInnerClass();
        localInner.display();
    }
}
```

4）匿名类，指的是没有类名的内部类。用于简化实现接口和继承类的代码，仅在创建对象时使用，例如回调逻辑定义场景。

```java
public class OuterClass {
    interface Greeting {
        void greet();
    }

    public void sayHello() {
        Greeting greeting = new Greeting() {
            @Override
            public void greet() {
                System.out.println("Hello, World!");
            }
        };
        greeting.greet();
    }
}
```

局部内部类用的比较少，常用成员内部类、静态内部类和匿名内部类。

实际上内部类是一个编译层面的概念，像一个语法糖一样，经过编译器之后其实内部类会提升为外部顶级类，和外部类没有任何区别，所以**在 JVM 中是没有内部类的概念的**。