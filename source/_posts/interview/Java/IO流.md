---
title: IO流
date: 2021-11-29 15:35:40
tags: 面试
categories:
- [interview, interview-java]
---

## IO流特点
* 最基础的是字节
* 单向
* 顺序读写
* 由InputStream、Writer、OutputStream、Reader四个基类为基础组成，Writer实际上是自带解码的OutputStream，Reader实际上是自带编码的OutputStream

## IO流分类
### 按数据流向分（以内存为基准）：
  * 输入流：InputStream、Reader，即从其他位置输入到内存
  * 输出流：OutputStream、Writer，即从内存输出给其他设备

### 按数据类型分：
  * 字节流
  * 字符流

### 按角色分：
  * 节点流：可以从/向一个IO设备读/写数据的流，也称为低级流、主要流
  * 高级流：用于对一个已存在的流进行连接和封装，通过封装后的流来实现数据的读/写

### 按功能分：
  * 缓冲流：对应Buffer开头的那部分缓冲流泪，作用是增加一层缓冲，提高读写速度
  * 转换流：对应InputStreamReader、OutputStreamWriter，作用是对字符和字节进行转换
  * 序列化流：对应ObjectOutputStream、ObjectInputStream，作用是将一个对象序列化成文件，将序列化文件反序列化成对象
  * 打印流：对应PrintStream、PrintWriter，作用是打印各种东西


## IO流现有类
### 按数据类型分：
* 字节流：可用于任何类型的数据
  * InputStream（从其他位置输入内存）
    * FileInputStream
    * FilterInputStram
      * BufferedInputStream
      * DataInputStream
      * PushbackInputStream
    * ObjectInputStream
    * PipedInputStream
    * ByteArrayInputStream
  * OutputStream（从内存输出到其他位置）
    * FileOutputStream
    * FilterOutputStream
      * BufferedOutputSteam
      * DataOutputStream
      * PrintStream
    * ObjectOutputStream
    * PipedOutputStream
    * ByteArrayOutputStream


* 字符流：只能处理字符或字符串
  * Writer（从内存中把数据写入到其他位置）
    * BufferedWriter
    * StringWriter
    * PipedWriter
    * CharArrayWriter
    * FilterWriter
    * OutputStreamWriter
      * FileWriter
    * PrintWriter
  * Reader（从其他位置把数据读到内存）
    * BufferedReader
    * StringReader
    * PipedReader
    * CharArrayReader
    * FilterReader
      * PushbackReader
    * InputStreamReader
      * FileReader

### 按功能分：
* 处理流：
  * 缓冲操作类
    * BufferedInputStream
    * BufferedOutputSteam
    * BufferedWriter
    * BufferedReader
  * 基本数据类型操作类
    * DataInputStream
    * DataOutputStream
  * 对象序列化操作类
    * ObjectInputStream
    * ObjectOutputStream
  * 转换操作类
    * InputStreamReader
    * OutputStreamWriter
  * 打印操作类
    * PrintStream
    * PrintWriter

* 节点流
  * 文件操作类
    * FileInputStream
    * FileOutputStream
    * FileReader
    * FileWriter
  * 管道操作类
    * PipedInputStream
    * PipedOutputStream
    * PipedReader
    * PipedWriter
  * 数组操作类
    * ByteArrayInputStream
    * ByteArrayOutputStream
    * CharArrayReader
    * CharArrayWriter
