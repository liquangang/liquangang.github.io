---
title: Spring
date: 2022-04-18 19:31:33
tags: Q&A
categories:
- [Q&A, Q&A-java]
---
## 为什么要使用 spring？
### 一句话概括
* 省去很多非业务层代码的研发工作，提高javaweb应用开发效率
### 详解
* 基于POJO的轻量级和最小侵入式编程；POJO（Plain Ordinary Java Object）即简单Java对象，spring竭力避免污染你的代码，尽量解除我们的代码与spring之间的耦合。具备非侵入式变成的思想，耦合低，代码污染小
* 通过依赖注入和面向接口编程实现松耦合：降低模块内部不同类之间的依赖，当在某一个类当中使用其他类时，通过spring来管理对象的创建于销毁，spring提供了一种组建内部不同类低耦合协作的一种方式
* 基于切面和管理进行声明式编程：对于日志管理等通用模块，采用面向切面的方式，使其他模块在编程时完全不需要了解这些部分的相关逻辑与代码
* 通过切面和模板减少样板式代码：面向切面编程消除了大量的重复代码，比如调用初始化等等

## 解释一下什么是 aop？
* AOP（Accept Oriented Programming）即面向切面编程，把编程看成是多个切面的实现，比如安全检查、日志打印、实际业务处理等，通过对方法进行拦截，按照需要的顺序，放入不同的切面代码
* OOP（Object Oriented Programming）即面向对象编程，把编程看成是多个对象之间的交互，主要功能是继承、封装、多态
* Java实现AOP的方式：
  * 编译器：编译器把切面代码编译进字节码
  * 类加载器：在目标类被装在到JVM时，通过一个特殊的类加载器，对目标类的字节码重新“增强”
  * 运行期：基于JVM的动态代理实现，Spring就是使用该方式实现的切面编程

## 解释一下什么是 ioc？
* IOC（Inversion of Control）即控制反转，又称DI（Dependency Injection）即依赖注入，目的是将组件的创建&配置与组建的使用分离，spring当中使用极为广泛

## spring 有哪些主要模块？
### 什么是Spring bean
* bean时spring程序构成的基础之一，是被spring实例化、组装并由spring管理的java对象
* 默认情况下，spring中的bean都是以单利形式存在的

### spring中的主要模块
|模块名称|作用|
|---|---|
|Spring Core|框架基础部分，提供IOC功能实现和bean的创建、配置|
|Spring AOP|提供面向切面功能|
|Spring Context|是一个配置文件，向Spring框架提供上下文信息；<br />提供各种企业服务，比如JNDI、电子邮件、国际化、校验、调度等功能；<br />提供框架式bean访问方式，其他程序可以通过Context访问Spring的bean资源|
|Spring DAO|提供数据库相关的各种功能，对JDBC进行二次封装|
|Spring ORM（Object Relation Mapper）|Spring对多个ORM框架进行了封装，达成一致的编程风格，方便维护|
|Spring Web|Web层使用的Web框架式可选的，可以使用Spring的MVC，也可以使用Struts、Servlet等，该模块主要作用是管理web框架，方便使用web框架|
|Spring MVC|Spring提供的一个MVC方式实现的web应用服务器|

## spring 常用的注入方式有哪些？
### 相关名词解释
* DI（Dependency Injection）即依赖注入：当Spring创建被调用者的实例时，会自动将其注入调用者的实例中，这个就是依赖注入
* IOC（Inversion of Control）即控制反转：当一个java实例需要调用另一个java实例，且使用Spring框架的情况下，被调用者不再需要调用者来创建和配置，而是由Spring来完成，这就是控制反转
### 三种依赖注入方式
* setter注入：Spring会自行实现一个set+首字母大写+变变量名的方法，然后用反射调用该方法实现依赖注入
* 构造方法注入：通过在配置文件中标记好依赖关系，然后通过调用构造方法进行依赖注入
* 注解注入：Autowire，内部由三个constructor、byName、byType组成

## spring 中的 bean 是线程安全的吗？
* 结论：不安全

## spring 支持几种 bean 的作用域？
* singleton：单例，默认作用域，有线程安全问题，不过spring中大多是无状态单例bean，也是线程安全的，对于有状态的，可以使用ThreadLcal来解决线程安全问题
* prototype：原型，每次创建一个对象，线程之间没有共享，所以安全
* request: 请求，每次http请求一个对象，参考单例bean
* session：会话，每一个会话共享一个实例，不同会话使用不同实例，参考单例bean
* global-session：全局会话，所有会话共享一个实例，参考单例bean

## spring 自动装配 bean 有哪些方式？
### 自动装备定义
* Spring IOC容易将创建和配置好的bean赋值到需要调用这些bean的调用者

### 自动装备方式
* default：默认方式，与no相同
* no：不自动装配，会根据ref参数完成装配
* byName：根据名称进行装配
* byType：根据类型进行装配
* constructor：根据构造函数进行装配

## spring 事务实现方式有哪些？
### 什么是事务
* 事务即一组需要执行的操作，这些操作作为一个整体，要么全都成功，要么全都失败
* 特性：原子性（Atomiciy）、一致性（Consistency）、隔离性（Isolation）、持久性（Durability），简称ACID

### Spring事务实现方式
* 声明式事务：
  * 基于XML配置文件的方式
  * 基于注解（@Transaction）的方式
* 手动编码实现事务
