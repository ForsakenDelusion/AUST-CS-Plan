Optional 是 Java 8 引入的一个容器类，它用来表示一个值可能存在或不存在。

常见的使用方式如下：

```java
Optional<User> userOption = Optional.ofNullable(userService.getUser(...));
if (!userOption.isPresent()) {....}
```

Optional 设计出来的意图是什么， Java 语言架构师 Brian Goetz 是这么说的：

> Our intention was to provide a limited mechanism for library method return types where there needed to be a clear way to represent "no result", and using null for such was overwhelmingly likely to cause errors.


意思就是：Optional 可以给返回结果提供了一个表示无结果的值，而不是返回 null。

简单理解下，Optional 其实就是一个壳，里面放着原先的值，至于这个值是不是 null 另说，反正拿到的这个壳肯定不是 null。

![企业微信截图_c7362dfe-26af-4ae0-be83-57ebefcdcbfc.png](https://pic.code-nav.cn/mianshiya/question_picture/1772087337535152129/UmdCliuo_c7362dfe-26af-4ae0-be83-57ebefcdcbfc_mianshiya.png)

网上比较流行的说法是 Optional 可以避免空指针，我不太赞同这种说法。因为最终的目的是拿到 Optional 里面存储的值，如果这个值是 null，不做额外的判断，直接使用还是会有空指针的问题。

我认为 Optional 的好处在于可以简化平日里一系列判断 null 的操作，使得用起来的时候看着不需要判断 null，纵享丝滑，表现出来好像用 Optional 就不需要关心空指针的情况。

而事实上是 Optional 在替我们负重前行，该有的判断它替我们完成了，而且用了 Optional 最后拿结果的时候还是小心的，盲目 get 一样会抛错，Brian Goetz 说 get 应该叫 getOrElseThrowNoSuchElementException。

我们来看一下代码就很清楚 Optional 的好处在哪儿了。比如现在有个 yesSerivce 能 get 一个 Yes，此时需要输出 Yes 所在的省，此时的代码是这样的：

```java
Yes yes = getYes();
if (yes != null) {
    Address yesAddress = yes.getAddress();
    if (yesAddress != null) {
        Province province = yesAddress.getProvince();
        System.out.println(province.getName());
    }
}
throw new NoSuchElementException(); //如果没找到就抛错
```

如果用 Optional 的话，那就变成下面这样：

```java
Optional.ofNullable(getYes())
        .map(a -> a.getAddress())
        .map(p -> p.getProvince())
        .map(n -> n.getName())
        .orElseThrow(NoSuchElementException::new);
```

可以看到，如果用了 Optional，代码里不需要判空的操作，即使 address 、province 为空的话，也不会产生空指针错误，这就是 Optional 带来的好处！

## 扩展

关于  Optional 还有个性能问题，我们看一下：

Optional 里有 orElseGet  和 orElse 这两个看起来挺相似的方法，都是处理当值为 null 时的兜底逻辑。可能你也在一些文章上看到说用 orElseGet 不要用 orElse ，因为在 Optional 有值时候 orElse 仍然会调用方法，所以后者性能比较差。其实从上面分析我们知道不论 Optional 是否有值，orElse 和 orElseGet  都会被执行，所以是怎么回事呢？

看下这个代码：

![企业微信截图_01705210-0d9e-4acb-aff4-c8a99b27e7b5.png](https://pic.code-nav.cn/mianshiya/question_picture/1772087337535152129/9eUmKX3m_01705210-0d9e-4acb-aff4-c8a99b27e7b5_mianshiya.png)

这样看来 orElse 确实性能会差，奇怪了，难道是 bug？

我们来看下源码：

![企业微信截图_8f3f1e44-8baf-45a5-9bc3-5803f0b5008f.png](https://pic.code-nav.cn/mianshiya/question_picture/1772087337535152129/J3T4rWrv_8f3f1e44-8baf-45a5-9bc3-5803f0b5008f_mianshiya.png)

可以看到两者的入参不同，一个就是普通参数，一个是 Supplier。我们已经得知不论Optional.ofNullable 返回的是否是空 Optional，下面的逻辑还是会执行，所以 orElse 和 orElseGet 这两个方法无论如何都会执行。

因此 orElse(createYes()) 会被执行，在参数入栈之前，执行了 createYes 方法得到结果，然后入栈，而 orElseGet 的参数是 Supplier，所以直接入栈，然后在调用 other.get 的时候，createYes 方法才会被触发执行，这就是两者的区别之处。

所以才会造成上面表现出的性能问题，因此不是 BUG，也不是有些文章说的 Optional 有值 orElse 也会被执行而 orElseGet 不会执行这样不准确的说法，相信现在你的心里很有数了。
