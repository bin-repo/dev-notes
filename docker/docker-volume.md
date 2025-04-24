# docker-volume（数据卷）

## 主机默认存放位置

- `/var/lib/docker/volumes/卷名`

## 查询

```sh
docker volume ls
docker volume ls | grep my_volume
```

## 创建

```sh
docker volume create my_volume
```

## 详情

```sh
docker volume inspect my_volume
```

## 挂载

```sh
# 当不存在数据卷my_volume时会自动创建
docker run -v my_volume:/my_path my_image
```
