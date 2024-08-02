### 直接回答：

重载：在同一个类中定义多个方法，它们具有相同的名字但参数列表不同。主要用于提供相同功能的不同实现。

重写：在子类中定义一个与父类方法具有相同签名的方法，以便提供子类的特定实现。主要用于实现运行时多态性。

### 扩展解析：

重载：指在同一个类中定义多个方法，这些方法具有相同的名字但参数列表不同（参数类型、数量或顺序不同）。

**这里要注意和返回值没有关系**，方法的签名是名字和参数列表，不包括返回值。

**重载通常用于提供同一操作的不同实现，例如构造函数的重载、不同类型输入的处理等**。

重载简单示例代码：

```java
public class OverloadingExample {
    // 重载方法：参数数量不同
    public void print(int a) {
        System.out.println("Printing int: " + a);
    }

    // 重载方法：参数类型不同
    public void print(String a) {
        System.out.println("Printing String: " + a);
    }

    // 重载方法：参数类型和数量不同
    public void print(int a, int b) {
        System.out.println("Printing two ints: " + a + ", " + b);
    }
}
```
---

重写：指在子类中定义与父类方法具有相同签名（方法名、参数列表）的一个方法，方法返回类型与父类一致，或者是其子类（协变返回类型）。

且子类方法定义的访问修饰符，不能比父类更严格。例如父类方法是 `protected`，那么子类方法不能是 `private`，但可以是 `public`。

且子类方法抛出的异常必须与父类一致，或者是其父类异常的子类。

**重写通常用于在子类中提供父类方法的具体实现，以实现多态性。例如，子类对父类方法进行扩展或修改以适应特定需求**。

重写简单示例代码：

```java
class Parent {
    public void display() {
        System.out.println("Parent display");
    }
}

class Child extends Parent {
    @Override
    public void display() {
        System.out.println("Child display");
    }
}

public class OverridingExample {
    public static void main(String[] args) {
        Parent obj = new Child();
        obj.display(); // 输出 "Child display"
    }
}
```