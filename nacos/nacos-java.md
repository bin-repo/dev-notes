# Nacos Java SDK 使用手册

## Maven 依赖

```xml
<dependency>
    <groupId>com.alibaba.nacos</groupId>
    <artifactId>nacos-client</artifactId>
    <version>${version}</version>
</dependency>
```

## Maven 纯净版依赖

- 由于Nacos Java SDK在2.0版本后引入了gRPC，为了避免用户业务引入的gRPC版本与之不同导致冲突

```xml
 <properties>
    <!-- 2.1.2版本以上支持纯净版客户端 -->
    <nacos.version>2.4.2</nacos.version>
</properties>

<dependencies>
    <dependency>
        <groupId>com.alibaba.nacos</groupId>
        <artifactId>nacos-client</artifactId>
        <version>${nacos.version}</version>
        <!-- 指定纯净版SDK -->
        <classifier>pure</classifier>
    </dependency>
    <!-- 使用纯净版时必须要引入同版本nacos-api和nacos-common，否则可能出现运行时找不到类的问题 -->
    <dependency>
        <groupId>${project.groupId}</groupId>
        <artifactId>nacos-common</artifactId>
        <version>${nacos.version}</version>
    </dependency>
    <dependency>
        <groupId>${project.groupId}</groupId>
        <artifactId>nacos-api</artifactId>
        <version>${nacos.version}</version>
    </dependency>
</dependencies>
```

## 初始化SDK

- 使用默认配置

```java
String serverAddr = "localhost:8848";

ConfigService configService = NacosFactory.createConfigService(serverAddr);
NamingService namingService = NacosFactory.createNamingService(serverAddr);
```

- 使用自定义配置
  - 默认优先级：`properties > 命令行参数 > 环境参数 > 默认值`

```java
Properties properties = new Properties();

properties.setProperty(PropertyKeyConst.SERVER_ADDR, "localhost:8848");
properties.setProperty(PropertyKeyConst.NAMESPACE, "${namespaceId}");

ConfigService configService = NacosFactory.createConfigService(properties);
NamingService namingService = NacosFactory.createNamingService(properties);
```

## 配置管理API

- `dataId` 建议采用类似包名`点分隔`形式，如 com.xxx.yyy
- `group` 建议采用`产品名:模块名`形式，如 xxx:yyy
- `timeoutMs` 超时时间（ms），建议3000
- `listener` 监听器（回调函数）
- `content` 内容长度不超过100K
- `type` 配置类型（PROPERTIES/XML/JSON/TEXT默认/HTML/YAML/TOML）
- `casMd5` 前配置内容的md5

### 获取配置

```java
public String getConfig(String dataId, String group, long timeoutMs) throws NacosException;
```

### 监听配置

```java
public void addListener(String dataId, String group, Listener listener);
```

### 删除监听

```java
public void removeListener(String dataId, String group, Listener listener);
```

### 发布配置

```java
public boolean publishConfig(String dataId, String group, String content) throws NacosException;
public boolean publishConfig(String dataId, String group, String content, String type) throws NacosException;
```

```java
try {
    // 初始化配置服务，控制台通过示例代码自动获取下面参数
    String serverAddr = "{serverAddr}";
    String dataId = "{dataId}";
    String group = "{group}";
    Properties properties = new Properties();
    properties.put("serverAddr", serverAddr);
    ConfigService configService = NacosFactory.createConfigService(properties);
    boolean isPublishOk = configService.publishConfig(dataId, group, "content");
    System.out.println(isPublishOk);
} catch (NacosException e) {
    e.printStackTrace();
}
```

### 删除配置

```java
public boolean removeConfig(String dataId, String group) throws NacosException;
```

### 带监听器的获取配置

```java
String getConfigAndSignListener(String dataId, String group, long timeoutMs, Listener listener) throws NacosException;
```

### 带Compare-And-Swap（CAS）的发布配置

```java
boolean publishConfigCas(String dataId, String group, String content, String casMd5) throws NacosException;
boolean publishConfigCas(String dataId, String group, String content, String casMd5, String type) throws NacosException;
```

## 服务发现API

### 注册实例

```java
void registerInstance(String serviceName, String ip, int port) throws NacosException;
void registerInstance(String serviceName, String groupName, String ip, int port) throws NacosException;
void registerInstance(String serviceName, String ip, int port, String clusterName) throws NacosException;
void registerInstance(String serviceName, String groupName, String ip, int port, String clusterName) throws NacosException;
void registerInstance(String serviceName, Instance instance) throws NacosException;
void registerInstance(String serviceName, String groupName, Instance instance) throws NacosException;
```

```java
// 示例
NamingService naming = NamingFactory.createNamingService(System.getProperty("serveAddr"));

// 以下注册请求等同
naming.registerInstance("nacos.test.service", "127.0.0.1", 8848);
naming.registerInstance("nacos.test.service", "DEFAULT_GROUP", "127.0.0.1", 8848);
naming.registerInstance("nacos.test.service", "127.0.0.1", 8848, "DEFAULT");
naming.registerInstance("nacos.test.service", "DEFAULT_GROUP", "127.0.0.1", 8848, "DEFAULT");
Instance instance = new Instance();
instance.setIp("127.0.0.1");
instance.setPort(8848);
instance.setClusterName("DEFAULT");
naming.registerInstance("nacos.test.service", instance);
naming.registerInstance("nacos.test.service", "DEFAULT_GROUP", instance);
```

