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

## 说一下 spring 的事务隔离？
### 事务隔离特性
|特性|特性描述|
|---|---|
|原子性|强调事务的不可分割|
|一致性|事务执行前后数据的完整性保持一致|
|隔离性|一个事务的执行不应受到其他事务的影响|
|持久性|事务执行结束，数据就持久化到数据库里|

### 事务隔离为了解决的问题
|要解决的问题|问题描述|
|---|---|
|脏读|表示一个事务能读取到另一个未提交的事务中的数据|
|幻读|一个事务由于另一个事务insert数据造成多次查询数据不一致|
|不可重复读|一个事务由于另一个事务update导致多次查到的记录不一致|

### spring事务隔离级别
|级别|级别描述|能否避免脏读|能否避免幻读|能否避免不可重复读|
|---|---|---|---|---|
|DEFAULT，默认|使用数据默认的隔离级别，mysql默认可重复读，oracle默认已提交读|mysql能，oracle能|mysql否，oracle否|mysql能，oracle否|
|READ UNCOMMITED 即未提交读|三种问题都有可能发生|否|否|否|
|READ COMMITED， 即已提交读|能避免脏读，但是不可重复读和幻读依然有可能发生|能|否|否|
|REPEATABLE READ， 即可重复读|可以避免脏读和不可重复读，但是幻读依然可以发生|能|否|能|
|SERIALIZABLE, 即串行化|避免所有问题|能|能|能|

## spring mvc 有哪些组件？
### 核心部分：
|组成部分|作用|对应类|
|---|---|---|
|Model|业务模型：处理业务请求|Handler|
|View|视图：渲染视图|实现类、jsp等|
|Controller|前段控制器：接收请求，响应结果|DispatcherServlet|

### 三大组件：
|组件名称|作用|
|---|---|
|HandlerMapping（处理器映射器）|将URL和处理器进行映射，可以根据URL找到对应的处理器|
|HandlerAdapter（处理器适配器）|适配并执行响应的处理器|
|ViewResolver（视图解析器）|根据视图名称，解析成一个视图对象|

## 说一下 spring mvc 运行流程？
* 前端发出请求，DispatcherServlet收到请求
* DispatcherServlet向HandlerMapping请求，获取到HandlerExecutionChan，该对象存储着处理器信息
* DispatcherServlet使用HandlerExecutionChan向HandlerAdapter请求，让其适配处理器并让处理器完成请求处理
* HandlerAdapter适配处理器，并告诉Handler完成请求处理
* Handler处理完成后，返回ModelAndView给HandlerAdapter，然后返回给DispatcherServlet
* DispatcherServlet使用ModelAndView向ViewResolve请求解析视图，ViewResolve返回视图对象
* DispatcherServlet使用视图对象向View请求其完成渲染，View将渲染好的视图返回给DispatcherServlet
* DispatcherServlet将响应返回给前端

## @RequestMapping 的作用是什么？
### 简介
* 作用：用来处理请求的映射
* 修饰对象：类、方法
* 特点：在类上使用时，表示所配置内容为该类中所有接口的父路径

### 包含属性
* value：指定请求地址
* method：指定请求类型，post或者get等
* consumes：指定请求内容处理类型（Content-Type）
* produces：指定返回的内容类型，请求方指定返回数据类型，返回数据类型与此项配置值相同时，参会返回成功
* params：指定请求地址中包含的参数
* headers：指定request中必须包含某些指定的header值，才允许请求

## @Autowired 的作用是什么？

* 作用：完成IOC或者ID的自动装配流程
* 修饰对象：类成员变量、方法、构造函数

# Soring boot
## 什么是spring boot？
|||
|---|---|
|是什么|一个框架|
|诞生目的|简化新spring应用的搭建以及开发过程|
|特点|使用了特定方式配置，使开发人员不再需要定义样板化的配置|

## 为什么要用 spring boot？或者说使用spring boot的优势
* 简化配置，不需要太多的xml配置文件
* 基于spring进行构建，是开发者快速入门，门槛低
* spring boot可以独立创建应用，不需要依赖各种web应用容器
* 内置tomcat，不需要打成jar包，可以直接在tomcat中运行
* 提供maven极简配置，以及可视化的各种监控功能
* 为微服务spring cloud提供了基础，是微服务构建变得很简单
* spring boot可以整合各种各样的框架，并可以很好地集成
* 活跃的社区论坛，以及丰富的开发文档

## spring boot 核心配置文件是什么？
* application.yml
* bootstrap.properties

