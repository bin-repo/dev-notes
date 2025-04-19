# sonatype-nexus-docker（容器化部署）

## 官方镜像

```sh
# 从dockerhub上拉取官方最新镜像
docker pull sonatype/nexus3
```

## 默认参数

```sh
# 安装路径
NEXUS_HOME="/opt/sonatype/nexus"
# 数据目录（配置、日志、数据等）
NEXUS_DATA="/nexus-data"
# 启动参数
INSTALL4J_ADD_VM_PARAMS="-Xms1200m -Xmx1200m -XX:MaxDirectMemorySize=2g \
-Djava.util.prefs.userRoot=${NEXUS_DATA}/javaprefs"
# 上下文路径
NEXUS_CONTEXT="/"
```

## 运行容器

- 映射端口

```sh
docker run -d -p 8081:8081 --name nexus sonatype/nexus3
```

- 调整启动参数

```sh
docker run -d -p 8081:8081 --name nexus \
-e INSTALL4J_ADD_VM_PARAMS="-Xms2g -Xmx2g -XX:MaxDirectMemorySize=3g \
-Djava.util.prefs.userRoot=/some-other-dir" sonatype/nexus3
```

- 调整上下文路径

```sh
docker run -d -p 8081:8081 --name nexus \
-e NEXUS_CONTEXT=nexus sonatype/nexus3
```

- 使用数据卷持久化

```sh
# 创建数据卷
docker volume create --name nexus-data
# 挂载数据卷
docker run -d -p 8081:8081 --name nexus \
-v nexus-data:/nexus-data sonatype/nexus3
```

- 使用主机目录持久化

```sh
# 创建主机数据目录
mkdir /var/lib/nexus/nexus-data
chown -R 200 /var/lib/nexus/nexus-data
# 挂载主机目录
docker run -d -p 8081:8081 --name nexus \
-v /var/lib/nexus/nexus-data:/nexus-data sonatype/nexus3
```

## 查看日志

```sh
docker logs -f nexus
```

## 进入容器

```sh
docker exec -it nexus /bin/bash
```

## 功能检查

- 检查运行是否正常（`http://localhost:8081/`）
- 默认用户（admin/admin123）
