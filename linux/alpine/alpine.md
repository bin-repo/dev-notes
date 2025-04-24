# [alpine](https://alpinelinux.org/)

Small. Simple. Secure.
Alpine Linux is a security-oriented, lightweight Linux distribution based on musl libc and busybox.

## 下载（ISO）

```sh
# 官方源
wget https://dl-cdn.alpinelinux.org/alpine/v3.21/releases/x86_64/alpine-standard-3.21.3-x86_64.iso
```

```sh
# 镜像源
wget https://mirrors.aliyun.com/alpine/v3.21/releases/x86_64/alpine-standard-3.21.3-x86_64.iso
```

## 容器（Docker）

```sh
# 官方源
docker pull alpine:3.21.3
```

```sh
# 镜像源
docker pull docker.xuanyuan.me/alpine:3.21.3

# 重命名
docker tag docker.xuanyuan.me/alpine:3.21.3 alpine:3.21.3
docker rmi docker.xuanyuan.me/alpine:3.21.3
```

```sh
docker run -d --name alpine3213 alpine:3.21.3
docker exec -it alpine3213 /bin/sh
```

## 替换源

- 修改`/etc/apk/repositories`文件内容
- 将官方源替换为国内镜像源加速安装包下载

```sh
# 官方源
https://dl-cdn.alpinelinux.org/alpine/v3.21/main
https://dl-cdn.alpinelinux.org/alpine/v3.21/community
```

```sh
# 镜像源
https://mirrors.aliyun.com/alpine/v3.21/main
https://mirrors.aliyun.com/alpine/v3.21/community
```

## 软件包管理（`apk`）

```sh
# 检查软件包安装状态
apk list openjdk*

# 安装
apk add openjdk8-jre

# 安装详情
apk -L info openjdk8-jre

# 卸载
apk del openjdk8-jre
```

## 问题

- alpine中openjdk-jre安装包8、17、21版本似乎均存在问题，加载libfontmanager.so库时异常，导致依赖该库的jar无法正常工作，如easyexcel组件等。
