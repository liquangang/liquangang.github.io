---
title: MyBatis
date: 2022-04-27 15:25:07
tags: Q&A
categories:
- [Q&A, Q&A-java]
---

## mybatis 中 #{}和 ${}的区别是什么？
||#{}|${}|
|---|---|---|
|作用|预处理|字符串替换|
|处理流程|Mybatis会先将#{}替换成？，然后调用PreparedStatement中的set方法来赋值|将${}替换成变量的值|
|特点|可以有效防止sql注入，提高系统安全性||

## mybatis 有几种分页方式？
1、数组分页
2、sql分页
3、拦截器分页
4、RowBounds分页

## mybatis 逻辑分页和物理分页的区别是什么？
||逻辑分页|物理分页|
|---|---|---|
|实现位置|主要靠代码来分页，从表中读取全量数据，用代码分页，依赖于代码实现|直接使用可以分页的sql语句完成，依赖于sql语句实现|
|访问数据库次数|访问一次即可完成分页|没获取一页数据都需要访问数据库|
|资源占用|内存占用大|数据库压力大|
|速度|不一定谁快|
|实时性|只读取一次，读取之后的变化无法提现|实时读取一页，实时性高|
|如何选择|逻辑分页速度上优势，但是物理分页在其他方面的优势更明显，建议物理分页|

## mybatis 是否支持延迟加载？延迟加载的原理是什么？
* 仅支持association对象（查询结果中包含一对一类型，比如人员包含身份证信息这种）和collection对象（查询结果中包含一对多类型，比如人员的房子这个，一个人可能有多套房子）
* 打开方式：在配置文件中配置lazyLoadingEnabled=true|false
* 懒加载原理：在get方法中判断对象为空时，去构造

## 说一下 mybatis 的一级缓存和二级缓存？
||一级缓存|二级缓存|
|---|---|---|
|简介|基于PerpetualCache的HashMap本地缓存|基于PerpetualCache的HashMap实现，也可以使用外部存储资源，比如Ehcache，redis|
|存储作用域|作用域session，当session flush或者close之后，该session中的cache就会清空|Mapper（namSpace）|
|默认状态|默认代开|默认不打开|

## mybatis 和 hibernate 的区别有哪些？
||mybatis|Hibernate|
|---|---|---|
|相同点|都是ORM（对象关系映射）框架|
|是否需要开发者编写sql语句|需要，半自动框架|不需要，全自动框架|
|适合场景|直接编写原生sql，灵活度高，可以更好的控制sql执行性能，适合对关系数据库模型要求不高、需求变化频繁的软件开发|Hibernate对象/关系映射能力强，数据库无关性好，对于关系模型要求高的软件，可以使用Hibernate，可以节省很多代码，提高效率|

## mybatis 有哪些执行器（Executor）？
|执行器|简介|
|---|---|
|SimpleExecutor|每执行一次update或者select，就产生一个statement对象，用完立即销毁|
|ReuseExecutor|有一个重复使用Map，key时sql，value是可以重复使用的statement，存在就使用，不存在才会创建|
|BatchExecutor|会缓存多个statement对象，然后统一执行，批处理不支持select，原因是JDBC不支持批处理select|

## mybatis 分页插件的实现原理是什么
* 简介：使用mybatis提供的插件接口，通过自定义插件实现分页
* 具体流程：在插件的拦截方法内拦截sql，对sql进行修改，根据dialect添加对应的物理分页参数和物理分页语句

## mybatis 如何编写一个自定义插件？
### 自定义原理
通过对mybatis的四大对象拦截来实现

### Mybatis的四大对象介绍
|对象名称|流程|
|---|---|
|Executor|执行器，主要是log记录|
|StatementHandler|sql语法构建|
|ParameterHandler|参数处理|
|ResultSetHandler|结果集处理|

### 具体实现过程
#### 需要实现Mybatis的Interceptor接口
```
public interface Interceptor {
    Object intercept(Invocation invocation) throws Throwable; // 拦截器具体处理逻辑方法
    Object plugin(Object target); // 根据签名signatureMap生成动态代理对象
    void setProperties(Properties properties); // 设置Properties属性
}
```

#### 一个@Interceptor可以配置多个@Signature，@Signature内部参数含义如下：
|参数名称|参数作用|
|---|---|
|type|表示拦截类，是Executor还是其他三个|
|method|表示拦截方法|
|args|表示方法参数|

#### 代码演示：
```
@Intercepts({@Signature(
  type= Executor.class,
  method = "update",
  args = {MappedStatement.class,Object.class})})
public class ExamplePlugin implements Interceptor {
  public Object intercept(Invocation invocation) throws Throwable {
  Object target = invocation.getTarget(); //被代理对象
  Method method = invocation.getMethod(); //代理方法
  Object[] args = invocation.getArgs(); //方法参数
  // do something ...... 方法拦截前执行代码块
  Object result = invocation.proceed();
  // do something .......方法拦截后执行代码块
  return result;
  }
  public Object plugin(Object target) {
    return Plugin.wrap(target, this);
  }
  public void setProperties(Properties properties) {
  }
}
```
