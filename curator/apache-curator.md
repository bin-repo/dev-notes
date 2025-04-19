# apache-curator

- Apache Curator is a Java/JVM client library for Apache ZooKeeper
- zookeeper的java客户端开源库

## 源码

- apache-curator-4.2.0-source-release.zip

## 主要组件

- curator-recipes（公共基础组件）
- curator-client（ZK客户端实现）
- curator-framework（封装高级接口）
- curator-examples（各组件示例代码）

## Maven（pom.xml）

```xml
<!-- 添加curator-framework、curator-client、curator-recipes依赖 -->
<dependency>
    <groupId>org.apache.curator</groupId>
    <artifactId>curator-framework</artifactId>
    <version>4.2.0</version>
</dependency>
```

## 示例代码

```java
RetryPolicy retryPolicy = new ExponentialBackoffRetry(1000, 3)
CuratorFramework client = CuratorFrameworkFactory.newClient(zookeeperConnectionString, retryPolicy);
client.start();
client.create().forPath("/my/path", myData);
```
