# mysql-system-variables-80

MySQL 8.0 System Variables

## 系统参数命名提示

- 系统参数名称中分词包含`短横线-`或`下划线_`
- 命令程序查看系统参数名称通常为`短横线`
- 命令行中系统参数名称通常为`短横线`
- 系统表中查询系统参数名称通常为`下划线`
- 配置文件中系统参数名称`短横线`和`下划线`均可（建议统一使用`下划线`）

## 系统参数默认值

```sh
mysqld --verbose --help
# 部分重要参数
mysqld --verbose --help | grep basedir
mysqld --verbose --help | grep datadir
mysqld --verbose --help | grep secure-file-priv
mysqld --verbose --help | grep character-set-server
mysqld --verbose --help | grep collation-server
mysqld --verbose --help | grep default-authentication-plugin
mysqld --verbose --help | grep default-storage-engine
mysqld --verbose --help | grep lower-case-table-names
mysqld --verbose --help | grep max-allowed-packet
mysqld --verbose --help | grep wait-timeout
```

## 系统参数实际值

### SHOW VARIABLES Statement

- `SHOW [GLOBAL | SESSION] VARIABLES [LIKE 'pattern' | WHERE expr]`

```sql
SHOW VARIABLES;
SHOW VARIABLES LIKE 'innodb_data_file_path';
```

### SELECT Statement

```sql
SELECT @@GLOBAL.innodb_data_file_path;
```

### Performance Schema System Variable Tables

- `global_variables` 表
- `session_variables` 表
- `variables_by_thread` 表
- `persisted_variables` 表
- `variables_info` 表

```sql
SELECT * FROM performance_schema.global_variables;
```

## 系统参数设置方式

`注意`：部分系统参数在数据库初始化时一次性写死，后期无法修改！

- 配置文件中设置（如：`secure_file_priv`）
- 命令行参数（如：`--secure-file-priv`）
- 相关系统表数据更新（update）

## 系统参数说明

### `basedir` 安装目录

- Path to installation directory.
- All paths are usually resolved relative to this.
- `--basedir=/usr/`（默认）
- `--basedir=/usr/local/mysql/`（建议）

### `datadir` 数据目录（schema）

- Path to the database root directory.
- `--datadir=/var/lib/mysql/`（默认）

### `secure_file_priv` 数据目录（import、export）需手动创建

- Limit LOAD DATA, SELECT OUTFILE, LOAD_FILE() to files within specified directory.
- `--secure-file-priv=/var/lib/mysql-files/`（建议，DEB、RPM源安装时默认）
- `--secure-file-priv=/usr/local/mysql/mysql-files/`（二进制安装时默认）

### `pid_file` 进程文件

- Pid file used by safe_mysqld.
- `--pid-file=/var/run/mysqld/mysqld.pid`（默认）

### `socket` 网络文件

- Socket file to use for connection.
- `--socket=/var/lib/mysql/mysql.sock`（默认）

### `port` 服务端口

- Port number to use for connection or 0 to default to.
- `--port=3306`（默认）

### `character_set_server` 全局字符集

- Set the default character set.
- `--character-set-server=utf8mb4`（默认）

### `collation_server` 全局字符集校对规则

- Set the default collation.
- `--collation-server=utf8mb4_0900_ai_ci`（默认，该规则字符集大小写不敏感）
- `--collation-server=utf8mb4_0900_as_cs`（可选，该规则字符集大小写敏感）

### `lower_case_table_names` 小写表名

- 设置为0时根据windows、linux、macos不同系统机制区分大小写
- 设置为1时不区分大小写 
- `--lower-case-table-names=1`（默认，表名大小写不敏感）

### `default_authentication_plugin` 认证插件

- The default authentication plugin used by the server to hash the password.
- `--default-authentication-plugin=caching_sha2_password`（默认）
- `--default-authentication-plugin=mysql_native_password`（可选）

### `default_storage_engine` 存贮引擎

- The default storage engine for new tables.
- `--default-storage-engine=InnoDB`（默认）

### `log_bin` BINLOG日志文件

- Configures the name prefix to use for binary log files.
- `--log-bin=binlog`（默认，主从同步或数据重建时的重要依赖文件）

### `binlog_format` BINLOG日志格式

- The format used when writing the binary log.
- `--binlog-format=ROW`（默认，可选值ROW、STATEMENT、MIXED）

### `max_allowed_packet` 最大数据包长度限制

- Max packet length to send to or receive from the server.
- 须注意`insert`批量插入和`select`结果集数据量不能超过限值
- `--max-allowed-packet=67108864`（默认64M）
- `--max-allowed-packet=128M`（按实际业务需求调整）

### `connect_timeout` 连接超时（秒）

- The number of seconds the mysqld server is waiting for a connect packet before responding with 'Bad handshake'.
- 建立连接超时（握手超时）
- `--connect-timeout=10`（默认）

### `net_read_timeout` 网络读数据超时（秒）

- Number of seconds to wait for more data from a connection before aborting the read.
- 从网卡接收请求数据超时
- `--net-read-timeout=30`（默认）

### `net_retry_count` 网络读数据重试次数

- If a read on a communication port is interrupted, retry this many times before giving up.
- `--net-retry-count=10`（默认）

### `net_write_timeout` 网络写数据超时（秒）

- Number of seconds to wait for a block to be written to a connection before aborting the write.
- 向网卡发送应答数据超时
- `--net-write-timeout=60`（默认）

### `wait_timeout` 等待超时（秒）连接闲置超时

- The number of seconds the server waits for activity on a connection before closing it.
- 连接建立后超过该时间无请求和数据往来将被断开连接
- `--wait-timeout=28800`（默认8小时）
