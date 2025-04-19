# apache-kafka

- A distributed streaming platform as a Messaging System、as a Storage System、for Stream Processing
- 用Scala和Java编写，是一种高吞吐量的分布式发布订阅消息系统，它可以处理消费者规模的网站中的所有动作流数据

## 术语

- Broker（集群中的服务器节点）
- Topic（消息类别）
- Partition（每个Topic包含一个或多个Partition）
- Producer（负责发布消息到Broker）
- Consumer（从Broker读取消息的客户端）

## 下载安装

```sh
wget http://mirrors.hust.edu.cn/apache/kafka/2.1.0/kafka_2.11-2.1.0.tgz
tar -xzvf kafka_2.11-2.1.0.tgz
```

## 运行

```sh
# 启动服务
bin/zookeeper-server-start.sh config/zookeeper.properties
bin/kafka-server-start.sh config/server.properties
```

```sh
# 创建主题
bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
bin/kafka-topics.sh --list --zookeeper localhost:2181
```

```sh
# 生产消息
bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test
```

```sh
# 消费消息
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning
```

## 集群

```sh
# 启动服务
bin/zookeeper-server-start.sh config/zookeeper.properties

# 节点1
cp config/server.properties config/server-1.properties
# broker.id=1
# listeners=PLAINTEXT://:9093
# log.dirs=kafka-logs1

# 节点2
cp config/server.properties config/server-2.properties
# broker.id=2
# listeners=PLAINTEXT://:9094
# log.dirs=kafka-logs2

bin/kafka-server-start.sh config/server-1.properties &
bin/kafka-server-start.sh config/server-2.properties &
```

```sh
# 创建主题
bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 3 --partitions 1 --topic my-replicated-topic
bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic my-replicated-topic
bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic test
```

```sh
# 生产消息
bin/kafka-console-producer.sh --broker-list localhost:9092 --topic my-replicated-topic
```

```sh
# 消费消息
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --from-beginning --topic my-replicated-topic
```

```sh
# 容错测试

# 关闭节点1
ps aux | grep server-1.properties
kill -9 $PID

bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic my-replicated-topic
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --from-beginning --topic my-replicated-topic
```
