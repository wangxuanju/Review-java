# Spring
## 简单介绍一下Spring,什么是IOC、DI、AOP以及常用的注解有哪些？
#### Spring是一个分层的一站式轻量级开发框架。
#### core和beans模块提供了IOC和DI的特性；AOP模块可以定义方法拦截器和切入点等，减弱了代码的耦合。
### Spring的优点：
#### 方便解耦，简便开发；对AOP编程和声明式事务的支持；方便程序进行测试；方便集成各种优秀框架；对JavaEE中难用的API（如JDBC、JavaMail等）提供了封装，降低了其使用难度。

### IOC
#### 以前由我们自己实例化的对象，现在交给Spring容器来进行实始化，对象实始化的权利发生了反转。（获取依赖对象的方式被反转了）
### DI
#### 使用JavaBeans对象的set方法或带参数的构造方法在需要对象时将其属性自动设置为所需要值的过程。
（IOC或DI把应用程序的代码量降到最低，以最小的代价和侵入性使松耦合得以实现）
### AOP
#### 将一个个对象某些类似的方法横向抽成一个切面，对这个切面进行诸如权限控制、事务管理、记录日志等公用操作处理的过程。（AOP是OOP的补充和完善，减少了重复代码，降低了模块之间的耦合度，有利于未来的可操作性性和可扩展性）

### Spring常用注解
开启注解或者指定Spring需要扫描的包：<context:annotation-config/>或<context:component-scan base-package="cn.itheima.annotation"/>
常用注解：
@required:设置方法
@Autowired:设置方法，构造方法和变量
@Qualifier:和@Autowired配合使用，用于消除bean自动装配的歧义
```java
@Value("王")
private String name;简单的属性注入
@Autowired
private IuserDao userDao;复杂的属性注入
@Value @Autowired可以修饰属性也可以修饰setter方法


@Autowired
@Qualifier("userDao"）
private IuserDao userDao;二者配合使用可根据名称进行注入



@Component的三个衍生的注解
@Repository dao层
@Service service层
@Controller web层（表现层）
```

## 什么是Spring beans?
#### Spring beans是那些形成Spring应用的主干Java程序，被Spring IOC容器初始化、装配和管理，通过容器配置的元数据创建
# SpringMVC

# MyBatis
