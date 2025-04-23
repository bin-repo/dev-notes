# docker-container（容器）

## 查看容器（`docker ps`）

```sh
docker ps    # 正在运行
docker ps -a # 所有
```

## 运行容器（`docker run`）

- `docker run <options> <image_name>[:tag]`
  - `-d` 后台运行
  - `-it` 提供交互终端
  - `-p host_port:container_port` 端口映射
  - `-v volume_name:container_dir` 数据卷挂载（数据持久化）
  - `-v /host_path_to/dir_or_file:container_dir_or_file` 主机目录或文件挂载（数据持久化）
  - `--name=container_name` 容器名
  - `--network=network_name` 网络名
  - `--restart=always` 重启机制

```sh
docker run -d -p 8080:80 --name=mycontainer docker/welcome-to-docker
```

## 容器信息（`docker inspect`）

```sh
docker inspect mycontainer
```

## 容器日志（`docker logs`）

```sh
docker logs mycontainer
```

## 文件复制（`docker cp`）

- 从主机复制到容器

```sh
docker cp app.conf mycontainer:/opt
```

- 从容器复制到主机

```sh
docker cp mycontainer:/opt/app.conf .
```

## 进入容器（`docker exec`）

```sh
docker exec -it mycontainer /bin/bash
```

## 启动容器（`docker start`）

```sh
docker start mycontainer
```

## 重启容器（`docker restart`）

```sh
docker restart mycontainer
```

## 停止容器（`docker stop`）

```sh
docker stop mycontainer
```

## 删除容器（`docker rm`）

```sh
docker rm mycontainer
```