### 注销实例

```java
// 与注册实例对应
void deregisterInstance(String serviceName, String ip, int port) throws NacosException;
void deregisterInstance(String serviceName, String groupName, String ip, int port) throws NacosException;
void deregisterInstance(String serviceName, String ip, int port, String clusterName) throws NacosException;
void deregisterInstance(String serviceName, String groupName, String ip, int port, String clusterName) throws NacosException;
void deregisterInstance(String serviceName, Instance instance) throws NacosException;
void deregisterInstance(String serviceName, String groupName, Instance instance);
```

### 获取全部实例

```java
List<Instance> getAllInstances(String serviceName) throws NacosException;
List<Instance> getAllInstances(String serviceName, String groupName) throws NacosException;
List<Instance> getAllInstances(String serviceName, boolean subscribe) throws NacosException;
List<Instance> getAllInstances(String serviceName, String groupName, boolean subscribe) throws NacosException;
List<Instance> getAllInstances(String serviceName, List<String> clusters) throws NacosException;
List<Instance> getAllInstances(String serviceName, String groupName, List<String> clusters) throws NacosException;
List<Instance> getAllInstances(String serviceName, List<String> clusters, boolean subscribe) throws NacosException;
List<Instance> getAllInstances(String serviceName, String groupName, List<String> clusters, boolean subscribe) throws NacosException;
```

### 获取健康或不健康实例列表

```java
List<Instance> selectInstances(String serviceName, boolean healthy) throws NacosException;
List<Instance> selectInstances(String serviceName, String groupName, boolean healthy) throws NacosException;
List<Instance> selectInstances(String serviceName, boolean healthy, boolean subscribe) throws NacosException;
List<Instance> selectInstances(String serviceName, String groupName, boolean healthy, boolean subscribe) throws NacosException;
List<Instance> selectInstances(String serviceName, List<String> clusters, boolean healthy) throws NacosException;
List<Instance> selectInstances(String serviceName, String groupName, List<String> clusters, boolean healthy) throws NacosException;
List<Instance> selectInstances(String serviceName, List<String> clusters, boolean healthy, boolean subscribe) throws NacosException;
List<Instance> selectInstances(String serviceName, String groupName, List<String> clusters, boolean healthy, boolean subscribe) throws NacosException;
```

### 获取一个健康实例

```java
Instance selectOneHealthyInstance(String serviceName) throws NacosException;
Instance selectOneHealthyInstance(String serviceName, String groupName) throws NacosException;
Instance selectOneHealthyInstance(String serviceName, boolean subscribe) throws NacosException;
Instance selectOneHealthyInstance(String serviceName, String groupName, boolean subscribe) throws NacosException;
Instance selectOneHealthyInstance(String serviceName, List<String> clusters) throws NacosException;
Instance selectOneHealthyInstance(String serviceName, String groupName, List<String> clusters) throws NacosException;
Instance selectOneHealthyInstance(String serviceName, List<String> clusters, boolean subscribe) throws NacosException;
Instance selectOneHealthyInstance(String serviceName, String groupName, List<String> clusters, boolean subscribe) throws NacosException;
```

### 监听服务（订阅）

```java
void subscribe(String serviceName, EventListener listener) throws NacosException;
void subscribe(String serviceName, String groupName, EventListener listener) throws NacosException;
void subscribe(String serviceName, List<String> clusters, EventListener listener) throws NacosException;
void subscribe(String serviceName, String groupName, List<String> clusters, EventListener listener) throws NacosException;
```

### 取消监听服务（取消订阅）

```java
void unsubscribe(String serviceName, EventListener listener) throws NacosException;
void unsubscribe(String serviceName, String groupName, EventListener listener) throws NacosException;
void unsubscribe(String serviceName, List<String> clusters, EventListener listener) throws NacosException;
void unsubscribe(String serviceName, String groupName, List<String> clusters, EventListener listener) throws NacosException;
```

### 批量注册服务实例

```java
void batchRegisterInstance(String serviceName, String groupName, List<Instance> instances) throws NacosException;
```

### 批量注销服务实例

```java
void batchDeregisterInstance(String serviceName, String groupName, List<Instance> instances) throws NacosException;
```

### 带选择器的监听服务

```java
void subscribe(String serviceName, NamingSelector selector, EventListener listener) throws NacosException;
void subscribe(String serviceName, String groupName, NamingSelector selector, EventListener listener) throws NacosException;
```

### 取消带选择器的监听服务

```java
void unsubscribe(String serviceName, NamingSelector selector, EventListener listener) throws NacosException;
void unsubscribe(String serviceName, String groupName, NamingSelector selector, EventListener listener) throws NacosException;
```

### 分页获取服务列表

```java
ListView<String> getServicesOfServer(int pageNo, int pageSize) throws NacosException;
ListView<String> getServicesOfServer(int pageNo, int pageSize, String groupName) throws NacosException;
```

### 获取当前客户端所监听的服务列表

```java
List<ServiceInfo> getSubscribeServices() throws NacosException;
```
