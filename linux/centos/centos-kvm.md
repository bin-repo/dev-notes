# KVM 虚拟机

Linux内核的虚拟化技术（Kernel-based Virtual Machine），使用硬件虚拟化技术（由Intel VT-x和AMD-V等CPU虚拟化指令集支持），将物理服务器划分为多个虚拟机，使用QEMU作为虚拟机监控程序，对磁盘、网络、IO设备等资源进行管理。

## CentOS7下安装部署

### 检查硬件虚拟化VT是否支持

```sh
# 返回结果大于0则支持
egrep -c '(vmx|svm)' /proc/cpuinfo
```

### 安装KVM和相关软件包

```sh
# 安装
yum install -y qemu-kvm qemu-kvm-tools qemu-img bridge-utils libvirt virt-install virt-manager

# 验证
virt-manager
```

### 创建一个网桥（可选）

```sh
cp /etc/sysconfig/network-scripts/{ifcfg-ens33,ifcfg-br0}
```

- 修改网桥配置

```sh
# ifcfg-br0
TYPE="Bridge"
NAME="br0"
DEVICE="br0"
```

- 修改网卡配置

```sh
# ifcfg-ens33
BRIDGE=br0
# IPADDR=
# PREFIX=
# GATEWAY=
# DNS1=
```

- 重启网络

```sh
systemctl restart network
ifconfig
```

## 启动QEMU

```sh
virt-manager
```

## 配置存储空间

- 双击 QEMU 界面 `QEMU/KVM` 可查看 `Overview`、`Virtual Networks`、`Storage`、`Network Interfaces`
- 选择 `Storage` 分别添加 `default`、`ISO`、`KVM` 目录
  - default 默认路径为 `/var/lib/libvirt/images`
  - ISO 用于存放系统镜像源文件，路径自定义（预留足够空间）
  - KVM 用于存放虚拟机文件，路径自定义（预留足够空间）

## 创建虚拟机

- 上传系统镜像到`ISO`目录（`scp`命令）
- `KVM`目录创建卷（如：ubuntu.qcow2）
- 创建虚拟机

## KVM操作

```sh
# 查看虚拟机
virsh list --all
```

```sh
# 开启虚拟机
virsh start xxx

# 关闭
virsh shutdown xxx

# 挂起
virsh suspend xxx

# 由挂起恢复
virsh resume xxx

# 强制关机
virsh destroy xxx
```

```sh
# 设置随物理机一起自动启动
virsh autostart xxx

# 取消自动启动
virsh autostart --disable xxx
```

```sh
# 通过虚拟机配置文件启动
virsh create /etc/libvirt/qemu/xxx.xml

# 备份虚拟机配置文件
virsh dumpxml xxx > /backup/xxx.xml
```

```sh
# 创建快照
virsh snapshot-create xxx

# 查看快照
virsh snapshot-list xxx

# 恢复快照zzz
virsh snapshot-revert xxx zzz

# 删除快照zzz
virsh snapshot-delete xxx zzz

# 快照重命名
virsh snapshot-edit xxx --snapshotname zzz --rename

# 克隆
virt-clone -o xxx -n localhost -f yyy.qcow2
```
