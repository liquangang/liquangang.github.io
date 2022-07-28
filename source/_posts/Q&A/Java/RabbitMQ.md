---
title: RabbitMQ
date: 2022-05-06 19:47:29
tags: Q&A
categories:
- [Q&A, Q&A-java]
---

## RabbitMQ使用场景
1、跨系统异步通信
2、多应用之间解耦
3、应用内流程同步变异步
4、整体架构即采用消息驱动
5、应用内部解耦

## RabbitMQ内部角色
|角色|简介|
|---|---|
|生产者|消息创建者|
|消费者|消息接收者|
|代理|RabbitMQ本身，用于存储转发消息，快递功能|

## RabbitMQ有哪些重要组件
|组建|简介|
|---|---|
|ConnectionFactory|应用程序与RabbitMQ建立的连接管理器，在应用中使用|
|Channel|消息推送使用的通道|
|Exchange|用于接收、分配消息|
|Queue|用于存储消息|
|RoutingKey|把生产者生产的消息分配到Exchange上|
|BindingKey|标记Exchange与Queue绑定规则|

## RabbitMQ的vhost作用
vhost用于隔离不用应用权限，实现一个RabbitMQ被多个不用的应用使用的功能

## RabbitMQ消息如何发送
1、与RabbitMQ服务进行连接，客户端与RabbitMQ建立tcp连接，并通过人证
2、建立channel
3、发消息

## RabbitMQ如何保证消息稳定性
1、事务功能
2、channel提供confirm功能

## RabbitMQ如何保证不丢失消息
1、消息持久化
2、ACK确认机制
3、设置集群镜像模式
4、消息补偿机制

## 保证消息持久化的条件是哪些
1、声明队列必须声明durable设置为true
2、消息推送投递模式必须设置持久化，deliveryModel设置为持久
3、消息已经到达持久化交换器
4、消息已经到达持久化队列

## RabbitMQ持久化有什么缺点
1、消息持久化会用到磁盘，此时吞吐量就会受到磁盘读写速度影响，可以通过更换高读写速度的磁盘来部分解决

## RabbitMQ有几种广播类型
|广播类型|简介|
|---|---|
|fanout|所有bind到Exchange的queue都可以接收消息|
|direct|通过routingkey和Exchange决定那个queue唯一接受消息|
|topic|所有符合routingkey（可以是个表示式）绑定规则的queue都可以接收消息|

## RabbitMQ怎么实现延迟消息队列
1、消息过期后进入死信消息队列，再由Exchange转发到延迟消息队列
2、使用插件（RabbitMQ-delayed-message-exchange）实现

## RabbitMQ集群有什么用
1、实现高可用
2、实现高容量

## RabbitMQ节点有哪些类型
|节点类型|简介|
|---|---|
|磁盘节点|消息存储到磁盘|
|内存节点|消息存储到内存中，重启会丢消息|

## RabbitMQ搭建集群需要注意哪些问题
1、各集群之间必须使用--link连接，此属性不能忽略
2、各节点使用的erlang cookie值必须相同，此值用于各节点之间认证
3、整个集群必须包含一个磁盘节点

## RabbitMQ每个节点是其他节点的完整拷贝吗，为什么
|||
|---|---|
|RabbitMQ每个节点是其他节点的完整拷贝吗|不是|
|为什么|1、存储空间考虑<br/>2、性能考虑|

## RabbitMQ集群中唯一一个磁盘节点崩溃了会发生什么情况
集群依然可以运行，但是已经出于不可用状态了，此时不能更改任何东西，且消息也无法实现持久化了

## RabbitMQ对集群节点停止顺序有要求吗？
有，需要最后关闭磁盘节点，先关闭内存节点会导致消息丢失
