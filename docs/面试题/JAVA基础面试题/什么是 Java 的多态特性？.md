多态其实是一种抽象行为，它的主要作用是让程序员可以面对抽象编程而不是具体的实现类，这样写出来的代码扩展性会更强。

大家可能不是很理解什么是抽象什么是具体，我举个可能不是很恰当，但是很好理解的例子：比如某个人很喜欢吃苹果，我们在写文章描述他的时候可以写他很喜欢吃苹果，也可以写他很喜欢吃水果。

水果就是抽象，苹果就是具体的实现类。

假设这个人某天开始换口味了，他喜欢吃桃子了，如果我们之前的文章写的是水果，那么完全不需要改，如果写的是苹果，是不是需要把苹果替换成桃子了？

这就是多态的意义。

再举个代码的例子：

比如 `Person person = new Student()`

Person 是父类，含有一个工作的方法，student 重写工作方法，比如上学。

```java
class Person {
   void work() {
       System.out.println("工作");
   }
}

class Student extends Person {
   @Override
   void work() {
       System.out.println("上学");
   }
}

public class Test {
   public static void main(String[] args) {
       Person person = new Student();
       person.work(); // 输出 "上学"
   }
}
```

这样在使用的时候，对象都是 person，但是 new 不同的实现类，表现的形式不同，这也就从字面上解释的什么叫多态。