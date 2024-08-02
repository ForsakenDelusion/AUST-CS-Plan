Exception 是程序正常运行过程中可以预料到的意外情况，应该被开发者捕获并且进行相应的处理。

Error 是指在正常情况下不太可能出现的情况，绝大部分的 Error 都会导致程序处于不正常、不可恢复的状态，也就是挂了。

所以不便也不需被开发者捕获，因为这个情况下你捕获了也无济于事。

Exception和Error都是继承了Throwable类，在Java代码中只有继承了Throwable类的实例才可以被throw或者被catch。

顺便我再提一提异常处理的注意点，之前写过文章总结过：

>1. 尽量不要捕获类似Exception这样通用的异常，而应该捕获特定的异常。

软件工程是一门协作的艺术，在日常的开发中我们有义务使自己的代码能更直观、清晰的表达出我们想要表达的信息。

但是如果你什么异常都用了Exception，那别的开发同事就不能一眼得知这段代码实际想要捕获的异常，并且这样的代码也会捕获到可能你希望它抛出而不希望捕获的异常。

>2. 不要 “吞” 了异常

如果我们捕获了异常，不把异常抛出，或者没有写到日志里，那会出现什么情况？线上除了 bug 莫名其妙的没有任何的信息，你都不知道哪里出错以及出错的原因。

这可能会让一个简单的bug变得难以诊断，而且有些同学比较喜欢用 catch 之后用e.printStackTrace()，在我们产品中通常不推荐用这种方法，一般情况下这样是没有问题的但是这个方法输出的是个标准错误流。

public void printStackTrace() 
<font color="red">Prints this throwable and its backtrace to the standard error stream</font> This method prints a stack method <font color="blue">fillInStackTrace().</font> The format of this information depends on the impremenentation of the <font color="blue">printStackTrace(java.io.PrintStream)</font> method of this class, which can be overridden in subclasses.
 

比如是在分布式系统中，发生异常但是找不到stacktrace。

所以最好是输入到日志里，我们产品可以自定义一定的格式，将详细的信息输入到日志系统中，适合清晰高效的排查错误。

>3. 不要延迟处理异常

比如你有个方法，参数是个 name，函数内部调了别的好几个方法，其实你的name传的是 null 值，但是你没有在进入这个方法或者这个方法一开始就处理这个情况，而是在你调了别的好几个方法然后爆出这个空指针。

这样的话明明你的出错堆栈信息只需要抛出一点点信息就能定位到这个错误所在的地方，经过了好多方法之后可能就是一坨堆栈信息。


> 4. 只在需要try-catch的地方try-catch，try-catch的范围能小则小

只要必要的代码段使用try-catch，不要不分青红皂白try住一坨代码，因为try-catch中的代码会影响JVM对代码的优化，例如重排序。

> 5. 不要通过异常来控制程序流程

一些可以用if/else的条件语句来判断例如null值等，就不要用异常，异常肯定是比一些条件语句低效的，有 CPU 分支预测的优化等。

而且每实例化一个 Exception 都会对栈进行快照，相对而言这是一个比较重的操作，如果数量过多开销就不能被忽略了。

> 6. 不要在finally代码块中处理返回值或者直接return

在 finally 中 return 或者处理返回值会让发生很诡异的事情，比如覆盖了 try 中的 return ，或者屏蔽的异常。