## spring boot 配置文件有哪几种类型？它们有什么区别？
||application.yml|bootstrap.properties|
|---|---|---|
|加载方式|spring boot自动从classpath中加载|spring boot会自动从classspath中加载|
|文件内容格式|key：value|key=value|
|加载顺序|整体文件加载后于bootstrap，内部配置项加载也有先后顺序|先于application|
|可配置项功能|应用级别，是当前应用的配置文件|系统级别，用来加载外部配置，比如配置中心的配置信息|

## spring boot 有哪些方式可以实现热部署？
* 模板热部署
* 使用调试模式debug实现热部署
* spring-boot-devtools
* spring loaded
* JRebel
|热部署方式|部署方式|特点|
|---|---|---|
|模板热部署|在application或者bootstrap中关闭模板引擎的缓存即可||
|debug模式|运行时使用debug模式即可|1、最简单快速；<br/>2、无法对配置文件、方法名称改变、在增加类及方法进行热部署，使用范围有限|
|spring-boot-devtools|在spring boot中添加依赖即可实现，在pom.xml添加spring-boot-devtools依赖|1、作用范围广；<br/>2、使用重启策略实现，相当于手动帮你点了手动重启；<br/>3、默认关闭模板缓存|
|Spring Loaded|在run configuration中配置|1、与debug类似，作用范围有限；<br/>2、不依赖debug模式，正常情况下即可生效|
|JRebel|通过插件安装支持|1、收费；<br/>2、最好的java热部署工具|

## jpa 和 hibernate 有什么区别？
||JPA|Hibernate|Spring Data Jpa|
|---|---|---|---|
|简介|全称Java Persistence API，是一套ORM（对象关系映射）规范，可以理解为是一套接口|是JPA的一种实现|是对JPA和Hibernate进行了二次封装，将Spring与JPA进行更好的结合|

# Spring cloud
## 什么是 spring cloud？
|||
|---|---|
|简介|一系列框架的有序集合，提供了分布式系统开发的一站式解决方案|
|诞生目的|为开发者提供一套简单易懂、易部署、易维护的分布式系统开发工具包|
|特点|1、基于spring boot；<br/>2、没有重复造轮子，将各家成熟的、经得住考验的各种框架结合|


## spring cloud 断路器的作用是什么？
* 当某个服务单元发生故障后，通过断路器的监控，向调用方返回一个错误响应，而不是长时间的等待，避免线程因服务故障长时间占用资源不释放，避免故障蔓延

## spring cloud 的核心组件有哪些？
|组件|简介|
|---|---|
|Eureka|微服务注册管理中心|
|Ribbon|客户端负载均衡|
|Hystrix|断路器，用来处理服务故障|
|Fegin|用于简化微服务之间的调用|
|Zuul|网关，一系列的过滤器|


----
## 为什么要使用spring
|||
|---|---|
|综述|省去很多非业务层代码研发的工作，提升javaweb服务研发效率，降低研发难度|
|详解|1、spring非常轻量且非侵入式，耦合低，污染小<br/>2、通过非常方便的依赖注入以及面向接口编程，可以实现业务代码之间的松耦合<br/>3、支持面向切面编程，可以非常方便的剥离不同层面的逻辑之间的依赖<br/>4、整体配置量少且简单|


## 什么是aop
|||
|---|---|
|aop简介|Aspect-Oriented Programming，面向切面编程，把一个流程里面的日志打印、安全检查等部分流程看成是一个切面，即面向一个流程中的某一部分进行编程|

## 什么是ioc
|||
|---|---|
|ioc简介|Inversion of Control，控制反转，也成依赖注入，目的是将组件的创建与配置自动化并且与使用进行分离|

## spring有哪些主要模块
|模块名称|模块作用|
|---|---|
|core|框架基础部分，提供ioc实现及bean的配置、管理|
|context|提供上下文信息以及很多企业级功能，比如邮件等|
|dao|JDBC的抽象层，与数据库交互部分，避免与业务代码耦合|
|orm|映射模块，比如mybatis等|
|aop|提供aop开发能力|
|web|提供对其他框架的支持与管理功能|
|MVC|提供了一套MVC开发框架规范|

## spring常用的注入方式
1、构造方法注入
2、setter方法注入
3、注解注入

## spring中的bean是线程安全的吗
不是，spring不会保证bean线程安全

## spring支持的bean的作用域
1、单例
2、普通属性
3、一次请求
4、一次会话
5、全局会话

## spring自动装配bean有哪些方式
|方式|简介|
|---|---|
|隐式的bean发现机制和自动装配|XML中配置依赖关系，同时代码中需要实现相关的setter、getter方法接口|
|xml中显示配置|1、default<br/>2、no<br/>3、byType<br/>4、byName<br/>5、constructor|
|java代码中配置|@Autowired|
