# java JMS（消息服务）

## 介绍

- JMS（Java Message Server）消息服务
- 通用接口规范
- 各消息服务商实现该接口

## 术语

- `Server` 服务商（`S端`）MessageServer
- `Provider` 生产者（`P端`）MessageProvider
- `Consumer` 消费者（`C端`）MessageConsumer
- `PTP` 点对点消息模型（`P2P`）PointToPoint
- `Pub`/`Sub` 发布/订阅消息模型 Publish/Subscribe
- `Queue` 消息队列
- `Topic` 消息主题
- `ConnectionFactory` 连接工厂（创建`P`/`C`端到`S`端的连接）
- `Connection` 连接（建立`P`端与`C`端之间的连接）
- `Destination` 消息目的地（`PTP`模型时为`Queue`；`Pub`/`Sub`模型时为`Topic`）
- `Session` 会话（一个发送或接收消息的线程）

## 主要接口

- `ConnectionFactory`
- `Connection`
- `Destination`
- `MessageConsumer`
- `MessageProducer`
- `Message`
- `Session`

## 消息接口

- `StreamMessage`
- `MapMessage`
- `TextMessage`
- `ObjectMessage`
- `BytesMessage`

## 接口实现

- `ActiveMQ`（Apache）
- `RocketMQ`（Alibaba）
- `RabbitMQ`
- `MSMQ`（Microsoft）
- `MQSeries`（IBM）
- `MessageQ`（BEA）
