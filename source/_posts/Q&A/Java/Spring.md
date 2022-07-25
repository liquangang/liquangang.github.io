---
title: Spring
date: 2022-04-18 19:31:33
tags: Q&A
categories:
- [Q&A, Q&A-java]
---

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

## spring事务的实现方式
|||
|---|---|
|事务定义|一组操作，这些操作作为一个整体，要么全都执行成功，要么全都执行失败|
|实现方式|1、手动编码实现，手动调用beginTransaction()、commit()、rollback()等方法<br/>2、通过@transcationnal实现|

## 说一下spring事务隔离
|||
|---|---|
|事务隔离意义|解决事务同时执行过程中出现的脏读、幻读、不可重复读问题|
|多个事务同时执行会出现的问题|1、脏读：一个事务可以读取到另一个事务未提交的数据<br/>2、一个事务由于另一个事务同时执行insert操作造成多次查询结果不一致问题<br/>3、不可重复读：一个事务多次查询到的同一条数据由于另一个事务的update操作导致不一致|
|事务隔离特性|1、原子性<br/>2、一致性<br/>3、隔离性<br/>4、持久性|

## spring mvc执行流程
1、前端发起请求，DispatcherServlet收到请求
2、DispatcherServlet向HandlerMapping请求获得HandlerExecutionChan(包含处理器信息)
3、DispatcherServlet使用HandlerExecutionChan向HandleAdapter发请求
4、HandlerAdapter向Handler发请求
5、Handler响应请求，生成ModelAndView，返回给DispatcherServlet
6、DispatcherServlet使用ModelAndView向ViewResolve发请求，ViewResolve返回view
7、DispatcherServlet将view渲染成最终的视图并完成对前端的响应

## spring mvc有哪些组件
|组件|简介|
|---|---|
|DispatcherServlet|中央控制器，串整个流程|
|Controller|处理器，具体处理请求的部分|
|HandlerMapping|映射处理器，让DispatcherServlet找到属于自己的Controller|
|ModelAndView|Controller处理结果|
|ViewResolver|视图解析器，解析ModelAndView|
|Interceptors|拦截器，负责拦截配置好的请求|

## @RequestMapping作用
一个用来处理请求的注解，参数可配置请求地址、请求方法、请求参数等

## @Autowired作用
注入依赖

## 什么是spring boot
一个为了简化spring应用的配置及开发过程的框架

## 为什么要使用spring boot
1、配置简单
2、依然基于spring构建应用，学习成本低
3、可以独立构建应用，不需要依赖web应用容器
4、内置tomcat，不需要jar包，即可在tomcat中运行
5、提供maven极简配置以及各种可视化监控功能
6、给spring cloud提供支持，降低微服务构建难度
7、spring boot可以整合各种框架
8、社区活跃

## spring boot的核心配置文件是什么
1、application.yml
2、bootstrap.properties

## spring boot有哪几种配置文件，区别是什么
||application.yml|bootstrap.properties|
|---|---|---|
|加载方式|从classpath中读取|
|加载顺序|先加载bootstrap.properties(系统配置)，再加载application.yml(应用配置)|
|文件内容格式|key：value|key=value|
|配置内容范围|应用配置|系统配置|

## spring boot有哪些方式可以实现热部署
1、模板热部署
2、debug
3、spring-boot-devtools
4、spring loaded
5、JRebal

## jpa、hibernate区别
||jpa|hibernate|
|---|---|---|
|区别|java制定的一套ORM接口，也是一种规范|jpa接口的具体实现|

## spring cloud是什么
|||
|---|---|
|简介|一系列框架的有序集合，目的是为分布式系统的构建提供支持|
|特点|基于spring boot，整合了许多经典框架、库等资源，没有重复造轮子|

## spring cloud 断路器作用
|||
|---|---|
|作用|避免故障蔓延|
|实现|当某个故障节点被调用时，断路器会立马返回一个错误，使调用方尽快释放资源|

## spring cloud 核心组件
|组件|作用|
|---|---|
|Eureka|服务发现|
|Ribbon|负载均衡|
|Hystrix|断路器|
|Feign|服务间调用|
|Zuul|网关|
