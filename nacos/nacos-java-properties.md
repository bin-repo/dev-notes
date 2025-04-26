# Nacos Java SDK 配置参数列表

## 通用参数

- `serverAddr | SERVER_ADDR` Nacos Server的地址列表（逗号分隔）
- `contextPath | CONTEXT_PATH` 上下文路径（默认nacos）
- `endpoint | ENDPOINT` 接入点域名或IP
- `endpointPort | ENDPOINT_PORT` 接入点端口（默认8080）
  - `${endpoint}:${endpointPort}/nacos/serverlist`
- `endpointContextPath | ENDPOINT_CONTEXT_PATH` 接入点上下文（默认nacos）
  - `${endpoint}:${endpointPort}/${endpointContextPath}/serverlist`
- `clusterName | CLUSTER_NAME` 集群名（默认serverlist）
  - `${endpoint}:${endpointPort}/${endpointContextPath}/${clusterName}`
- `endpointQueryParams | ENDPOINT_QUERY_PARAMS` 请求参数（key=value）
- `namespace | NAMESPACE` 命名空间ID
- `username | USERNAME` 开启鉴权功能后（用户名）
- `password | PASSWORD` 开启鉴权功能后（口令）
- `accessKey | ACCESS_KEY` 使用阿里云RAM鉴权时
- `ecretKey | SECRET_KEY` 使用阿里云RAM鉴权时
- `ramRoleName | RAM_ROLE_NAME` 使用阿里云RAM鉴权时
- `signatureRegionId | SIGNATURE_REGION_ID` 使用阿里云RAM鉴权时
- `logAllProperties | LOG_ALL_PROPERTIES` 是否打印全量参数（默认false），包含自定义properties、JVM和环境变量，主要用户调试和问题排查

## 配置中心相关参数

仅在初始化配置中心ConfigService时生效

- `clientWorkerMaxThreadCount | CLIENT_WORKER_MAX_THREAD_COUNT` 最大线程池个数
- `clientWorkerThreadCount | CLIENT_WORKER_THREAD_COUNT` 最大线程池个数（优先级高）
- `enableRemoteSyncConfig | ENABLE_REMOTE_SYNC_CONFIG` 远程同步配置（默认false）开启可能影响启动监听的速度
- `configRequestTimeout | CONFIG_REQUEST_TIMEOUT` 配置请求超时时间

## 注册中心相关参数

仅在初始化注册中心NamingService时生效

- `namingLoadCacheAtStart | NAMING_LOAD_CACHE_AT_START` 启动时读取本地磁盘缓存来初始化数据（默认false）
- `namingCacheRegistryDir | NAMING_CACHE_REGISTRY_DIR` 本地磁盘缓存目录名拓展名，用于同一节点中区分多个实例
- `namingAsyncQuerySubscribeService | NAMING_ASYNC_QUERY_SUBSCRIBE_SERVICE` 开启异步查询订阅服务的功能（默认false）
- `namingPollingMaxThreadCount | NAMING_POLLING_MAX_THREAD_COUNT` 最大线程池个数
- `namingPollingThreadCount | NAMING_POLLING_THREAD_COUNT` 最大线程池个数（优先级高）
- `namingRequestDomainMaxRetryCount | NAMING_REQUEST_DOMAIN_RETRY_COUNT` 请求最大重试次数（默认3）
- `namingPushEmptyProtection | NAMING_PUSH_EMPTY_PROTECTION` 开启推空保护功能（默认false）
- `redoDelayTime | REDO_DELAY_TIME` 链接断开后，间隔多长时间检查并进行redo操作（默认3000ms）
- `redoDelayThreadCount | REDO_DELAY_THREAD_COUNT` 执行redo操作的线程数（默认1）
- `namingRequestTimeout | NAMING_REQUEST_TIMEOUT` 注册请求超时时间

## 连接相关参数

## 其他参数

```properties
nacos.server.port = 8848
nacos.naming.exposed.port = 8848
nacos.env.first = PROPERTIES | JVM |ENV
```
