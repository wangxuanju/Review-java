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
（三种方法给Spring容器配置元数据：xml配置文件、基于Java的注解和基于Java的配置）
### Spring beans的生命周期
#### bean定义：配置文件中用<bean></bean>标签来定义
#### bean初始化：
配置文件中指定init-method属性来完成
实现org.springframwork.beans.factory.InitalizingBean接口
#### Bean调用 三种方式可以得到bean实例进行调用（BeanWrapper/BeanFactory/ApplicationContext）
#### Bean销毁
配置文件指定destroy-method属性
实现org.springframwork.beans.factory.DisposeableBean接口


### Bean的自动装配
IOC容器会自动简历JavaBean之间的关联关系，无须在配置文件中描述JavaBean之间的依赖关系
### Spring中Bean的作用域？
所创建的bean实例如果可以共享，就是Singleton（默认的作用域），如果每次从Spring容器请求bean时都创建一个新的bean实例就是protype
（web应用场景中，request/session/application/global Session等）
### Spring的内部bean
当一个bean仅被用作另一个bean的属性时，能被声明为一个内部bean（Spring基于xml的配置元数据中，在<property/>或<constructor-org/>元素内使用<bean/>元素）

## BeanFactory与Application与ApplicationContext的区别？
BeanFactory是基础类型的IOC容器，提供完整的IOC服务支持；

ApplicationContext是在BeanFactory的基础上构建，除了支持BeanFactory的所有功能外，还支持事件发布、国际化支持等。ApplicationContext管理的对象，在容器启动后默认全部初始化并绑定完成。
#### ApplicationContext的实现类：
FileSystemXmlApplicationContext文件路径获取/ClassPathXmlApplicationContext类路径获取/webXmlApplicationContext

## Spring中xml配置和注解配置比较？
xml（繁琐、代码独立），注解（简洁，代码耦合），一般二者配合使用

## Spring事务及其传播属性？
事务是一系列的动作，这些动作必须全部完成；如果一个动作失败，就回滚到开始状态。

事务的四大特性：

原子性：要么全部完成，要么全部失败（完全不起作用）

一致性：一旦事务完成，必须确保它所建模的业务处于一致的状态

隔离性：许多事务会同时处理相同的数据，每个事务都应该与其它事务隔离开来

持久性：一旦事务完成，无论发生什么系统错误，结果都不应该受到影响（通常事务被写入持久化存储器中）
### 传播行为
当事务方法被另一个事务方法调用时，必须指定事务该如何传播

### Spring中事务是如何实现的，有哪些事务处理机制？
Spirng提供了多种事务管理器，将事务管理的职责委托给相关的平台框架的事务来实现；Spring事务管理器的接口是org.springframework.transaction.PlatformTransactionManager,通过这个接口，Spring为各个平台如JDBC/Hiberante等提供了对应的事务管理器。

## Spring中的设计模式？
单例模式：配置文件中设置bean默认为单例模式

依赖注入：贯穿于BeanFactory/ApplicationContext接口的核心理念

前端控制器模式：Spring提供了前端控制器DispatchServlet来对请求进行分发

工厂模式：Spring中使用beanFactory来创建对象的实现

# SpringMVC
SpringMVC是一个MVC的流程框架，分离了控制器、分派器、模型对象和处理程序对象的角色，这种分离让它们更容器进行定制。
## SpringMVC的工作原理
a:用户向服务器发送请求，请求被前端控制器DispatchServlet捕获

b:其对请求的URL进行解析，根据URL调用HandlerMapping将请求映射到处理器HandlerExcutonChain

c:DispatchServlet根据获得的Handler选择一个合适的HandlerAdapter适配器

d:Hander返回的ModelAndView()只是一个逻辑视图，通过ViewRosolver视图解析器转化为真正的视图view

f：DispatchServlet通过model解析出ModelAndView()中的参数进行解析最终展现出完整的view并返回给客户端
## SpringMVC常用的注解有哪些？
@RequestMapping请求URL映射

@RequestBody实现接收Http请求的json数据，将其转化为Java对象

@ResponseBody将controller方法返回对象转化为json响应给客户
# MyBatis
MyBatis是基于Java的持久层框架，内部封装了JDBC，使开发者只需要关注SQL语句本身，不用在处理加载驱动、创建连接、创建statement等复杂的过程。

MyBatis通过xml配置或注解的方式将要执行的各种statement配置起来，并通过Java对象和statement中的SQL的动态参数进行映射生成最终执行的SQL语句，最后由MyBatis框架执行SQL并将结果返回给客户端。
## MyBatis的编程步骤是什么样的？
1、创建SqlSessionFactory
2、通过SqlSessionFactory创建SqlSession
3、通过SqlSession执行数据库操作
4、调用session.commit()提交事务
5、调用ssssion.close()关闭会话

## MyBatis缓存，二者区别？
MyBatis通过缓存策略来减少数据库的查询次数
### 一级缓存
基于PerpetualCache的HashMap本地缓存，存储作用域为Session，SqlSession级别的缓存，只要SqlSession没有flush或close，它就存在
### 二级缓存
也是基于PerpetualCache的HashMap缓存（默认），存储作用域为Mapper(Namespace),并且可以自定义存储源，多个SqlSession去操作同一个Mapper映射的SQL语句共用二级缓存

# SpringBoot
SpringBoot解决了Spring配置繁琐复杂的缺点，基于约定优先于配置的原则，让开发人员投入到逻辑业务的编写之中，提高了开发效率，缩短了项目周期
## SpringBoot的优点
SpringBoot提供了一种快速使用Spring的方式，提供更快的入门体验，开箱即用，没有代码生成也无须xml配置。
## SpringBoot的核心功能
起步依赖：本质上是Maven项目对象模型（pom.xml）,定义了对其它库的传递依赖（起步依赖的作用就是进行依赖的传递）

自动配置：是Spring自动完成的

（SpringBoot项目要配置起步依赖spring-boot-starter-parent；如果集成SpringMVC进行Controller开发，要导入spring-boot-starter-web）

```java
@SpringBootApplication #标注SpringBoot启动类
public class MySpringBootApplication{
    public static void main(String[] args){
        SpringApplication.run(MySpringBootApplication.class);#参数为启动类的字节码对象
        # 代表运行SpringBoot的启动类
    
    }
}

```
