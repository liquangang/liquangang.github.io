---
title: IO流
date: 2021-11-29 15:35:40
tags: 面试
categories:
- [interview, interview-java]
---

## IO流最基础的是字节

## IO流分类
* 按数据流向分（以内存为基准）：
  * 输入流：InputStream、Writer，即从其他设备写入内存
  * 输出流：OutputStream、Reader，即从内存读取给其他设备


* 按数据类型分：
  * 字节流
  * 字符流

## IO流相关类
### 字节流：可用于任何类型的数据
* InputStream（从其他设备写入内存）
  * FileInputStream
  * FilterInputStram
    * BufferedInputStream
    * DataInputStream
    * PushbackInputStream
  * ObjectInputStream
  * PipedInputStream
  * ByteArrayInputStream
* OutputStream（从内存写入到其他位置）
  * FileOutputStream
  * FilterOutputStream
    * BufferedOutputSteam
    * DataOutputStream
    * PrintStream
  * ObjectOutputStream
  * PipedOutputStream
  * ByteArrayOutputStream

### 字符流：只能处理字符或字符串
* Writer（从其他设备写入内存）
  * BufferedWriter
  * StringWriter
  * PipedWriter
  * CharArrayWriter
  * FilterWriter
  * OutputStreamWriter
    * FileWriter
  * PrintWriter
* Reader（从内存写入到其他位置）
  * BufferedReader
  * StringReader
  * PipedReader
  * CharArrayReader
  * FilterReader
    * PushbackReader
  * InputStreamReader
    * FileReader

## 特殊类介绍
### 缓冲流类
* 组成：主要是Buffer开头的那部分类
* 作用：增加一层缓冲，提高读写速度

### 转换流类
* 组成：InputStreamReader、OutputStreamWriter
* 作用：字符与字节之间进行转换

### 序列化流
* 作用：将一个对象序列化成文件，将序列化文件反序列化成对象
* 组成：ObjectOutputStream、ObjectInputStream

### 打印流
* 作用：打印各种东西
* 组成：PrintStream、PrintWriter

### Properties属性类
* 作用：属性读写
* 关联：内部使用到了IO部分类来实现属性读写
