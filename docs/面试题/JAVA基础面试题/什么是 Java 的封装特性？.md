封装（Encapsulation）是面向对象编程（OOP）的核心概念之一，它指的是将对象的数据（属性）和行为（方法）组合在一起，并隐藏内部的实现细节。

```java
public class Car {
    private String model; // 私有属性，外部无法直接访问
    private int year;

    // 构造方法
    public Car(String model, int year) {
        this.model = model;
        this.year = year;
    }

    // getter 方法
    public String getModel() {
        return model;
    }

    // setter 方法
    public void setModel(String model) {
        this.model = model;
    }

    // 行为方法
    public void startEngine() {
        System.out.println("Engine started for " + model);
    }
}

public class EncapsulationExample {
    public static void main(String[] args) {
        Car myCar = new Car("Toyota", 2021);
        myCar.startEngine(); // 使用公共方法

        // 使用 getter 和 setter 方法访问和更新属性
        System.out.println("Car model: " + myCar.getModel());
        myCar.setModel("Honda");
    }
}
```

### 关键点

1）数据隐藏：

封装允许对象隐藏其内部状态和实现细节，只暴露出一个可以被外界访问和操作的接口。

2）访问控制：

通过使用访问修饰符（如 private、protected、public），封装可以限制对类成员的访问权限。

3）创建对象：

封装使得创建具有复杂内部结构的对象变得简单，因为用户只需要通过公共接口与之交互。

4）接口与实现分离：

封装将对象的接口与其实现分离，这样即使实现改变，接口保持不变，对使用对象的客户代码影响较小。

5）数据抽象：

封装提供了一种抽象，只显示必要的信息，隐藏不必要的实现细节。

