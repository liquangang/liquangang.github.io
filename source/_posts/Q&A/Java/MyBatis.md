---
title: MyBatis
date: 2022-04-27 15:25:07
tags: Q&A
categories:
- [Q&A, Q&A-java]
---

## Mybatis中#{}、${}区别
||#{}|${}|
|---|---|---|
|作用|预处理|字符串替换|
|内部流程|先将#{}替换成？，然后调用PreparedStatement的set方法复制|将${}替换成变量的值|
|特点|防止sql注入，提升系统安全性|

## MyBatis有几种分页方式
1、数组分页
2、sql分页
3、拦截器分页
4、RowBounds分页

## Mybatis逻辑分页、物理分页区别
||逻辑分页|物理分页|
|---|---|---|
|实现|全量读取，代码分页|sql语句包含读取和分页操作|
|访问次数|读取一次即可获得所有分页|获取每页数据都需要读取数据库|
|资源占用|内存压力大|数据库压力大|
|速度|伯仲之间|
|实时性|较差，只读取一次|实时读取，实时性高|
|如何选择|默认建议使用物理分页，如果需要一次性获取所有分页，可以使用逻辑分页|

## Mybatis是否支持延迟加载，延迟加载原理是什么
|||
|---|---|
|是否支持|部分支持，仅支持association对象（一对一，比如人员身份信息）和collection对象（一对多，人员拥有的房产）|
|打开懒加载功能|配置文件中配置即可|
|懒加载原理|get时判断对象为null，就创建对象|

## Mybatis的一级、二级缓存
||一级缓存|二级缓存|
|---|---|---|
|实现|基于hashmap|基于hashmap，也可以使用其他存储源，比如redis|
|作用域|session|Mapper（nameSpace）|
|默认是否开启|默认开启|默认不开启，使用二级缓存的属性类需要实现序列化接口|

## Mybatis、hibernate区别
||Mybatis|hibernate|
|---|---|---|
|相同点|都是ORM框架|
|是否需要开发者编写sql|需要，半自动框架|不需要，全自动框架|
|适合场景|适合关系数据模型较弱，场景灵活程度高，需求变动大，频繁更改sql的场景|适合关系数据模型强，数据库无关性好的场景|

## Mybatis有哪些执行器
|执行器|简介|
|---|---|
|SimpleExecutor|每执行一次update、select，就生成一个statement，用完销毁|
|ReuseExecutor|会重复使用statement，会将statement保存到map中，key是sql语句，不存在就创建statement|
|BatchExecutor|缓存多个statement，并统一执行，不支持select，因为jdbc不支持批处理select|

## Mybatis分页插件实现原理
通过自定义插件实现分页，具体是在拦截到sql语句后，添加分页语句实现

## 如何编写一个自定义插件
### 一个@Interceptor可以配置多个@Signature，@Signature内部参数含义如下：
|参数名称|参数作用|
|---|---|
|type|表示拦截类，是Executor还是其他三个|
|method|表示拦截方法|
|args|表示方法参数|

### 代码演示：
```
@Intercepts({@Signature(
  type= Executor.class,
  method = "update",
  args = {MappedStatement.class,Object.class})})
public class ExamplePlugin implements Interceptor {

  // 拦截器具体处理逻辑方法
  public Object intercept(Invocation invocation) throws Throwable {
  Object target = invocation.getTarget(); //被代理对象
  Method method = invocation.getMethod(); //代理方法
  Object[] args = invocation.getArgs(); //方法参数
  // do something ...... 方法拦截前执行代码块
  Object result = invocation.proceed();
  // do something .......方法拦截后执行代码块
  return result;
  }

  // 根据签名signatureMap生成动态代理对象
  public Object plugin(Object target) {
    return Plugin.wrap(target, this);
  }

  // 设置Properties属性
  public void setProperties(Properties properties) {
  }
}
```
