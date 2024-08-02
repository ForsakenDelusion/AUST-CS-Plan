这题一般会出现在笔试题中，例如让你手写一个基于 Java 实现网络通信的代码。

Java 的网络编程主要利用 java.net 包，它提供了用于网络通信的基本类和接口。

Java 网络编程的基本概念：
- IP 地址：用于标识网络中的计算机。
- 端口号：用于标识计算机上的具体应用程序或进程。
- Socket（套接字）：网络通信的基本单位，通过 IP 地址和端口号标识。
- 协议：网络通信的规则，如 TCP（传输控制协议）和 UDP（用户数据报协议）。

Java 网络编程的核心类：
- Socket：用于创建客户端套接字。
- ServerSocket：用于创建服务器套接字。
- DatagramSocket：用于创建支持 UDP 协议的套接字。
- URL：用于处理统一资源定位符。
- URLConnection：用于读取和写入 URL 引用的资源。

示例代码参考(以下代码时基于 TCP 通信的，一般笔试考察的都是 TCP)：

服务端代码：
```java
import java.io.*;
import java.net.*;

public class TCPServer {
    public static void main(String[] args) {
        try (ServerSocket serverSocket = new ServerSocket(8080)) {
            System.out.println("Server is listening on port 8080");

            while (true) {
                Socket socket = serverSocket.accept();
                //异步处理，优化可以用线程池
                new ServerThread(socket).start();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

class ServerThread extends Thread {
    private Socket socket;

    public ServerThread(Socket socket) {
        this.socket = socket;
    }

    public void run() {
        try (PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
             BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()))) {

            // 读取客户端消息
            String message = in.readLine();
            System.out.println("Received: " + message);

            // 响应客户端
            out.println("Hello, client!");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

客户端代码：

```java
import java.io.*;
import java.net.*;

public class TCPClient {
    public static void main(String[] args) {
        try (Socket socket = new Socket("localhost", 8080);
             PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
             BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()))) {

            // 发送消息给服务器
            out.println("Hello, server!");

            // 接收服务器的响应
            String response = in.readLine();
            System.out.println("Server response: " + response);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```