---
title: javaWeb
date: 2022-03-28 16:25:19
tags: Q&A
categories:
- [Q&A, Q&A-java]
---

## JSP、servlet区别
||JSP|servlet|
|---|---|---|
|简介|一种动态网页技术标准|一种网络服务技术标准|
|核心区别|偏向view层的交互|偏向逻辑层操作|
|实现区别|本质上就是servlet，编译时会转化成servlet，本质上是对servlet的简化|java类|
|其他区别|有内置对象|全是java类，无内置对象|

## JSP、Servlet、Tomcat、Structs、Apache、Nginx、正向代理、反向代理是什么
|技术|简介|意义|
|---|---|---|
|Servlet|Java官方出品的一套JAVA HTTP web server 规范、工具|指定HTTP WEB SERVER规范、降低程序员非业务层代码工作量|
|JSP|java web server, 本质是servlet, 集合了html，更适合动态网页网络应用服务|在需要进行网页交互的网络应用中提供解决方案|
|Tomcat|集合了servlet、jsp、java websocket的java web server，同时提供可视化配置功能|提供更强大、易用的java web server解决方案|
|Structs|基于servlet，增加model、view、controller层的一套java web server解决方案|提供一套规范化的MVC设计模式的java web server 解决方案|
|Apache|一个HTTP web server解决方案|Apache官方提供的一套http web server解决方案|
|Nginx|http web server解决方案，适合高并发场景|适合高并发场景的http web server解决方案|
|正向代理、反向代理|正向代理就是client被代理，反向代理就是server被代理|

## JSP有哪些内置对象，作用是什么
|对象|作用|
|---|---|
|request|client请求信息|
|response|server响应信息|
|pageContent|页面上下文|
|session|clent与server之间的会话|
|application|server声明周期|
|out|server给client传输内容的输出流|
|config|初始化时，jsp引擎向jsp页面传递的信息|
|page|jsp页面本身|
|exception|页面异常对象|

## jsp的四种作用域
|作用域|简介|对应操作类|
|---|---|---|
|application|整个服务的声明周期期间|ServletContext|
|session|http会话开始到结束|session|
|request|http请求到结束|request|
|page|页面打开到关闭|pageContext|

## session、cookie区别
||session|cookie|
|---|---|---|
|存在位置|server|client|
|容量|较大|较小|
|安全性|较好|较差|
|简述|二者分别存放在client和server上，用来操作数据，二者配合可以完成用户校验，用户登录有效期、用户状态记录等功能，cookie相当于是server存在client上的一部分数据|

## session工作原理
当前使用的session本质就是一个map，可以根据我们的需求来定制内部的数据，可以暂存或者持久化等等都可以，主要就是用来记录数据使用

## 客户端禁止cookie，session还能用吗
按照jsp当中cookie与session的设计来说，是不能用了，session当中的sessionId依赖cookie，cookie没了，就找不到对应session了，但是者本身就是一中实现方案而已，我们可以设计其他的方案来替代，比如在url中拼接sessionId

## Spring mvc 、Struts区别
||Spring mvc|Structs|
|---|---|---|
|简介|都是web server MVC模式下的开发框架|
|机制|面向方法实现|面向类实现|
|性能|较好|较差|
|单例、多例|建议单例|无法单例|
|入口|servlet|Filter|
|配置量|基本没有什么配置|需要进行较多配置|
|方法|方法之间比较独立|方法之间共享成员变量|
|内存占用|较省|较费|
|设计思想|AOP，过程中加入自己的操作|OOP，拦截后自己来|

## 避免sql注入
1、过滤输入内容，校验字符串
2、参数化查询
3、安全测试、安全审计（Code Review）
4、避免使用动态sql
5、数据库重要数据加密
6、数据库权限控制
7、避免数据库直接与用户交互

## 什么是xss共计，如何避免
|||
|---|---|
|定义|使用html攻击web应用|
|避免策略|1、对输入输出进行过滤、转义处理<br/>2、校验html标签|

## 什么是CSRF攻击，如何避免
|||
|---|---|
|定义|盗用某用户信息，发送恶意请求|
|避免策略|1、阻止不明外域访问，比如校验请求地址<br/>2、关键操作添加验证码<br/>3、增加cookie、token验证策略|
