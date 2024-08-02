## 剖析 StringBuilder 

首先因为已经有现有的实现作为参考，所以回答诸如此类的问题，不要急，先回想一下平日用这个StringBuilder 都用了哪些方法。

- append
- insert
- delete
- replace
- charAt
- ....

大致就这么几个，没必要说太全，这不是小学课文背诵，关键方法提出来就行了。

脑子浮现这几个方法之后，直接说出来即可：StringBuilder 主要用于动态拼接字符串，大致需要实现 append、insert...等功能。

然后底层使用 char 数组来存储字符，用 count 来记录存放的字符数。

![image.png](https://pic.code-nav.cn/mianshiya/question_picture/1772087337535152129/8VJ4iJFj_image_mianshiya.png)

这里可能会被面试官插入问：String 底层不也是用的 char 数组存放吗？两者有啥区别？

![企业微信截图_d7449805-d279-4fcf-b750-cddcc955fb18.png](https://pic.code-nav.cn/mianshiya/question_picture/1772087337535152129/0yEQaxjH_d7449805-d279-4fcf-b750-cddcc955fb18_mianshiya.png)

展示的机会就来了呀！String 被 final 修饰，且内部的 char 也被 private 和 final 修饰了，所以是不可变的，是典型的 Immutable 类，因此其不可变性，保证了线程安全，能实现字符串常量池等。

ok，咱们继续。

由于 StringBuilder 底层是用 char 数组存放字符，而数组是连续内存结构，为了防止频繁地复制和申请内存，需要提供 capacity 参数来设置初始化数组的大小，这样在预先已经知晓大字符串的情况下，可以减少数组的扩容次数，有效的提升效率！


![Snipaste_2024-04-27_14-06-06.jpg](https://pic.code-nav.cn/mianshiya/question_picture/1783397053004488705/Snipaste_2024-04-27_14-06-06_mianshiya.jpg)

图片这里一定要点破：数组是连续内存的结构，并且要体现出你有节省内存和提高效率的意识，熟悉 HashMap 的同学对这类操作应该很有经验。

我们来看下调用 AbstractStringBuilder 这个父类的构造器。

![Snipaste_2024-04-27_14-06-44.jpg](https://pic.code-nav.cn/mianshiya/question_picture/1783397053004488705/Snipaste_2024-04-27_14-06-44_mianshiya.jpg)

图片可以看到，就是直接new申请数组没啥花头。

> append

我们来看下 append 操作。


![企业微信截图_d4963921-fb68-4d8d-9993-0018c952d986.png](https://pic.code-nav.cn/mianshiya/question_picture/1772087337535152129/0obNSjpt_d4963921-fb68-4d8d-9993-0018c952d986_mianshiya.png)

可以看到 append 有多个实现，毕竟我们平日啥都类型都直接 append ，那底层是怎么实现这些类型转换的呢？

我们拿 append(int) 来举个例子，其他类型本质都是一样的。


![Snipaste_2024-04-27_14-14-19.jpg](https://pic.code-nav.cn/mianshiya/question_picture/1783397053004488705/Snipaste_2024-04-27_14-14-19_mianshiya.jpg)

主要逻辑已经在图中标识了，熟悉 HashMap 八股文的同学一看就知道老套路了，先看看 append 的 int值转成 char 需要占数组的几位，然后计算一下现在的数组够不够放，如果不够就扩容一下，然后再把 int 转成 char 放进去，再更新现有的字符数。

所以面试回答 append 实现的时候，直接把上面那段话的思路说一下即可。

面试官可能会追问：怎么扩容的呀？

我们直接看下 ensureCapacityInternal 这个方法的实现


![Snipaste_2024-04-27_14-15-43.jpg](https://pic.code-nav.cn/mianshiya/question_picture/1783397053004488705/Snipaste_2024-04-27_14-15-43_mianshiya.jpg)


直接就是 Arrays.copyOf，进行一波扩容加拷贝，扩容之后的数组容量为之前的两倍+2。

这时候想必有很多同学好奇，前面是如何根据传入的 int 来计算得知所占的字符位数？即上面代码的Integer.stringSize 方法，注意这个方法已经跑到 Integer 这个类中啦！不是 AbstractStringBuilder的实现了。

![Snipaste_2024-04-27_14-19-52.jpg](https://pic.code-nav.cn/mianshiya/question_picture/1783397053004488705/Snipaste_2024-04-27_14-19-52_mianshiya.jpg)

哈哈，你以为会经过一番看不懂的位运算？

实际上就是查表法！直接列了各个位数的边界值依次存放在数组中，然后判断大小再根据数组下标算出位数，就是这么简单、方便、高效！

再来看下 int 是如何转换成 char 然后插入到数组中的，即Integer.getChars方法。


![Snipaste_2024-04-27_14-20-46.jpg](https://pic.code-nav.cn/mianshiya/question_picture/1783397053004488705/Snipaste_2024-04-27_14-20-46_mianshiya.jpg)

身为底层实现，还是很细的，可以仔细看下上面的逻辑，位运算看不懂没事，注释已经把原有的公式写出来的，对照着看看，还是能理解的，这里我就不再赘述了。

然后各位也应该注意到上面的DigitOnes、DigitTens这两个数组了，没错还是熟悉的查表法！


![Snipaste_2024-04-27_14-22-19.jpg](https://pic.code-nav.cn/mianshiya/question_picture/1783397053004488705/Snipaste_2024-04-27_14-22-19_mianshiya.jpg)

你们可以选几个数字带入算一算，很准的，哈哈，至于 digits 也一样，还是查表。

图片其实我们常用的 String.valueOf(int i)，内部实现一样也是通过Integer.stringSize 和Integer.getChars 来完成的。

![Snipaste_2024-04-27_14-23-07.jpg](https://pic.code-nav.cn/mianshiya/question_picture/1783397053004488705/Snipaste_2024-04-27_14-23-07_mianshiya.jpg)

好了，这波操作下来，想必拨开了很多对 StringBuilder 的迷雾吧~

> insert

再来看看 insert，我们还是拿 int 的插入来举例：


![Snipaste_2024-04-27_14-24-22.jpg](https://pic.code-nav.cn/mianshiya/question_picture/1783397053004488705/Snipaste_2024-04-27_14-24-22_mianshiya.jpg)

可以看到，这里是把 int 转成 string 了，然后调用以下的方法：


![Snipaste_2024-04-27_14-24-55.jpg](https://pic.code-nav.cn/mianshiya/question_picture/1783397053004488705/Snipaste_2024-04-27_14-24-55_mianshiya.jpg)

注释写的很明白了，没什么花头，主要逻辑就是插入前先判断下数组长度足够，若不够就扩容，然后移动字符，给待插入的位置腾出空间，然后往对应位置插入字符，最后更新 StringBuilder 已有的字符数。

是吧，很直白的逻辑。

## delete

这个就更简单了，就是一个数组的删除操作，没什么花头。

![Snipaste_2024-04-27_14-26-03.jpg](https://pic.code-nav.cn/mianshiya/question_picture/1783397053004488705/Snipaste_2024-04-27_14-26-03_mianshiya.jpg)

剩下的replace、charAt 等等方法就不提了，没有什么花头，总结来说都是数组的操作，有兴趣的自行去看看吧~

## 总结

这样看下来，想必对 StringBuilder 的内部实现已经很清晰了吧！就是数组的操作，而数组的特性就是内存连续，下标访问快。

针对内存连续这点，又要保持 StringBuilder 的动态性，那不可避免的就需要扩容操作，扩容操作简单来说就是申请一个更大 char 数组，把老 char 数组的数据拷贝过去。

对了，从源码来看，StringBuilder 没有实现缩容操作。

所以回答这个设计题的时候，先说下需要实现哪些关键方法：append、delete 等等，然后点明底层是 char 数组实现，在执行 append、insert 等操作的时候需要先判断数组容量是否足够容纳字符来判断是否需要扩容，然后修改之类的操作就是调用 System.arraycopy 来完成字符串的变更。

因为原生的 StringBuilder 没有实现缩容操作，所以你可以提一下在 delete 的时候，判断下，如果删除的字符过多，为了节省内存，实现缩容的操作。

然后还可以再提一下，char 数组是可以优化的，底层可以用 byte 数组+一个 coder 标志位来实现，这样更节省内存，因为 char 占用两个字节，这样对于 latin 系的字符来说，太大了，就很浪费，所以用 byte 数组，然后配备一个 coder 来标识所用的编码。

嘿嘿，其实 jdk 9 之后就是这样实现的，但是你可以假装不知道呀，装的像你自己想出来的优化，你看看这多细呀~疯狂加分！

来看下源码，我的是 jdk 11版本~，可以看到已经变成 byte 数组了， coder 也用一个 byte 标识。


![Snipaste_2024-04-27_14-27-01.jpg](https://pic.code-nav.cn/mianshiya/question_picture/1783397053004488705/Snipaste_2024-04-27_14-27-01_mianshiya.jpg)

再看下 append 的方法的实现：


![企业微信截图_0fe540a7-7ace-44e3-8302-f9c720143f51.png](https://pic.code-nav.cn/mianshiya/question_picture/1772087337535152129/R7G5Ca0v_0fe540a7-7ace-44e3-8302-f9c720143f51_mianshiya.png)

没骗你吧，用 coder 来判断所用的编码，进行区分操作~

好了，这样一波回答下来，细节就很细了，满分！