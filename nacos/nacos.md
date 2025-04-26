# [nacos](https://nacos.io/)

## 下载

```sh
wget https://download.nacos.io/nacos-server/nacos-server-2.4.1.zip
```

## 单机部署

```sh
bin/startup.sh -m standalone
bin/shutdown.sh
```

## 容器部署（Docker）

- 拉取镜像

```sh
docker pull nacos/nacos-server:v2.4.1
```

- 运行容器（使用内置的`Derby`数据库）

```sh
docker run -it \
-e PREFER_HOST_MODE=hostname \
-e MODE=standalone \
-e NACOS_AUTH_IDENTITY_KEY=serverIdentity \
-e NACOS_AUTH_IDENTITY_VALUE=security \
-e NACOS_AUTH_TOKEN=SecretKey012345678901234567890123456789012345678901234567890123456789 \
-p 8848:8848 \
--name nacos2 \
nacos/nacos-server:v2.4.1 \
bin/bash
```

## 容器部署（Docker Compose）

- 项目演示

```sh
git clone https://github.com/nacos-group/nacos-docker.git
```

- example下含多个部署方式配置文件可选

```sh
cd nacos-docker
docker-compose -f example/standalone-derby.yaml up
```

## 容器部署（Kubernetes）

- 项目演示

```sh
git clone https://github.com/nacos-group/nacos-k8s.git
```

- 快速启动

```sh
cd nacos-k8s
chmod +x quick-startup.sh
./quick-startup.sh
```

## 服务注册

```sh
curl -X POST 'http://127.0.0.1:8848/nacos/v1/ns/instance?serviceName=nacos.naming.serviceName&ip=20.18.7.10&port=8080'
```

## 服务发现

```sh
curl -X GET 'http://127.0.0.1:8848/nacos/v1/ns/instance/list?serviceName=nacos.naming.serviceName'
```

## 删除服务

```sh
curl -X DELETE 'http://127.0.0.1:8848/nacos/v1/ns/instance/list?serviceName=nacos.naming.serviceName&ip=20.18.7.10'
```

## 发布配置

```sh
curl -X POST "http://127.0.0.1:8848/nacos/v1/cs/configs?dataId=nacos.cfg.dataId&group=test&content=HelloWorld"
```

## 获取配置

```sh
curl -X GET "http://127.0.0.1:8848/nacos/v1/cs/configs?dataId=nacos.cfg.dataId&group=test"
```

## 删除配置

```sh
curl -X DELETE "http://127.0.0.1:8848/nacos/v1/cs/configs?dataId=nacos.cfg.dataId&group=test"
```

## 控制台

```sh
curl http://127.0.0.1:8848/nacos
```

## 系统参数

- `{nacos.home}/conf/application.properties` 应用参数（APP）
- `{nacos.home}/bin/startup.sh` 环境参数（JVM）高优先级

## 自定义数据库镜像

```Dockerfile
FROM mysql:8.0.31
ADD nacos-mysql-schema.sql /docker-entrypoint-initdb.d/nacos-mysql.sql
RUN chown -R mysql:mysql /docker-entrypoint-initdb.d/nacos-mysql.sql
EXPOSE 3306
CMD ["mysqld", "--character-set-server=utf8mb4", "--collation-server=utf8mb4_unicode_ci"]
```
