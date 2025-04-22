# mysql-replication-80

MySQL 8.0 Replication 主从复制

## Binary Log File Position Based Replication

- the source and each replica must be configured with a unique ID (using the `server_id` system variable)
- each replica must be configured with information about the source's host name, log file name, and position within that file
- using a `CHANGE REPLICATION SOURCE TO` statement (from MySQL 8.0.23) or `CHANGE MASTER TO` statement (before MySQL 8.0.23) on the replica

### system variable `server_id`

```sql
-- default = 1
show variables like 'server_id';

-- 分别设置源（source）和副本（replicas）的各自服务ID，可选值范围[1,2^32)
set global server_id = 2;
```

### system variable `log_bin` or option `--log-bin`

```sql
-- default = ON
show variables like 'log_bin';

-- 设置源（source）enabled binary log file : /var/lib/mysql/binlog
set global log_bin = ON;
```

```sh
# binary log file name
mysqld --log-bin=binlog
```

### create a user for replication

```sql
-- on source
create user 'repl'@'%' identified by 'password';
grant replication slave on *.* to 'repl'@'%';
```

### obtaining the replication source binary log coordinates

```sql
-- one session lock table to prevent update 
flush tables with read lock;
```

```sql
-- another session obtain binary log file and position
-- show master status;
show master status\G
```

### choosing a method for data snapshots

- If the source database contains existing data it is necessary to copy this data to each replica

```sh
# the --master-data option which automatically appends the CHANGE REPLICATION SOURCE TO | CHANGE MASTER TO statement 
# required on the replica to start the replication process
mysqldump --all-databases --master-data > dbdump.db
```

```sql
-- one session where you acquired the read lock, release the lock
unlock tables;
```

### use data snapshots on replicas

```sh
mysql < dbdump.db
```

### setting the source configuration on the replica

```sql
-- before mysql 8.0.23
change master to
master_host='source_host',
master_user='replication_user',
master_password='replication_password',
master_log_file='binary_log_file',
master_log_pos=binary_log_file_position;
```

```sql
-- from mysql 8.0.23
change replication source to
source_host='source_host',
source_user='replication_user',
source_password='replication_password',
source_log_file='binary_log_file',
source_log_pos=binary_log_file_position;
```

### check

```sql
-- 查看有哪些副本 on source
show replicas;

-- 查看副本状态 on source
show processlist \G;

-- 查看副本状态 on replica
show replica status\G
```

### pause and start replica

```sql
-- before mysql 8.0.22
stop slave;
start slave;
```

```sql
-- from mysql 8.0.22
stop replica;
start replica;
```
