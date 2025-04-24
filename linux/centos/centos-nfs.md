# NFS 网络文件系统（Network File System）

- 通过网络让不同的机器、不同的操作系统之间可以共享彼此的文件
- 一般用于存储共享视频、图片等静态数据

## 原理

### `NFS`服务端

- 设置共享目录、访问权限
- 启动`RPC`服务（portmap服务 port=111）
- 启动`NFS`服务（port=随机）
- 向`RPC`注册`NFS`服务端口

### `NFS`客户端

- 启动`RPC`服务（portmap服务）
- 获取服务器端`NFS`服务端口
- 将服务器共享的目录挂载到本地

## 示例

- 服务端

```sh
# 添加NFS共享目录
echo "/opt/sharedir *(rw,sync,no_root_squash)" >> /etc/exports

# 关闭防火墙
service iptables stop

# 启动NFS服务
service nfs restart
```

- 客户端

```sh
# 挂载NFS共享目录
mount -t nfs -o nolock -rw 172.16.10.10:/opt/sharedir /opt/sharedir
```

## `CentOS`部署`NFS`服务端

### 安装

```sh
# 其旧版为portmap
yum install -y rpcbind

# 包含两个daemons守护进程（rpc.nfsd、rpc.mountd）
yum install -y nfs-utils
```

### 启动（设置开机自启动）

```sh
# 启动RPC服务
systemctl start rpcbind
systemctl enable rpcbind

# 启动NFS服务
systemctl start nfs-server nfs-secure-server
systemctl enable nfs-server nfs-secure-server
```

### 设置防火墙

```sh
firewall-cmd --permanent --add-service=nfs
firewall-cmd --reload
```

### 设置共享目录

- 创建共享目录

```sh
mkdir -p /home/{public,protected}
```

- 配置文件`/etc/exports`内添加内容

```text
# 共享目录路径 授权访问的客户端(权限)
/home/public 192.168.245.0/24(ro)
/home/protected 192.168.245.0/24(rw)
```

![权限说明](./img/nfs-perm.png '权限')

- 重载配置

```sh
systemctl reload nfs
```

### 运维

- 维护工具 `/usr/sbin/exportfs`
- 资源访问记录 `/var/lib/nfs/*tab`（其中`etab`权限设定值，`xtab`访问记录）

## `Linux`配置`NFS`客户端

### 查看共享资源

```sh
showmount -v # 查看版本信息
showmount -a # 查看本地挂载情况
showmount -e 服务器IP # 查看服务端共享资源
```

### 挂载共享目录

- 创建挂载目录

```sh
mkdir /mnt/{public,data}
```

- 配置文件`/etc/fstab`内添加内容

```text
192.168.245.128:/home/public    /mnt/public   nfs   defaults 0 0
192.168.245.128:/home/protected /mnt/data     nfs   defaults 0 1
```

- 重载配置

```sh
mount -a
```

- 检查文件系统挂载情况

```sh
df -Th
```

## `Windows`配置`NFS`客户端

- 控制面板`程序和功能`添加`NFS`组件

![NFS组件](./img/nfs-windows-1.png 'NFS客户端')

- 映射网络驱动器

![映射网络驱动器](./img/nfs-windows-2.png '挂载共享目录')

- 权限问题处理

```text
注册表中HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ClientForNFS\CurrentVersion\Default键下
新建两个OWORD(64)：
AnonymousGid = 0
AnonymousUid = 0
```
