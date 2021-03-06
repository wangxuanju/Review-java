# 一、运行时数据区域：
Java虚拟机在执行Java程序的过程中会把它所管理的内存划分为若干个不同的数据区域。

（这些区域都有各自的用途，以及创建和销毁的时间，有的区域随着虚拟机进程的启动而存在，有的区域则依赖用户线程的启动和结束而建立和销毁。）
## 程序计数器
程序计数器是一块较小的内存区域，它可以看作是当前线程所执行的字节码的行号指示器。在虚拟机的概念模型里，字节码解释器工作时就是通过改变这个计数器
的值来选取下一条需要执行的字节码指令，分支、循环、跳转、异常处理、线程恢复等基础功能都需要依赖这个计数器来完成。

（由于Java虚拟机的多线程是通过线程轮流切换并分配处理器执行时间来实现的，在任何一个确定的时刻，一个处理器都只会执行一条线程中的指令。因此，为了线程切换后能恢复到正确的执行位置，每条线程都需要有一个独立的程序计数器，各条线程之间的计数器互不影响，独立存储，我们成这类内存区域为“线程私有”的内存）
## Java虚拟机栈
Java虚拟机栈也是线程私有的，它的生命周期与线程相同。虚拟机栈描述的是为Java方法执行的内存模型：每个方法在执行的同时都会创建一个站帧用于存储局部变量表、操作数栈、动态链接、方法出口灯信息。每一个方法从调用直至执行完成的过程，就对应着一个栈帧咋虚拟机中入栈到出栈的过程。

（在Java虚拟机规范中，对这个区域规定了两种异常状况：如果线程请求的栈深度大于虚拟机所允许的深度，将抛出StackOverflowError异常；如果虚拟机栈可以动态扩展，如果扩展时无法请到足够的内存，就会抛出OutOfMemoryError异常。）
## 本地方法栈
本地方法栈与虚拟机栈之间的区别是虚拟机栈为虚拟机执行Java方法服务，而本地方法栈则为虚拟机使用到的Native方法服务。
## Java堆
对应大多数应用来说，Java堆是Java虚拟机所管理的内存中最大的一块。Java堆是被所有线程共享的一块内存区域，在虚拟机启动时创建。此内存区域的唯一目的就是存放对象实例，几乎所有的对象实例都在这里分配内存。

Java堆是垃圾收集器管理的主要区域，因此很多时候也被称为“GC堆”。Java堆中还可以细分为：新生代和老年代；在细致一点的有Eden空间、From Survivor空间、To Survivor空间的等。

（Java虚拟机规范规定，Java堆可以处以物质上不连续的内存空间上，只要逻辑上士连续的即可，就像我们的磁盘空间一样。在实现时，既可以实现成国定大小的，也可以是可扩展的，不过当前主流的虚拟机都是按照可扩展来实现的（通过-Xmx和-Xms控制））。
## 方法区
方法区是各个线程共享的内存区域，它用于存储已被虚拟机加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。

（Java虚拟机规范对方法区的限制非常宽松，除了和Java堆一样不需要连续的内存和可以选择固定大小或可扩展外，还可以选择不实现垃圾收集。相对而言，垃圾收集行为在这个区域是比较少出现的。）（根据Java虚拟机规范的规定，当方法区无法满足内存分配需求时，将抛出OutOfMemoryError异常。）
## 运行时常量池
运行时常量池是方法区的一部分。Class文件中除了有类的版本、字段、方法、接口等描述信息外，还有一项信息是常量池，用于存放编译期生成的各种字面量和符号引用，这部分内容将在类加载后进入方法区的运行时常量池存放。

（运行时常量池相对于Class文件常量池的另外一个重要特征是具备动态性。）
## 直接内存
直接内存（在JDK1.4中新加入NIO类，引入一种基于通道与缓冲区的I/O方式，它可以使用Native函数库直接分配堆外内存，然后通过一个存储在Java堆中DirectByteBuffer对象作为这块内存的引用进行操作。这样能在一些场合中显著提高性能，因此避免了在Java堆和Native堆中来回复制数据。）

本机直接内存的分配仍会受到本机总内存大小以及处理器寻址空间的限制。
