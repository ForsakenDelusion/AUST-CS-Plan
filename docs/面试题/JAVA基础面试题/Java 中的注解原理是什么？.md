注解其实就是一个标记，可以标记在类上、方法上、属性上等，标记自身也可以设置一些值。

有了标记之后，我们就可以在解析的时候得到这个标记，然后做一些特别的处理，这就是注解的用处。

比如我们可以定义一些切面，在执行一些方法的时候看下方法上是否有某个注解标记，如果是的话可以执行一些特殊逻辑(RUNTIME类型的注解)。

注解生命周期有三大类，分别是：

- RetentionPolicy.SOURCE：给编译器用的，不会写入 class 文件
- RetentionPolicy.CLASS：会写入 class 文件，在类加载阶段丢弃，也就是运行的时候就没这个信息了
- RetentionPolicy.RUNTIME：会写入 class 文件，永久保存，可以通过反射获取注解信息

所以我上文写的是解析的时候，没写具体是解析啥，因为不同的生命周期的解析动作是不同的。

像常见的：

```java
@Target(ElEMENT_TYPE.METHOD)
@Retention(RetentionPolicy.RUNTIME
    public @interface Override {
    }
)
```

就是给编译器用的，编译器编译的时候检查没问题就over了，class文件里面不会有 Override 这个标记。

再比如 Spring 常见的 Autowired ，就是 RUNTIME 的，所以**在运行的时候可以通过反射得到注解的信息**，还能拿到标记的值 required 。


```java
@Target(ElementType.CONSTRUCTOR,ElementType.FIELD,ElementType.METHOD,ElementType.PARAMETER,ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface Autowired {
    boolean required() default true;
}
```

所以注解的原理就是编译器在编译的时候会解析注解，然后根据注解的不同类型做不同的处理，解析注解就是解析注解里面的值，然后根据这些值做一些处理。

比如 Spring 在运行的时候就可以通过反射得到注解的信息，然后根据注解的值做一些依赖注入的操作。
```

所以注解就是一个标记，可以给编译器用、也能运行时候用。