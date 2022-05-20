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

## String属于基础数据类型吗？
不属于，string是引用类型，是对象，基础数据类型是byte、boolean、char、short、int、long、float、double

## java中操作字符串的类，它们的区别
||String|StringBuffer|StringBuilder|
|---|---|---|---|
|是否可变|不可变|可变|可变|
|线程安全|安全|安全|不安全|
|性能|高|较低|较高|
|使用场景|使用字符串常量时|多线程编辑字符串|单线程编辑字符串|

## String str = "i" 和String str = new String("i") 一样吗？
不一样，String str = "i" str指向的是常量池中的某块内存，String str = new String("i") 中的str指向的堆内存的某块区域

## 字符串反转
1、倒序遍历向另一个字符串中写
2、使用StringBuffer和StringBuilder中的reverse方法

## String类常用方法
|常用方法|作用|
|indexOf()|返回指定字符索引|
|charAt()|返回指定索引处字符|
|replace()|替换字符串|
|trim()|去除字符串两端空白|
|split()|分割字符串|
|getBytes()|返回字符数组|
|length()|字符串长度|
|toLowerCase()|转换小写字母|
|toUpperCase()|转换大写字母|
|subString()|截取字符串|
|equals()|判断字符串内容是否相同|
