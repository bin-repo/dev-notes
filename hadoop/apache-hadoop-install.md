# apache-hadoop 安装部署

## 预安装（以 root 用户）

### 安装 JDK、设置环境变量 JAVA_HOME

### 安装 SSH、RSYNC

```sh
# ubuntu
sudo apt-get install ssh rsync
# centos
sudo yum install ssh rsync
```

### 创建用户及组 hadoop

```sh
sudo groupadd -g 300 hadoop
sudo useradd -u 301 -g 300 -d /home/hadoop -m -r hadoop
sudo passwd hadoop
```

## 安装（以 hadoop 用户）

### 设置 SSH 免密登录

```sh
# 生成密钥文件 id_rsa 和 id_rsa.pub
ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
# 将公钥放置到许可证文件中
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 0600 ~/.ssh/authorized_keys
```

### 下载安装 Hadoop

```sh
# 稳定版
wget http://archive.apache.org/dist/hadoop/common/stable/hadoop-2.9.1.tar.gz
# 解压并移到默认安装目录
sudo tar xzvf hadoop-2.9.1.tar.gz -C /usr/local
sudo ln -s /usr/local/hadoop-2.9.1 /usr/local/hadoop
```

### 脚本中指定 JAVA_HOME

```sh
# etc/hadoop/{hadoop-env.sh,mapred-env.sh,yarn-env.sh}
export JAVA_HOME=/usr/local/java
```

## Single Node Cluster（单节点部署 HDFS 集群和 YARN 集群）

### Standalone Operation

```sh
mkdir input
cp etc/hadoop/*.xml input
bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.9.1.jar \
grep input output 'dfs[a-z.]+'
cat output/*
```

### Pseudo-Distributed Operation

```sh
# core-site.xml
fs.defaultFS（文件系统） = hdfs://localhost:9000

# hdfs-site.xml
dfs.replication（文件系统数据块副本数） = 1

# 首次启动时须执行此格式化命令对HDFS进行初始化
bin/hdfs namenode -format

# 启动HDFS集群（NameNode - http://localhost:50070/）
sbin/start-dfs.sh

# 业务
bin/hdfs dfs -mkdir /user
bin/hdfs dfs -mkdir /user/<username>
bin/hdfs dfs -put etc/hadoop input
bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.9.1.jar \
grep input output 'dfs[a-z.]+'
bin/hdfs dfs -get output output ; cat output/*  
# bin/hdfs dfs -cat output/*

# 停止HDFS集群
sbin/stop-dfs.sh
```

### YARN on a Single Node

```sh
# mapred-site.xml
mapreduce.framework.name = yarn

# yarn-site.xml
yarn.nodemanager.aux-services = mapreduce_shuffle

# 首次启动时须执行此格式化命令对HDFS进行初始化
bin/hdfs namenode -format

# 启动YARN集群（ResourceManager - http://localhost:8088/）
sbin/start-dfs.sh
sbin/start-yarn.sh

# 业务

# 停止YARN集群
sbin/stop-dfs.sh
sbin/stop-yarn.sh
```

## Multi Nodes Cluster（多节点部署 HDFS 集群和 YARN 集群）

### Fully-Distributed Operation

- 默认配置：core-default.xml && hdfs-default.xml && yarn-default.xml && mapred-default.xml
- 定制化配置：etc/hadoop/core-site.xml && hdfs-site.xml && yarn-site.xml && mapred-site.xml

```sh
# 准备4台主机并安装Hadoop
# 设置主机名（HOSTNAME）并进行DNS设置（/etc/hosts）：172.16.10.x node.x (x = 1~4)
# 配置SSH免密登录（主节点node.1的公钥分发到从节点node.2、node.3、node.4进行合并）

# core-site.xml
# HDFS集群NameNode节点URL；等
fs.defaultFS = hdfs://node.1:9000
hadoop.tmp.dir = /usr/local/hadoop/data

# hdfs-site.xml
# 指定各节点（NameNode、DataNode）本地存储目录；等
dfs.replication = 3
dfs.namenode.name.dir
dfs.datanode.data.dir
dfs.namenode.secondary.http-address = node.2:50090
dfs.namenode.secondary.https-address = node.2:50091

# yarn-site.xml
# 配置各节点（ResourceManager、NodeManager）参数
yarn.resourcemanager.hostname = node.1
yarn.nodemanager.aux-services = mapreduce_shuffle

# mapred-site.xml
# 配置MapReduce是否启用YARN框架；等
mapreduce.framework.name = yarn

# etc/hadoop/slaves
# 从节点列表（主机名&IP）
# 主节点将以SSH方式登入从节点启动相应Hadoop模块
for i in 1..4 do echo node.${i} >> slaves; done

```

```sh
# 仅首次启动时在namenode节点（node.1）上执行
hdfs namenode -format 或 hadoop namenode -format
```

```sh
# 逐个模块启动
hadoop-daemon.sh start namenode
hadoop-daemon.sh start datanode
yarn-daemon.sh start resourcemanager
yarn-daemon.sh start nodemanager
```

```sh
# 集群整体启动
sbin/start-dfs.sh
sbin/start-yarn.sh
jps # 查看进程

# 测试任务
hadoop jar hadoop-mapreduce-examples-xx.jar pi 20 50

# 整体停止
sbin/stop-dfs.sh
sbin/stop-yarn.sh
```
