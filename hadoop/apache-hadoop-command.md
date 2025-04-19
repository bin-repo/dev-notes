# apache-hadoop 文件操作命令

## 命令

### hdfs（仅针对HDFS文件系统）

```sh
hdfs dfs 参数 对象
```

```sh
hdfs dfs -ls /
hdfs dfs -mkdir /hello
hdfs dfs -put xxx.cfg /hello
```

### hadoop（除HDFS外还支持其他文件系统）

```sh
hadoop fs 参数 对象
```

```sh
hadoop fs -ls hdfs://namenode:host/
hadoop fs -ls file:///opt/hadoop/data/
```

## 命令参数

### ls 查看目录结构

```sh
-ls <路径>
```

### lsr 递归查看目录结构

```sh
-lsr <路径>
```

### du 统计目录下文件大小

```sh
-du <路径>
```

### dus 汇总统计目录下文件（夹）大小

```sh
-dus <路径>
```

### count 统计文件（夹）数量

```sh
-count [-q] <路径>
```

### mv 移动

```sh
-mv <源路径> <目的路径>
```

### cp 复制

```sh
-cp <源路径> <目的路径>
```

### rm 删除文件/空白文件夹

```sh
-rm [-skipTrash] <路径>
```

### rmr 递归删除

```sh
-rmr [-skipTrash] <路径>
```

### put 上传文件

```sh
-put <多个本地文件> <hdfs路径>
```

```sh
# 支持标准输入
echo abc | hadoop fs -put - /hdfs/test/echoin.txt
ls /usr/local/hadoop | hadoop fs -put - /hdfs/test/hadooplist.txt
```

### copyFromLocal 从本地复制

```sh
-copyFromLocal <多个本地文件> <hdfs路径>
```

### moveFromLocal 从本地移动

```sh
-moveFromLocal <多个本地文件> <hdfs路径>
```

### getmerge 合并到本地

```sh
-getmerge <源路径> <本地路径>
```

### cat 查看文件内容

```sh
-cat <hdfs路径>
```

### text 查看文件内容

```sh
-text <hdfs路径>
```

### copyToLocal 复制到本地

```sh
-copyToLocal [-IgnoreCrc] [-crc] [hdfs源路径] [本地路径]
```

### moveToLocal 移动到本地

```sh
-moveToLocal [-crc] [hdfs源路径] [本地路径]
```

### mkdir 创建文件夹

```sh
-mkdir <hdfs路径>
```

### setrep 修改副本数量

```sh
-setrep [-P] [-w] <副本数> <路径>
```

### touchz 创建空白文件

```sh
-touchz <文件路径>
```

### stat 查看文件统计信息

```sh
-stat [format] <路径>
```

### tail 查看文件尾部信息

```sh
-tail [-f] <文件>
```

### chmod 修改权限

```sh
-chmod [-R] <权限模式> [路径]
```

### chown 修改属主

```sh
-chown [-R] [属主][:[数组]] 路径
```

### chgrp 修改属组

```sh
-chgrp [-R] 属组名称:路径
```

### help 帮助

```sh
-help
```
