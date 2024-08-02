在 Java 中其实分了两大类异常，受检异常（checked exception）和非受检异常（unchecked exception），**它们之间的差别主要在于是否是编译时检查**。

受检异常（checked exception）其实就是**编译时异常**，继承自 Exception，即在编译阶段检查代码中可能会出现的异常，需要开发者显示的捕获（catch）或声明抛出（throw）这种异常，否则编译就会报错，这是一种强制性规范。

常见的有：IOException、SQLException、FileNotFoundException 等等。

非受检异常（unchecked exception）就是**运行时异常**，继承自 RuntimeException 类。是指在运行期间可能会抛出的异常，编译期不强制要求处理，之所以不强制是因为它可以通过完善代码避免报错。

常见的有：NullPointerException、ArrayIndexOutOfBoundsException、ArithmeticException 等等。