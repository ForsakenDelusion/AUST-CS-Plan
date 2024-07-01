---
profileName: FskDe7usion
postId: "60"
postType: post
categories:
  - 7
---
首先输入

```shell
/usr/libexec/java_home -V
```

查看java版本

然后打开.zshrc配置文件修改配置
```shell
# 设置 JDK 17
export JAVA_17_HOME=/Users/yu/Library/Java/JavaVirtualMachines/azul-17.0.10/Contents/Home
# 设置 JDK 8
export JAVA_8_HOME=/Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home
# 默认JDK 17
export JAVA_HOME=$JAVA_17_HOME
# alias命令动态切换JDK版本
alias jdk8="export JAVA_HOME=$JAVA_8_HOME"
alias jdk17="export JAVA_HOME=$JAVA_17_HOME"
```

`JAVA_X_HOME`后面跟的就是上一部查看版本中显示的路径,X表示版本