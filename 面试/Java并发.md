# 线程
## 创建多线程的两种方式
### 第一种方式：
定义一个类继承Thread；

重写run（）方法；

创建子类对象；

调用start()方法开启线程并让线程执行
### 第二种方式：
定义类实现Runnable接口；

覆盖接口中的run方法；

创建Thread类的对象；

将Runnable接口的子类对象作为参数传递给Thread类的构造函数，调用Thread类的start方法开启线程
```java
TicketThread tt = new TicketThread();
Thread t = new Thread(tt);
t.setName("wang");
t.start();
```
## 进程与线程
进程：一次程序的执行，是操作系统管理的基本的运行单元。
线程：在进程中独立运行的子任务。

## 多线程中常用的方法
#### Thread.sleep()指定的毫秒内，休眠当前正在执行的线程
#### yield()当前线程已经完成了生命周期中最重要的部分，可以切换给其它线程来执行
#### join()在线程中调用另一个线程的join()方法，会先将当前线程挂起，直到目标线程结束

#### currentThread()返回代码正在被哪个线程调用的信息
#### getId()取得线程的唯一标识

#### isAlive()判断当前线程是否处于活动状态（线程启动尚未结束）
#### interrupt()仅仅在当前线程中打了一个停止的标记（并不是真正的停止线程）

#### 多线程中使用suspend()方法暂停线程，使用resume()方法恢复线程的执行

### 判断线程是否是停止状态？
#### this.interrupted()当前线程是否已中断
#### this.isInterrupted（）测试当前线程是否已中断

### wait()
调用wait()方法使得线程等待某个条件满足，线程等待时会被挂起，当这个条件满足时，其它线程会调用notify()或notifyAll()来唤醒挂起的线程
### wait()和sleep()的区别
wait()是Object的方法，sleep()是Thread的静态方法；wait()会释放锁，而sleep()不会。




