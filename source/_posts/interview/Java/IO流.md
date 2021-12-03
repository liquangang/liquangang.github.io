---
title: IO流
date: 2021-11-29 15:35:40
tags: 面试
categories:
- [interview, interview-java]
---

## 参考资料
* [资料1](https://cloud.tencent.com/developer/article/1461049)
* [资料2](https://www.kancloud.cn/imnotdown1019/java_core_full/1012272)

## 概念解释
* IO模型、IO方法：即实现IO所采用的方式，BIO、NIO、AIO是Java官方支持的三种方式，比如读写文件、进程间交互等有IO操作的都可以使用官方支持的三种方式

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

## Java支持的IO模型（即Java官方支持的IO方法）
### BIO（Blocking I/O）：同步且阻塞IO模式，同步且阻塞的实现IO处理
* 使用场景：适合连接数较少且固定架构的情况
* 特点：编程简单，不需要过多考虑系统过载、限流等问题；并发能力差，资源占用高，不能承受十万甚至百万级连接

### NIO（Non-Blocking/New I/O）：同步非阻塞IO模型，client多个连接server开一个线程进行处理，客户端的请求会注册到多路复用器上，server会轮询多路复用器，发现请求后就进行处理
* 使用场景：适合高负载、高并发场景，适合连接数目多且连接比较短的情况
* 实现NIO的三部分：
  * 缓冲区Buffer：NIO基于块进行数据处理，这些数据块通过Buffer的实现类来进行读取，Buffer（接口）实现类有ByteBuffer、IntBuffer等
  * 通道Channel：通过Channel实现数据的读写，通道是全双工，可同时读写，channel（接口）实现类有FileChannel、DatagramChannel、SocketChannel、ServerSocketChannel等
  * 多路复用器Selector：轮询注册在其上的channel，如果某个channel发出读写请求并处于就绪状态，会被其轮询到，然后通过selectionKey可以获取到就绪的channel集合，然后进行后续IO操作，
    * Selector只能管理非阻塞channel，所以阻塞的FileChannel不能被其管理
    * 监听事件注册：serviceSocketChannel.register(selector, SelectionKey.OP_ACCEPT)
    * 监听事件：
      * OP_ACCEPT：接受就绪，ServiceSocketChannel使用
      * OP_READ：读取就绪，SocketChannel使用
      * OP_WRITE：写入就绪，SocketChannel使用
      * OP_CONNECT：连接就绪，SocketChannel使用

### AIO（Asynchronous I/O）：也就是NIO2，异步非阻塞IO模型，多个有效的client请求才启动server多个线程，特点是系统处理完才通知server去创建线程处理
* 使用场景：适合高负载、高并发场景，适用于连接数多且时间长的场景
* 特点：基于事件和回调机制实现；不会阻塞，当后台处理完成时，系统会通知相应线程继续操作

### IO模型总结
* 同步阻塞：一个线程，顺序执行
* 同步非阻塞：一个线程，顺序执行，遇到暂时没执行结果的行，先跳过执行后面的，然后通过某种方式比如轮询来查看无执行结果行的结果
* 异步阻塞：一个线程中异步执行多个任务，其中一个任务执行时，其他任务需要阻塞等待
* 异步非阻塞：有多个线程执行任务，所有的线程互不干预，各自干各自的活
