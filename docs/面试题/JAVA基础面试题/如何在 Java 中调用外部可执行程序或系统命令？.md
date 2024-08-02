面试中一般不会问这题，大家仅做了解即可（除非是特殊岗位的一些场景）

在 Java 中，可以使用 Runtime 类或 ProcessBuilder 类来调用外部可执行程序或执行系统命令。这两种方法都能创建一个子进程来执行指定的命令或程序。接下来就是这两个类的简单使用：

1）使用 Runtime.exec()
Runtime 类提供了 exec() 方法，它允许你执行外部命令。相对于 ProcessBuilder 比较简单。

使用例子如下：

<img src="https://pic.code-nav.cn/mianshiya/question_picture/1783393747989405698/1img_mianshiya.png" alt="1img.png" width="100%" />

如果还需要获取返回的内容，可以通过 Process 对象中的 getInputStream 方法来获取字符输入流对象。

简单解释一下：
- 执行命令：使用 `Runtime.getRuntime().exec` 方法执行命令。
- 等待进程结束：使用 `waitFor` 方法等待进程结束并获取退出码。

2）使用 ProcessBuilder
ProcessBuilder 类提供了一个更灵活和强大的方式来管理外部进程。它允许你设置环境变量、工作目录，以及重定向输入和输出流。

使用 ProcessBuilder 的例子：  

<img src="https://pic.code-nav.cn/mianshiya/question_picture/1783393747989405698/1img_1_mianshiya.png" alt="1img_1.png" width="100%" />

简单解释一下：

- 创建 ProcessBuilder 实例：使用 ProcessBuilder 创建一个新的进程。
- 设置命令：通过 command 方法指定要执行的命令及其参数或像例子直接在构造函数内写入。
- 启动进程：使用 start 方法启动进程。
- 读取输出：通过 getInputStream 获取进程的输入流，并读取输出。
- 等待进程结束：使用 waitFor 方法等待进程结束并获取退出码。