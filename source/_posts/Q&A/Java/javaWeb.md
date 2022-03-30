---
title: javaWeb
date: 2022-03-28 16:25:19
tags: Q&A
categories:
- [Q&A, Q&A-java]
---

### servlet是什么？
* 是一个java web应用服务器，servlet就是一个java官方封装好的HTTP应用服务器功能集合（也可以说规范，比如实现了识别http请求，复用TCP连接等底层操作），即是一个Java官方提供的HTTP服务器功能集合或者规范，方便我们基于此进行应用服务的开发，将精力集中在业务层的编码中即可
* 诞生的原因或者目的：方便开发者快速开发java web服务，为java web服务提供一套规范

### jsp是什么？
* [参考文章](https://www.liaoxuefeng.com/wiki/1252599548343744/1266262958498784)
* 是一个java web应用服务器，全称Java server Pages
* 样子是一个html文件，然后里面内嵌着java代码，用来实现动态网页的开发，这种方式更适合前后端融合的形式，一个人编写比较方便
* 用来开发动态网页应用的一种方式，静态网页之中包含java代码，以实现动态响应能力
* 实际运行时会被编译成servlet，本质是servlet的另一种形式

### Tomcat是什么？
* Tomcat是集合了Servlet、JSP、Java WebSocket等多种网络服务功能的一个更大的java web 服务器，并且还具有可视化配置页面等功能

### Apache是什么？
* 是一个web服务功能集合，全称Apache HTTP Server，只支持HTTP服务

### Nginx是什么？
* 一款轻量级web服务器，跟Apache核心功能类似，都是HTTP服务器，特点是更适合高并发场景等

### 正向代理、反向代理
* 正向代理：VPN即正向代理，即代理会真的替代客户端发请求，而非转发，此时客户端的请求是被整整替代的，所以正向代理，代理的是客户端
* 反向代理：即代理只是转发请求，并没有代理客户端发请求，然后服务器响应，此时服务器被代理
* 总结：正向代理，即客户端被代理的情况，反向代理是服务端被代理的情况

### jsp 和 servlet 有什么区别？
||jsp|servlet|
|---|---|---|
|本质|jsp本质就是servlet，是servlet的一种简易实现方式，或者说是servlet的拓展，JVM只能识别java代码，是web服务器将jsp代码编译成java代码|servlet是java官方提供你的一套http服务器功能集合，或者说一种http服务器规范，方便开发者快速开发应用服务，将精力集中在业务上|
|适用场景|jsp是在HTML中包含了java代码，所以本身包含可视化页面，更容易实现动态网页应用|servlet内部更多地是各种逻辑层，没有可视化相关的内容，更适合做逻辑层、控制层等|
|特点|jsp侧重于可视化部分|servlet侧重于逻辑控制部分|
|诞生目的|简化servlet的使用，使servlet跟HTML更好的结合起来，更好的实现java web应用|为开发者提供java web应用服务开发的规范或者工具，提高开发者效率|


### jsp 有哪些内置对象？作用分别是什么？
|jsp内置对象名称|对应servlet类|作用|
|---|---|---|
|request|javax.servlet.http.HttpServletRequest|client请求信息，http协议头信息、cookie、请求参数等|
|response|javax.servlet.http.HttpServletResponse|server响应client请求，返回信息|
|pageContent|javax.servlet.jsp.PageContext|页面上下文|
|session|javax.servlet.http.HttpSession|client与server之间的会话|
|application|javax.servlet.ServletContext|获取服务端应用生命周期信息|
|out|javax.servlet.jsp.JspWriter|server给client传输内容的输出流|
|config|javax.servlet.ServletConfig|初始化是，jsp引擎向jsp页面传递的信息|
|page|java.lang.Object|指向jsp页面本身|
|exception|	java.lang.Throwable|页面异常对象|


### 说一下 jsp 的 4 种作用域？
* 作用域：即信息共享范围，类似于public、private这种
* 四种作用域介绍：
|作用域范围|信息传递类|
|---|---|
|application：即服务启动到停止的时间|ServletContext|
|session：http会话开始到结束的时间|session|
|request：http请求到结束的时间|request|
|page：当前页面打开到关闭的时间|pageContext|
