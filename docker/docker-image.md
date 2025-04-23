# docker-image（镜像）

## 查看本地镜像（`docker images`）

```sh
# 镜像列表
docker images
docker image ls
```

```sh
# 检查特定镜像
docker images | grep openjdk
```

## 检索远程仓库镜像（`docker search`）

```sh
docker search openjdk
```

## 拉取镜像（`docker pull`）

- 从官方镜像仓库拉取镜像（`hub.docker.com`）

```sh
# docker pull <image_name>[:tag]
docker pull openjdk    # latest
docker pull openjdk:8
```

- 从私有镜像仓库（或第三方仓库）拉取镜像

```sh
# docker pull <register>/<image_name>[:tag]
docker pull myregister.com/openjdk    # latest
docker pull myregister.com/openjdk:8
```

## 推送镜像（`docker push`）

```sh
# 须先注册用户
docker push myregister.com/openjdk:8
```

## 复制本地镜像（`docker tag`）

- 仅增加了引用名而已

```sh
# docker tag <src_image_name:tag> <dst_image_name:tag>
docker tag myregister.com/openjdk:8 openjdk:8
```

## 查看镜像构建历史（`docker image history`）

```sh
# list the image's layers
docker image history openjdk:8
```

## 导出本地镜像（`docker save`）

```sh
# docker save -o <local_image_file> <image_name:tag>
docker save -o openjdk-8.tar openjdk:8
```

## 导入本地镜像（`docker load`）

```sh
# docker load -i <local_image_file>
docker load -i openjdk-8.tar
```

## 删除本地镜像（`docker rmi`）

```sh
# docker rmi <image_name_or_id>
# docker image rm <image_name_or_id>
docker rmi openjdk:8
```

## 制作镜像（`docker build`）

- 编写 `Dockerfile` 文件
- 然后 `docker build` 构建镜像

```sh
# 默认 Dockerfile
docker build .
```

```sh
# 指定文件 xxx.Dockerfile
docker build --file xxx.Dockerfile .
docker build -f xxx.Dockerfile .
```

```sh
# 指定镜像 TAG
docker build -t xxxx:latest .
```
