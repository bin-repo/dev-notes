# apache-hadoop

## 简介

- The Apache™ Hadoop™ project develops open-source software for reliable, scalable, distributed computing
- 分布式计算框架（HDFS、YARN、MapReduce）

## 版本演变

### Hadoop 1.0

- MapReduce（作业调度和集群资源管理、分布式运算）
- HDFS（分布式文件系统）

### Hadoop 2.0

- MapReduce（分布式运算）
- YARN（作业调度和集群资源管理）
- HDFS（分布式文件系统）

### Hadoop 3.0

- MapReduce（分布式运算）A YARN-based system for parallel processing of large data sets 大数据并行处理编程框架
- YARN（作业调度和集群资源管理）A framework for job scheduling and cluster resource management
- HDFS（分布式文件系统）Hadoop Distributed File System 分布式存储
- Common（基础公共工具）The common utilities that support the other Hadoop modules
- QZone（对象存储组件）An object store for Hadoop
- Submarine（机器学习引擎）A machine learning engine for Hadoop

## 关联项目

### Ambari

集群WEB集中管理及监控（A web-based tool for provisioning, managing, and monitoring Apache Hadoop clusters which includes support for Hadoop HDFS, Hadoop MapReduce, Hive, HCatalog, HBase, ZooKeeper, Oozie,Pig and Sqoop. Ambari also provides a dashboard for viewing cluster health such as heatmaps and ability to view MapReduce, Pig and Hive applications visually alongwith features to diagnose their performance characteristics in a user-friendly manner）

### Avro

数据序列化系统（A data serialization system）

### Cassandra

多主节点弹性数据库，避免单点故障（A scalable multi-master database with no single points of failure）

### Chukwa

管理大型分布式系统的数据集合系统（A data collection system for managing large distributed systems）

### HBase

分布式数据库、支持大表（A scalable, distributed database that supports structured data storage for large tables）

### Hive

数据库查询工具、类SQL（ A data warehouse infrastructure that provides data summarization and ad hoc querying）

### Mahout

机器学习和数据挖掘库（A Scalable machine learning and data mining library）

### Pig

并行计算数据流语言框架（A high-level data-flow language and execution framework for parallel computation）

### Spark

计算引擎（A fast and general compute engine for Hadoop data. Spark provides a simple and expressive programming model that supports a wide range of applications, including ETL, machine learning, stream processing, and graph computation）

### Tez

业务处理框架、可能取代MapReduce（A generalized data-flow programming framework, built on Hadoop YARN, which provides a powerful and flexible engine to execute an arbitrary DAG of tasks to process data for both batch and interactive use-cases.

Tez is being adopted by Hive™, Pig™ and other frameworks in the Hadoop ecosystem, and also by other commercial software (e.g. ETL tools), to replace Hadoop™ MapReduce as the underlying execution engine）

### ZooKeeper

高性能协调服务（A high-performance coordination service for distributed applications）

## 参考书籍

- Hadoop技术内幕：深入解析Hadoop Common和HDFS架构设计与实现原理
- Hadoop技术内幕：深入解析YARN架构设计与实现原理
- Hadoop技术内幕：深入解析MapReduce架构设计与实现原理（RPC框架、JobTracker实现、TaskTracker实现、Task实现、作业调度器实现）
- Hadoop权威指南（Hadoop:The Definitive Guide）
- Hadoop实战（Hadoop in Action）
- Hadoop技术详解（Hadoop Operations）
- Pro Hadoop
