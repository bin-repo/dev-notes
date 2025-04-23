# docker-network（网络）

## 四种网络模式

- bridge
- host
- none
- container

## 初始化网络

- 安装docker时已自动创建三个网络：bridge、host、none

```sh
# bridge
docker network create --driver bridge \
  --subnet 172.17.0.0/16 --gateway 172.17.0.1 \
  --opt "com.docker.network.bridge.name=docker0" bridge
```

```sh
# host
docker network create --driver host host
```

```sh
# none
docker network create --driver null none
```

- 自定义网桥

```sh
# bridge 
docker network create --driver bridge \
  --subnet 10.10.10.0/24 --gateway 10.10.10.1 \
  --opt "com.docker.network.bridge.name=docker1" mybridge
```

## `bridge` 网桥模式（default）

- 创建容器时未指定网络或者 `--network` 指定网桥时，容器内会创建 `eth0` 网卡，由网桥自动分配地址
- 当通过 `--network` 指定自定义网桥时亦可配合 `--ip` 为容器指定静态地址
- 使用 `-P` 进行随机端口映射，或者 `-p host_port:container_port` 进行指定端口映射

```sh
# 使用默认网桥bridge(docker0)
docker run -it --name c1 centos:7.9.2009
docker run -it --name c2 --network bridge centos:7.9.2009
```

```sh
# 使用自定义网桥
docker run -it --name c3 --network mybridge --ip 10.10.0.100 centos:7.9.2009
```

## `host` 主机网络共享模式

- 容器内执行 `ifconfig` 和主机执行 `ifconfig` 显示内容一致，无需进行端口映射
- 主机和容器无网络隔离，安全性较差，须特别注意网络安全访问控制

```sh
# 与主机网卡及IP地址相同
docker run -it --name c4 --network host centos:7.9.2009
```

## `container` 容器网络共享模式

- 仅共享容器的网卡及IP地址，其他资源仍然是隔离的
- 容器内不会创建 `eth0` 网卡

```sh
# 共享网络的容器必须处于运行状态，否则容器启动失败
docker run -it --name c5 --network container:c1 centos:7.9.2009
```

## `none` 无网络模式

- 与外界无网络通信，运行较独立的功能或测试
- 容器内不会创建 `eth0` 网卡

```sh
# 脱机状态
docker run -it --name c6 --network none centos:7.9.2009
```

## 网络相关命令

- 查看所有网络

```sh
docker network ls
```

- 创建一个新网络
  - `docker network create {options} {name}`
  - 指定驱动程序 `--driver bridge|host|overlay|none`
  - 指定子网 `--subnet`
  - 指定网关 `--gateway`
  - 指定动态分配的地址范围 `--ip-range`
  - 启用IPv6 `--ipv6`

```sh
# 命令帮助
docker network create --help
```

```sh
# 子网分配
docker network create --driver bridge \
  --subnet 192.168.1.0/24 \
  --gateway 192.168.1.1 \
  --ip-range 192.168.1.0/25 \
  --ipv6 net192
```

```sh
# 网络参数
docker network create --driver bridge \
  --subnet 10.10.10.0/24 \
  --gateway 10.10.10.1 \
  --opt "com.docker.network.bridge.name=docker1" \
  --opt "com.docker.network.driver.mtu=1500" net10
```

- 查看网络详情

```sh
docker network inspect bridge
docker network inspect host
docker network inspect none
docker network inspect net10
```

- 将一个容器连接到一个网络
  - `docker network connect {mynetwork} {mycontainer}`
  - 自动添加 `eth1` 网卡，可自动获取地址或通过 `--ip` 指定静态地址

```sh
docker network connect mybridge vm1
docker network connect --ip 10.10.10.200 mybridge vm1
```

- 将一个容器从一个网络断开
  - `docker network disconnect {mynetwork} {mycontainer}`
  - 自动删除 `eth1` 网卡

```sh
docker network disconnect mybridge vm1
```

- 删除一个或多个网络
  - `docker network rm {name|id} {name|id}`

```sh
docker network rm mybridge
```
