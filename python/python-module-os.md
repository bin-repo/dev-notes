# python-module-os（系统模块）

## 模块导入

```py
import os
```

## 模块方法

```py
# 检验权限模式
os.access(path,mode)

# 当前工作目录
os.getcwd()

# 当前工作目录的Unicode对象
os.getcwdu()

# 改变当前工作目录
os.chdir(path)

# 更改权限
os.chmod(path,mode)

# 更改所有者
os.chown(path,uid,gid)

# 改变当前进程的根目录
os.chroot(path)

# 设置路径的标记为数字标记
os.chflags(path,flags)

# 创建硬链接（dst指向src）
os.link(src,dst)

# 创建软链接（dst指向src）
os.symlink(src,dst)

# 同chflags，设置文件数字标记，但无软链接
os.lchflags(path,flags)

# 同chmod，修改链接文件权限
os.lchmod(path,mode)

# 同chown，更改文件所有者，但不追踪链接
os.lchown(path,uid,gid)

# 同stat，但没有软链接
os.lstat(path)

# 返回软链接所指向的文件
os.readlink(path)

# 删除文件路径
os.unlink(path)

# 从原始设备号中提取设备major号码
os.major(device)

# 从原始设备号中提取设备minor号码
os.minor(device)

# 以major和minor组成新的设备号
os.makedev(major,minor)

# 文件和文件夹名字列表
os.listdir(path)

# 递归创建文件夹
os.makedirs(path[,mode])

# 创建文件夹
os.mkdir(path,mode=0777)

# 仅能删除文件，否则异常
os.remove(path)

# 递归删除目录
os.removedirs(path)

# 删除空目录，否则异常
os.rmdir(path)

# 文件或目录重命名
os.rename(src,dst)

# 递归进行重命名
os.renames(old,new)

# 创建命名管道
os.mkfifo(path,mode=0666)

# 创建一个文件系统节点
os.mknod(filename[,mode=0600,device])

# 创建一个管道，返回一对文件描述符(r,w)分别为读和写
os.pipe()

# 从一个command打开一个管道
os.popen(command[,mode[,bufsize]])

# 打开一个新的伪终端对,返回pty和tty的文件描述符
os.openpty()

# 文件的系统配置信息
os.pathconf(path,name)

# 文件信息
os.stat(path)

# 决定stat_result是否以float对象显示时间戳
os.stat_float_times([newvalue])

# 文件系统统计信息
os.statvfs(path)

# 返回文件的访问和修改的时间
os.utime(path,times)

# 打开文件
fd = os.open(file,flags[,mode])

# 设定文件指针位置
os.lseek(fd,pos,how)

# 读取bsize字节的字符串，达到文件尾则返回空字符串
os.read(fd,bsize)

# 写入字符串,返回实际写入长度
os.write(fd,str)

# 关闭文件描述符
os.close(fd)

# 关闭[fd_low,fd_high)区间的所有文件描述符
os.closerange(fd_low,fd_high)

# 与fd关联的进程组
os.tcgetpgrp(fd)

# 设置fd关联的进程组
os.tcsetpgrp(fd,pg)

# fd是打开的且与tty设备相连，则返回True
os.isatty(fd)

# 与fd关联的tty终端设备的名称
os.ttyname(fd)

# 复制文件描述符
os.dup(fd)

# 将文件描述符fd复制到fd2
os.dup2(fd,fd2)

# 通过文件描述符改变当前工作目录
os.fchdir(fd)

# 通过文件描述符改变权限
os.fchmod(fd,mode)

# 通过文件描述符改变所有者
os.fchown(fd,uid,gid)

# 强制将文件写入磁盘，但不强制更新文件的状态信息
os.fdatasync(fd)

# 文件的系统配置信息，name为检索值
os.fpathconf(fd,name)

# 文件描述符状态
os.fstat(fd)

# 文件系统信息
os.fstatvfs(fd)

# 强制将文件写入硬盘
os.fsync(fd)

# 文件裁剪
os.ftruncate(fd,length)

# 通过文件描述符创建一个文件对象
file = os.fdopen(fd[,mode[,bufsize]])
```
