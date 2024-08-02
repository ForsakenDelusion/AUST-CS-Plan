Java 的 I/O 流（Input/Output Streams）是用于处理输入和输出操作的类和接口，主要用于读取和写入数据，可以处理不同类型的数据源和目标，如文件、网络连接、内存缓冲区等等。

首先需要了解 I/O 流分为两类：

- 输入流（Input Stream）：用于读取数据的流。
- 输出流（Output Stream）：用于写入数据的流。

基于这两种输入输出的类型，按照处理的数据类型还可以进行分类：

1）字节流（Byte Streams）：用于处理字节数据，适用于所有类型的 I/O 操作。

输入流：InputStream，常用以下几个输入流：
- FileInputStream：从文件中读取字节数据。
- BufferedInputStream：为输入流提供缓冲功能，提高读取性能。
- DataInputStream：读取基本数据类型的数据。


输出流：OutputStream，常用以下几个输出流：
- FileOutputStream：将字节数据写入文件。
- BufferedOutputStream：为输出流提供缓冲功能，提高写入性能。
- DataOutputStream：写入基本数据类型的数据。

2）字符流（Character Streams）：用于处理字符数据，适用于文本文件。

输入流：Reader，常用以下几个输入流：
- FileReader：从文件中读取字符数据。
- BufferedReader：为字符输入流提供缓冲功能，提高读取性能。
- InputStreamReader：将字节流转换为字符流。

输出流：Writer，常用以下几个输出流：

- FileWriter：将字符数据写入文件。
- BufferedWriter：为字符输出流提供缓冲功能，提高写入性能。
- OutputStreamWriter：将字符流转换为字节流。

### 扩展：Java 的 I/O 必备知识：
 
- 理解基本的 I/O 类和接口：如 InputStream、OutputStream、Reader、Writer 及其常见子类。
- 理解缓冲流的作用：如 BufferedReader、BufferedWriter、BufferedInputStream、BufferedOutputStream，它们可以提高 I/O 操作的性能。
- 异常处理：I/O 操作容易出现 IOException，需要进行适当的异常处理。
- 资源管理：使用 try-with-resources ，确保 I/O 流在使用完毕后正确关闭。
- 字符编码：理解和正确使用字符编码（如 UTF-8），避免乱码。
- NIO（New I/O）：了解 Java NIO（如 java.nio 包中的类），它提供了更高效的 I/O 操作，适用于需要高性能 I/O 的场景。