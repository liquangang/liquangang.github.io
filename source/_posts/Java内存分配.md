---
title: Java内存分配
date: 2021-08-31 11:14:46
tags: 编程
categories:
- [Java, Java基础]
---

### 内存区域、内存模型
* 内存区域：即运行时数据区域，指JVM对于不同类型数据在内存中的存储方式
* 内存模型（JMM：Java Memory Model）：定义了线程与主内存之间的抽象关系，即JVM在内存中的工作方式，即JVM使用内存区域中的数据的方式

### JDK8之后的内存区域：
```
* Native Method Stacks（本地方法栈）
* Program Counter Register（程序计数器）
* JVM Stacks（虚拟机栈）
    * 栈帧1（方法A）
        * 局部变量表
        * 操作栈
        * 动态连接
        * 方法返回地址
    * 栈帧2（方法B）
        * 局部变量表
        * 操作栈
        * 动态连接
        * 方法返回地址
* Heap（堆区）
    * Young区（新生代）
        * Eden
        * S0
        * S1
    * Old区（老年代）
* Metaspace（元数据区）
    * 常量池
    * 方法元信息
    * klass类元信息
* CodeCache（JIT编译产物） 
```

### 程序计数器
* 作用：当前线程所执行的字节码的行号指示器，当多线程切换时，使线程恢复后找到正确的执行位置
* 特点：
    * 内存占用少
    * 每个线程有自己的计数器，线程私有
    * 当前线程执行Java方法，计数器保存虚拟机中字节码指令地址；执行Native方法，记录null
    * 唯一一个在JVM规范中没有规定OutOfMemoryError的区域