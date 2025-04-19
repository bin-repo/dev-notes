# apache-spark

- 基于内存的计算框架
- 支持多种开发语言（Scala、Python、Java等）

## 主要功能模块

### Spark SQL

- 可使用熟知的SQL查询语言来运行数据分析

### Spark Streaming

- 可实现实时数据流处理

### GraphX

- 分布式图处理框架，可用于图表计算

### MLlib

- 可扩充的机器学习库
- 算法包括分类与回归、支持向量机、回归、线性回归、决策树、朴素贝叶斯、聚类分析、协同过滤等

## 安装部署

### 预安装（Scala）

- 可编译为Java字节码，在JVM上运行，具备跨平台能力
- spark支持scala、java、python等语言，但其本身是用scala语言开发的

```sh
# 下载
wget https://downloads.lightbend.com/scala/2.11.12/scala-2.11.12.tgz
# 解压
tar xvf scala-2.11.12.tgz -C /usr/local
ln -s /usr/local/scala-2.11.12 /usr/local/scala
# 环境变量
export SCALA_HOME=/usr/local/scala
export PATH=$PATH:$SCALA_HOME/bin
```

### 安装（Spark）

```sh
# 下载
wget http://archive.apache.org/dist/spark/spark-2.3.2/spark-2.3.2-bin-hadoop2.7.tgz
# 解压
tar zxf spark-2.3.2-bin-hadoop2.7.tgz -C /usr/local
ln -s /usr/local/spark-2.3.2-bin-hadoop2.7 /usr/local/spark
# 环境变量
export SPARK_HOME=/usr/local/spark
export PATH=$PATH:$SPARK_HOME/bin
```

```sh
# 交互终端（启动scala环境）
spark-shell
```

## 本地运行

```sh
# 本地4线程运行
spark-shell --master local[4]
```

```sh
# 读取本地文件
scala> val textFile = sc.textFile("file:/usr/local/spark/README.md")
# 记录数
scala> textFile.count()
```

```sh
# 读取HDFS文件（须先启动HDFS集群）
scala> val textFile = sc.textFile("hdfs://master:9000/hdfs/test/xx.txt")
# 记录数
scala> textFile.count()
```

## 在Hadoop YARN集群上运行

```sh
# 设置环境变量HADOOP_CONF_DIR或YARN_CONF_DIR
export HADOOP_CONF_DIR=/usr/local/hadoop/etc/hadoop
```

```sh
# 进入scala交互终端
spark-shell --master yarn --deploy-mode client
```

## 在Spark Standalone Cluster上运行

```sh
# 多节点安装部署Spark

# spark-env.sh
SPARK_MASTER_HOST、SPARK_MASTER_PORT、SPARK_WORKER_CORES、SPARK_WORKER_MEMORY等

# 主节点
start-master.sh

# 从节点
start-slave.sh <master-spark-URL>

# 客户端
spark-shell --master spark://IP:PORT

# 设置从节点列表（spark/conf/slaves）

# 启动Spark集群
start-all.sh

# Spark集群环境下读取本地文件操作时，需保证每个节点都存在该文件，否则报错；
# 建议将文件存到HDFS上，再进行处理
```

## 运行在其他平台（见官网手册）

- Apache Mesos
- Kubernetes

## spark-submit 提交任务

```sh
# 将Spark应用JAR包提交到YARN集群上运行
spark-submit --class path.to.your.Class --master yarn --deploy-mode cluster [options] <app jar> [app options]

--master local # 本地一个线程运行
--master local[K] # 本地K个线程运行
--master local[*] # 本地运行，Spark自动调度多核CPU
--master spark://master:port # 在Spark Standalone Cluster上运行
--master mesos://master:port # 在Apache Mesos上运行
--master yarn-client # 在Yarn Client上运行
--master yarn-cluster # 在Yarn Cluster上运行
```

## 与Hadoop集群集成

- conf/spark-env.sh
- 三种方法设定SPARK_DIST_CLASSPATH
- 可集成不同版本的Hadoop集群

```sh
# If 'hadoop' binary is on your PATH
export SPARK_DIST_CLASSPATH=$(hadoop classpath)

# With explicit path to 'hadoop' binary
export SPARK_DIST_CLASSPATH=$(/path/to/hadoop/bin/hadoop classpath)

# Passing a Hadoop configuration directory
export SPARK_DIST_CLASSPATH=$(hadoop --config /path/to/configs classpath)
```

## 核心RDD

- 基于内存系统的弹性分布式数据集（Resilient Distributed Dataset）

### RDD三种基本运算

- 转换（Transformation）：由已有数据或已有RDD生成新RDD，仅记录转换过程，不进行实际执行
- 动作（Action）：按记录转换过程进行实际处理，生成数值、数组或写入文件系统
- 持久化（Persistence）：对于会重复使用的RDD，在内存中进行持久化，以提高执行性能

### 创建RDD

- 创建的过程也是转换
- var rdd = sc.parallelize(data)

### Action

- reduce(func)
- collect()
- count()
- first()
- take(n)
- takeSample(withReplacement, num, [seed])
- takeOrdered(n, [ordering])
- saveAsTextFile(path)
- countByKey()
- foreach(func)
- saveAsSequenceFile(path) # Java and Scala
- saveAsObjectFile(path) # Java and Scala

### Transformation

- map(func)
- filter(func)
- flatMap(func)
- mapPartitions(func)
- mapPartitionsWithIndex(func)
- sample(withReplacement, fraction, seed)
- union(otherDataset)
- intersection(otherDataset)
- distinct([numPartitions])
- groupByKey([numPartitions])
- reduceByKey(func, [numPartitions])
- aggregateByKey(zeroValue)(seqOp, combOp, [numPartitions])
- sortByKey([ascending], [numPartitions])
- join(otherDataset, [numPartitions])
- cogroup(otherDataset, [numPartitions])
- cartesian(otherDataset)
- pipe(command, [envVars])
- coalesce(numPartitions)
- repartition(numPartitions)
- repartitionAndSortWithinPartitions(partitioner)

### Persistence

- persist()
- cache()
- unpersist()
