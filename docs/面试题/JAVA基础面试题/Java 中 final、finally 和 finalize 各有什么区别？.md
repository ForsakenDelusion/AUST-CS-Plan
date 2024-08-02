### 回答

- final：用于类、方法和变量，表示不可改变或不可继承。
- finally：用于 try-catch 块中，无论是否抛出异常，finally 块中的代码总会执行。
- finalize：是 Object 类中的方法，供垃圾收集器在回收对象之前调用，但由于其局限性和不确定性，不推荐使用。


### 扩展：final
final 是一个关键字，其可以用来修饰变量、方法以及类等，被修饰之后的部分不可变、不可以被重写或者不可以被继承。

#### final 修饰变量
fianl 修饰变量之后，被修饰的变量不可以被二次修改，即变成了我们常说的常量。
```java
final int x = 10;
// x = 20; // 这一部分如果修改的的话会报错 Cannot assign a value to final variable 'x'
```
由代码中的错误可见，x 的值不可以被修改，这个时候的 x 即变成了一个常量。

#### final 修饰方法
final 修饰的方法无法被子类进行重写，如下图所示：

```java
public class Test{
    public final void testOverride(){//注意是方法名的final
        System.out.println("Override");
    }
}
class TestExtend extends Test{
    @Override
    public void testOverride(){//他会提示:override method is final
        System.out.println("Override Extend");
    }
}
```

我们可以看见，当 final 修饰了父类的方法之后，子类是无法对父类方法进行重写的，其会导致编译异常

#### final 修饰的类不能被继承

如下图所示，我们会发现 final 修饰的类无法被子类继承

```java
public final class Test{//注意是类名的final
    public void testOverride(){
        System.out.println("Override");
    }
}
class TestExtend extends Test{//他会提示:Cannot inherit from final 'Test'

}
```

### 扩展：finally
finally 是主要应用于异常处理，它经常和try、catch块一起搭配使用。无论是否捕获或处理异常，finally 块中的代码总是会执行（程序正常执行的情况）。通常用于关闭资源，如输入/输出流、数据库连接等。

```java
try {
    // 可能产生异常的代码
} catch (Exception e) {
    // 异常处理代码
} finally {
    // 正常情况下总是执行的代码块，常用于关闭资源
}
```

### 扩展：finalize

finalize 是 Object 类的一个方法，用于垃圾收集过程中的资源回收。在对象被垃圾收集器回收之前，finalize 方法会被调用，用于执行清理操作（例如释放资源）。然而，**finalize 方法已经被弃用**，且不推荐使用，因为它不保证及时执行，并且其使用可能导致性能问题和不可预测的行为。

```java
protected void finalize() throws Throwable {
    // 在对象被回收时执行清理工作
}
```