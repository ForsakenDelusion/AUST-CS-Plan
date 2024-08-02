因为根据实践发现大部分的数据操作都集中在值比较小的范围，因此 Integer 搞了个缓存池，默认范围是 -128 到 127，可以根据通过设置 `JVM-XX:AutoBoxCacheMax=<size>` 来修改缓存的最大值，最小值改不了。

实现的原理是int 在自动装箱的时候会调用Integer.valueOf，进而用到了 IntegerCache。

![image-20210228112742081.png](https://pic.code-nav.cn/mianshiya/question_picture/1783397053004488705/image-20210228112742081_mianshiya.png)

没什么花头，就是判断下值是否在范围之内，如果是的话去 IntegerCache 中取。

IntegerCache 在静态块中会初始化好缓存值。

![image-20210228112757226.png](https://pic.code-nav.cn/mianshiya/question_picture/1783397053004488705/image-20210228112757226_mianshiya.png)

所以这里还有个面试题，就是啥 Integer 127 之内的相等，而超过 127 的就不等了，因为 127 之内的就是同一个对象，所以当然相等。

不仅 Integer 有，Long 也是有的，不过范围是写死的 -128 到 127。

![image-20210228112817173.png](https://pic.code-nav.cn/mianshiya/question_picture/1783397053004488705/image-20210228112817173_mianshiya.png)

对了 Float 和 Double 是没有滴，毕竟是小数，能存的数太多了。

