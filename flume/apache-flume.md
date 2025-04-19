# apache-flume

- Is a distributed, reliable, and available service for efficiently collecting, aggregating, and moving large amounts of log data
- 分布式、弹性、有用的服务，可用于大量数据的收集、聚合、移动（常用于日志采集）

## 架构

- Source（数据源--数据采集）
- Channel（数据渠--数据加工）
- Sink（下沉--数据分发或存储）

## Source支持

- Avro、Thrift、Exec、JMS、SpoolingDirectory、Taildir、Kafka、NetCat、SequenceGenerator、Syslog、HTTP、Stress等

## Channel支持

- Memory、JDBC、Kafka、File、SpillableMemory、PseudoTransaction等

## Sink支持

- HDFS、Hive、Logger、Avro、Thrift、IRC、FileRoll、HBase、MorphlineSolr、ElasticSearch、Kafka、HTTP等

## Data model

![数据模型](./data-model.png "data model")

## 下载

```sh
# 程序
wget http://mirrors.hust.edu.cn/apache/flume/stable/apache-flume-1.8.0-bin.tar.gz
# 源码
wget http://mirrors.hust.edu.cn/apache/flume/stable/apache-flume-1.8.0-src.tar.gz
```

## 安装

```sh
tar xzvf apache-flume-1.8.0-bin.tar.gz
```

## 环境变量（JAVA_HOME、FLUME_HOME、PATH）

## 运行

```sh
bin/flume-ng help
bin/flume-ng version

# 启动代理（根据不同业务需求设置代理名称并编写配置文件）
bin/flume-ng agent -n $agent_name -c conf -f conf/flume-conf.properties.template

# 启动级联（将指定的本地文件发送给其它代理）
bin/flume-ng avro-client -H $agent_host -p $agent_port -F $file
```

## 示例

- 监听localhost:44444收到的报文，并在logger中输出内容
- 可通过telnet localhost 44444进行测试
- 分布式应用时配置文件可由zookeeper维护

### 配置（example.conf）

```conf
# A single-node Flume configuration

# Name the components on this agent
a1.sources = r1
a1.sinks = k1
a1.channels = c1

# Describe/configure the source
a1.sources.r1.type = netcat
a1.sources.r1.bind = localhost
a1.sources.r1.port = 44444

# Describe the sink
a1.sinks.k1.type = logger

# Use a channel which buffers events in memory
a1.channels.c1.type = memory
a1.channels.c1.capacity = 1000
a1.channels.c1.transactionCapacity = 100

# Bind the source and sink to the channel
a1.sources.r1.channels = c1
a1.sinks.k1.channel = c1
```

### 命令

```sh
# 本地配置
bin/flume-ng agent --conf conf --conf-file example.conf --name a1 -Dflume.root.logger=INFO,console
# 分布式配置
bin/flume-ng agent --conf conf -z zkhost:2181,zkhost1:2181 -p /flume --name a1 -Dflume.root.logger=INFO,console
```
