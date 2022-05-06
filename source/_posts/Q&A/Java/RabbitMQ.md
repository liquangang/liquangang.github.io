---
title: RabbitMQ
date: 2022-05-06 19:47:29
tags: Q&A
categories:
- [Q&A, Q&A-java]
---

## rabbitmq 的使用场景有哪些？
* 跨系统的异步通信
* 多应用交互解耦
* 应用内同步变异步
* 消息驱动的架构方式
* 应用需要更灵活的耦合方式
* 跨局域网、城市的通讯（比如cdn）

## rabbitmq 有哪些重要的角色？
|角色|简介|
|---|---|
|生产者|消息创建者，负责创建和推送数据到消息服务器|
|消费者|消息接收方，用于处理数据和确认消息|
|代理|RabbitMQ本身，扮演快递角色，本身不生产消息，传输和管理消息|

## rabbitmq 有哪些重要的组件？
|组建名称|简介|
|---|---|
|ConnectionFactory（连接管理器）|应用于rabbit之间建立的连接的管理器，程序代码中使用|
|Channel（信道）|消息推送使用的通道|
|Exchange（交换器）|用于接收、分配消息|
|Queue（队列）|用于存储生产者消息|
|RoutingKey（路由键）|告诉交换器，需要放到哪个队列中，需要与bindingkey一起使用|
|BindingKey（绑定建）|用于标记交换器与队列的绑定规则，当消息的路由键与绑定建相同时，交换器会将该消息放到绑定建对应的队列中|

## rabbitmq 中 vhost 的作用是什么？
vhost可以理解为broker，即min-RabbitMQ server，其内部含有rabbitmq的所哟组件，特点是拥有独立的权限系统，可以用于权限隔离，即一个RabbitMQ可以让多个应用以权限隔离的方式同时使用

## rabbitmq 的消息是怎么发送的？
连接到RabbitMQ服务器，然后通过认证，然后通过通过信道发送消息，信道是建立在tcp真实连接上的虚拟连接

## rabbitmq 怎么保证消息的稳定性？
* 提供事务功能
* 可将channel设置为confirm模式，RabbitMQ会将消息发送情况返回给生产者
