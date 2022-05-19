---
title: Java基础
date: 2022-05-19 20:24:10
tags: Q&A
categories:
- [Q&A, Q&A-java]
---
## JDK、JRE区别
||JDK|JRE|
|---|---|---|
|全称|Java Developer Kit：Java开发工具包|Java Runtime Environment：Java运行时环境|
|作用|提供Java开发环境，开发工具，用于开发java程序|提供java运行环境，用于运行java程序|
|联系|JDK包含JRE|

## == 和 equals 区别
||==|equals|
|---|---|---|
|作用|1、判断基本数据类型值是否相等<br/>2、判断引用类型引用是否相同|1、与==相同，判断基本数据类型值是否相等<br/>2、如果引用类型数据对应的类或者父类重写了equals方法，就执行重写的equals方法，否则与==相同，即判断引用是否相同|
|相同点|基本数据类型使用时都是判断值是否相等|
|不同点|引用类型==是判断引用是否相同，如果引用类型对应的类或者父类重写了equals方法，那么执行重写的equals，否则与==相同|

## hashcode相等，equals一定为true吗
不一定，不同字符串的hashcode存在相等情况，但equals是false

## final作用
|||
|---|---|
|类|不能被继承|
|方法|不能被重写|
|变量|必须初始化，之后不能修改，基本数据类型会变成常量，引用类型引用不能变，但引用对象属性可以变|

## Math.round(-1.5) 结果
* Math.round()作用是四舍五入取整，所以结果-1
