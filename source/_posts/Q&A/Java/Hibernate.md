---
title: Hibernate
date: 2022-04-24 17:53:12
tags: Q&A
categories:
- [Q&A, Q&A-java]
---

## 为什么要使用 hibernate？使用Hibernate的优势
1、对JDBC访问数据代码做了封装，大大简化了数据库访问层的重复性代码；
2、Hibernate是一个基于JDBC的主流持久化框架，是一个优秀的ORM实现，很大程度上简化了DAO层的编码工作；
3、Hibernate基于Java的反射机制，而不是字节码增强称必须来实现透明性；
4、Hiroshima性能非常好，因为他是个轻量级框架，映射灵活性出色，支持各种关系数据库，支持一对一到一对多的复杂关系


## 什么是 ORM 框架？
### 简介
ORM（Object Relation Mapper）即对象关系映射，是为了解决面向对象与关系型数据库存在的互不匹配的技术框架，它通过描述java对象与数据库表之间的关系，自动将java应用中的对象持久化到关系型数据库中，在java对象与数据库表之间建立一座桥梁，这个桥梁就是映射关系

### 主流ORM框架
|框架名称|简介|
|---|---|
|MyBatis|一个半自动映射框架，互联网目前比较流行|
|Hibernate|全自动映射框架|


## hibernate 中如何在控制台查看打印的 sql 语句？
* 方式1（在properties中添加配置项）：
```
spring.jpa.properties.hibernate.show_sql=true // 控制台是否打印
spring.jpa.properties.hibernate.format_sql=true // 格式化sql语句
spring.jps.properties.hibernate.use_sql_comments=true // 指出是什么操作生成了该语句
```
* 方式2（在yml文件中修改配置项）
```
spring:
  jpa:
    properties:
      format_sql: true // 格式化sql语句
      show_sql: true // 控制台是否打印
      use_sql_comments: true // 指出是什么操作生成了该语句
```


## hibernate 有几种查询方式？
|查询方式|简介|
|---|---|
|HQL|Hibernate Query language，Hibernate官方推荐查询方式，语法结构上与sql类似，使用Hibernate中的Query对象执行HQl操作|
|QBC|Query By Criteria，Criteria对象提供了一种面向对象式的查询方式，Criteria需要使用sessio对象获得|
|SQL|即原生SQL语句方式查询|

## hibernate 实体类可以被定义为 final 吗？
* 可以声明为final类
* 缺点：java不允许在final类中使用代理，所以Hibernate使用代理模式在延迟关联情况下提高性能的手段就会失效，所以该做法不建议采用
* 补救方式：将所有public方法在一个接口中声明，并让该final类实现该接口

## 在 hibernate 中使用 Integer 和 int 做映射有什么区别？
* 使用Integer的情况下，Hibernate可以根据Integer是否为null而判断是否是临时对象
* 使用int，需要在hbm映射文件中声明unsaved-value=0

## hibernate 是如何工作的？
1、读取并解析配置文件
2、读取并解析映射信息
3、创建SessionFactory
4、打开session
5、创建并启动事务Transation
6、操作数据，进行持久化操作
7、提交事务
8、关闭session
9、关闭sessionFactory

## get()和 load()的区别？
* get：生成sql，立即加载，有直接返回对象，没有返回null
* load：不生成sql，延迟加载，会有个代理返回一个id，如果直接使用对象的具体属性的时候，会返回对象不存在的异常

## 说一下 hibernate 的缓存机制？
### Hibernate分为一级缓存和二级缓存
||一级缓存|二级缓存|
|---|---|---|
|有效范围|事务范围内|从应用启动到结束|
|级别|session级别|sessionFactory级别|
|开启关闭|内置，无法卸载或关闭|可选，手动开启，默认不开启|

### 重点关注
* 缓存在内存中保存了一份，更新完数据库后要同步更新
* Hibernate的二级缓存时不支持分布式缓存的，需要使用cache、redis等中央缓存来替代

### 适合放到二级缓存中的数据
* 很少被修改的数据
* 经常被查询的数据
* 不是很重要的数据
* 不会被并发访问的数据
* 常量数据

## hibernate 对象有哪些状态？
||Transient（瞬时）|Persistent（持久）|Detached（托管）|
|---|---|---|---|
|产生状态|对象刚new出来，还没id，设了其他值|调用了save、saveOrUpdate，有id|当session close之后|


## 在Hibernate中getCurrentSession和openSession的区别是什么
||getCurrentSession|openSession|
|---|---|---|
|获取session是否是同一个|是|不是|
|特点|没有会创建|每次都会新建，使用完需要执行close操作|

## Hibernate实体类必须有无参构造函数吗？为什么
* 必须，Hibernate框架会调用无参构造函数创建实例对象
* 如果不提供任何构造函数，虚拟机会自动提供无参构造函数，如果提供了有参构造函数，此时必须手动提供无参构造函数，否则会报错
