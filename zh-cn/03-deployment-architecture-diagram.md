# 部署架构设计

![访问统计](https://visitor-badge.glitch.me/badge?page_id=senlypan.cloudgaming.03-deployment-architecture-diagram&left_color=blue&right_color=red)

> 作者: 大厂研究员
>
> 更新: 2022-08-18

## 概述

### 📖 定义

描述后端系统具体如何部署，对应 4+1 视图的物理视图。参考 [《阿里云 - 运用RUP 4+1视图方法进行软件架构设计》](https://developer.aliyun.com/article/458980)

![](../_media/image/02-system-architecture-diagram/4+1.jpg)

### 🌏 使用场景

1. 总体架构设计；
2. 运维规划和优化；
3. 面试、晋升。

### 🎨 画图技巧

1. 使用 **图标** 代替区块。

### 🛠️ 工具推荐

1. [ProcessOn - 制图共享工具](https://www.processon.com/)
2. [Cloudcraft - 部署架构图设计工具](https://www.cloudcraft.co/)

### 👉 部署示例

![](../_media/image/03-deployment-architecture-diagram/demo-001.jpg)


## 云游戏平台部署架构

![](../_media/image/03-deployment-architecture-diagram/deployment-architecture-diagram-001.jpg)


详见 [ProcessOn - 云游戏平台部署架构](https://www.processon.com/view/link/62ff5d350e3e7437cac1c423)

!> 图片预览效果不佳，具体请打开以上详细链接


## 流量网关（Nginx）

`待补充`

## 网关中心

### 常见网关对比

> 目前常见的开源网关大致上按照语言分类有如下几类:

| 语言        | 网关 | 
| ---------------| ----- |
| Nginx + lua    | OpenResty、Kong、Orange、Abtesting gateway 等 |
| Java           | Zuul/Zuul2、Spring Cloud Gateway、Kaazing KWG、gravitee、Dromara soul 等 |
| Go             | Janus、fagongzi、Grpc-gateway |
| .net           | Ocelot |
| NodeJS         | Express Gateway、Micro Gatewa |

> 按照使用数量、成熟度等来划分，主流的有 4 个：

- **OpenResty** 
    - Nginx + Lua
- **Kong** 
    - Nginx + Lua + OpenResty
- **Zuul/Zuul2** 
    - Java
- **Spring Cloud Gateway**
    - Java

### 选型参考

> 互联网企业常见的方案有基于 Openresty 的 Kong、Orange，基于 Go 的 Tyk 和基于 Java 的 Zuul。

| 技术项          | 概述  |
| --------------- | ----- |
| Zuul            | 是一种提供动态路由、监视、弹性、安全性等功能的边缘服务，Zuul 是 Netflix 出品的一个基于 JVM 路由和服务端的负载均衡器。 |
| Tyk             | 是一个基于 Go 实现的开源 API 网关服务， Tyk 提供一个 API 管理平台，其中包括 API 网关、API 分析、开发人员门户和 API 管理面板。|
| Kong            | Kong 是 Mashape 提供的一款 API 管理软件，它本身是基于 Nginx + Lua 的，但是比 Nginx 提供了更简单的配置方式，数据采用了 Apache Cassandra/PostgreSQL 存储并提供了一些优秀的插件，比如验证、日志、调用频率限制等。|
| Orange          | 和 Kong 类似也是基于 OpenResty 的一个 API 网关程序。|
| apiaxle         | Nodejs 实现的一个 API 网关。|
| api-umbrella    | Ruby 实现的一个 API 网关。|

> 几种网关的对比

| 维度     |  Zuul 1       | OpenResty 自建     | Kong                    | Orange                    | Zuul 2        | SpringCloudGateway | 
| -----    | ---------     | -----------------  | ------------------------ | -------------------------| -------------| --------------------| 
| WEb容器  |  Servlet       |                   |                         |                           | Netty Server  |  WebFlux           | 
| 线程模型  | 阻塞          |                   |                         |                           | 非阻塞         |  非阻塞             | 
| 支持Http  | ✔️           |                   |                         |                           | ✔️            |  ✔️                | 
| 支持dubbo | ❌           |                   |                         |                           | ❌            |  ❌                | 
| 效率     |  一般          |  高                | 高                      | 高                        | 一般          |  一般               | 
| 开发语言 |  Java          |  Lua               | Lua                     | Lua                       | Java         | Java                | 
| 技术栈   |  Springboot    |  Nginx + Lua       | Nginx + Lua + OpenResty | Nginx + Lua + OpenResty   | Springboot    | Springboot         | 
| 存储     |                |  Redis、Memcached  | Cassandra、PostgreSQL   | MySQL                     |               |                     | 
| 服务注册 |  Eureka、Consul |  Consul、ETCD     | Consul、ETCD             | Consul/ETCD               |               |                     | 
| 管理界面 |  内置           |  开源             | 第三方开源                | 开源                      |               |                     | 
| 社区     |  成熟           |  成熟             | 相对成熟，用户问题汇总，社区，插件开源| 少，个人开发者             |开源不久，资料少 | spring社区成熟，但gateway资源较少| 
| 代码     |  开源           |  开源             | 开源，更新频繁            | 开源                       |               |                     | 
| 学习成本 |  一般           |  简单易用，但是需要进行的lua开发很多 | 简单易用，api转发通过管理员接口配置，开发需要lua脚本 | 较高   | 参考资料较少   |   简单易用 | 
| 维护成本 |  一般           |  普通，需要维护lua脚本  | 较高，需要维护lua脚本  | 较高                       | 可维护性较差 |spring系列可扩展强，易配置 可维护性好| 
| 扩展     |  支持           |  自建              | 支持集群                  | 支持集群                  |               |                     | 
| 多节点   |  支持           |  自建              | 支持                      | 需要开发                  |               |                     | 
| 功能     |  丰富           |  自建              | 丰富，部分开源 + 商业      | 丰富                     |               |                      | 
| 服务编排  | ❌            |                    |                           |                           | ❌            |  ❌                | 
| 限流     |                |  需要lua开发        | 根据秒，分，时，天，月，年，根据用户进行限流。可在原码的基础上进行开发 | |可以通过配置文件配置集群限流和单服务器限流亦可通过filter实现限流扩展|可以通过IP，用户，集群限流，提供了相应的接口进行扩展|
| 鉴权     |                |  需要lua开发        | 支持普通鉴权，Key Auth鉴权，HMAC，auth2.0 | | filter中实现| 支持普通鉴权、auth2.0 | 
| 监控     |                |  需要开发           | 可上报datadog，记录请求数量，请求数据量，应答数据量，接收于发送的时间间隔，状态码数量，kong内运行时间 | | filter中实现 | Gateway Metrics Filter |

### 业务网关体系结构

![](../_media/image/03-deployment-architecture-diagram/gateway-001.png)

### 流量与业务网关

![](../_media/image/03-deployment-architecture-diagram/gateway-002.png)

### 部署架构参考

![](../_media/image/03-deployment-architecture-diagram/gateway-003.png)

### 网关选型参考

- [InfoQ - 天翼账号网关系统架构演进历程](https://xie.infoq.cn/article/c6703d216c43c2b522b9b4ffa)

- [InfoQ - 业务网关的落地实践](https://www.infoq.cn/article/cAcwMUNMJMQpIxGJYkcS)

- [博客园 - 亿级流量架构之网关设计思路、常见网关对比](https://www.cnblogs.com/Courage129/p/14446586.html)

## 消息服务

> 几种常用MQ对比

| 维度    | ActiveMQ                       | RabbitMQ                       | RocketMQ             | Kafka              | 
|-------|--------------------------------|--------------------------------|----------------------|-----------------| 
| 多语言支持 | 支持，JAVA优先                      | 语言无关                           | 只支持Java              | 支持，Java优先       |
| 单机吞吐量 | 万级                             | 万级                             | 10万级                 | 10万级              | 
| 时效性   | ms级                            | 微秒级                            | ms级                  | ms级以内          | 
| 持久化   | 内存、文件、数据库                      | 内存、文件，支持数据堆积，但数据堆积会影响生产速率      | 磁盘文件        | 磁盘文件，只要磁盘容量足够，可以做到无限消息堆积 | 
| 功能支持  | MQ领域的功能极其完备                    | 基于erlang开发，所以并发能力很强，性能极其好，延时很低 | MQ功能较为完善，还是分布式的，扩展性好 | 功能较为简单，主要支持简单的MQ功能，在大数据领域的实时计算以及日志采集被大规模使用，是事实上的标准 | 
| 可用性   | 高（主从）                          | 高（主从）                          | 非常高（分布式）             | 非常高（分布式）        | 
| 消息丢失  | 低                              | 低                              | 非常高（分布式）             | 中              | 
| 社区活跃度 | 高                              | 高                              | 中                    | 高              | 
| 成熟度   | 成熟                             | 成熟                             | 比较成熟                 | 成熟日志领域         | 
| 支持协议  | OpenWirte、Stomp、rest、amop、xmpp | AMQP                           | 自己定义的一套              |            | 
| 事务    | 支持                             | 不支持                            | 支持                   |                | 
| 负载均衡  | 支持                             | 支持                             | 支持                   |                | 
| 部署方式  | 独立、嵌入                          | 独立                             | 独立                   |                | 


#### mq基本架构
![](../_media/image/03-deployment-architecture-diagram/mq-base-architecture.jpg)

#### kafka集群架构
![](../_media/image/03-deployment-architecture-diagram/kafka-architecture.png)

#### rocketmq集群架构
![](../_media/image/03-deployment-architecture-diagram/rocketmq-architecture.png)

#### activemq集群架构
##### 1.p2p
![](../_media/image/03-deployment-architecture-diagram/activemq-p2p.png)

##### 2.p/s
![](../_media/image/03-deployment-architecture-diagram/activemq-ps.png)

#### rabbitmq集群架构
![](../_media/image/03-deployment-architecture-diagram/rabbitmq-architect.jpeg)

## 文件服务

`待补充`

## 任务调度

### xxl-job 架构

![](../_media/image/03-tech-architecture-diagram/xxl-job.png)
### 部署
![](../_media/image/03-tech-architecture-diagram/xxl-job-deployment-001.jpg)
### 任务调度
![](../_media/image/03-tech-architecture-diagram/xxl-job-dispatch.jpg)
### 执行器注册
![](../_media/image/03-tech-architecture-diagram/xxl-job-executor.jpg)
## 分布式事务

`待补充`

## 配置中心与注册中心

`待补充`

## 缓存服务

`待补充`

## 关系数据库服务（MySQL）

`待补充`

## 自动化构建测试发布服务

![](../_media/image/03-tech-architecture-diagram/auto-build-test-publish.png)
### 部署
![](../_media/image/03-tech-architecture-diagram/auto-build-test-publish-002.jpg)

## 容器化部署

`待补充`

## 日志中心

`待补充`

## 分布式事务集群

`待补充`

## 大数据中心（数据采集分析）

### 数据分析技术架构

![data_analyze_framework](../_media/image/03-outline-design/data_analyze_framework.png)

### 数据分析开发流程

![data_analyze_development_flow](../_media/image/03-outline-design/data_analyze_development_flow.png)

## 性能监控中心（全链路追踪）

`待补充` 

## 参考

- [极客专栏 - 如何画好架构图](https://u.geekbang.org/lesson/381) 👍👍👍

- [微信 - 如何画好一张架构图？](https://mp.weixin.qq.com/s/2HjvNnfP7bLNQF5xh8PxIQ)