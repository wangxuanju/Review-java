# Java基础
## ==与equals()方法的区别？
==  基本类型，判断两个值是否相等；引用类型，两个变量是否引用同一对象。

equals（） 引用对象是否等价（等价的两个对象hashcode（）返回的散列值一定相同，散列值相同的两个对象不一定等价）

（hashcode（）：返回散列值）
## 重写与覆盖

重写：子类的访问权限必须大于等于父类的访问权限；子类方法的返回类型必须为父类方法或其子类型

覆盖：相同的名字，不同的参数（不允许存在名字相同，参数相同，仅仅返回类型不同的方法）

## 接口和抽象类的比较
接口是一种like-A关系，提供了一种方法实现契约；
抽象类是一种is-A关系，即子类对象必须能替换掉所有的父类对象。

一个类可实现多个接口，但不能继承多个抽象类；接口字段只能是static和final类型的，即接口成员只能是public的。（很多情况下，接口优先于抽象类，因为接口可以灵活的为一个类添加行为）

## String、StringBuffer和StringBuilder
String不可变，线程安全；StringBuilder可变，非线程安全；StringBufer可变，线程安全，内部使用synchronized进行同步。

# 集合
容器包括Collection和Map两种，Collection存储着对象的集合，Map存储着键值对的映射表。
## Collection
set：
HashSet(哈希表）/LinkedHashSet（双向链表）

List:
ArrayList（动态数组）/LinkedList（双向链表）/Vector（动态数组）
## ArrayList和Vector的比较？
二者均基于动态数组实现，其中Vector是同步的线程安全，开销较ArrayList大，访问速度更慢；推荐使用ArrayList，因为同步操作可以由程序员自己控制。

Vector每次扩容请求为其大小的两倍，而ArrayList是1.5倍。
## ArrayList和LinkedList的比较？
ArrayList基于动态数组实现，支持随机访问，如果需要大量随机访问的情景建议使用ArrayList（查询快，增删慢）
LinkedList基于双向链表实现，添加和删除更快，如果需要经常插入或删除元素建议使用LinkedList（查询慢，增删快）
（Vector基于动态数组实现，同步、线程安全，查询慢，增删慢）

## ArrayList的扩容机制？
ArrayList添加元素时使用ensureCapactityInternal()方法来保证容量足够，不够则用grow()方法进行扩容（新容量为旧容量的1.5倍），扩容时调用Arrays.copyOf()把原数组整个复制到新数组中，最好在创建ArrayList对象时就指定大概容量的大小，减少扩容操作的次数。

Queue：
LinkedList（双向链表）/priorityQueue（堆）

Map：
HashTable（哈希表）/HashMap（哈希表）/LinkedHashMap(双向链表）
## HashTable和HashMap的区别
HashTable是线程安全的一个集合，不允许空值，多个线程访问时不需要为它的方法实现同步（使用synchronized来进行同步）
HashMap是Map的一个子接口，线程不安全，不允许键值重复（允许值重复），允许空键和空值，效率较HashTable高（不能保证随着时间的推移Map中的元素次序是不变的）。
## HashMap与ConcurrentHashMap的区别？（深究）

二者实现上类似，但ConcurrentHashMap采用了分段锁（Segment）的机制，多个线程可以同时访问不同分段锁上的桶，使其并发度更高；（Segment通过继承ReentrantLock来进行加锁，每次需要加锁都锁住一个Segment，只要保证每个Segment是线程安全的，也就实现了全局的线程安全）

## HashTable和ConcurrentHashMap的区别?
二者都是线程安全的，但HashTable是遗留类，建议使用ConcurrentHashMap,与之相比效率更高，因为引入了分段锁。
## HashMap和LinkedHashMap？
LinkedHashMap继承HashMap，具有和它一样的快速查找特性，内部维护了一个双向链表，用来维护插入顺序或LRU顺序。

## 集合的安全性问题
ArrayList/HashMap/HashSet都不是线程安全的，Vector和HashTable是线程安全的

Collections工具类提供了相关API，可以让三个不安全的集合变成安全的

Collections.synchronizedCollection(c)

Collections.synchronizedList(list)

Collections.synchronizedMap(m)

Collections.synchronizedSet(s)

实现原理将核心方法添加上了synchronized关键字（这几个函数传入什么类型返回什么类型）
## Collection和Collectons的区别？
Collection是集合框架的父接口，对集合对象进行基本操作的通用接口方法

Collectons是一个包装类，就像一个工具类提供一系列有关集合操作的静态多态方法，服务于Collection框架。
