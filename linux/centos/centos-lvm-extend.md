# centos 磁盘扩容

## 查看文件系统挂载信息

```sh
# 文件系统 /dev/mapper/centos-root 挂载点 /
df -h
```

## 通过以下方式对vmware虚拟机硬盘扩容

- 改变原磁盘大小（/dev/sda）
- 新增硬盘（/dev/sdb）

## 对新增加的硬盘进行分区

```sh
fdisk /dev/sda
```

- m 查看帮助
- p 查看已有分区
- n 新增分区
  - 分区类型 p（primary）
  - 分区号 3（default）
  - 起始扇区（default）
  - 结束扇区（default）
- t 修改分区类型
  - 分区号 3
  - Hex代码 8e（Linux LVM）
  - w（保存）
- q（退出）

```sh
# 重启系统
reboot
```

## 检查新设备分区

```sh
ls /dev/sda*
```

## 格式化新设备分区

```sh
mkfs.ext3 /dev/sda3
```

## 添加新LVM到已有的LVM组实现扩容

```sh
lvm
```

- `vgdisplay` 查看VolumeGroup
- `pvcreate /dev/sda3` 新分区创建虚拟卷
- `vgextend centos /dev/sda3` 新分区加入到虚拟卷组centos
- `vgdisplay -v` 查看 `Free PE / Size` 行的`PE`和Size可用值
- `lvextend -l+${PE} /dev/mapper/centos-root` 扩容
- `vgdisplay` 查看 `VG Size`行数据应已增大
- `quit` 退出数据卷管理

## 文件系统扩容

```sh
df -h
xfs_growfs /dev/mapper/centos-root
df -h
```

## 物理硬盘扩容同理（注意设备盘符即可）
