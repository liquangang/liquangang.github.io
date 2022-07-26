---
title: Hibernate
date: 2022-04-24 17:53:12
tags: Q&A
categories:
- [Q&A, Q&A-java]
---

## 为什么要使用hibernate
1、对JDBC访问数据库流程进行了封装，简化了访问流程
2、是一个优秀的ORM框架，简化了DAO层的编码工作
3、hibernate使用反射机制，而不是字节码来增强程序透明性
4、hibernate性能好，本身是个轻量级框架，映射灵活性好，支持各种关系数据库，支持一对一到多对多的复杂关系

## 什么是ORM框架
ORM全称Object-Relational Mapping，即将代码中的model与关系数据库中的数据建立起映射

## hibernate如何在控制台查看打印的sql语句
1、properties文件中配置
2、yml文件中配置

## hibernate有几种查询方式
|查询方式|简介|
|---|---|
|HQL|hibernate官方推荐，使用query对象进行查询|
|QBC|使用Criteria对象查询|
|SQL|原生sql|

## hibernate实体类可以被定义为final吗
|||
|---|---|
|是否可以被定义成final|可以|
|是否建议定义成final|不建议，hibernate会使用代理提升性能，使用final之后代理就无法实现了|
|如何补救|将所有public方法放到一个接口中，final类再实现这个接口即可|

## hibernate中Integer、int映射有什么区别
||Interger|int|
|---|---|---|
|是否可以为null|可以|不可以|
|使用区别|hibernate本身是面向对象框架，更建议使用对象|使用int需要进行一些特殊配置|

## hibernate是如何工作的
1、读取并解析配置文件
2、读取并解析映射文件
3、创建SessionFactory
4、打开session
5、创建并启动事务Transation
6、操作数据，进行持久化操作
7、提交事务
8、关闭session
9、关闭SessionFactory

## get()、load()区别
||get()|load()|
|---|---|---|
|是否生成sql|生成|不生成|
|是否立即记载|立即加载|延迟加载|
|返回内容|有直接返回，没有返回null|会返回一个代理id|
|异常|内部未定义异常|会返回属性不存在异常|

## hibernate的缓存机制
||一级缓存|二级缓存|
|---|---|---|
|有效范围|事务范围内|应用生命周期|
|级别|session|sessionFactory|
|开启|自动，无法卸载或关闭|手动，默认不开启|
|其他特点||不支持分布式存储，需要的话需要使用其他方案，比如redis等|

## hibernate对象有哪些状态
|状态|产生情况|
|---|---|
|瞬时|刚new出来，还没id，与session无关联|
|持久|有id，与session有关联|
|脱管|无id，session close之后，与session无关联|

## hibernate getCurrentSession、openSession区别
||getCurrentSession|openSession|
|---|---|---|
|获取的是否是同一个session|是|不是|
|特点|获取的是同一个session，没有会创建|每次新建session，需要手动关闭|

## hibernate实体类必须要有无参构造函数吗，为什么
|||
|---|---|
|是否必须有无参构造函数|必须，因为hibernate使用无参构造函数创建对象|
|特殊说明|如果没有写任何构造函数的情况下，默认是有无参构造函数的，如果写了构造函数就必须提供无参构函数|
