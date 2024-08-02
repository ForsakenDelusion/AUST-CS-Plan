SPI（Service Provider Interface）服务提供接口是 Java 的机制，主要用于实现模块化开发和插件化扩展。
SPI 机制允许服务提供者通过特定的配置文件将自己的实现注册到系统中，然后系统通过反射机制动态加载这些实现，而不需要修改原始框架的代码，从而实现了系统的解耦、提高了可扩展性。

一个典型的 SPI 应用场景是 JDBC（Java 数据库连接库），不同的数据库驱动程序开发者可以使用 JDBC 库，然后定制自己的数据库驱动程序。

此外，我们使用的主流 Java 开发框架中，几乎都使用到了 SPI 机制，比如 Servlet 容器、日志框架、ORM 框架、Spring 框架。**所以这是 Java 开发者必须掌握的一个重要特性**！

### 如何实现 SPI？
分为系统实现和自定义实现。

#### 系统实现
其实 Java 内已经提供了 SPI 机制相关的 API 接口，可以直接使用，这种方式最简单。
1) 首先在 resources 资源目录下创建 META-INF/services 目录，并且创建一个名称为要实现的接口的空文件



2) 在文件中填写自己定制的接口实现类的 完整类路径，如图：

![image.webp](https://pic.code-nav.cn/mianshiya/question_picture/1783397053004488705/image_mianshiya.webp)



3) 直接使用系统内置的 ServiceLoader 动态加载指定接口的实现类，代码如下：

```java
// 指定序列化器
Serializer serializer = null;
ServiceLoader<Serializer> serviceLoader = ServiceLoader.load(Serializer.class);
for (Serializer service : serviceLoader) {
    serializer = service;
}
```

上述代码能够获取到所有文件中编写的实现类对象，选择一个使用即可。

#### 自定义 SPI 实现

系统实现 SPI 虽然简单，但是如果我们想定制多个不同的接口实现类，就没办法在框架中指定使用哪一个了，也就无法实现我们 “通过配置快速指定序列化器” 的需求。

所以我们需要自己定义 SPI 机制的实现，只要能够根据配置加载到类即可。

比如读取如下配置文件，能够得到一个 序列化器名称 => 序列化器实现类对象 的映射，之后就可以根据用户配置的序列化器名称动态加载指定实现类对象了

```java
jdk=com.yupi.yurpc.serializer.JdkSerializer
hessian=com.yupi.yurpc.serializer.HessianSerializer
json=com.yupi.yurpc.serializer.JsonSerializer
kryo=com.yupi.yurpc.serializer.KryoSerializer
```