# 线程
## 多线程的两种方式
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

