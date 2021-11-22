---
title: 双等号、equals、hashCode区别
date: 2021-11-22 22:47:01
tags: 面试
categories:
- [interview, interview-java]
---

## 参考资料
* [参考文章1](https://www.jianshu.com/p/5a7f5f786b75)

## ==：判断的是两个变量对应的内存中的值是否相等
* 基本数据类型比较值
* 引用类型比较内存地址

## equals：不重写时与"=="功能一致，其在Object方法列表中，可重写该方法
* 特点：
    * 重写需要遵循java对该方法重写的规范（对称性、反射性、类推性、一致性、非空性）
    * 未重写时与"=="功能一致
    * 当某个类要在散列表中使用时，重写该方法的同时必须重写hashCode方法，否则该方法无效
    
## HashCode：获取哈希码（散列码，为了提升散列表查找性能），该哈希码作用是确定该对象在哈希表中索引位置
* 特点：
    * 该方法在Object的方法，所以所有类都继承该方法
    * 该方法只在该对象被散列表（例如HashMap、HaskTable、HashSet）所使用时，才会使用到该方法，其他情况下没用
    * 该方法可以通过重写进行自定义
    * 当同时使用到该方法和equals时，hashcode相等，但equals不一定相等，但equals相等，hashcode一定相等