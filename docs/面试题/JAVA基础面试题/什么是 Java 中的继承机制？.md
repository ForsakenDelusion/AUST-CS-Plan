Java 中的继承是面向对象编程（OOP）的一个核心概念，它允许新创建的类（称为子类或派生类）继承现有类（称为父类或基类）的属性和方法。

通过继承，子类可以复用、扩展和修改父类的行为，提高了代码的复用性，实现了多态。

简单举例看下代码就了解了，在 Java 中主要通过 extends 实现继承：

```java
class Animal {
    void breathe() {
        System.out.println("Breathing");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Barking");
    }
    
    @Override
    void breathe() {
        System.out.println("Breathing through lungs");
    }
}

public class InheritanceExample {
    public static void main(String[] args) {
        Animal myAnimal = new Dog(); // 多态性
        myAnimal.breathe(); // 调用 Dog 类的 breathe 方法
        ((Dog) myAnimal).bark(); // 向下转型并调用 Dog 类的 bark 方法
    }
}
```

重写使用 @Override 注释来标明，并且**方法签名（方法名称、方法参数类型与顺序）必须与父类中的方法相同**。

Java 只支持单继承，即一个类只能继承一个直接父类。但是，通过接口（interfaces），Java 实现了多继承的功能。